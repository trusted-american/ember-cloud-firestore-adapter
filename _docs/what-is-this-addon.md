---
layout: doc
title: What's This Addon?
category: Introduction
order: 1
cenchat:
  id: ember-cloud-firestore-adapter_docs
  text: Get help
---

This is an unofficial Ember Data Adapter and Serializer for Cloud Firestore. It's completely unrelated to [EmberFire](https://github.com/firebase/emberfire) but it's purpose is the same.

## Features

Similar to EmberFire, it supports:

- **Customizable data structure** - There's an opinionated default on how your data will be structured but there's enough API to make it fit to your existing ones
- **Realtime bindings** - Listen to realtime updates easily
- **Authentication** - Integrate [Firebase Authentication](https://firebase.google.com/products/auth/) powered by [Ember Simple Auth](https://github.com/simplabs/ember-simple-auth)
- **FastBoot** - Perform server-side rendering to speed up your boot time

## Why Was This Built?

This was built becase EmberFire development is super slow. It was in fact believed to be abandoned at one point. As an example, the next commit from the core maintainers after v2 was released took roughly 1 year. Also, an overhaul of EmberFire for v3 is now in the works but it's been in release candidate state for 6 months now.

In order to continue development with Ember and Cloud Firestore, I had to build this addon and make it generic enough to be used by other developers too.

---

[Next: Getting Started »](getting-started)
