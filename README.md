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
/*
 * @param {Function} callback
 * @param {Number} time
*/
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
/*
 * @param {Function} callback
 * @param {Number} time
*/
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
/*
 * @param {Array} arr
 * @param {Function} callback
*/
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
/*
 * @param {Array} arr
 * @param {Function} callback
 * @param {Any} initialValue
*/
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
/*
 * @param {Array} arr
 * @param {Function} callback
*/
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

## find
```javascript
/*
 * @param {Array} arr
 * @param {Function} callback
*/
function find(arr, callback) {
    for(let i = 0; i < arr.length; i++) {
        let res = callback(arr[i], i);
        if(res) return arr[i];
    }
    return undefined;
}
```

## findIndex
```javascript
/*
 * @param {Array} arr
 * @param {Function} callback
*/
function findIndex(arr, callback) {
    for(let i = 0; i < arr.length; i++) {
        let res = callback(arr[i], i);
        if(res) return i;
    }
    return -1;
}
```

## every and some
```javascript
/*
 * @param {Array} arr
 * @param {Function} callback
*/
function every(arr, callback) {
    for(let i = 0; i < arr.length; i++) {
        if(!callback(arr[i], i)){
            return false;
        }
    }
    return true;
}

function some(arr, callback) {
    for(let i = 0; i < arr.length; i++) {
        if(callback(arr[i], i)) return true;
    }
    return false;
}
```

## concat
```javascript
function concat(arr, ...args) {
    const res = [...arr];
    args.forEach(function(item) {
        if(Array.isArray(item)) {
            res.push(...item)
        }else {
            res.push(item);
        }
    });

    return res;
}
```

## slice
```javascript
function slice(arr, begin, end) {
    const res = [];
    begin = begin || 0;
    if(begin > arr.length) return res;

    end = end || arr.length;
    if(end > begin) end = arr.length;

    for(let i = 0; i < arr.length; i++) {
        if(i >= begin && i < end) {
            res.push(arr[i]);
        }
    }
    return arr;
}
```

<br/>
<br/>
<br/>

# 数组去重

## unique
```javascript
function unique(arr) {
    const res = [];
    arr.forEach(function(item) {
        if(res.indexOf(item) === -1) {
            res.push(item);
        }
    });
    return res;
}

function unique2(arr) {
    const res = [];
    const container = {};
    arr.forEach(function(item) {
        if(container[item] === undefined) {
            container[item] = true;
            res.push(item);
        }
    });
    return res;
}

function unique3(arr) {
    return [...new Set(arr)];
}
```
