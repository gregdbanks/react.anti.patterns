# Top Ten React Anti-Patterns with examples

## [Not Using the useCallback Hook When It Would Be Beneficial:](examples/callback.md)

This is like telling your friends the same joke over and over again, each time as if it's the first. Sure, your joke might be hilarious, but without some memoization, your friends will soon stop laughing. Use useCallback to keep those punchlines fresh!

## [Forgetting to Debounce or Throttle:](examples/debounce.md)

Remember that kid who asked "Are we there yet?" every two seconds during a long car ride? That's your app making API calls every keystroke without throttling or debouncing. Let's learn from our parents and add some throttling to keep our sanity.

## [Prop Drilling Disaster:](examples/drilling.md)

This is the equivalent of playing a game of telephone at a 100-story building, passing a message from the top to the bottom, one floor at a time. By the time it gets to the bottom, it’s no longer “React is awesome!” but “Green moss on some?” Context or Redux can save you from this drill.

## [Huge Component Syndrome:](examples/huge.md)

This is like that one closet in your house where you keep stuffing random things until it becomes a towering mess. Break your giant components down into smaller, reusable ones. Don't let your components become that cluttered closet!

## [Using Index as Key:](examples/key-index.md)

That's like naming your children after their birth order. Sure, Child_1 and Child_2 are easy to remember, but what happens when Child_1 moves out? Using unique keys helps React keep track of your components, even when they move around.

## [Ignoring Component Lifecycles:](examples/lifecycles.md)

Not dealing with lifecycles is like refusing to acknowledge birthdays. No matter how much you ignore them, they still happen! Embrace lifecycles and handle them properly to keep your app running smoothly.

## [Mutating State Directly:](examples/mutate.md)

This is like sneaking in and changing the script of a play while it's being performed. It's confusing for everyone and disrupts the flow of the show. Always use setState or useState's updater function to change state, for the sake of your app's performance and your own sanity.

## [Overusing Refs:](examples/ref.md)

Like using a chainsaw to cut a sandwich, refs are a powerful tool, but not always the right one for the job. Use state for things that trigger re-render and leave refs for those rare cases where you need to break the rules.

## [Not Handling Side Effects Correctly:](examples/sideeffects.md)

Forgetting to handle side effects is like leaving the stove on when you leave the house. Sure, you might get away with it a few times, but sooner or later, you're going to regret it. Use useEffect to manage side effects and avoid unpleasant surprises.

## [State Updates Too Frequently:](examples/state.md)

This is like trying to catch up with a friend by calling them every five minutes. It's excessive and inefficient. Instead, batch your state updates and give your app (and your friend) some breathing room.
