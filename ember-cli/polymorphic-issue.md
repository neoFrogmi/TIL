# Polymorphic issue
This Post describe a problem with the model's associations in our project with Ember-cli and how was fixed.

In our project, we have an association beetwen two models through a polymorphic association:

### Model Activity:
screens DS.hasMany('screen', {async: true}, {polymorphic: true})

### Model Screen:
activity DS.belongsTo('activity', {async: true})

This model (Screen) has two models that extends it.

The problem is that when create a new Screen's child, the association is not updated in the view.

After searching the problem, I found this issue in the Ember data repository:

https://github.com/emberjs/data/issues/2065

So the solution to this problem is change this boolen in app.js from true to false:

Ember.MODEL_FACTORY_INJECTIONS = false;



### I consider important to review the fix:
https://github.com/hjdivad/data/commit/ba2f46d85fc27bbf38bdce5e20288f6815e34591

To understand why the problem remains in the ember version that we used in our project.
