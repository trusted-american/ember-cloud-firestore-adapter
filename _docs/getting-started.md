---
layout: doc
title: Getting Started
category: Introduction
order: 2
cenchat:
  id: ember-cloud-firestore-adapter_docs
  text: Get help
---

This addon is compatible with Ember v3.x and above but the docs assumes that you're using at least Ember and Ember Data v3.11.

## Installation

This addon requires some peer dependencies. Install the correct versions of each package, which are listed by the command:

```bash
npm info ember-cloud-firestore-adapter peerDependencies
```

Once you've installed it, you can now install the addon itself:

```bash
ember install ember-cloud-firestore-adapter
```

## Configuration

### 1. Setup Firebase Configuration

Add a firebase property in your config/environment.js.

```javascript
let ENV = {
  ...

  firebase: {
    apiKey: '<api_key>',
    authDomain: '<auth_domain>',
    databaseURL: '<database_url>',
    projectId: '<project_id>',
    storageBucket: '<storage_bucket>',
    messagingSenderId: '<messaging_sender_id>'
  },

  ...
}
```

### 2. Create Your Application Adapter

Create an application adapter by running:

```bash
ember generate adapter application
```

Change it to look something like this:

```javascript
import CloudFirestoreAdapter from 'ember-cloud-firestore-adapter/adapters/cloud-firestore';

export default CloudFirestoreAdapter.extend({
  referenceKeyName: 'foobar',
});
```

#### Adapter Settings

These are the settings currently available:

  - `firestoreSettings` - An object specifying the custom configurations for your Cloud Firestore instance. See [here](https://firebase.google.com/docs/reference/js/firebase.firestore.Settings). (Defaults to null)
  - `referenceKeyName` - Name of the field that will indicate whether a document is a reference to another one. (Defaults to `referenceTo`)

---

[Next: Data Structure »](data-structure)
