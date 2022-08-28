## React

[10 React Antipatterns to avoid - code This not That by fireship](https://www.youtube.com/watch?v=b0IZo2Aho9Y)

1. Write a big component and break them into components using the vscode extension 'glean'

2. Nesting
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
