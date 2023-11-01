<!-- ## Prop Drilling Disaster:

In a deeply nested component structure, you might find yourself passing props through various layers even when some intermediate components don't use them. That's prop drilling, and it's about as fun as a root canal.

## Wrong way:

```jsx
import React, { useState } from "react";
import "./styles.css";

const Grandparent = () => {
  const [name, setName] = useState("Fred");
  const [age, setAge] = useState(70);
  return <Parent name={name} age={age} />;
};

const Parent = ({ name, age }) => {
  return <Uncle name={name} age={age} />;
};

const Uncle = ({ name, age }) => {
  return <Cousin name={name} age={age} />;
};

const Cousin = ({ name, age }) => {
  return <Child name={name} age={age} />;
};

const Child = ({ name, age }) => {
  return (
    <p>
      Hi, my name is {name} and I am {age} years old
    </p>
  );
};

export default function App() {
  return <Grandparent />;
}
```

_To avoid drilling holes in your component hierarchy, React Context or state management libraries like Redux or MobX can help. Here's how the same example could look with Context:_

## Right way with context;

```jsx
import React, { useState, useContext } from "react";
import "./styles.css";

const NameContext = React.createContext();
const AgeContext = React.createContext();

const Grandparent = () => {
  const [name, setName] = useState("Fred");
  const [age, setAge] = useState(70);
  return (
    <NameContext.Provider value={name}>
      <AgeContext.Provider value={age}>
        <Parent />
      </AgeContext.Provider>
    </NameContext.Provider>
  );
};

const Parent = () => {
  return <Uncle />;
};

const Uncle = () => {
  return <Cousin />;
};

const Cousin = () => {
  return <Child />;
};

const Child = () => {
  const name = useContext(NameContext);
  const age = useContext(AgeContext);
  return (
    <p>
      Hi, my name is {name} and I am {age} years old
    </p>
  );
};

const App = () => {
  return <Grandparent />;
};

export default App;
```

## Right Way with Redux:

```jsx
import React from "react";
import { createStore } from "redux";
import { Provider, useSelector } from "react-redux";
import "./styles.css";

// The initial state of our store
const initialState = {
  name: "Fred",
  age: 70
};

// The reducer function, which describes how the state should change in response to actions
const reducer = (state = initialState, action) => {
  switch (action.type) {
    default:
      return state;
  }
};

// Create the Redux store
const store = createStore(reducer);

const Grandparent = () => {
  return <Parent />;
};

const Parent = () => {
  return <Uncle />;
};

const Uncle = () => {
  return <Cousin />;
};

const Cousin = () => {
  return <Child />;
};

const Child = () => {
  // Use Redux's useSelector hook to access data from the store
  const name = useSelector(state => state.name);
  const age = useSelector(state => state.age);
  return (
    <p>
      Hi, my name is {name} and I am {age} years old
    </p>
  );
};

const App = () => {
  return (
    <Provider store={store}>
      <Grandparent />
    </Provider>
  );
};

export default App;

```

_Now Parent doesn't need to worry about name, and we didn't have to drill any props. It's like magic, but better because it's code!_ -->

Certainly! To make the example more practical and reflect a realistic use case, let's consider a UI where we have a user profile settings panel that is deeply nested within a user interface. We'll start by showing the prop drilling problem with a UI component hierarchy and then refactor it using both React Context and Redux to manage the state more efficiently.

## Prop Drilling in a User Profile Settings UI:

Suppose we have a user profile settings UI that allows users to update their name and age. These settings are deeply nested in the component tree.

### Wrong way:

```jsx
import React, { useState } from "react";
import "./styles.css";

// Imagine this as the top-level component that contains the settings panel.
const SettingsPanel = () => {
  const [userName, setUserName] = useState("Alice");
  const [userAge, setUserAge] = useState(28);
  return <UserProfile userName={userName} userAge={userAge} />;
};

// Intermediate component that doesn't use the props but passes them down.
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
      <input type="text" value={userName} onChange={(e) => {}} />
      <input type="number" value={userAge} onChange={(e) => {}} />
    </div>
  );
};

export default function App() {
  return <SettingsPanel />;
}
```

To avoid passing props through intermediate components, we can use React Context or Redux.

### Right way with React Context:

```jsx
import React, { useState, useContext } from "react";
import "./styles.css";

const UserNameContext = React.createContext();
const UserAgeContext = React.createContext();

const SettingsPanel = () => {
  const [userName, setUserName] = useState("Alice");
  const [userAge, setUserAge] = useState(28);
  return (
    <UserNameContext.Provider value={userName}>
      <UserAgeContext.Provider value={userAge}>
        <UserProfile />
      </UserAgeContext.Provider>
    </UserNameContext.Provider>
  );
};

// No longer passing props directly down!
const UserProfile = () => {
  return <UserForm />;
};

const UserForm = () => {
  return <UserFields />;
};

const UserFields = () => {
  const userName = useContext(UserNameContext);
  const userAge = useContext(UserAgeContext);
  return (
    <div>
      <input type="text" value={userName} onChange={(e) => {}} />
      <input type="number" value={userAge} onChange={(e) => {}} />
    </div>
  );
};

const App = () => {
  return <SettingsPanel />;
};

export default App;
```

### Right Way with Redux:

```jsx
import React from "react";
import { createStore } from "redux";
import { Provider, useSelector } from "react-redux";
import "./styles.css";

// The initial state of our Redux store.
const initialState = {
  userName: "Alice",
  userAge: 28
};

// The reducer function to handle state changes.
const reducer = (state = initialState, action) => {
  switch (action.type) {
    // Here you could handle actions to update userName and userAge
    default:
      return state;
  }
};

const store = createStore(reducer);

const SettingsPanel = () => {
  return <UserProfile />;
};

const UserProfile = () => {
  return <UserForm />;
};

const UserForm = () => {
  return <UserFields />;
};

const UserFields = () => {
  const userName = useSelector(state => state.userName);
  const userAge = useSelector(state => state.userAge);
  return (
    <div>
      <input type="text" value={userName} onChange={(e) => {}} />
      <input type="number" value={userAge} onChange={(e) => {}} />
    </div>
  );
};

const App = () => {
  return (
    <Provider store={store}>
      <SettingsPanel />
    </Provider>
  );
};

export default App;
```

Both Context and Redux solutions here provide a way to access state in deeply nested components without the need to pass props down through every level of the component tree. This leads to cleaner, more maintainable code.
