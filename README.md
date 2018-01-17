This is a PURE copy of the porthole library proposed by TernaryLabs [View Original Repo](https://github.com/ternarylabs/porthole) to make it available via npm.

### Installation
```bash
npm install porthole-proxy --save
```

> For you convenience, here is a copy of the Readme file of the library. 
> I only updated the `<script>` tag to make it consistent with the `node_modules` hierarchy.

---
Porthole is a small library for secure cross-domain iFrame communication.

### Usage
Include the Javascript.

```html
<script type="text/javascript" src="node_modules/porthole-proxy/lib/porthole.min.js"></script>
```

Create your content iFrame. This is where the guest content lives. Make sure to give it a name.

```html
<iframe id="guestFrame" name="guestFrame" src="http://other-domain.com/">
</iframe>
```

Define an event handler if you want to receive messages.

```javascript
function onMessage(messageEvent) {  
    /*
   messageEvent.origin: Protocol and domain origin of the message
   messageEvent.data: Message itself
   messageEvent.source: Window proxy object, useful to post a response 
   */
}
```

Create a window proxy object on the main page.

```javascript
var windowProxy;
window.onload=function(){ 
    // Create a proxy window to send to and receive 
    // messages from the iFrame
    windowProxy = new Porthole.WindowProxy(
        'http://other-domain.com/proxy.html', 'guestFrame');

    // Register an event handler to receive messages;
    windowProxy.addEventListener(onMessage);
};
```

Create a window proxy object in the iFrame.

```javascript
var windowProxy;
window.onload=function(){ 
    // Create a proxy window to send to and receive 
    // messages from the parent
    windowProxy = new Porthole.WindowProxy(
        'http://parent-domain.com/proxy.html');

    // Register an event handler to receive messages;
    windowProxy.addEventListener(function(event) { 
        // handle event
    });
};
```

Send a message.

```javascript
windowProxy.post({'action': 'supersizeme'});
```

Note that if you have multiple iFrames, you can create as many WindowProxy objects as needed.

### Update
	
The library has been updated. It is not compatible with previous versions.

* Support JSON serialization
* Bug fix for IE 8
* Bug fix for multiple event handler in native browser support.

### Unit Tests
	rake jasmine

### Demo
<http://sandbox.ternarylabs.com/porthole/>

### Project Page
<http://ternarylabs.github.com/porthole/>