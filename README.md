# React Hooks Chearsheet
## useState Hook
useState to Create State Variables
```
import "./styles.css";
import React from 'react';

export default function App() {
  const [language] = React.useState('React!!!')
  
  return <h1>I am learning {language}</h1>;
}
```
Update State Variables
```
import "./styles.css";
import React from 'react';

export default function App() {
  const [language, setLanguage] = React.useState('React!!!')
  
  function changeLanguage() {
    setLanguage('React Hooks')
  }
  
  return <h1 onClick={changeLanguage}>I am learning {language}</h1>;
}
```
Can Be Used Once Or Many Times
```
import "./styles.css";
import React from "react";

export default function App() {
  const [language, setLanguage] = React.useState("React!!!");
  const [years] = React.useState(0);
  function changeLanguage() {
  setLanguage("React Hooks");
}

  return (
    <div>
      <h1 onClick={changeLanguage}>
      I've learned {language} for {years} years
      </h1>
      <button>Add Year</button>
    </div>
  );
}
```
Update State based on Previous Value
```
import "./styles.css";
import React from "react";

export default function App() {
  const [language, setLanguage] = React.useState("React!!!");
  const [years, setYears] = React.useState(0);
  function changeLanguage() {
  setLanguage("React Hooks");
  }
  
  function addYear() {
  setYears(prev => prev + 1)
  }
  
  return (
    <div>
      <h1 onClick={changeLanguage}>
      I've learned {language} for {years} years
      </h1>
      <button onClick={addYear}>Add Year</button>
    </div>
  );
}
```
Manage State with an Object
```
import "./styles.css";
import React from "react";

export default function App() {

  // const [language, setLanguage] = React.useState("React!!!");
  // const [years, setYears] = React.useState(0);

  const [state, setState] = React.useState({
    language: "React",
    years: 0
  })
  
  function changeLanguage() {
    setState({...state, language: "React Hooks"});
  }
  
  function addYear() {
    setState(prev => {
      return {
      ...prev,
      years: prev.years + 1
      }
    })
  }
  
  return (
    <div>
      <h1 onClick={changeLanguage}>
      I've learned {state.language} for {state.years} years
      </h1>
      <button onClick={addYear}>Add Year</button>
    </div>
  );
}
```
## useEffect Hook
useEffect to Perform Side Effects
```
import "./styles.css";
import React from "react";

export default function App() {
  React.useEffect(() => {
    document.body.style.background = 'navy';
    document.body.style.color = 'white';
  })
  
  return (
    <div>
      <h1>React App</h1>
    </div>
  );
}
```
Run Again when a Value Changes
```
import "./styles.css";
import React from "react";

  export default function App() {
    const [color, setColor] = React.useState('navy')
    React.useEffect(() => {
      document.body.style.background = color;
      document.body.style.color = 'white';
    }, [color]);
    function changeColor() {
     setColor('gold')
  }
  
  return (
    <div>
      <h1>React App</h1>
      <button onClick={changeColor}>Change color</button>
    </div>
  );
}
```
Unsubscribe by Returning a Function
```
import "./styles.css";
import React from "react";

export default function App() {
  const [color, setColor] = React.useState('navy')
  
  React.useEffect(() => {
    document.body.style.background = color;
    document.body.style.color = 'white';
    window.addEventListener('keydown', handleEnterButton)
    
    return () => {
      window.removeEventListener('keydown', handleEnterButton)
    }
  }, [color]);
  
  function changeColor() {
    setColor('gold')
  }
  
  function handleEnterButton(event) {
    if (event.keyCode === 13) {
      setColor('red')
    }
  }
  
  return (
    <div>
      <h1>React App</h1>
      <button onClick={changeColor}>Get color</button>
    </div>
  );
}
```
Fetch Data from an API
```
import "./styles.css";
import React from "react";

export default function App() {
  const [color, setColor] = React.useState('navy')
  const [user, setUser] = React.useState(null)
  
  React.useEffect(() => {
    fetch('https://randomuser.me/api/')
    .then(res => res.json())
    .then(data => setUser(data.results[0]))
  }, [])
  
  React.useEffect(() => {
    document.body.style.background = color;
    document.body.style.color = 'white';
    window.addEventListener('keydown', handleEnterButton)
    return () => {
    window.removeEventListener('keydown', handleEnterButton)
    }
  }, [color]);
  
  function changeColor() {
    setColor('gold')
  }
  
  function handleEnterButton(event) {
    if (event.keyCode === 13) {
    setColor('red')
    }
  }
  
  return (
    <div>
      <h1>React App</h1>
      <button onClick={changeColor}>Get color</button>
      <br />
      <br />
      Current user: <pre>{JSON.stringify(user, null, 2)}</pre>
    </div>
  );
}
```

