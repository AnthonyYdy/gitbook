[TOC]

* 用setTimeout 实现  setInterVal
```js
function mySetInterval(fn,delay){
    setTimeout(()=>{
            mySetInterval(fn,delay);
            fn()
    },delay)
}
```

* 归并排序

```js
function merge(arr1,arr2){
    let len1 = arr1.length - 1
    let len2 = arr2.length - 1
    let len = len1 + len2 + 1
    while(len2>=0){
        if(arr1[len1]>arr2[len2]){
            arr1[len] = arr1[len1]
            len1--
            len--
        }else{
            arr1[len] = arr2[len2]
            len2--
            len--
        }
    }
    return arr1
}
```