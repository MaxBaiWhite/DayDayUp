1. 基本结构
2. Promise 状态和值
```js
const PENDING = 'PENDING'
const FULFILLED = 'FULFILLED'
const REJECTED = 'REJECTED'
const isFunction = variable => typeof variable === 'function'
class MyPromise {
    constructor (handle) {
        if (!isFunction(handle)) {
            throw new Error('MyPromise must accept a function as a parameter')
        }
        // 声明初始状态，值，成功队列及失败队列
        this._status = PENDING
        this._value = undefined
        this._fulfilledQueues  = []
        this._rejectedQueues   = []
        try {
          handle(this._resolve.bind(this), this._reject.bind(this))
        } catch (e) {
          this._reject(e)
        }
    }
    _resolve (val) {
        if (this._status !== PENDING) return
        function run() {
            function runResolved () {
                let cb = null
                while (cb = this._fulfilledQueues.shift) {
                    cb(val)
                } 
            }
            function runRejected () {
                let cb = null
                while (cb = this._rejectedQueues.shift) {
                    cb(val)
                } 
            }
            if (val instanceof MyPromise) {
                val.then(value => {
                  this._value = value
                  this._status = FULFILLED
                  runResolved(value)
                },value => {
                  this._value = value
                  this._status = REJECTED
                  runRejected(value)
                })
            } else {
                this._value = val
                this._status = FULFILLED
                runResolved(val)
            }
        }
        setTimeout(run, 0)
    }
    _reject (err) {
        if (this._status !== PENDING) return
        function run() {
            let cb = null
            while (cb = this._rejectedQueues.shift) {
                cb(err)
            }
        }
        setTimeout(run, 0)
    }
    then (onFulfilled, onRejected) {
      const { _value, _status } = this
      switch (_status) {
        // 当状态为pending时，将then方法回调函数加入执行队列等待执行
        case PENDING:
          this._fulfilledQueues.push(onFulfilled)
          this._rejectedQueues.push(onRejected)
          break
        // 当状态已经改变时，立即执行对应的回调函数
        case FULFILLED:
          onFulfilled(_value)
          break
        case REJECTED:
          onRejected(_value)
          break
      }
      // 返回一个新的Promise对象
      return new MyPromise((onFulfilledNext, onRejectedNext) => {
          let fulfilled = value => {
              try {
                  if(!isFunction(onFulfilled)) {
                      let res = onFulfilled(value)
                      if (res instanceof MyPromise) {
                          res.then(onFulfilledNext, onRejectedNext)
                      } else {
                          onFulfilledNext(value)
                      }
                  } else {
                      onFulfilledNext(value)
                  }
              } 
              catch (e) {
                onRejected(e)
              }
          }
          
          let rejected = err => {
              try {
                if (isFunction(onRejected)) {
                    let res = onRejected(err)
                    if (res instanceof MyPromise) {
                        res.then(onFulfilledNext,onRejectedNext)
                    }
                } else {
                    onRejectedNext(err)
                }
              } catch (e) {
                onRejectedNext(e)
              }
          }
      })
    }
}
```
3. Promise 的 then 方法
`promise.then(onFulfilled, onRejected)`
```js

```