# Sample - Register and receive browser notifications

### 1. Get the required Javascript files and configuration from Firebase Console.

You will need two files, the core firebase SDK and the firebase messaging SDK. You can also follow steps 1 through 3 of the [official Google documentation](https://firebase.google.com/docs/web/setup).
``` html
<!-- The core Firebase JS SDK is always required and must be listed first -->
<script src="https://www.gstatic.com/firebasejs/6.0.1/firebase-app.js"></script>

<!-- TODO: Add SDKs for Firebase products that you want to use
    https://firebase.google.com/docs/web/setup#config-web-app -->
<script src="https://www.gstatic.com/firebasejs/6.0.1/firebase-messaging.js"></script>

<script>
    // setting a timeout to allow the browser to load the above files
    // a document.onload() or $(document).ready() could work as well depending on the situation.
    setTimeout(function() {
        // TODO: Your web app's Firebase configuration (see official docs above to learn how to obtain it)
        var firebaseConfig = {
            apiKey: "api-key",
            authDomain: "project-id.firebaseapp.com",
            databaseURL: "https://project-id.firebaseio.com",
            projectId: "project-id",
            storageBucket: "project-id.appspot.com",
            messagingSenderId: "sender-id",
            appID: "app-id",
        };

        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);

        // TODO1: Register a service worker for background notifications. (see below steps)
        // TODO2: Use the onMessage event to receive foreground notifications. (see below steps)

    }, 1000);
</script>
```

### 2. Request browser registration

To request browser registration use the snippet below. For a better user experience we recommended calling the code upon user interaction - e.g. button click.

``` js
var messaging = firebase.messaging();
messaging.requestPermission()
.then(function() {
    messaging.getToken()
    .then(function(token) {
        console.log('user token:', token);
        // TODO: Store the token somewhere (like the server, or browser local storage)
        //localStorage.setItem("subtoken", token);
    });
});
```

### 3. Configure the browser to receive messages

To be [able to receive foreground or background notifications](https://firebase.google.com/docs/cloud-messaging/js/topic-messaging#handle_messages_when_your_web_app_is_in_the_foreground) you must define a Firebase messaging service worker.

Prerequisites for a service worker:
1. The website must have a `manifest.json` file defined.
2. The website must be served through HTTPS.
3. Browser support. Service workers are supported by Chrome, Firefox, Opera, Microsoft Edge and Safari. You can see all the browsers on the [Can I Use](https://caniuse.com/#feat=serviceworkers) site.

Add the following to the website `manifest.json`. Make sure to add the browser sender ID exactly as shown (do not change the value). [Docs](https://firebase.google.com/docs/cloud-messaging/js/client#configure_the_browser_to_receive_messages)
``` json
{
  "gcm_sender_id": "103953800507"
}
```
For improved user experience you could also specify [PWA related parameters](https://developers.google.com/web/fundamentals/web-app-manifest/) in the `manifest.json` file. Follow the docs to [test your manifest](https://developers.google.com/web/fundamentals/web-app-manifest/#test). Here is an example.
``` json
{
    "short_name": "My App",
    "name": "My Demo App",
    "display": "standalone",
    "start_url": "<start page for your app>",

    "gcm_sender_id": "103953800507"
}
```

### 4. Register a service worker for background notifications.

Create a new .js file on your website with the following code. Let's name it `fcm_sw.js`.
``` javascript
importScripts('https://www.gstatic.com/firebasejs/4.8.1/firebase-app.js');
importScripts('https://www.gstatic.com/firebasejs/4.8.1/firebase-messaging.js');

// Fixes `Service worker does not have the 'fetch' handler` error for PWA service workers
self.addEventListener('fetch', function(event) {
    //console.log('Service Worker fetch event url', event.request.url);
});

// Initialize the Firebase app in the service worker by passing in the
// messagingSenderId.
// TODO: Add your web app's Firebase configuration
firebase.initializeApp({
    apiKey: "api-key",
    authDomain: "project-id.firebaseapp.com",
    databaseURL: "https://project-id.firebaseio.com",
    projectId: "project-id",
    storageBucket: "project-id.appspot.com",
    messagingSenderId: "sender-id",
    appID: "app-id",
});

// Retrieve an instance of Firebase Messaging so that it can handle background
// messages.
const messaging = firebase.messaging();

```

Add the following code in place of *TODO1* in the snippet from step 1.
``` js
navigator.serviceWorker
    .register('fcm_sw.js')
    .then((registration) => {
        firebase.messaging().useServiceWorker(registration);
    });
```

When background messages are received the default browser/OS notification will popup.

### 5. Use the onMessage event to receive foreground notifications.

Add the following code in place of *TODO2* in the snippet from step 1.
``` js
var messaging = firebase.messaging();
messaging.onMessage(function(payload) {
    console.error('Message received. ', payload);
});
```

**Note:** When the app is in foreground, **the default browser/OS notification will NOT be shown**, instead you will have to handle that yourself inside the onMessage event handler by triggering some kind of UI element in your site / browser window.