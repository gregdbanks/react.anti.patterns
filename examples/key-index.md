## Using Index as Key:

## Wrong Way:

```jsx
const names = ["John", "Paul", "George", "Ringo"];

function Beatles() {
  return (
    <ul>
      {names.map((name, index) => (
        <li key={index}>{name}</li>
      ))}
    </ul>
  );
}
```

Seems harmless, right? But using the index as the key can lead to unpredictable behavior if the list gets re-ordered or items get added or removed. It's like trying to find your way home when the street numbers keep changing!

Instead, try to use unique, stable identifiers as keys:

## Right Way:

```jsx
const beatles = [
  { id: "1", name: "John" },
  { id: "2", name: "Paul" },
  { id: "3", name: "George" },
  { id: "4", name: "Ringo" },
];

function Beatles() {
  return (
    <ul>
      {beatles.map((beatle) => (
        <li key={beatle.id}>{beatle.name}</li>
      ))}
    </ul>
  );
}
```

Now each Beatle has their own unchanging ID, and no one gets lost when the band lineup changes!
