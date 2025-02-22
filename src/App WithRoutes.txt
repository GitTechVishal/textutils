import "./App.css";
import Alert from "./components/Alert";
import About from "./components/About";
import Navbar from "./components/Navbar";
import TextForm from "./components/TextForm";
import React, { useState } from "react";
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";

function App(props) {
  //? useState Hook We are handling dark mode complet website
  const [mode, setmode] = useState("light");
  const [alert, setAlert] = useState(null);
  const showAlert = (mesage, type) => {
    setAlert({
      msg: mesage,
      type: type,
    });
    setTimeout(() => {
      setAlert(null);
    }, 1500);
  };
  const toggleMode = () => {
    if (mode === "light") {
      setmode("dark");
      document.body.style.backgroundColor = "#042743";
      document.body.style.color = "white";
      showAlert("Dark Mode is enabled", "success");
      document.title = "TextUtils - Dark Mode";
    } else {
      setmode("light");
      document.body.style.backgroundColor = "white";
      document.body.style.color = "black";
      showAlert("Light Mode is enabled", "success");
      //? to show title
      document.title = "TextUtils - Light Mode";
      //? To Show Title Change After 2 seconds
      // setInterval(() => {
      //   document.title = "TextUtils is Amazing Mode";
      // }, 2000);
      // setInterval(() => {
      //   document.title = "Install TextUtils Now";
      // }, 1500);
    }
  };
  return (
    <>
      <Router>
        {/*<Navbar title = "TextUtilsP" aboutText="About Text" link="Home"/>*/}
        <Navbar title="TextUtilities" mode={mode} toggleMode={toggleMode} />
        <Alert alert={alert} />
        {/* <div className="container my-3"></div> */}
        <div className="container my-3">
          <Routes>
            <Route
              exact
              path="/"
              element={
                <TextForm
                  showAlert={showAlert}
                  heading="Enter the text to analyze below"
                  mode={mode}
                />
              }
            />
            <Route exact path="/about" element={<About />} />
          </Routes>
        </div>
      </Router>
    </>
  );
}

export default App;
