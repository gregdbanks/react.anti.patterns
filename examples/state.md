[![Watch the video](https://img.youtube.com/vi/9gQutLF95Vo/hqdefault.jpg)](https://youtu.be/u4_uQB1LS0U)

[Click here for Codesandbox](https://codesandbox.io/s/state-updates-tvhrs4)

<!-- ## State Updates Too Frequently:

This is like having an over-enthusiastic friend who calls you every time they find a new cat video. Sure, you love cats, but this is just too much!

```jsx
function HyperactiveComponent() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    for (let i = 0; i < 5; i++) {
      setCount(count + 1);
    }
  };

  return <button onClick={handleClick}>Increase</button>;
}
```

Here, handleClick is trying to update count five times, but count won't actually change until the component re-renders. So, you end up incrementing the original count five times and setting the state to count + 1, not count + 5 as you might expect. This is like trying to leapfrog yourself—it just doesn't work!

The solution is to use the functional form of setState, which takes the previous state as a parameter and returns the new state:

```jsx
function CalmComponent() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    for (let i = 0; i < 5; i++) {
      setCount((prevCount) => prevCount + 1);
    }
  };

  return <button onClick={handleClick}>Increase</button>;
}
```

Now setCount is called with a function that takes the latest count and returns count + 1. This way, all the updates are applied correctly, and your state is as calm as a zen master in a meadow. -->
