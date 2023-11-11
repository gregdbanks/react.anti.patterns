[![Watch the video](https://img.youtube.com/vi/9gQutLF95Vo/hqdefault.jpg)](https://www.youtube.com/watch?v=bKt2-ct-B70)

[Click here for Codesandbox](https://codesandbox.io/s/huge-zvtkgr)

<!-- ## Huge Component Syndrome!

Here, DoesEverythingComponent is doing WAY too much. State management, fetching, event handling, UI rendering - you name it, it's probably here. This component is like a one-man band in a small room - it's loud, chaotic, and you're likely to trip over something.

The solution, as before, is to break this monstrosity down into smaller, reusable components. The process would be the same as the previous example, but on a larger scale. Your app will thank you, and your users (and fellow developers) will too!

```jsx
import "./styles.css";

import React, { useState, useEffect } from "react";

const DoesEverythingComponent = ({ user }) => {
  // User states
  const [name, setName] = useState(user?.name);
  const [email, setEmail] = useState(user?.email);
  const [password, setPassword] = useState("");
  const [avatar, setAvatar] = useState(user?.avatar);

  // Social media states
  const [tweets, setTweets] = useState([]);
  const [followedUsers, setFollowedUsers] = useState([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  // Handlers for input changes
  const handleChange = (event, setter) => {
    setter(event.target.value);
  };

  // Mock fetching tweets
  const fetchTweets = async () => {
    setLoading(true);
    try {
      // Replace this with actual fetching code
      const fetchedTweets = [
        { id: 1, title: "First Tweet", content: "Hello World!" }
      ];
      setTweets(fetchedTweets);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  };

  // Mock fetching followed users
  const fetchFollowedUsers = async () => {
    setLoading(true);
    try {
      // Replace this with actual fetching code
      const fetchedUsers = [{ id: 1, name: "Jane Doe" }];
      setFollowedUsers(fetchedUsers);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  };

  // Fetch tweets and followed users on component mount
  useEffect(() => {
    fetchTweets();
    fetchFollowedUsers();
  }, []);

  return (
    <div>
      <h1>{name}'s Profile</h1>
      <img src={avatar} alt={`${name}'s avatar`} />
      <input value={name} onChange={(e) => handleChange(e, setName)} />
      <input value={email} onChange={(e) => handleChange(e, setEmail)} />
      <input
        value={password}
        onChange={(e) => handleChange(e, setPassword)}
        type="password"
      />
      {/* Display loading and error states */}
      {loading && <p>Loading...</p>}
      {error && <p>Error: {error}</p>}

      {/* Display tweets */}
      <h2>Tweets</h2>
      {tweets.map((tweet) => (
        <div key={tweet.id}>
          <h3>{tweet.title}</h3>
          <p>{tweet.content}</p>
        </div>
      ))}

      {/* Display followed users */}
      <h2>Followed Users</h2>
      {followedUsers.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
};

export default function App() {
  const user = {
    name: "John Doe",
    email: "john@example.com",
    avatar: "link-to-avatar.jpg"
    // other user properties
  };
  return (
    <>
      <DoesEverythingComponent user={user} />
    </>
  );
}

```

Lets break it up into more readable parts and improve composition

```js
import React, { useState, useEffect } from "react";

// UserProfileComponent
const UserProfileComponent = ({ user, handleChange }) => {
  const [name, setName] = useState(user?.name);
  const [email, setEmail] = useState(user?.email);
  const [password, setPassword] = useState("");
  const [avatar, setAvatar] = useState(user?.avatar);

  return (
    <>
      <h1>{name}'s Profile</h1>
      <div style={{ width: "15%", height: "auto" }}>
        <img
          src={avatar}
          alt={`${name}'s avatar`}
          style={{ width: "100%", height: "auto", borderRadius: "50%" }}
        />
      </div>
      <input value={name} onChange={(e) => handleChange(e, setName)} />
      <input value={email} onChange={(e) => handleChange(e, setEmail)} />
      <input
        value={password}
        onChange={(e) => handleChange(e, setPassword)}
        type="password"
      />
    </>
  );
};

// UseFetchDataHook
const useFetchData = (fetchFunction) => {
  const [data, setData] = useState([]);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      setLoading(true);
      try {
        const result = await fetchFunction();
        setData(result);
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    };
    fetchData();
  }, [fetchFunction]);

  return { data, loading, error };
};

// TweetsComponent
const TweetsComponent = () => {
  const fetchTweets = async () => {
    // Simulate fetching data
    return [
      { id: 1, title: "First Tweet", content: "Hello World!" },
      { id: 2, title: "Second Tweet", content: "Another tweet here." }
    ];
  };
  const { data: tweets, loading, error } = useFetchData(fetchTweets);

  return (
    <div>
      <h2>Tweets</h2>
      {loading && <p>Loading...</p>}
      {error && <p>Error: {error}</p>}
      {tweets.map((tweet) => (
        <div key={tweet.id}>
          <h3>{tweet.title}</h3>
          <p>{tweet.content}</p>
        </div>
      ))}
    </div>
  );
};

// FollowedUsersComponent
const FollowedUsersComponent = () => {
  const fetchFollowedUsers = async () => {
    // Simulate fetching data
    return [
      { id: 1, name: "Jane Doe" },
      { id: 2, name: "John Smith" }
    ];
  };
  const { data: followedUsers, loading, error } = useFetchData(fetchFollowedUsers);

  return (
    <div>
      <h2>Followed Users</h2>
      {followedUsers.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
};

// DoesEverythingComponent
const DoesEverythingComponent = ({ user }) => {
  const handleChange = (event, setter) => {
    setter(event.target.value);
  };

  return (
    <div>
      <UserProfileComponent user={user} handleChange={handleChange} />
      <TweetsComponent />
      <FollowedUsersComponent />
    </div>
  );
};


export default function App() {
  const user = {
    name: "John Doe",
    email: "john@example.com",
    avatar: "link-to-avatar.jpg"
    // other user properties
  };
  return (
    <>
      <DoesEverythingComponent user={user} />
    </>
  );
}
``` -->
