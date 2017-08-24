# ti-widow-stack

Manage iPhone and Android windows in same code base.

## Get it [![gitTio](http://gitt.io/badge.svg)](http://gitt.io/component/ti-window-stack)

Download the latest distribution [ZIP-file](https://github.com/HazemKhaled/TiWidowStack/releases) and consult the [Titanium Documentation](http://docs.appcelerator.com/titanium/latest/#!/guide/Using_a_Module) on how install it, or simply use the [gitTio CLI](http://gitt.io/cli):

`$ gittio install ti-window-stack`

## Public methods

### `setNavigationWindow(_navigationWindow)`

Set external created NavigationWindow.

* ___navigationWindow__ `Ti.UI.iOS.NavigationWindow` NavigationWindow to set.

### `setTargetInDrawer(targetInDrawer)`

Setter of targetInDrawer.

* __targetInDrawer__ `Number` Constants: `WindowStack.CENTER_WINDOW`, `WindowStack.RIGHT_WINDOW` or `WindowStack.LEFT_WINDOW`.

### `open(_window, drawer, params)`

Open window into the stack, you can pass instance from nl.fokkezb.drawer to open this window into drawer center window.

* ___window__ `Ti.UI.Window/Ti.UI.View` Window or View to open.
* __drawer__ `nl.fokkezb.drawer` Drawer instance. (Optional)
* __params__ `openWindowParams` Animation or display properties to use when opening the window. (Optional)

### `getSize()`

Retrieve the size of the current window stack as a `Number`.

### `isRootLevel()`

Clarify if the current stack has more than one root level or not by returning a `Boolean`.

### `isNotRootLevel()`

Clarify if the current stack has more than one root level or not by returning a `Boolean`.

### `close(_window)`

Pop a specific `Ti.UI.Window` from the stack.

* ___window__ `Ti.UI.Window/Ti.UI.View` Window or View to close.

### `back()`

Closes the most recent openned `Ti.UI.Window` in the stack.

### `home(_params)`

By default, closes all the windows, one after the other, starting for the current window. User sees all the windows getting closed.

* ___params__ `Array` _params.animated: Controls wether to animate when all windows are getting closed or not.

### `destroy(drawer, closeCallBack)`

Close all Windows, close the navigationWindow or drawer.

* __drawer__ `nl.fokkezb.drawer` Drawer to close. (Optional)
* __closeCallBack__ `Callable` Will call it after close last screen. (Optional)

## Events

Whenever a `Ti.UI.Window` is openned or closed by our library, we'll trigger a `ti-window-stack:sizechanged` event which payload will be the one coming from the according Titanium event `open` or `close`.

This is pretty useful when you want to listen to the size of the stack and act upon within the UI of your application. Let's say you have a main menu button visible or not within the UI and you'd like to inject it or not depending on how many levels your stack has:

```js
$.window.addEventListener('ti-window-stack:sizechanged', function (e) {
    if (Alloy.Globals.windowStack.getSize() > 0) {
        // e.source --> Ti.UI.Window
        e.source.LeftNavButton = Alloy.createController("menuButton").getView();
    }
});
```

## Examples

### [Example #1](https://github.com/HazemKhaled/SideMenu-with-NavigationWindow-for-Titanium)

Side menu example using [Fokke Drawer Widget](http://gitt.io/component/nl.fokkezb.drawer) over [NappDrawer](http://gitt.io/component/dk.napp.drawer) or [DrawerLayout](https://github.com/manumaticx/Ti.DrawerLayout) ![gif](https://raw.githubusercontent.com/hazemkhaled/SideMenu-with-NavigationWindow-for-Titanium/master/screens/iphone.gif) ![gif](https://raw.githubusercontent.com/hazemkhaled/SideMenu-with-NavigationWindow-for-Titanium/master/screens/android.gif)

### [Example #2](https://github.com/HazemKhaled/TiTODOs)

Simple Todo app

![gif](https://raw.githubusercontent.com/hazemkhaled/TiTODOs/master/screen.gif)

## How to

Check [#Examples](#examples) for now

## Contributions

Your issues and pull requests are most welcome.

### Changelog

**v1.1.4**

* Untabify (using 4 spaces tabs).
* Adding public function `size()`.
* Change the order we interact with the stack before opening a new window.
* Linting + documentation.

**v1.1.3**

* Fix back compatibility with iOS 9.3.

**v1.1.2**

* Now home function can work without the noisy effect, thanks [@Claymm](https://github.com/Claymm).
* Fix bug with Titanium SDK 5.5.0.GA.

**v1.1.1**

* Fix destroy on Android can't call callback function.

**v1.1.0**

* Allow to manage right or left side menus window stack, [related issue](https://github.com/viezel/NappDrawer/issues/188): `windowStack.setTargetInDrawer(windowStack.LEFT_WINDOW);`.

**v1.0.4**

* Fix window can't close on Android.

**v1.0.3**

* Better implementation for home method.

**v1.0.2**

* Small fix for center window menu in Android.

**v1.0.1**

* Now you can modify Android menu of the drawer container window directly from your center view.

**v1.0.0**

* First version with home, back and destroy methods.
