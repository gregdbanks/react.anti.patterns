[![Watch the video](https://img.youtube.com/vi/9gQutLF95Vo/hqdefault.jpg)](https://www.youtube.com/watch?v=LI5VbiGCCXk)

[Click here for Codesandbox](https://codesandbox.io/s/callbacks-h4gt3c)

<!-- Below we have the react anti-pattern of not using useCallBack fro expensive functions

```jsx
import React, { useState, useEffect, useCallback } from "react";

// A spinner component to indicate an ongoing operation
const Spinner = () => <div>Waiting...</div>;

// A child component that accepts a callback
const ChildComponent = ({ callback }) => {
  const [loading, setLoading] = useState(false);

  useEffect(() => {
    setLoading(true);
    const timer = setTimeout(() => {
      callback();
      setLoading(false);
    }, 1000);

    return () => clearTimeout(timer);
  }, [callback]);

  return loading ? <Spinner /> : <div>Operation done!</div>;
};

// The parent component without useCallback
const ParentWithoutCallback = () => {
  const [value, setValue] = useState("");

  const callback = () => {
    console.log("Operation performed without useCallback");
  };

  return (
    <div>
      <ChildComponent callback={callback} />
      <input
        value={value}
        placeholder="Type here (without useCallback)"
        onChange={(e) => setValue(e.target.value)}
      />
    </div>
  );
};

// The parent component with useCallback
const ParentWithCallback = () => {
  const [value, setValue] = useState("");

  const callback = useCallback(() => {
    console.log("Operation performed with useCallback");
  }, []);

  return (
    <div>
      <ChildComponent callback={callback} />
      <input
        value={value}
        placeholder="Type here (with useCallback)"
        onChange={(e) => setValue(e.target.value)}
      />
    </div>
  );
};

// Main App component
const App = () => {
  return (
    <div>
      <h2>Without useCallback</h2>
      <ParentWithoutCallback />
      <h2>With useCallback</h2>
      <ParentWithCallback />
    </div>
  );
};

export default App;
``` -->
