# Vue架构师培训相关笔记

## 第二节课，手写Vue的相关重点知识
```
/**
    这段代码，形成了典型的闭包，函数作用于内，一旦有一些局部的变量，通过函数暴露给了外界，key,val都会在内存中被保存，函数defineReactive执行一次就会被保存一份
*/
function defineReactive(obj, key, val) {
        Object.defineProperty(obj, key, {
            get() {
                console.log('get', val);
                return val;
            },
            set(newValue) {
                if (newValue !== val) {
                    val = newValue;
                    console.log('set', val);
                    update(newValue);
                }
            }
        });
    }
```