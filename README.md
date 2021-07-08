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

## bind

```javascript
function bind(Fn, thisArg, ...args) {
    return function(...args2) {
        // 调用call函数
        return call(Fn, thisArg, ...args, ...args2);
    }
}
```

## 函数节流(throttle)
```javascript
function throttle(callback, wait) {
    let start = 0;
    return function(e) {
        let now = Date.now();
        if(now - start >= wait) {
            callback.call(this, e);
            start = now;
        }
    }
}
```
