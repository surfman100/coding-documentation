## React
Tips on using the React framework

- [Arrow functions](#arrowfunctions)
- [Destructing](#destructing)
- [Spread Operator](#spread)
- [Hooks](#useeffect)
- [Fragments](#fragments)
- [Component Composition](#composition)

# Arrow functions <a name="arrowfunctions"></a>
if only returning a value, use arrow function expressions with **concise** body  
```
const Search = () => (  
  <div>  
    <p>Hello</p>  
  </div>  
);  
```

arrow function expressions can also be used with **block** body if need logic and return value
```
const Search = () => {  
  /* other logic */
  
  return (
  <div>  
    <p>Hello</p>  
  </div>
  );  
};  
```

# Events
React synthetic event is a wrapper for the browsers native event

# Destructing <a name="destructing"/></a>
```
const user = {
  firstName: 'Bill',
  lastName: 'Tierney'
}; 

//Instead of 
const firstName = user.firstName;
const lastName = user.lastName;

//can use
const {firstName, lastName} = user;
```
so we can changes components from
```
const List(props) => {
  //use props.list
}
```
to
```
const List({list}) => {
  //use list
}
```

# Spread Operator <a name="spread"/></a>
Use the three dots to spread all key/value pairs of an object to another object
```
const user = {
  ...profile,
  gender: 'male',
  ...address
}
```

this simplifies our components in React
```
<Item key={item.key} {...item} />

const Item = ({title, url, author}) => {
```

**Note** Use nested destructuring only when it improves readability!

# Hooks <a name="useeffect"/></a>
**useState** is used for values that change over time  
**useEffect** is used to opt into the lifecycle of your components to introduce side-effects  
**customHooks** is used if you want to use both of the hooks above  
**useRef** is used to implement imperative code rather than standard declarative code

# Fragments <a name="fragments"/></a>
When you want to return sibling elements and not just a single element. 
```
const Search = () => (  
<>  
  <label>  
  <input>  
<>  
);  
```
# Component Composition <a name="composition"/></a>
be aware of the **children** prop
