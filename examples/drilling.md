![Prop Drilling](https://youtu.be/9gQutLF95Vo?si=i_a6in3RMM2JvkXR)


<!-- 
```js

import React, { useState } from "react";
import "./styles.css";

const SettingsPanel = () => {
  const [userName, setUserName] = useState("Alice");
  const [userAge, setUserAge] = useState(28);
  return <UserProfile />;
};

// Then we need to pass the props all the way down so UserFields has those values
const UserProfile = () => {
  return <UserForm />;
};

// Another intermediate component that simply passes the props down.
const UserForm = () => {
  return <UserFields />;
};

// The final component that actually needs the data to display the form fields.
const UserFields = () => {
  return (
    <div>
      <p>age: {userAge}</p>
      <p>username: {userName}</p>
    </div>
  );
};

export default function App() {
  return <SettingsPanel />;
}

```

```js

import React, { useState } from "react";
import "./styles.css";

const SettingsPanel = () => {
  const [userName, setUserName] = useState("Alice");
  const [userAge, setUserAge] = useState(28);
  return <UserProfile userName={userName} userAge={userAge} />;
};

// Then we need to pass the props all the way down so UserFields has those values
const UserProfile = ({ userName, userAge }) => {
  return <UserForm userName={userName} userAge={userAge} />;
};

// Another intermediate component that simply passes the props down.
const UserForm = ({ userName, userAge }) => {
  return <UserFields userName={userName} userAge={userAge} />;
};

// The final component that actually needs the data to display the form fields.
const UserFields = ({ userName, userAge }) => {
  return (
    <div>
      <p>age: {userAge}</p>
      <p>username: {userName}</p>
    </div>
  );
};

export default function App() {
  return <SettingsPanel />;
}

```

```js
import React, { useState } from "react";
import "./styles.css";

const SettingsPanel = () => {
  const [userName, setUserName] = useState("Alice");
  const [userAge, setUserAge] = useState(28);
  const [userIsDarkMode, setUserIsDarkMode] = useState(false);
  return (
    <UserProfile
      userName={userName}
      userAge={userAge}
      userIsDarkMode={userIsDarkMode}
      setUserIsDarkMode={setUserIsDarkMode}
    />
  );
};

const UserProfile = ({ userName, userAge, userLocation, userWeather, userIsDarkMode, setUserIsDarkMode }) => {

  return (
    <UserForm
      userName={userName}
      userAge={userAge}
      userIsDarkMode={userIsDarkMode}
      setUserIsDarkMode={setUserIsDarkMode}
    />
  );
};

const UserForm = ({
  userName,
  userAge,
  userIsDarkMode,
  setUserIsDarkMode
}) => {
  return (
    <UserFields
      userName={userName}
      userAge={userAge}
      userIsDarkMode={userIsDarkMode}
      setUserIsDarkMode={setUserIsDarkMode}
    />
  );
};

const UserFields = ({
  userName,
  userAge,
  userIsDarkMode,
  setUserIsDarkMode
}) => {
  return (
    <div
      style={{
        backgroundColor: userIsDarkMode ? "#000" : "",
        color: userIsDarkMode ? "#fff" : "#000"
      }}
    >
      <h2>{userName}</h2>
      <h3>{userAge}</h3>
      <button onClick={() => setUserIsDarkMode(!userIsDarkMode)}>
        Toggle Dark Mode
      </button>
    </div>
  );
};

export default function App() {
  return <SettingsPanel />;
}
```


```js
import React, { useState } from "react";
import "./styles.css";

const SettingsPanel = () => {
  const [userName, setUserName] = useState("Alice");
  const [userState, setUserState] = useState("TX");
  const [userIsDarkMode, setUserIsDarkMode] = useState(false);
  return (
    <UserProfile
      userName={userName}
      userState={userState}
      userIsDarkMode={userIsDarkMode}
      setUserIsDarkMode={setUserIsDarkMode}
    />
  );
};

const UserProfile = ({
  userName,
  userState,
  userIsDarkMode,
  setUserIsDarkMode
}) => {

  return (
    <UserForm
      userName={userName}
      userState={userState}
      userIsDarkMode={userIsDarkMode}
      setUserIsDarkMode={setUserIsDarkMode}
    />
  );
};

const UserForm = ({
  userName,
  userState,
  userIsDarkMode,
  setUserIsDarkMode
}) => {
  return (
    <UserFields
      userName={userName}
      userState={userState}
      userIsDarkMode={userIsDarkMode}
      setUserIsDarkMode={setUserIsDarkMode}
    />
  );
};

const UserFields = ({
  userName,
  userState,
  userIsDarkMode,
  setUserIsDarkMode
}) => {
  return (
    <div
      style={{
        backgroundColor: userIsDarkMode ? "#000" : "",
        color: userIsDarkMode ? "#fff" : "#000"
      }}
    >
      <h2>{userName}</h2>
      <h3>{userState}</h3>
      <h3>Location</h3>
      <p>lat: {userLocation.lat}</p>
      <p>lat: {userLocation.long}</p>
      <p>{userWeather}</p>
      <button onClick={() => setUserIsDarkMode(!userIsDarkMode)}>
        Toggle Dark Mode
      </button>
    </div>
  );
};

export default function App() {
  return <SettingsPanel />;
}
```
Updating is also a lot of work!

There are many downsides to prop drilling and thats why most people consider it an anti pattern in react. 
Function testing as well as composition are harder because you have this chain of props to consider when testing or rendering a component in isolation

To solve this prop passing we can introduce a state management library, such as redux, mobX, or context. For our solution we will utilize context.

Solution Context:


* lets go ahead and add it at the top, the provider, and then add them directly to UserFields
* Now we can remove all the props from the middle components

```js
import React, { useState, createContext, useContext } from "react";
import "./styles.css";

// Creating a context
const UserContext = createContext();

const SettingsPanel = () => {
  const [userName, setUserName] = useState("Alice");
  const [userState, setUserState] = useState("TX");
  const [userIsDarkMode, setUserIsDarkMode] = useState(false);

  // The context value that will be supplied to any descendants of this component.
  const contextValue = {
    userName,
    userState,
    userIsDarkMode,
    setUserIsDarkMode
  };

  return (
    <UserContext.Provider value={contextValue}>
      <UserProfile />
    </UserContext.Provider>
  );
};

const UserProfile = () => {
  // No props are being passed down anymore
  return <UserForm />;
};

const UserForm = () => {
  // No props are being passed down anymore
  return <UserFields />;
};

const UserFields = () => {
  // Using useContext to consume the context
  const {
    userName,
    userState,
    userIsDarkMode,
    setUserIsDarkMode
  } = useContext(UserContext);

  return (
    <div
      style={{
        backgroundColor: userIsDarkMode ? "#000" : "",
        color: userIsDarkMode ? "#fff" : "#000"
      }}
    >
      <h2>{userName}</h2>
      <h3>{userState}</h3>
      <h3>Location</h3>
      <p>lat: {userLocation.lat}</p>
      <p>long: {userLocation.long}</p> 
      <p>{userWeather}</p>
      <button onClick={() => setUserIsDarkMode(!userIsDarkMode)}>
        Toggle Dark Mode
      </button>
    </div>
  );
};

export default function App() {
  return <SettingsPanel />;
}

```

This is much nicer and now UserForm and UserProfile dont need to know anything about the values in the SettingsPanel. -->
