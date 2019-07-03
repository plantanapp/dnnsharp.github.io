# Create Android Message

This action generates the needed JSON configuration for the specific Android push notification parameters. It's output can be passed to the **Firebase - Send push notification** action.

Parameters:

* **Priority** - Sets the priority of the message (high or normal).

* **Collapse Key** - Sets a collapse key for the message. Collapse key serves as an identifier for a group of messages that can be collapsed, so that only the last message gets sent when delivery can be resumed. A maximum of 4 different collapse keys may be active at any given time. Supports tokens.

* **Time to live** - Sets the time-to-live duration of the message. Format: `<days>.<hours>:<minutes>:<seconds>` (e.g. `0.00:10:00`). Supports tokens.

* **Title localization key** - Sets the key of the title string in the app's string resources to use to localize the title text. Supports tokens.

* **Message Title** - Sets the title of the Android notification. When provided, overrides the title set via the Title parameter of the Firebase - Send push notification action. Supports tokens.

* **Body localization key** - Sets the key of the body string in the app's string resources to use to localize the body text. Supports tokens.

* **Message Body** - Sets the body of the Android notification. When provided, overrides the body set via the Body parameter of the Firebase - Send push notification action. Supports tokens.

* **Message Icon** - Sets the icon of the Android notification. Supports tokens.

* **Message Color** - Sets the notification icon color. Supports tokens.

* **Message Sound** - Sets the sound to be played when the device receives the notification. Supports tokens.

* **Message Click Action** - Sets the action associated with a user click on the notification. Supports tokens.