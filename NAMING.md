Naming
---

> There are only two hard things in Computer Science: cache invalidation and naming things.
>
> -- Phil Karlton [[1](https://martinfowler.com/bliki/TwoHardThings.html)]

In general we adopt [this](https://medium.com/@alexmngn/how-to-better-organize-your-react-applications-2fd3ea1920f1) strategy with some tweaks.

* `services/foo/index.js` exports everything from `services/foo/foo.service.js`
  - The code lives in `foo.service.js`
* Upper `CamelCase` for Componenets and Collections only
* Lower `camelCAse` for everything else

# Example

    /src
      /components 
        /Button 
        /Notifications
          /components
            /ButtonDismiss  
              /images
              /locales
              /specs 
              /index.js
              /styles.scss
          /index.js
          /styles.scss
      /scenes
        /Home 
          /components 
            /ButtonLike
          /services
            /processData
          /index.js
          /styles.scss
        /Sign 
          /components 
            /FormField
          /scenes
            /Login
            /Register 
              /locales
              /specs
              /index.js
              /styles.scss
      /services
        /api
        /geolocation
        /session
          /actions.js
          /index.js
          /reducer.js
        /users
          /actions.js
          /api.js
          /reducer.js
      index.js 
      store.js

# OUT OF DATE

The rest of this is out of date and probably doesn't apply any more.

# Collections

* Collections are plural, like `Items`, `Products`, `Stories`
* Collections get a `.mutate` namespace like `Stories.mutate`, server side (see the [mutator pattern](https://dweldon.silvrback.com/methods)), these check and call through the collection methods
  - `Stories.mutate.insert()`
  - `Stories.mutate.update()`
  - `Stories.mutate.remove()`
* Collections always `deny()` all, no client side access ever

# Methods

Custom methods to insert / update / remove / etc.

* `story.insert`
* `story.update`
* `story.update.title` - A custom method to update some subset of the whole story
* `story.remove`

# Routes & Components

Both always singular.

## Routes

* `item.index` 
* `item.single`
* `item.new` - create a new `item`
* `item.edit` - edit an existing `item`, requires an `_id`

## Components

We try to follow the route names where possible

* `*Index` - a route level component, a list
* `*Single` - a route level component, show one
* `*View` - a single, full size view of an item
* `*Item` - the card view of an item, usually compressed, optional
  - If the `*Item` component doesn't exist, the `*View` could be used instead
* `*List` - a list of the `*Item` components, a grid for example

### Examples

* `ItemIndex` - the `/items` URL
  - `ItemList` - a list of `items`
    - `ItemItem` - a single card of `item`
* `ItemSingle` - the `/items/:_id` URL
  - `ItemView` - a single `item`
* `ItemNew` - the `/items/new` URL
  - `ItemForm` - the form to create / update an `item`
* `ItemEdit` - the `/items/:_id/edit` URL
  - `ItemForm` - the form to create / update and `item`
* `FooIndex` - the `/foos` URL
  - `FooList` - a list of `foos`, can be used elsewhere
    - `FooItem` - a single card `foo`
* `FooSingle` - the `/foos/:_id` URL
  - `FooView` - a single `foo`

# Publications

Publications are **always** plural, even when publishing only 1 result.

* `stories` - the default stories publication
* `stories.byId` - publish a single story by ID
* `stories.byIds` - publish multiple stories by IDs, an array
* `stories.byAuthorId` - publish stories by `authorId`
* `stories.mine` - publish stories that are "mine"
* `stories.foo` - any other custom story publication
