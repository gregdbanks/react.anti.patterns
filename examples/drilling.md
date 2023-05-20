## Prop Drilling Disaster:

In a deeply nested component structure, you might find yourself passing props through various layers even when some intermediate components don't use them. That's prop drilling, and it's about as fun as a root canal.

## Wrong way:

```jsx
function Grandparent() {
  const [name, setName] = useState("Fred");
  return <Parent name={name} />;
}

function Parent({ name }) {
  // Parent doesn't use name but it has to accept it to pass it to Child. Ugh!
  return <Child name={name} />;
}

function Child({ name }) {
  return <p>Hi, my name is {name}</p>;
}
```

_To avoid drilling holes in your component hierarchy, React Context or state management libraries like Redux or MobX can help. Here's how the same example could look with Context:_

## Right way with context;

```jsx
const NameContext = React.createContext();

function Grandparent() {
  const [name, setName] = useState("Fred");
  return (
    <NameContext.Provider value={name}>
      <Parent />
    </NameContext.Provider>
  );
}

function Parent() {
  // Parent no longer needs to deal with name, yay!
  return <Child />;
}

function Child() {
  const name = useContext(NameContext);
  return <p>Hi, my name is {name}</p>;
}
```

## Right Way with Redux:

```jsx
import { Provider, connect } from "react-redux";

function Grandparent() {
  // Grandparent doesn't need to know about name at all
  return <Parent />;
}

function Parent() {
  // Same here, Parent doesn't need to know about name
  return <Child />;
}

let Child = ({ name }) => {
  // Child can read name directly from the Redux store
  return <p>Hi, my name is {name}</p>;
};

// Connect Child to the Redux store
Child = connect((state) => ({ name: state.name }))(Child);

function App() {
  // Wrap your app in a Provider to make the Redux store available to all components
  return (
    <Provider store={store}>
      <Grandparent />
    </Provider>
  );
}
```

_Now Parent doesn't need to worry about name, and we didn't have to drill any props. It's like magic, but better because it's code!_
