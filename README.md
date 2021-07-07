# 函数相关

## call

```javascript
function call(Fn, thisArg, ...args) {
    if (thisArg === undefined || thisArg === null) {
        obj = globalThis;
    }

    thisArg.temp = Fn;
    let result = thisArg.temp(...args);
    delete thisArg.temp;
    return result;
}
```

## apply

```javascript
function apply(Fn, thisArg, args) {
    if (thisArg === undefined || thisArg === null) {
        obj = globalThis;
    }

    thisArg.temp = Fn;
    let result = thisArg.temp(...args);
    delete thisArg.temp;
    return result;
}
```
