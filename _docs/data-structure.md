---
layout: doc
title: Data Structure
category: Introduction
order: 3
cenchat:
  id: docs
  text: Get help
---

There's an opinionated default on how this addon will structure your Cloud Firestore data. More of it will be explained below but basically:

  - Documents are stored under a collection derived from their camelized and pluralized model name (e.g. `user` = `users`, `city` = `cities`, and `blog-post` = `blogPosts`)
  - Attributes are camelized
  - Relationships are stored as `Reference` [data type](https://firebase.google.com/docs/firestore/manage-data/data-types#data_types) instead of their IDs
  - One-to-many relationships are only persisted in the `belongsTo` side.

There are however, APIs that would allow the adapter to consume whatever data structure that you already have.

## Example Data

Below demonstrates some simple Ember Data models and how they'd look like when persisted in Cloud Firestore.

### Group Model

```javascript
import Model, { attr, hasMany } from '@ember-data/model';

export default Model.extend({
  name: attr('string'),
  posts: hasMany('post'),
  members: hasMany('user')
});
```

### Post Model

```javascript
import Model, { attr, belongsTo } from '@ember-data/model';

export default Model.extend({
  body: attr('string'),
  createdOn: attr('timestamp'),
  title: attr('string'),
  author: belongsTo('user'),
  group: belongsTo('group')
});
```

### User Model

```javascript
import Model, { attr, hasMany } from '@ember-data/model';

export default Model.extend({
  name: attr('string'),
  groups: hasMany('group'),
  posts: hasMany('post')
});
```

### Persisted Structure

```json
{
  "groups": {  // Root-level collection
    "group_a": {
      "name": "Group A",

      "members": {  // Subcollection
        "user_a": {
          "referenceTo": "<reference to users/user_a>"
        }
      }
    }
  },

  "posts": { // Root-level collection
    "post_a": {
      "body": "Post A Body",
      "createdOn": "January 1, 2017 at 12:00:00 AM UTC+8",
      "title": "Post A Title",
      "author": "<reference to users/user_a>",
      "group": "<reference to groups/group_a>"
    }
  },

  "users": {  // Root-level collection
    "user_a": {
      "name": "User A",

      "groups": {  // Subcollection
        "group_a": {
          "referenceTo": "<reference to groups/group_a>"
        }
      }
    }
  }
}
```

Notes:
  - Notice that we don't have a `posts` subcollection in `groups/group_a` and `users/user_a`. This is because in one-to-many relationships, only the `belongsTo` side gets persisted.
  - Relationships are saved as `Reference` [data type](https://firebase.google.com/docs/firestore/manage-data/data-types#data_types) instead of its ID of type string.
  - `referenceTo` is a **reserved** attribute to indicate that a field is a reference to another document. You can configure this to be named as something else. This works as follows:
    - When you fetch a `Group` document under `users/user_a/groups/group_a` and it has a `referenceTo` property to `groups/group_a`, it will return the document under that instead.
    - If the `referenceTo` doesn't exist, it would return the `users/user_a/groups/group_a` as the document.

---

[Next: Finding Records »](finding-records)
