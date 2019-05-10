# Create iOS Message

This action generates the needed JSON configuration for the specific iOS push notification parameters. It's output can be passed to the **Firebase - Send push notification** action.

Parameters:

* **Thread Id** - Sets the app-specific identifier for grouping notifications. Supports tokens.

* **Category** - Sets the type of the notification. Supports tokens.

* **Mutable Content** - Sets a value indicating whether to include the mutable-content property in the message. Supports tokens.

* **Badge** - Sets the badge to be displayed with the message. Supports tokens.

* **Title localization key** - Sets the key of the title string in the app's string resources to use to localize the title text. Supports tokens.

* **Message Title** - Sets the title of the alert. When provided, overrides the title set via the Title parameter of the Send Firebase push notification action. Supports tokens.

* **Subtitle localization key** - Sets the key of the subtitle string in the app's string resources to use to localize the subtitle text. Supports tokens.

* **Message Subtitle** - Sets the subtitle of the alert. When provided, overrides the title set via the Title parameter of the Send Firebase push notification action. Supports tokens.

* **Body localization key** - Sets the key of the body string in the app's string resources to use to localize the body text. Supports tokens.

* **Message Body** - Sets the body of the alert. When provided, overrides the body set via the Body parameter of the Send Firebase push notification action. Supports tokens.

* **Message Launch Image** - Sets the launch image for the notification action. Supports tokens.

* **Message Action Localization Key** - Sets the key of the text in the app's string resources to use to localize the action button text. Supports tokens.

* **Message Sound** - Sets the name of a sound file in your app's main bundle or in the Library/Sounds folder of your app's container directory. Supports tokens.