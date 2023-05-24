## Prop Drilling Disaster:

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

_Now Parent doesn't need to worry about name, and we didn't have to drill any props. It's like magic, but better because it's code!_
