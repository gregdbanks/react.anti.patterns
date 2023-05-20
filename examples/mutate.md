## Mutating State Directly:

```jsx
function NaughtyComponent() {
  const [counter, setCounter] = useState(0);

  const handleClick = () => {
    counter = counter + 1; // Oh no, direct state mutation!
  };

  return <button onClick={handleClick}>Increase</button>;
}
```

_Just like with class components, this is a big no-no. Instead, use the setter function returned by useState:_

````jsx
function GoodComponent() {
  const [counter, setCounter] = useState(0);

  const handleClick = () => {
    setCounter(counter + 1); // Much better!
  }

  return <button onClick={handleClick}>Increase</button>;
}
```

Now your counter state is being updated correctly, and React is much happier. This is like using the washing machine instead of trying to clean your clothes by stomping on them in a bucket... much more civilized!
````
