# JavaScript

```
运算符环境搭建 # 浏览器 <script>
语法
    基础语法
        注释
        变量定义 # var
            变量类型 # 全局变量 本地变量
            数据类型 # 对应字面量
        运算符
        流程控制
        数组
        对象
        函数
```

# Node

```
环境搭建 # NodeJS WebStorm
    命令行
        node
        npm # http://username:password@server:port
            install # -g --save --save-dev
            uninstall
            add
            update
            cache # cache clean --force
            info
            link
            config # set get delete registry https://registry.npm.taobao.org 镜像 proxy=http://127.0.0.1:8087 https-proxy http://server:port 设置https代理
模块
    os
    http
    fs
Yarn # yarn
    命令行
        yarn
            init
            add # package@version latest tag
            remove
            upgrade
            install
            cache # ls clean
            config # set registry https://registry.npm.taobao.org --global //yarn是Facebook公司替代npm的工具 这里是设置国内的的镜像源。  disturl https://npm.taobao.org/dist --global
            
```

# Vue

```

    命令行
        vue

```

Vue 指令

Vue 修饰符

Vue 循环

Vue 条件判断

Vue 双向数据绑定

Vue 事件处理

Vue 路由

Vue 自定义指令

# React

```
state环境搭建
    命令行
        create-react-app
JSX
	注释
元素数组
样式
表达式
class 属性
for 属性
组件
    组件定义
        props defaultProps
        state
    生命周期
    事件处理
React Native
    环境搭建 # react-native-cli 安装脚手架
        项目结构
    命令行
        react-native
        	init # --version 0.55.4 指定版本
        	run-ios
        	run-android
        	upgrade
        	start # --reset-cache 清楚缓存
```

# PropTypes

```
支持的检验类型
React.PropTypes.array 数组类型
React.PropTypes.bool 布尔类型
React.PropTypes.func 函数类型
React.PropTypes.number 数字类型
React.PropTypes.object 对象类型
React.PropTypes.string 字符串类型
React.PropTypes.node 可渲染节点
React.PropTypes.element React 元素
React.PropTypes.instanceOf(Message) 某个对象的实例
React.PropTypes.oneOf(['News', 'Photos']) 枚举类型
React.PropTypes.oneOfType([
      React.PropTypes.string,
      React.PropTypes.number,
      React.PropTypes.instanceOf(Message)
    ]) 指定类型
React.PropTypes.arrayOf(React.PropTypes.number) 指定类型数组
React.PropTypes.objectOf(React.PropTypes.number) 指定类型的属性构成的对象
React.PropTypes.shape({
      color: React.PropTypes.string,
      fontSize: React.PropTypes.number
    }) 特定 shape 参数的对象
React.PropTypes.func.isRequired 不可为null
React.PropTypes.any.isRequired
```

# Argular

```
环境配置

Argular 2
    环境配置
    命令行
        ng
            new # 创建项目
            serve # --open
```

# Hybrid

```
Cordova
    
        命令行
            cordova # -v
                create # 创建项目
                platform # add rm
                run # 运行项目
PhoneGap
    环境搭建 # phonegap@latest
        命令行
            phonegap # -v
                create # 创建项目
                serve
                run # android 运行项目
```