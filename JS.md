## JavaScript

### Debug JavaScript like a pro

1. Use computer property names.
   This displays our info as dictionaries (objects)

```javascript
console.log({ foo, bar, baz });
```

1. custom style what we are logging out. console.log("%c whatToLog, cssStyle)

```javascript
console.log("%c whatToLog", "color:green; font-weight: bold;");
```

3. Display as table using console.table. Is useful when displaying array of objects.

```javascript
console.table([foo, bar, baz]);
```

4. Keeping tract of time using console.time("functionName") to checktime performance

```javascript
console.time('looper')

let i = 0;
while (i< 1e6f){i ++}

console.timeEnd('looper')
```

5. Add console.trace to function to know when the function was defined and when it was called.
