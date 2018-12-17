通过减少重复和繁琐的任务极大促进和加快了开发工作流程，CLI 工具使现代 Web 开发更加便利。最新版的 Vue CLI 3 不仅功能强大、灵活，还提供了完整图形用户界面，使用新的 Vue CLI 及其 Vue UI GUI 可以更轻松第创建新的 Vue.js 项目。

# 什么是 Vue CLI

Vue CLI 是一组用于快速原型设计、简化应用程序搭建和进行高效项目管理的工具。它由三个主要的工具组成：CLI、CLI Servive、CLI Plugins

- CLI 是一个 npm 包，通过 vue 命令提供核心功能。它可以帮我们轻松地构建一个新项目（vue create）或者快速创建原始构思（vue serve）。如果我们想要对项目进行更具体和可视化的控制，可以通过运行 vue ui 命令打开 CLI 的 GUI。
- CLI Service 是一个开发依赖项（vue-cli-service 二进制文件），安装在使用 CLI 创建的每个项目中。它可以帮助我们开发项目（vue-cli-service serve）、打包（vue-cli-service build），以及检查内部 Webpack 项目的配置（vue-cli-service inspect）。
- CLI 插件也是 npm 包，为项目提供额外的功能。它们的名字以 @vue/cli-plugin-（内置插件）或 vue-cli-plugin-（社区插件）开头。我们可以在开发过程中通过 vue add 命令添加它们。

# Vue CLI 功能

 Vue CLI 是一个用于提升 Vue.js 开发工作流程的全功能系统。Vue CLI 凭借其丰富的功能集，可加速和简化 Vue.js 项目开发。让我们看看它都有哪些功能：

- 基于插件的架构。Vue CLI 完全围绕插件而构建，所以非常灵活和可扩展。我们可以选择在项目创建过程中添加哪些内置插件，还可以在创建项目后随时添加任意数量的插件。
- Vue CLI 完全可配置、可扩展和可升级。
- 提供了一系列官方预装插件，集成了前端生态系统的一流工具（Babel、ESLint、TypeScript、PWA、Jest、Mocha、Cypress 和 Nightwatch）。
- 一个默认预设，我们可以在项目创建期间或之后根据我们的需求进行修改。
- 无需弹出。与 React 和 Angular CLI 工具相比，我们可以在创建项目后随时安全地检查和调整项目的 Webpack 配置，无需弹出应用程序并切换到手动配置。
- 多页面支持。
- 无需任何配置即可进行即时原型设计。不同的构建目标可以生成不同版本的项目——我们可以使用同一个代码库构建 App、库或 Web 组件。
- 现代模式功能。构建适用于现代浏览器的应用程序，同时兼容旧版本的浏览器。
- 一个完整的 GUI，可轻松创建、更新和管理复杂项目。
- UI 插件 API。Vue UI 公开了一个插件 API，我们可以用它将自定义功能添加到 CLI 的 GUI 版本中。
- 来自社区的大量有用插件。

# Vue CLI 入门

首先，我们需要安装 Vue CLI 3。它需要 Node.js 8.9+（推荐 8.11.0+）才能运行。打开终端或命令提示符，然后运行：

```
npm install -g @vue/cli
```

安装完成后，可以开始使用 vue 命令。要检查一切是否正常，可以运行 vue --version。它将显示已安装的 Vue CLI 版本。

# 即时原型设计

尽管 Vue CLI 主要用于处理复杂项目，但我们也可以用它快速、轻松地试验我们的原始想法。可以通过安装全局 Vue CLI 服务插件来激活即时原型设计功能：

```
npm install -g @vue/cli-service-global
```

从现在开始，我们可以随意使用 vue serve 命令。我们使用以下内容创建 App.vue 文件：

```
<template>
  <h1>Hello, Vue!</h1>
</template>
```

然后在同一个目录运行：

```
vue serve
```

这将启动 Vue CLI 开发服务器，并在 http://localhost8080/ 上运行该应用程序。当我们使用浏览器打开这个地址时，将看到 Hello,Vue！。

# 创建一个新项目

vue create 命令通过一个交互式进程来选择新项目的选项。让我们运行它，并看看它都有哪些选项。

```
vue create vuecli-project
```

在第一个窗口中，我们被要求选择一个预设。内置的预设只有一个，也就是默认的。我们将选择第二个选项，即手动选择项目所需的功能，然后按 Enter 继续。

![img](https://mmbiz.qpic.cn/mmbiz_png/XIibZ0YbvibkX0ZtGgAqFEHn2Hq3icia76qRgiayc4XFY7ETRxytxWmDVsfiawvkQtQibyg6Rs1H1oFbpJ3AnibbUT7xmw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在下一个窗口中，我们使用箭头键向上或向下导航功能列表，并用空格键选择我们想要的选项。在这里，除了 Babel 和 Linter/Formatter，我还选择了 Router 和 Vuex。选择所需功能后，按 Enter 继续。

![img](https://mmbiz.qpic.cn/mmbiz_png/XIibZ0YbvibkX0ZtGgAqFEHn2Hq3icia76qRvnabzuKcPXH0vU93cpbPPnec6owdibCPdPKR2uJGAiaozCjKyXxIsSqw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在下一个窗口中，系统会询问是否使用 Router 历史记录模式。我按 Enter 键，使用默认值 Yes。

![img](https://mmbiz.qpic.cn/mmbiz_png/XIibZ0YbvibkX0ZtGgAqFEHn2Hq3icia76qRydfTTsgFwP1egwrbbnx0JJ4WvoEfEGJKKr3XRqXbC0AgLoBZEI1K5g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在下一个窗口中，我们需要选择如何配置 Linter。我选择了 ESLint + Prettier。

![img](https://mmbiz.qpic.cn/mmbiz_png/XIibZ0YbvibkX0ZtGgAqFEHn2Hq3icia76qRbgI27My4iagVYyIEib18iaXooU6qsZztE4vibladPZthoNnicb53Wwicyqxw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在下一个窗口中，我们选择何时使用 Linter 检查项目。我选择了 Lint on save，也就是每次在保存文件时应用 Lint。

![img](https://mmbiz.qpic.cn/mmbiz_png/XIibZ0YbvibkX0ZtGgAqFEHn2Hq3icia76qRT0yQdsYiaDsp0jBMB9vQdmrz3rLP8HgYx5hWCbAuLBq1CsfqHVSA2BA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在下一个窗口中，我们需要决定如何配置项目。是为每个功能使用单独的配置文件，还是在 package.json 文件中包含所有配置。我更喜欢使用单个配置文件，因此选择了 In package.json 选项。

![img](https://mmbiz.qpic.cn/mmbiz_png/XIibZ0YbvibkX0ZtGgAqFEHn2Hq3icia76qRyfKSQYzJ4jLGFC4gTibOzsn41eZiaP7FGEJkUAnIDIicSnNqqzSSJ0AwQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

在最后一个窗口中，我们将整个项目配置保存为一个易于使用的预设，用于未来的项目。预设保存在用户文件夹的.vuerc 文件中。

![img](https://mmbiz.qpic.cn/mmbiz_png/XIibZ0YbvibkX0ZtGgAqFEHn2Hq3icia76qRqXOVjlAnRRhkLqyqdRfKfzC4xwCNXNbYwje3snDyb9xqibXQicL1f43Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

完成这个过程后，将创建和配置项目，并下载和安装所需的软件包。

# 项目结构

在上面显示的项目文件夹中，有以下文件和文件夹：

- node_modules 文件夹包含了应用程序和开发工具所需的包。
- public 文件夹包含了静态项目资源文件，这些文件不会被包含在捆绑包中。
- src 文件夹包含了 Vue.js 应用程序的所有资源。
- .gitignore 包含了被排除在 Git 版本控制之外的文件和文件夹列表。
- babel.config.js 包含了 Babel 编译器的配置。
- package.json 包含了 Vue.js 开发所需的包列表以及用于开发工具的命令。
- package-lock.json 包含了项目所需的软件包及其依赖项的完整列表。
- README.md 包含了有关项目的一般性信息。

在上面显示的 src 文件夹中，我们有以下文件和文件夹：

- assets 文件夹用于放置应用程序所需的静态资源，这些资源将被包含在捆绑包中。
- components 文件夹用于放置应用程序的组件。
- views 文件夹用于放置通过 URL 路由功能来显示的组件。
- App.vue 是根组件。
- main.js 是创建 Vue 实例对象的 JavaScript 文件。
- router.js 用于配置 Vue 路由器。
- store.js 用于配置使用 Vuex 创建的数据存储。

默认项目配置包含了合理的设置，但如果有必要，我们也可以通过在项目文件夹中添加 vue.config.js 文件或通过向 package.json 文件添加 vue 部分来更改这些配置。

我们先试试第一种方法。我们创建一个 vue.config.js 文件，并在其中添加以下选项：

```
module.exports = {
  runtimeCompiler: true
}
```

这样就可以将组件模板定义为字符串，而不是使用模板元素。完整的配置选项请访问 Vue CLI Config 页面（https://cli.vuejs.org/config/）。

# 开发项目

Vue CLI Service 附带了三个默认脚本：serve、build 和 inspect。第一个用于开发过程。我们使用 npm run serve 命令运行我们的项目。

serve 命令将启动一个基于 webpack-dev-server 的开发服务器，它提供了热模块替换（HMR）功能。这意味着当我们修改并保存组件时，效果会立即反映出来，并且浏览器中的页面也会做出更新。

# 使用 Vue CLI 插件

在应用程序开发的某些时候，我们可能需要为项目添加一些额外的功能，为此我们需要安装 Vue CLI 插件。Vue CLI 插件可以修改 Webpack 配置，并向 vue-cli-service 注入新命令。要安装插件，我们需要使用 vue add 命令。

插件安装好以后，我们将在 src 文件夹中找到一个新的插件文件夹，新安装的插件就在这个文件夹中。

# 构建项目

在部署应用程序之前，你需要创建一组仅包含应用程序代码和内容的软件包以及它们所依赖的模块，以便可以将这些文件部署到生产环境的 HTTP 服务器种。

要构建应用程序，需要运行：

```
npm run build --modern
```

--modern 参数创建了两个版本的应用程序。其中一个针对可以支持最新 JavaScript 功能的现代浏览器，另一个是需要额外库来支持这些功能的旧浏览器。在部署好应用程序之后，选择使用哪个版本完全是自动化的！

注意：当我们运行 build 命令时，Vue CLI 允许我们指定——target 选项，将代码库用于不同的用途。默认构建目标为构建应用程序。我们还有两个选项可选择：将代码构建为库或 Web 组件。

构建过程完成后，将在项目根目录中创建 dist 文件夹。

# 使用 Vue UI

Vue CLI 3 功能非常强大，但也是要付出代价的，因为有太多的选项、命令和选项太多需要记住。这让得它变得更复杂，更难以使用。为了让一切回归到一个轻松愉快的状态，Guillaume Chau 创建了 Vue UI，极大简化了开发体验，并让它变得更加平易近人。

Vue UI 是使用自己的 UI 框架构建的，不需要 Electron 就可以在浏览器中运行它。只需在目录中运行 vue ui 命令即可。

启动 Vue 项目管理器，并选择“项目”选项卡。目前页还没有任何项目。我们需要通过 UI 创建新项目或导入使用 CLI 创建的项目。

我们切换到“创建”选项卡，浏览到应用程序所需的目录，然后单击“在此处创建新项目”。

在下一个页面，我们为项目文件夹命名，并选择包管理器。

在下一个页面，我们可以为项目选择预设。它可以是我们之前创建的默认、手动、远程或自定义预设。spa-simple 是自定义预设的一个示例。在这里，我们选择手动。

在下一个页面，我们选择要安装的插件。

最后，我们为选择安装的插件设置配置。然后，我们点击 Create Project 按钮。

创建好项目后，我们将被重定向到项目的仪表盘页面。

# 使用 Vue UI 项目仪表盘

“插件”部分列出了所有已安装的插件。要安装新插件，点击添加插件按钮即可。

我们可以搜索我们需要的插件，找到后点击 Install 按钮。在我们的例子中，我们搜索并安装了 bootstrap-vue 插件。

安装好插件后，我们可以在“配置”选项卡中设置选项。

在文件变更选项卡中，我们可以看到受影响的文件。在这里，我不想提交任何更改，所以我点了 Skip 按钮。

在 Dependencies 部分，我们列出了所有主要和开发依赖项。要添加依赖项，请单击“安装依赖项”按钮。

在模态窗口中，我们可以搜索主要或开发依赖项并安装它们。

在 Configuration 部分，我们可以添加的插件进行自定义设置。在这里，我们配置了 Vue CLI 和 ESLint 插件。

Tasks 部分为我们提供了一种便捷的方式来使用 Vue CLI 和其他插件提供的可用命令。在这个页面，我选择了 serve 任务。我们可以通过点击 Parameters 按钮来改变它的参数。

在模态窗口中，我们为要运行的任务选择参数。

当我们运行 serve 任务时，仪表盘将更新一些有用的信息。

当我们切换到 Output 选项卡，可以获取到任务日志。

当我们切换到 Analyzer 选项卡时，会得到一个有关整个项目信息的图表。

build 任务类似于 serve 任务，只是前者生成可用于生产环境部署应用程序包。

我们可以使用与 serve 任务相同的方式为 serve 任务设置参数。

inspect 任务的 Output 字段为我们提供了 Webpack 的配置信息。

我们使用 Vue UI 成功重新创建了我们的项目。正如我们所看到的，在使用 GUI 时，创建和配置过程变得更容易，也更愉快。

# 结论

在本文中，我们介绍了 Vue CLI 是一个完整的用于现代 Web 开发的系统。它让我们能够快速、轻松地使用整个 Vue 生态系统和第三方工具。当然，我们不一定要使用 Vue CLI，这是一种自主的选择。但如果是出于提高开发速度和质量方面的考虑，那么使用 Vue CLI 可以帮你更好地创建、管理和部署项目。[英文原文](https://code.tutsplus.com/tutorials/boost-your-vuejs-workflow-with-vue-cli-3--cms-32232)