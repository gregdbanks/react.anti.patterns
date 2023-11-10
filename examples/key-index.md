[![Watch the video](https://img.youtube.com/vi/9gQutLF95Vo/hqdefault.jpg)](https://www.youtube.com/watch?v=-xAETKXVfF4)

[Click here for Codesandbox](https://codesandbox.io/s/index-as-key-7f85ls)
<!-- ## Using Index as Key:

Given the code snippet in codesandbox we have 2 list. One that uses index as key and the other name(unique, meaning no duplicate names)

## Wrong Way:

```jsx
          <li key={index} className={highlighted[index] ? "highlighted" : ""}>
            {name}
            <button
              onClick={() =>
                setHighlighted((prev) => ({ ...prev, [index]: !prev[index] }))
              }
            >
              Toggle Background
            </button>
          </li>
```

Seems harmless, right? But using the index as the key can lead to unpredictable behavior if the list gets re-ordered or items get added or removed. It's like trying to find your way home when the street numbers keep changing!

React's reconciliation algorithm uses keys to track the identity of components across renders. When you use the index as a key and then shuffle the list, the keys remain the same even though the item they're associated with may have changed. 

Instead, try to use unique, stable identifiers as keys:

## Right Way:

```jsx
            <li
              key={name}
              className={highlighted[beatleIndex] ? "highlighted" : ""}
            >
              {name}
              <button
                onClick={() =>
                  setHighlighted((prev) => ({
                    ...prev,
                    [beatleIndex]: !prev[beatleIndex]
                  }))
                }
              >
                Toggle Background
              </button>
            </li>
```

Now each Beatle has their own unchanging ID, and no one gets lost when the band lineup changes! -->
