[![Watch the video](https://img.youtube.com/vi/9gQutLF95Vo/hqdefault.jpg)](https://youtu.be/izWiRHxsc_U)

[Click here for Codesandbox](https://codesandbox.io/s/debounce-qpmfrd)

<!-- ## Forgetting to Debounce or Throttle:

Suppose you have a component that performs a search whenever the user types into an input field. You might do something like this:

```jsx
function TooEagerSearch() {
  const [query, setQuery] = useState("");

  useEffect(() => {
    // Pretend this is an actual API call
    console.log(`API Call: Searching for ${query}`);
  }, [query]);

  return (
    <input
      type="text"
      value={query}
      onChange={(e) => setQuery(e.target.value)}
    />
  );
}
```

The issue here is that an API call is made for every single letter the user types. This is like calling your friend to tell them about every single move you make while cooking. "Now I'm cutting the onion. Now I'm sautéing the onion. Now I'm adding the garlic..." Your friend is going to get annoyed pretty fast!

To avoid this, you can use a debouncing or throttling function to limit the number of API calls made. Here's a simple debouncing implementation with lodash:

```jsx
import { debounce } from "lodash";

function ChillSearch() {
  const [query, setQuery] = useState("");

  const debouncedSearch = debounce((searchQuery) => {
    // Pretend this is an actual API call
    console.log(`API Call: Searching for ${searchQuery}`);
  }, 500); // Wait 500ms after the last call to debouncedSearch

  useEffect(() => {
    debouncedSearch(query);
    // Cancel the debounce on useEffect cleanup
    return () => {
      debouncedSearch.cancel();
    };
  }, [query]);

  return (
    <input
      type="text"
      value={query}
      onChange={(e) => setQuery(e.target.value)}
    />
  );
}
```

Now the API call won't be made until the user stops typing for 500ms. This is like only calling your friend to tell them the important bits about your cooking, not every single move you make. Much less annoying and far more efficient! -->
