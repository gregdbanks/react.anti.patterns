[![Watch the video](https://img.youtube.com/vi/9gQutLF95Vo/hqdefault.jpg)](https://youtu.be/XLSIUwuxpio)


[Click here for Codesandbox](https://codesandbox.io/s/ref-rfj9rr)


<!-- ## Overusing Refs:

Refs are useful for many things, like accessing a DOM node directly, but some folks use them for everything under the sun. It's like using a chainsaw to cut your sandwich - sure, it can do the job, but it's probably not the best tool for it!

```jsx
function RefOverkill() {
  const nameRef = useRef("");

  const handleNameChange = (event) => {
    nameRef.current = event.target.value;
  };

  return <input onChange={handleNameChange} />;
}
```

In this example, we're using a ref to store the input value. But this isn't a great use of refs. In fact, it's a bit like using a sledgehammer to hang a picture - complete overkill!

In this situation, useState would be a much better choice:

```jsx
function JustRight() {
  const [name, setName] = useState("");

  const handleNameChange = (event) => {
    setName(event.target.value);
  };

  return <input onChange={handleNameChange} />;
}
```

Now handleNameChange updates the name state, and the input's value is stored in a place that makes sense. This is like hanging that picture with a small hammer - just right!

Remember, refs are powerful, but they're not always the right tool for the job. Don't let the power go to your head! -->
