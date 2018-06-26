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
            inputValue = ''  // the input value is always stored here in the state not in the dom
        };
    }
    inputChange = (event) => {   // updating the state 
        this.setState({ inputValue: event.target.value })
    }
    render() {
        return (
            <input
                value={this.state.inputValue} // the value is always a copy of what's stored in state
                onChange={this.inputChange}  // the state is updated whenever the user changes this
            />
        )
    }
}
```