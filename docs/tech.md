# 技术选型和部署

### 前端

前端总体基于 React 框架进行编写，为 UI 编写方便使用了 antd 组件库。

前端开发思路以组件式开发为主，而不是页面式开发，用户的主页与边栏之间的交互操作均使用组件切换实现，而不是页面切换，在程序中对 react-router 的使用很少，降低了页面切换带来的效率影响及交互上的易用性降低。

### 后端

后端基于 Django 框架进行编写，采用 pytest作为视图函数的测试框架。生产环境中，使用uWSGI进行部署，采用python-dotenv存储环境配置，对于异步任务时的多进程管理，我们采用了 multiprocessing 库。

为统一各成员间的代码风格，后端开发中使用 black 作为自动代码风格格式化工具。