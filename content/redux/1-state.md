现在来实现表单提交事件的相应，添加`handleSubmit`如下


```js
<form onSub className="comment-form">
  	<input value={this.state.input} type="text" className="input" onChange={this.handleChange} />
  	<button type="submit" className="submit-btn" >提交</button>
</form>

```

然后定义 handleSubmit

```js
handleSubmit = (e) =>{
	e.preventDefault()
	console.log('form submitting...')
}

```
由于使用了ES6的胖箭头函数语法，所以使用中，就不需要.bind(this)了

###拿到input 的输入

首先添加 ref 如下：

```js
<input ref={ value => this.comment = value} type="text" className="input"/>

```
上面，ref 的意思是“指针”。后面大括号中的内容，也就是

```js
value => this.comment = value

```

是一个胖箭头函数。其中value 指代当前input这个节点对应的object ，然后，

```js
this.comment = value

```

就是把input对象，赋值给一个成员变量，目的是在整个class 之内，可以随处访问。
这样，如果想在handleSubmit 函数中拿到用户输入的文本，就
```js
handleSubmit = () =>{
	console.log(this.comment.value)
}
```
### 修改 state

到这里，如何从form 的输入框中拿到字符串，这个技巧我们就掌握了。同时，这也是最简单的一种方式，另外，还可以通过 “受控组件” 的形式来取值。

### 修改 state


先来讨论render() 的本性：

>一旦state变，render()自动被重新执行

所以，界面由两条评论变成三条，不用修改dom节点，直接改变setState 的值

### 清空 input

最后，我们还需要在提交之后，清空input里的字符串。

handleSubmit 中添加
```js
this.comment.value = ''

```

但是，如果一个form的input 比较多，那么下面的方式可能更好

```js
handleSubmit=()=> {
	this.myForm.reset()
}
```
<form ref={value=>this.myForm = value}
onSubmit ={this.handleSubmit} className="comment-form">