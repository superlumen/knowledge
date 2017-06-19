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
