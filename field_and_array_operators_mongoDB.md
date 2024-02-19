# MongoDB Update Operators

- [Field Update Operators](#field-update-operators)
  - [$setOnInsert](#setoninsert)
  - [$unset](#unset)
- [Array Update Operators]()
  - [$]()
  - [$[]]()
  - [$[&lt;identifier&gt;]]()
  - [$addToSet]()
  - [$pop]()

## `$setOnInsert`

If an update operation with upsert: true results in an insert of a document, then `$setOnInsert` assigns the specified values to the fields in the document. If the update operation does not result in an insert, `$setOnInsert` does nothing.

### Syntax

```javascript
db.collection.updateOne(
   <query>,
   { $setOnInsert: { <field1>: <value1>, ... } },
   { upsert: true }
)
```

MongoDB uses `<query>` to create a new document with `_id: 1. $setOnInsert` updates the document as specified.

Insert a new document using `db.collection.updateOne()` the `{upsert: true}` parameter.

```javascript
use world
```

#### With upsert attribute

```javascript
// if document with this index is not present in collection

db.test.updateOne(
  { index: 3 },
  {
    $set: { item: "apple" },
    $setOnInsert: { defaultQty: 100 },
  },
  { upsert: true }
);
```
#### Without upsert attribute
```javascript
db.test.updateOne(
  { index: 3 },
  {
    $set: { item: "apple" },
    $setOnInsert: { defaultQty: 100 },
  }
)
```



## `$unset`

The `$unset` operator deletes a particular field.

### Syntax 
```javascript
{ $unset: { <field1>: "", ... } }
```

### Example

```javascript
db.products.insertMany( [
   { "item": "chisel", "sku": "C001", "quantity": 4, "instock": true },
   { "item": "hammer", "sku": "unknown", "quantity": 3, "instock": true },
   { "item": "nails", "sku": "unknown", "quantity": 100, "instock": true }
] )
```
Update the first document in the products collection where the value of sku is unknown:

```javascript
db.products.updateOne(
   { sku: "unknown" },
   { $unset: { quantity: "", instock: "" } }
)
```
updateOne() uses the `$unset` operator to: 
- remove the quantity field
- remove the instock field

Check it : 
```
db.products.find({});
```


## `$` Positional operator
Acts as a placeholder to update the first element that matches the query condition.

The `positional $ operator` identifies an element in an array to update without explicitly specifying the position of the element in the array.

### Syntax
```javascript
{ "<array>.$" : value }
```

the `positional $  operator` acts as a placeholder for the first element that matches the query document, and the array field must appear as part of the query document.

## `$[]`
Acts as a placeholder to update all elements in an array for the documents that match the query condition.
## `$[<identifier>]`
Acts as a placeholder to update all elements that match the arrayFilters condition for the documents that match the query condition.
## `$addToSet`
Adds elements to an array only if they do not already exist in the set.
## `$pop`
Removes the first or last item of an array.