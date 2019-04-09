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