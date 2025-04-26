import React, { useState, useEffect } from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
import AppNavBar from "./components/AppNavBar";
import ProfileList from "./components/ProfileList";
import ProfileDetails from "./components/ProfileDetails";
import { Spinner } from "react-bootstrap";
import "./App.css";

function App() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users/")
      .then((res) => res.json())
      .then((res) => {
        setUsers(res);
        setLoading(false);
      });
  }, []);

  if (loading) {
    return (
      <div style={{ width: "100%", textAlign: "center", margin: "5rem auto" }}>
        <Spinner animation="border" />{" "}
      </div>
    );
  }

  return (
    <Router>
      <AppNavBar />
      <Switch>
        <Route exact path="/">
          <ProfileList users={users} />
        </Route>
        <Route path="/profile/:userID" component={ProfileDetails} />
      </Switch>
    </Router>
  );
}

export default App;
