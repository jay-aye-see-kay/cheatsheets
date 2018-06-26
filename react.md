# Component basics
General form
```jsx
// MyComponent.js

import React, { Component } from "react";
import OtherComponent from "./OtherComponent";

class MyComponent extends Component {
    constructor(props) {
        super(props);
        this.state = {
            ...
        };
    }
    someFunction = () => {
        ...
    }
    render() {
        return (
            <div className="wrapper">
                <OtherComponent/>
            </div>
        )
    }
}

export default MyComponent;
```

# One way input binding
```jsx
class ComponentWithInput extends Component {
    constructor(props) {
        super(props);
        this.state = {
            inputValue = ''
        };
    }
    inputChange = (event) => {
        this.setState({ inputValue: event.target.value })
    }
    render() {
        return (
            <input
                value={this.state.inputValue}
                onChange={this.inputChange}
            />
        )
    }
}
```