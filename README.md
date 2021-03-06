# Analysis Tool for Teambition

## Usage

First, use Bower to install GTA:

```bash
bower install gta
```

or with NPM:

```bash
npm install --save teambition/gta
```

Then, include the following script in your HTML and you are ready to go:

```html
<script id="gta-main"
  src="bower_component/gta/lib/index.js"
  data-baidu="ec912ecc405ccd050e4cdf452ef4xxxx"
  data-google="UA-3318xxxx-1"
  data-mixpanel="77e13d08ba42fe31932a1f1418aea7b2"
  data-customer="2ac3fd02efd1f9c57ae9"
  data-tbtracking="your actions path"
></script>
```

### Set User ID
```js
// Currently only Customer.io and Fullstory support userId
gta.setUser(id, user)
```

### Register Property
```js
gta.registerProperty(key, value)
gta.unregisterProperty(key)
```
All registered properties would be mixed with every events util unregister.

### Register Provider
```js
gta.registerProvider(name, Provider, $el)
```
Register third party provider. `$el` points to element stores gta config,
it could be omitted when config stores in `<script id='gta-main'>`.

### Register Plugin
```js
gta.registerPlugin(Plugin)
```
A plugin cloudn't be unregistered now, returns plugin instance.

### Set Current Page
```js
// Set the current page, default value of the 'page' field while invoking gta.events(gtaOptions)
gta.setCurrentPage('Home Page')
```

### Page View

Call the `pageview` function to record a new page view:
```js
// Use single object
gta.pageview({
    'page': '/my-overridden-page?id=1',
    'title': 'my overridden page'
})

// Use multiple string
gta.pageview('/api/hello', '?world');
```

### Events
#### Tips: 'page' equals to 'category' in old rules, 'type' equals to 'label' in old rules.

1. `data-gta` property in DOM element use similar key-value format (`{"key": "value"}`) like JSON, and quota could be omitted.
2.  Colon, comma and quota cannot be used in `key` and `value`.

You can set current page `page`, it will be automatically added to the gtaOptions:
```js
// It is usually called when the route change
gta.setCurrentPage('Tasks Page')
```

You can call the `event` function to track an event:
```js
gta.event({action: 'add content', page: 'Project Page', type: 'task', control: 'tasks layout', method: 'double-click'})
```

either add `data-gta='event'` to a DOM element as:
```html
<button data-gta="{action: 'add content', page: 'Project Page', type: 'task', control: 'tasks layout', method: 'double-click'}">click</button>
```

or preloading actions to format as:

1. `data-gta-hash` property in DOM element use to load actions.
```html
<script id="gta-main"
  ...
  data-tbtracking="your actions path"
></script>
```
2. `hash` is the target in your acions list.

```html
actions = [
  ...,
  {
    hash: hash
    action: 'add content',
    control: 'tasks layout',
    type: 'task',
  }
]

<button data-gta-hash="${hash}">click</button>
```

To automatically log gtaOptions, you can use the 'debug' mode:
```js
gta.debug = true
or
window._gta_debug = true
```
#### Warning! old rules not supported since v0.8.0

## API Documentations

* [Google Analytics](https://developers.google.com/analytics/devguides/collection/analyticsjs/)
* [Baidu Analytics](http://tongji.baidu.com/open/api/more?p=ref_trackPageview)
* [Mixpanel](https://mixpanel.com/help/reference/javascript)
* [Customer.io](https://customer.io/docs/api/javascript.html)
* [Fullstory](http://help.fullstory.com/using-ref/getting-started)
* [GrowingIO](https://help.growingio.com/Developer%20Document.html)
* [SensorsData](https://www.sensorsdata.cn/manual/js_sdk.html)

## Change Log

### 1.1.6
1. Support boot params for providers

### 1.1.5
1. Add `gta.login(userId)` support
2. Implement `login` method on TBPanel

#### 1.1.4
1. Add `data-tbtracking` support

#### 1.1.1 - 1.1.2
1. New Plugin: `distinct id`

#### 1.1.0
1. New provider: SensorsData

#### 1.0.12
1. Deferred provider loading

#### 1.0.11
1. Disable `displayfeatures` for Google Analytics

#### 1.0.9 - 1.0.10
1. Plugin `referral` and `utm` will only record at first time.
2. Plugin `referral` and `utm` now use encodeURIComponent to prevent unexpected cookie cut off.

#### 1.0.8
1. Plugin is able to filter event now.

#### 1.0.7
1. New plugin `referral plugin`

#### 1.0.5 - 1.0.6
1. `gta.registerPlugin` now returns plugin's instance

#### 1.0.4
1. TBPanel now accepts optional `scriptUrl`

#### 1.0.3
1. New API: `registerProvider`

#### 1.0.2
1. Now library can be exported to `window.Gta`

#### 1.0.1
1. Fix GTA crash when provider Baidu crash.

#### 1.0.0
1. New architecture
2. New APIs: `(un)register(Property|Plugin)`
