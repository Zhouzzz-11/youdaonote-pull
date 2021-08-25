1.进入测试目录

```javascript
cd /Users/sghl-11/test-demo/UI-cypress

```

2.安装（已有node、npm环境；node版本大于12.0.0，node安装见末尾）

```javascript
## 确保测试目录下已有node_modules或package.json
yarn init --yes
## 安装cypress
npm install cypress --save-dev
## demo运行
./node_modules/.bin/cypress open
## 测试目录下直接运行，在package.json中加
  "scripts": {
    "cypress:open": "cypress open"
  }
  
可运行命令
npm run cypress:open

```

附：nvm常用命令

● nvm install stable  安装最新稳定版 node

● nvm install <version>  安装指定版本，如：安装v4.4.0，nvm install v4.4.0

● nvm uninstall <version>  删除已安装的指定版本，语法与install类似

● nvm use <version>  切换使用指定的版本node

● nvm ls  列出所有安装的版本

