---
title: React面试-2
date:
updated:
type: "tags"
comments:
categories: 面试
description: React面试-2
keywords: React面试-2
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2431606259,2554064138&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---

# 1.React的Portal是干什么的
```js
Portals 提供了一种很好的将子节点渲染到父组件以外的 DOM 节点的方式。
现在有两个组件，Dog和Cat，我们想让Dog的子组件Puppy放到Cat里，当欺负Puppy的时候，即使相隔千里Dog也能感受到。怎么做？用portal！
ReactDOM.createPortal(child, container)

const dogRoot = document.getElementById("dog-house");
const catRoot = document.getElementById("cat-house");
//创建一个Puppy组件
class Puppy extends React.Component {
  constructor(props) {
    super(props);
    // 创建一个容器标签
    this.el = document.createElement("div");
  }
  componentDidMount() {
      // 把容器标签挂到 catRoot DOM下
    catRoot.append(this.el);
  }
  componentWillUnmount() {
    catRoot.removeChild(this.el);
  }
  render() {
      // 利用portal把Puppy的内容放到容器里
    return ReactDOM.createPortal(this.props.children, this.el);
  }
}


//创建Dog组件
class Dog extends React.Component {
  constructor(props) {
    super(props);
    this.state = { bark: 0 };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
      // 点击的时候 bark + 1
    this.setState((state) => ({
      bark: state.bark + 1,
    }));
  }

  render() {
     // 看上去Puppy组件是在Dog挂在Dog组件里，但其实它被挂载在其它地方
    return (
      <div onClick={this.handleClick}>
        <p>The number of times a big dog barks: {this.state.bark}</p>
        <h3>Dog: </h3>
        <p>I can't see my children, but I can feel them</p>
        <Puppy>
          <Bully target={'Puppy'}/>
        </Puppy>
        <Bully target={'Dog'}/>
      </div>
    );
  }
}

ReactDOM.render(<Dog />, dogRoot);


//再创建一个代替欺负Puppy的按钮组件
function Bully(props) {
  return (
    <>
      <button>Bully the {props.target}</button>
    </>
  );
}

第一个参数（child）是任何可渲染的 React 子元素，例如一个元素，字符串或碎片。第二个参数（container）则是一个 DOM 元素。
```

# 2.如何在React中使用innerHTML
```js
增加dangerouslySetInnerHTML属性，并且传入对象的属性名叫_html
function Component(props){
    return <div dangerouslySetInnerHTML={{_html:'<span>你好</span>'}}>
            </div>
}
```