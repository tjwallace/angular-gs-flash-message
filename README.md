# angular-gs-flash-message

[![Build Status](https://secure.travis-ci.org/garbles/angular-gs-flash-message.png?branch=master)](https://travis-ci.org/garbles/angular-gs-flash-message)

Frictionless flash messages for your AngularJS application. The `gs-flash-messages` directive is setup to support cross state flash messages.

### Installing

`bower install angular-gs-flash-message`

### Using

Include the package in your application:

```javascript
angular.module('app', ['gs.flash-message']);
```

Add the directive to your DOM and give it a name, _e.g._ `gabe`. You can have as many as you want (nesting?).

```html
<div data-gs-flash-messages="gabe"></div>
```

If you need to set the flash message and do not need to change state, use `$rootScope` to send a message.

```javascript
// depending on how the directive is set relative to where you are sending the message
// you may need to use either $rootScope.$emit or $rootScope.$broadcast
// see this for more information: https://docs.angularjs.org/api/ng/type/$rootScope.Scope

// notice how I used the same name as the directive
$rootScope.$emit('flash:gabe', {success: 'This is a success message.', error: 'This is an error message.'});
```

If you need to set the flash message after making a state change, set the `flash` key on the `$state.params` before transitioning.
```javascript
$state.params.flash = {
  // notice how I used the same name as the directive
  gabe: {
    success: 'This is a success message.',
    error: 'This is an error message.'
  }
}
```

Changing your state will otherwise always cause all open flash messages to close.
