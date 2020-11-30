---
title: React Native
date:
updated:
type: "tags"
comments:
categories: React
description: React Native
keywords: React Native
top_img: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=138416375,3718598577&fm=26&gp=0.jpg
cover: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=138416375,3718598577&fm=26&gp=0.jpg
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
# 1.环境配置

```
npx react-native init AwesomeProject

运行
cd AwesomeProject
yarn android
# 或者
yarn react-native run-android

记住路径不能使用中文
```

# 2.样式设置

```
const styles = StyleSheet.create({
  bigBlue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
  },
  red: {
    color: 'red',
  },
});
常见的做法是按顺序声明和使用style属性，以借鉴 CSS 中的“层叠”做法（即后声明的属性会覆盖先声明的同名属性）

宽高和弹性布局
	const styles = StyleSheet.create({
      container:{
        display:"flex",
        justifyContent:"center",
        alignItems:"center",
        flexDirection:"row"
      },
      bigBlue: {
        backgroundColor:"red",
        height:20,
        width:20,
        marginLeft:20
      },
    });
```

# 3.组件状态

```
状态
	
组件之间的传值
class Greeting extends Component {
  render() {
    return (
      <View style={{alignItems: 'center', marginTop: 50}}>
        <Text>Hello {this.props.name}!</Text>
      </View>
    );
  }
}

export default class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{alignItems: 'center'}}>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}

//实现登陆页面
register = (email)=>{
      alert(email)
  }
  render() {
    return (
      <View>
        <TextInput placeholder="请输入邮箱" onChangeText={(text)=>{this.changeemail(text)}}></TextInput>
        <TouchableOpacity onPress={()=>{this.register(this.state.email)}} style={{backgroundColor:"#7a42f4",padding:10,alignItems:"center",margin:15,height:40}}>
          <Text style={{color:"white"}}>注册</Text>
        </TouchableOpacity>
      </View>
    );
  }
```

# 4.组件库

```
React Native Elements
lottie-react-native
react-native-vector-icons
antd
```

# 5.存储组件库

```
AsyncStorage  安装组件
yarn add @react-native-community/async-storage
```

# 6.状态栏组件

```
StatusBar
```

# 7.网络请求

```
fetch
fetch('https://mywebsite.com/endpoint/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    firstParam: 'yourValue',
    secondParam: 'yourOtherValue',
  }),
});
function getMoviesFromApiAsync() {
  return fetch('https://facebook.github.io/react-native/movies.json')
    .then((response) => response.json())
    .then((responseJson) => {
      return responseJson.movies;
    })
    .catch((error) => {
      console.error(error);
    });
} .catch((error) =>{
        console.error(error);
      });
```

