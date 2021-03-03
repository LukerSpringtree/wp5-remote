# 
remote 暴露模块给host用

# 
shared 共享

任何一方加载过了,  另外一方就不需要加载了

shared: ['react', 'react-dom']

share scope, share是不能保证版本一致性的.
但是会用高优先级的.

version check
那怎么坚持呢?  默认用最高的版本.


#


# 
容器可以双向依赖

# 
 4-5 更多的是性能提升了, 用法上变化不大.

#
  publicPath 其实就是资源加载前面的路径.
  即, 如果你配了 publicPath 那么 资源请求第一个路径分隔符的值就是publicPath
  否则就为 "/"

# 
懒加载 , 异步引用
```js
const Comp01 = await import('remote/NewsList')

const Comp02 = React.lazy(() => import('host/Slides'))
```


```js

function lazy(fn) {
  return class extends React.Component{
    state = {Component: null}

    componentDidMount() {
      fn().then(result => {
        this.setState({Component: result.default})
      })
    }

    render() {
      let {Component} = this.state
      return Component?<Component/>: null;
    }
  }
}

```
# 
- tree shaking 是否能优化class里的方法?
- 答: 是可以的, 之前不行主要是webpack担心,影响到class类里面的副作用.
即, class里面的副作用被弄没了

babel它把. class -> fucntion语法的时候, 会有一些特殊的操作.
如果我们在类前面加上
/** PURE **/ 即可以进行tree shaking了

# 
用了模块联邦之后, 就可以不用乾坤了!

# 
共享资源包, 没有这个好


