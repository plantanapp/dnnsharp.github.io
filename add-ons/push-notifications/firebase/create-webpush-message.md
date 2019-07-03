# Create WebPush Message

This action generates the needed JSON configuration for the specific Web Push notification parameters. It's output can be passed to the **Firebase - Send push notification** action.

Parameters:

* **Direction** - Sets the direction in which to display the notification. Supported EXPR values: Auto, LeftToRight and RightToLeft. Supports tokens.

* **Renotify** - Boolean value. Sets whether the user should be notified after a new notification replaces an old one. Supports tokens.

* **Require Interaction** - Boolean value. Sets whether the notification should remain active until the user clicks or dismisses it, rather than closing it automatically. Supports tokens.

* **Silent** - Boolean value. Sets whether the notification should be silent. Supports tokens.

* **Badge** - Sets the URL of the image used to represent the notification when there is not enough space to display the notification itself. Supports tokens.

* **Message Title** - Sets the title text of the notification. When provided, overrides the title set via the Title parameter of the Send Firebase push notification action. Supports tokens.

* **Message Body** - Sets the body text of the notification. When provided, overrides the body set via the Body parameter of the Send Firebase push notification action. Supports tokens.

* **Message Icon** - Sets the URL to the icon of the notification. Supports tokens.

* **Message Image** - Sets the URL of an image to be displayed in the notification. Supports tokens.

* **Message Tag** - Sets an identifying tag for the notification. Supports tokens.

* **Message Actions** - Sets a collection of WebPush notification actions. You can define the name, title and icon (in URL format) of the action. Supports tokens.