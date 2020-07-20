# Test Tasks


Requirements:

- Stack - React with app state management library (Redux, MobX or Recoil), TypeScript. Functional style is preferable. No UI frameworks, or style libraries, CSS/SCSS only.
- All assets (images, icons) are of your choice. Inline SVG is preferable.

## Task 1 - Card View

Use fake data  to create responsive card view with header, sidebar and toolbar.

On the toolbar, the only button that should work is 'Add New'. Clicking on the button should show a modal window with simple form (design of your choice) to add a card to this list. Clicking on 'Info' link on the card redirects to empty page 'Info', clicking on the card, redirects to a simple product page of your design with card details present. Clicking on the 'burger' button next to 'Add New' reidrects to page with Task 2.

## Task 2 - List View

Similar to the frist task, produce the list view for the same data. On clicking on the line, the effect should be as per provided image below. Clicking on icon __i__ redirects to product page, mentioned before.

### Task 3 - Refactor

Refactor below example to React functional component with hooks and
TypeScript:

```JavaScript
import React, { Component } from "react";
import "bootswatch/journal/bootstrap.css";
// import "bootstrap/dist/css/bootstrap.css";
import "./App.css";

import { Navbar, NavItem, Nav, Grid, Row, Col } from "react-bootstrap";

const PLACES = [
  { name: "Palo Alto", zip: "94303" },
  { name: "San Jose", zip: "94088" },
  { name: "Santa Cruz", zip: "95062" },
  { name: "Honolulu", zip: "96803" }
];

class WeatherDisplay extends Component {
  constructor() {
    super();
    this.state = {
      weatherData: null
    };
  }
  
  componentWillMount() {
    const zip = this.props.zip;
    const URL = "http://api.openweathermap.org/data/2.5/weather?q=" +
      zip +
      "&appid=b1b35bba8b434a28a0be2a3e1071ae5b&units=imperial";
    fetch(URL).then(res => res.json()).then(json => {
      this.setState({ weatherData: json });
    });
  }
  
  componentWillUnmount() {
    this.setState({ weatherData:null })
  }
  
  render() {
    const weatherData = this.state.weatherData;
    if (!weatherData) return <div>Loading</div>;
    const weather = weatherData.weather[0];
    const iconUrl = "http://openweathermap.org/img/w/" + weather.icon + ".png";
    return (
      <div>
        <h1>
          {weather.main} in {weatherData.name}
          <img src={iconUrl} />
        </h1>
        <p>Current: {weatherData.main.temp}°</p>
        <p>High: {weatherData.main.temp_max}°</p>
        <p>Low: {weatherData.main.temp_min}°</p>
        <p>Wind Speed: {weatherData.wind.speed} mi/hr</p>
      </div>
    );
  }
}

class App extends Component {
  constructor() {
    super();
    this.state = {
      activePlace: 0
    };
  }
  render() {
    const activePlace = this.state.activePlace;
    return (
      <div>
        <Navbar>
          <Navbar.Header>
            <Navbar.Brand>
              React Simple Weather App
            </Navbar.Brand>
            <a href="https://github.com/ericvicenti/intro-to-react">Learn to build me</a>
          </Navbar.Header>
        </Navbar>
        <Grid>
          <Row>
            <Col md={4} sm={4}>
              <h3>Select a city</h3>
              <Nav
                bsStyle="pills"
                stacked
                activeKey={activePlace}
                onSelect={index => {
                  this.setState({ activePlace: index });
                }}
              >
                {PLACES.map((place, index) => (
                  <NavItem key={index} eventKey={index}>{place.name}</NavItem>
                ))}
              </Nav>
            </Col>
            <Col md={8} sm={8}>
              <WeatherDisplay key={activePlace} zip={PLACES[activePlace].zip} />
            </Col>
          </Row>
        </Grid>
      </div>
    );
  }
}

export default App;
```

Thank you and good luck!

