---
layout:           post
title:            React Context 学习
subtitle:         createContext 传入的默认值不起作用
date:             2019-08-13
anthor:           caiyun
header-img:       img/transform-img/transform-header.jpg	 
catalog:          true
tags:
    - React
---

今天学习 React Context 内容，根据官方文档输入如下代码

```JavaScript
import React, { Component, Fragment } from 'react';

const ThemeContext = React.createContext('light')

class App extends Component {
    render() {
        return (
            <Fragment>
                <ThemeContext.Provider value={'test'}>
                    < Toolbar />
                </ThemeContext.Provider>
            </Fragment >
        )
    }
}

function Toolbar() {
    return (
        <Fragment>
            <ThemedButton />
        </Fragment>
    )
}

class ThemedButton extends Component {
    static contextType = ThemeContext;

    render() {
        return (
            <Button theme={this.context} />
        )
    }
}

function Button(props) {
    return (
        <Fragment>
            {
                props.theme
            }
        </Fragment>
    )
}

export default App;
```

然后想测试下 `React.createContext` 传入的默认值是否起作用，于是将 `<ThemeContext.Provider value={'test'}>` 中的 `value{'test'}` 去掉了，但是发现 `React.createContext('light')` 中传入的 'light' 并没有发挥默认值的作用，然后查了些资料

解决方法：
去掉 ThemeContext 相关的 Provider，即将 `App` 组件更改为:

```javascript
    render() {
        return (
            <Fragment>
                <ThemeContext.Provider value={'test'}>
                    < Toolbar />
                </ThemeContext.Provider>
            </Fragment >
        )
    }
}
```

这样默认值就起作用了~~

参考文档：https://github.com/reagent-project/reagent/issues/370