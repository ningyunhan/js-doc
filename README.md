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

<br/>
<br/>
<br/>

# 函数防抖和节流

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

## 函数防抖(debounce)
```javascript
function debounce(callback, time) {
    let timeId = null;
    return function(e) {
        if(timeId !== null) {
            clearTimeout(timeId);
        }
        timeId = setTimeout(() => {
            callback.call(this, e);
            timeId = null;
        }, time);
    }
}
```

<br/>
<br/>
<br/>

# 数组相关API函数

## map
```javascript
function map(arr, callback) {
    const res = [];
    for(let i = 0; i < arr.length; i++) {
        res.push(
            callback(arr[i], i)
        );
    }
    return res;
}
```

## reduce 
```javascript
function reduce(arr, callback, initialValue) {
    let startIndex = initialValue === undefined ? 1 : 0;
    let result = initialValue === undefined ? arr[0] : initialValue;
    for(let i = startIndex; i < arr.length; i++) {
        result = callback(result, arr[i], i, arr);
    }
    return result;
}
```

## filter
```javascript
function filter(arr, callback) {
    const res = [];
    for(let i = 0; i < arr.length; i++) {
        let temp = callback(arr[i], i);
        if(temp) {
            res.push(arr[i]);
        }
    }
    return res;
}
```