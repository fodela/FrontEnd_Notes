## React

[10 React Antipatterns to avoid - code This not That by fireship](https://www.youtube.com/watch?v=b0IZo2Aho9Y)

1. Write a big component and break them into components using the vscode extension 'glean'

2. Nesting gotcha
   Instead of creating the child component into the parent, create a separate child component and pass the variables need to the child using props

```javascript
const Parent = ()=>{

    return (
        <div>
            <Child onClick={functionName} age={15}>
        </div>
    )
}
```

3. Failure to Memoize
   We can use useMemo() Hook to remember a value and call a function if and only if the value has changed.

```javascript
function workHard() {
	const [count, setCount] = useState(0);
	const [other, setOther] = useState(0);

	// const total = expensiveCalcutaion(count) --> in this the function will run again even if only other change and count does not change. This is inefficient
	const total = useMemo(() => expensiveCalculation(count), [count]);
}
```

4. Pointless div
   Use react Fragment or better yet the simpler syntax of and empty element

   ```html
   <React.Fragment>
        <ComponentOne/>
        <ComponentTwo/>
    </React.Fragment>

    <!-- OR -->

   <>
        <ComponentOne/>
        <ComponentTwo/>
    </>
   ```

5. Messy Files
   Follow the 'one component per file' rule. Each component could have it separate directory.

6. Huge bundles
   For big projects, there will be many js files hence large js bundles to be downloaded by the browser and slow initial page load
   to use dynamically import the component.
   use `const Button = React.lazy(()=> import("./Button"))`
   while loading display a fallback component using `<Suspense> fallback={<div>Loading...</div>}`

7. Props Drilling
   Refers to passing props down components that do not need until it reaches the target child.
   To fix this:

   1. we can use redux but that is a heavy handed approach.
   2. Use contextApi
      You provide that prop once and all the children nested inside can access it.

   ```javascript
   function PropDrilling() {
   	const [count] = useState(0);

   	return (
   		<CountContext.Provider value={count}>
   			<child />
   		</CountContext.Provider>
   	);
   }

   function child(){
    return <GrandChild>
   }

   function GrandChild(){
    const count = useContext(CountContext)
   }
   ```

   NB: Use sparingly because it makes it impossible to reuse the component unless that provider is a parent

8. Props Plowing (a made up term)

```javascript
//    instead of
<Person age={data.age} name={data.name} sex={data.sex}/>
//  use
<Person {...data} />
```

Code is less explicit so do not overuse

9. Try some curry

```javascript
// use
const handleIt = (v:number)=>{
    return (e.any)=> console.log(e,v)
}
return (
    <div>
    <input onChange={handleIt(1)} />
    <input onChange={handleIt(2)} />
    <input onChange={handleIt(3)} />
    </div>
)

// instead of
const handleIt = (e: any, v:number)=>{
    console.log(e,v)
}
return (
    div
    <input onChange={(e) => handleIt(e, 1)} />
    <input onChange={(e) => handleIt(e, 2)} />
    <input onChange={(e) => handleIt(e, 3)} />

)
```

10. Code smarter
    Build component with a bunch of different stateful value first then if things get too complex extract the logic into a custom hook a js function.

    ```javascript
    function useMetadata(){
        const [title, setTitle] = useState("hey)
        const [theme, setTheme] = useState("hey)
        const [ts, setTs] = useState(Date.now())

    }
    ```
