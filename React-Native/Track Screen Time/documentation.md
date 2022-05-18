**Challenge:** Track screen time of a user in the app

**solution**:
We can track the state of the app using AppState from react native.

```
import React, { useState } from 'react';
import {AppState} from 'react-native';

const appState = useRef(AppState.currentState);
const [appStateVisible, setAppStateVisible] = useState(appState.current);

useEffect(() => {
  const subscription = AppState.addEventListener('change', (nextAppState) => {
    appState.current = nextAppState;
    setAppStateVisible(appState.current);
  });

  return () => {
    subscription.remove();
  };
}, []);

```

The appState will return as "active" or "background". Based on this, we can write custom logic to track the time.

**Related Links:**

1. https://www.innoviacolabs.com/blog/how-to-calculate-screen-time-in-react-native
