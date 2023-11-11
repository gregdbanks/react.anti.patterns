[![Watch the video](https://img.youtube.com/vi/9gQutLF95Vo/hqdefault.jpg)](https://youtu.be/kosZe-ibPmM)

[Click here for Codesandbox](https://codesandbox.io/s/mutation-g788m7)

<!-- ## Mutating State Directly:

```jsx
import React, { useState } from "react";

// BadComponent: Demonstrates the wrong way to update state
function BadComponent() {
  let [counter, setCounter] = useState(0);

  const handleClick = () => {
    counter = counter + 1; // Direct mutation of state - this is wrong!
    console.log("Bad counter value:", counter); // You can log to show it changes locally but not in state
  };

  return (
    <div>
      <h2>Bad Component</h2>
      <p>Counter: {counter}</p>
      <button onClick={handleClick}>Increase</button>
    </div>
  );
}

// GoodComponent: Demonstrates the correct way to update state
function GoodComponent() {
  const [counter, setCounter] = useState(0);

  const handleClick = () => {
    setCounter(counter + 1); // Correct way using the setter function
  };

  return (
    <div>
      <h2>Good Component</h2>
      <p>Counter: {counter}</p>
      <button onClick={handleClick}>Increase</button>
    </div>
  );
}

// App component to render both Bad and Good components
function App() {
  return (
    <div>
      <BadComponent />
      <GoodComponent />
    </div>
  );
}

export default App;
```
 -->
