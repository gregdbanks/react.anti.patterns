## Not Handling Side Effects Correctly:

Here's an example of this anti-pattern. Suppose you have a component that fetches some data when it's first rendered. You're using a state variable to keep track of this data, but you haven't considered what happens if the component is unmounted before the fetch completes:

```jsx
function NaughtyComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("https://api.example.com/data")
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []);

  // Rest of the component...
}
```

This component may look fine at first glance, but there's a hidden pitfall: if the component unmounts before the fetch completes, you'll try to call setData on an unmounted component, which leads to a memory leak. This is like leaving the faucet running when you leave the house - it wastes resources and can lead to bigger problems!

To avoid this, you can use a cleanup function in your useEffect hook to cancel the fetch if the component unmounts:

```jsx
function WellBehavedComponent() {
  const [data, setData] = useState(null);
  const abortController = new AbortController();

  useEffect(() => {
    fetch('https://api.example.com/data', { signal: abortController.signal })
      .then(response => response.json())
      .then(data => setData(data))
      .catch(err => {
        if (err.name === 'AbortError') {
          console.log('Fetch aborted');
        } else {
          console.error('A real error occurred', err);
        }
      });

    return () => abortController.abort();
  }, []);

  // Rest of the component...
}
In this version, if the component unmounts before the fetch completes, the fetch is cancelled, preventing the memory leak. This is like making sure to turn off the faucet before you leave the house - it's much more responsible and avoids unnecessary waste!
```
