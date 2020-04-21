The iOS app supports deep links, which allows users to open the app with a
link so it immediately opens a library or content.

For example : 
- for content: `<a
href="salesmatik-public://www.dink.eu/deep_links?libraryId=fdbb0915-dd70-4f66-a212-32b6e0b3730c"
target="_blank">Open the library</a>`

- for library: `<a
href="salesmatik-public://www.dink.eu/deep_links?contentId=50344027-cbca-4cba-8e9e-5718fe4479ec"
target="_blank">Open some content</a>`

- use 'salesmatik-public://' to open the app on the default landing screen

Every app we build will have its own url scheme. salesmatik-public is the custom scheme for the App Store app.
