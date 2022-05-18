**Challenge:**
Deep linking - user will navigate to a specific page when clicking on a link outside the app

**Solution:**

**Configuring Android:**

First, we need to open our Manifest file and add the app name we will want to be referencing, in our case peopleapp.
In android/app/src/main, open AndroidManifest.xml and add the following intent filter below the last intent filter already listed, within the `<activity>` tag:

```
<intent-filter android:label="filter_react_native">
  <action android:name="android.intent.action.VIEW" />
  <category android:name="android.intent.category.DEFAULT" />
  <category android:name="android.intent.category.BROWSABLE" />
  <data android:scheme="peopleapp" android:host="people" />
</intent-filter>
```

The `<data>` tag specifies the URL scheme which resolves to the activity in which the intent filter has been added. In this example the intent filter accepts URIs that begin with peopleapp://people.
That is all we need as far as configuration goes. To test this out, open Android Studio. Open Run -> Edit Configurations and change the launch options to URL, passing in the following url: peopleapp://people/1

To redirect the user to different screens based on the URL:

```
 import { Linking } from 'react-native';
 useEffect(() => {
    Linking.getInitialURL().then((url: any) => {
      if (url) {
        const modifiedURL = url.replace(/.*?:\/\//g, '');
        const linkType = modifiedURL.split('/')[1];
        const id = modifiedURL.split('/')[2];
        if (linkType === 'n') {
          navigation.navigate('ReadEnd', {
            selectedNarrationID: id,
          });
        } else if (linkType === 'i') {
          navigation.navigate('MyContacts', {
            invitationID: id,
          });
        }
      }
    });
  }, []);
```

**Related Links:**

1. https://medium.com/react-native-training/deep-linking-your-react-native-app-d87c39a1ad5e
2. https://reactnavigation.org/docs/deep-linking
