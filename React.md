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
   We can use useMemo() Hookd to remember a value and call a function if and only if the value has changed.

```javascript
funtion workHard(){
    const [count, setCount] = useState(0);
    const [other, setOther] = usestate(0);

    // const total = expensiveCalcutaion(count) --> in this the function will run again even if only other change and count does not change. This is inefficient
    const total = useMemo(()=> expensiveCalculation(count), [count])
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
