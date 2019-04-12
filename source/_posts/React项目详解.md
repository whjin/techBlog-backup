---
title: React项目详解
date: 2019-04-09 20:02:01
category: ["前端"]
tags: ["react","javascript"]
comments:
---

# React项目指导 #

## 使用`webpack`需要安装的依赖 ##

1. `webpack`，`webpack-cli`，`react`，`react-dom`
2. `babel-loader`，`@babel/core`，`@babel/preset-env`，`@babel/preset-react`
3. 设置`.babelrc`，`{"presets": ["@babel/preset-env","@babel/preset-react"]}`
4. 设置`scripts`：
   
     ```javascript
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
    ```
5. 设置`webpack-dev-server`：   
    
    ```javascript
    devServer: {
      compress: true,
        port: 9000，
        hot: true
    },

    "start": "webpack-dev-server --config webpack.config.js" 
    ```
6. 设置`performance`：

    ```javascript
    performance: {
      hints: false
    }
    ```

<!--more-->

## `Component` ##

1. 基本组件

    ```javascript
    let title = <h1>Hello, world!</h1>
    
    ReactDOM.render(title,document.getElementById('root'))
    ```

2. 动态组件

    ```javascript
    import React from 'react';
    import ReactDOM from 'react-dom';
    
    let displayTime = () => {
      let nowTime = (
        <div>
          <span>现在时间：{new Date().toLocaleTimeString()}</span>
        </div>
      );
      ReactDOM.render(t
        nowTime,
        document.getElementById('root')
      );
    };
    
    setInterval(displayTime, 1000);
    ```

3. `class`组件构建器

    ```javascript
    import React, {Component} from 'react';
    import ReactDOM from 'react-dom';
    
    class HelloTitle extends Component {
      render() {
        return <h1>Hello,World!</h1>
      }
    }
    
    ReactDOM.render(
      <HelloTitle/>,
      document.getElementById('root')
    );
    ```

4. `props`属性

    ```javascript
    import React, {Component} from 'react';
    import ReactDOM from 'react-dom';
    
    class HelloTitle extends Component {
      render() {
        return <h1>Hello,{this.props.name}!</h1>
      }
    }
    
    let titleDiv = (
      <div>
        <HelloTitle name="React"/>
        <HelloTitle name="World"/>
      </div>
    );
    
    ReactDOM.render(
      titleDiv,
      document.getElementById('root')
    );
    ```

5. `props`多层使用

    ```javascript
    import React, {Component} from 'react';
    import ReactDOM from 'react-dom';
    
    class HelloTitle extends Component {
      render() {
        return <h1>Hello,{this.props.name}!</h1>
      }
    }
    
    class HelloDiv extends Component {
      render() {
        return <div><HelloTitle name={this.props.name}/></div>
      }
    }
    
    ReactDOM.render(
      <HelloDiv name="React"/>,
      document.getElementById('root')
    );
    ```

6. 组件复用

    ```javascript
    import React, {Component} from 'react';
    import ReactDOM from 'react-dom';
    
    class HelloTitle extends Component {
      render() {
        return <h1 style={this.props.style}>{this.props.content}</h1>
      }
    }
    
    class HelloDiv extends Component {
      render() {
        return <div>
          <HelloTitle content="比较大的字" style={{'fontSize': 18}}/>
          <HelloTitle content="比较小的字" style={{'fontSize': 12}}/>
        </div>
      }
    }
    
    ReactDOM.render(
      <HelloDiv/>,
      document.getElementById('root')
    );
    ```

## `Component`的状态`state`和生命周期 ##

### `state`属性 ###

```javascript
constructor(props) {
  super(props);
  this.state = {
    time: new Date().toLocaleTimeString()
  }
}

render() {
  return <h1>现在时间是{this.state.time}</h1>
}
```

组件构建完成后先执行的动作，`componentDidMount()`：

```javascript
componentDidMount() {
  let upTime = () => {
    this.setState({time: new Date().toLocaleTimeString()})
  };
  setInterval(upTime, 1000)
}
```

### `setState()`修改状态值 ###

```javascript
this.setState({time: new Date().toLocaleTimeString()})
```

### 生命周期 ###

1. 在`constructor`中初始化组件内部的资料。
2. 使用`render()`在网页上输出组件内容。
3. 输出后会执行`componentDidMount()`进行一次调用。
4. 当组件内部的`state`值被修改时执行`componentDidUpdate()`。
5. 当组件被移除时会执行`componentWillUnmount()`的内容一次。

## `Component`的事件处理 ##

1. 取得触发事件的DOM

```javascript
class InputGender extends Component {
  constructor(props) {
    super(props);
    this.state = {
      gender: ''
    };
    this.changeGender = this.changeGender.bind(this)
  }

  changeGender(event) {
    console.log(event.target.value);
    this.setState({
      gender: event.target.value
    });
  }

  componentDidUpdate() {
    console.log(`已将state.gender变动为：${this.state.gender}`)
  }

  render() {
    return (
      <select onChange={this.changeGender}>
        <option value="M">男</option>
        <option value="W">女</option>
      </select>
    )
  }
}
```

```javascript
class HelloTitle extends Component {
  render() {
    return <h1>{this.props.title}</h1>
  }
}

{(this.state.gender === 'M') ? <HelloTitle title="先生"/> : <HelloTitle title="女士"/>}
```

### 用绑定的`state`取得输入资料 ###

```javascript
class EasyForm extends Component {
  constructor(props) {
    super(props);
    this.state = {
      name: ""
    };
    this.changeState = this.changeState.bind(this);
    this.submitForm = this.submitForm.bind(this);
  }

  changeState(event) {
    this.setState({
      name: event.target.value,
    });
  }

  submitForm(event) {
    let element = document.querySelector('span');
    element.innerHTML = `${this.state.name}`;
    event.preventDefault()
  }

  render() {
    return (
      <div>
        <form onSubmit={this.submitForm}>
          <label>姓名：</label>
          <input id="name" name="name" onChange={this.changeState} value={this.state.name}/>
          <input type="submit" value="提交" style={{'marginLeft': 6}}/>
        </form>
        <p>现在输入的名字是：<span style={{'color': '#FF7F24'}}></span></p>
      </div>
    )
  }
}
```

### 受控组件 ###

```javascript
class EasyForm extends Component {
  constructor(props) {
    super(props);
    this.state = {
      lists: [
        {id: '01', listName: '写文章', check: false},
        {id: '02', listName: '写代码', check: false},
        {id: '03', listName: '旅游', check: true},
        {id: '04', listName: '踢球', check: true},
        {id: '05', listName: '公益', check: false},
      ]
    };
    this.submitForm = this.submitForm.bind(this);
    this.changeState = this.changeState.bind(this);
  }

  changeState(index) {
    let arrLists = this.state.lists;
    arrLists[index].check ? arrLists[index].check = false : arrLists[index].check = true;
    this.setState({
      lists: arrLists,
    });
  }

  submitForm(event) {
    let status = "目前做了：";
    this.state.lists.map((list) => list.check ? status += `${list.listName} ` : '');
    console.log(status);
    event.preventDefault()
  }

  render() {
    let lists = this.state.lists.map((list, index) => (
      <div key={list.id}>
        <input type="checkbox"
               checked={list.check}
               onChange={this.changeState.bind(this, index)}
               key={list.id}
        />
        <label>{list.listName}</label>
      </div>
    ));
    return (
      <form onSubmit={this.submitForm}>
        <div>
          <label>每日待办清单：</label>
          {lists}
        </div>
        <input type="submit" value="发送表单"/>
      </form>
    )
  }
}
```

### 非受控组件 ###

```javascript
class EasyForm extends Component {
  constructor(props) {
    super(props);
    this.submitForm = this.submitForm.bind(this);
    this.filebox = React.createRef()
  }

  submitForm(event) {
    console.log(`选择文档为：${this.filebox.current.files[0].name}`)
    event.preventDefault()
  }

  render() {
    return (
      <form onSubmit={this.submitForm}>
        <div>
          <label>上传文档：</label>
          <input type="file" ref={this.filebox}/>
        </div>
        <input type="submit" value="送出表单"/>
      </form>
    )
  }
}
```