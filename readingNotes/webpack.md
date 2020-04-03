# 《Webpack》    

## 1. 工作流程

### 1.初始化阶段

1. 初始化参数

    从配置文件和shell语句读取参数。

2. 实例化compiler

    compiler 负责文件监听和启动编译。
3. 加载插件

    依次调用插件的apply方法，让插件可以监听后续所有事件节点。

4. environment

    开始应用node.js的文件风格到compiler

5. entry-option

    读取entry配置文件

6. after-plugins

    调用完插件apply的方法

7. after-resolvers

    初始化配置resolver

### 2.编译阶段

1. run

    启动一次编译
    
2. watch-run

    和run类似，他是出于监听模式下的run
    
3. compile

    告诉插件一次新的编译启动，并传递给插件compiler对象
    
4. compilation 

    以开发者运行时，每当文件变化，便有一个新的compilation被创建。
    
    compilation阶段的小事件
    
    1.build-module
    
        使用对应的loader去转变一个模块
        
    2.normal-module-loader
        
        loader转换后，使用acorn解析转换后的内容，输出对应的语法树
        
    3.program
    
        分析AST抽象语法树，遇到require时将其加入以来的模块列表中，容易对新找出的模块依赖进行递归分析
        
    4.seal
    
        所有模块转换完成，生成chunk
    
    
     

5. make 

    一个新的compilation被创建，即将冲entry开始读取文件，根据配置的loader进行编译
    
6. after-compile 

    完成一次编译
    
7. invalid

    每当文件不存在报错
    
### 3. 输出阶段

1. should-emit

    所有文件已生成，询问插件哪些文件输出，哪些不输出

2. emit

    执行文件输出，获取或修改输出文件内容
    
3. after-emit

    文件输出完成
    
4. done

    完成一次编译
    
5. failed

    在编译中遇到异常，导致webpack退出
    

    






 


