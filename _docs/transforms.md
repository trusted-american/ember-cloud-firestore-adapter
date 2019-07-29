---
layout: doc
title: Transforms
category: Essentials
order: 4
cenchat:
  id: ember-cloud-firestore-adapter_docs
  text: Get help
---

## Timestamp

Timestamp transform is provided as a convenience to [`firebase.firestore.FieldValue.serverTimestamp()`](https://firebase.google.com/docs/reference/js/firebase.firestore.FieldValue#.serverTimestamp).

```javascript
import Model from 'ember-data/model';
import attr from 'ember-data/attr';

export default Model.extend({
  title: attr('string'),
  createdOn: attr('timestamp'),
});
```

In the example above, whenever you save a record who's `createdOn` is not of `Date` instance it will use the server timestamp. Otherwise, it will use that same `Date` instead.

---

[Next: Authentication »](authentication)
