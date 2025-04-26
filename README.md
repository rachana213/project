// App.jsx
import React, { useState, useEffect } from "react";
import "./App.css";

function App() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((response) => response.json())
      .then((data) => {
        setUsers(data);
        setLoading(false);
      });
  }, []);

  return (
    <div className="App">
      <header>
        <h1>User List</h1>
      </header>
      {loading ? (
        <p>Loading...</p>
      ) : (
        <ul>
          {users.map((user) => (
            <li key={user.id}>
              <h3>{user.name}</h3>
              <p>{user.email}</p>
              <a href={`http://${user.website}`} target="_blank" rel="noopener noreferrer">
                Visit Website
              </a>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

export default App;
