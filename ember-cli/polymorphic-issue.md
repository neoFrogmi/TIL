# Polymorphic issue
This Post describe a problem with the model's associations in our project with Ember-cli and how it was fixed.

We have an association beetwen two models through a polymorphic association:

### Model Activity:
```js
screens DS.hasMany('screen', {async: true}, {polymorphic: true})
```

### Model Screen:
```js
activity DS.belongsTo('activity', {async: true})
```

The Screen model has two models to extends it.

The problem is when we create a new Screen's child, the association is not updated in the view.

After some research about the problem, I've found an [issue#2065](https://github.com/emberjs/data/issues/2065) in the Ember data repository.

So, the quick fix to this problem is change `Ember.MODEL_FACTORY_INJECTIONS` in app.js from true to false:

```js
Ember.MODEL_FACTORY_INJECTIONS = false;
```

Suggest review this [workaround](https://github.com/hjdivad/data/commit/ba2f46d85fc27bbf38bdce5e20288f6815e34591) in order to understand why the problem remains in the ember version.
