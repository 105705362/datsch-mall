## 1.java开发环境安装


### 1.1开发环境

以下版本是最低要求的！！！ 提问问题前请注意开发环境！！

| 工具      | 版本    |
|---------|-------|
| jdk     | 17    |
| mysql   | 5.7+  |
| redis   | 4.0+  |
| nodejs  | 14-16 |
| xxl-job | 2.4.0 |


### 1.2 安装jdk + mysql + redis + maven

如果不了解怎么安装jdk的，可以参考 [菜鸟教程的java相关](https://www.runoob.com/java/java-environment-setup.html)
- 教程展示的是oracle，需要自行搜索openjdk的下载链接，下载jdk17版本

如果不了解怎么安装mysql的，可以参考  [菜鸟教程的mysql相关](https://www.runoob.com/mysql/mysql-install.html) 

如果不了解怎么安装maven的，可以参考  [菜鸟教程的maven相关]( https://www.runoob.com/maven/maven-setup.html ) 

如果对于redis的安装并不了解的，可以参考 [菜鸟教程的redis相关](https://www.runoob.com/redis/redis-install.html)

安装相对简单，网上也有很多教程，这里就不多讲述。安装完按需对redis进行配置，后启动redis服务即可。

### 2.启动

- 推荐使用idea，安装lombok插件后，使用idea导入maven项目
- 将yami_shop.sql导入到mysql中，修改`application-dev.yml`更改 datasource.url、user、password
- 通过修改`shop.properties` 修改七牛云、阿里大鱼等信息
- 修改`api.properties` 修改当前接口所在域名，用于支付回调
- 启动redis，端口6379
- 通过`WebApplication`启动项目后台接口，`ApiApplication` 启动项目前端接口
- xxl-job定时任务，通过github或者gitee下载xxl-job的已经打包好的源码，把`XxlJobConfig.class`这个文件的代码注释打开，配置yml文件中相关xxl-job配置即可使用


## 3.vue开发环境安装

这是一套正常的vue启动流程。如果你无法理解，可能要先学习一下vue...

#### 3.1 安装nodejs

[NodeJS](https://nodejs.org)  项目要求最低 18.12.0，推荐 20.9.0

如果不了解怎么安装nodejs的，可以参考   [菜鸟教程的nodejs相关](https://www.runoob.com/nodejs/nodejs-install-setup.html)



#### 3.2 安装依赖启动项目

项目要求使用 [pnpm](https://www.pnpm.cn/)  包管理工具

使用编辑器打开项目，在根目录执行以下命令安装依赖

```bash
pnpm i
```

如果不想使用 pnpm，请删除 `package.json` 文件中  `preinstall`  脚本后再进行安装

```json
{
    "scripts" : {
        "preinstall": "npx only-allow pnpm"  // 使用其他包管理工具（npm、yarn、cnpm等）请删除此命令
    }
}
```


H5端和平台端修改文件`.env.production`（生产环境）/ `.env.development`（开发环境）
里面的`VITE_APP_BASE_API`为api接口请求地址， `VITE_APP_RESOURCES_URL`为静态资源文件url 

```json
// api接口请求地址
VITE_APP_BASE_API = 'http://127.0.0.1:8085'

// 静态资源文件url
VITE_APP_RESOURCES_URL = 'https://img.mall4j.com/'

```

mall4m小程序端修改文件`utils\config.js`，里面的`domain`为api接口请求地址

注意！！如果启动uni项目或者小程序，默认后台api服务端口号为8086，
如果启动后台项目，默认后台admin服务端口号为8085，请对照仔细填写后再启动，如遇401状态码，仔细检查端口号是否配置正确！
如果后台启动后，图形验证码显示“接口验证失败数过多，请稍后再试”，请F12打开network确定连接的admin服务端口号是否正确，ip或域名是否正确，
如果有配置nginx，还要确认下项目访问路径是否正确，可以通过地址+/doc.html来访问接口文档确定是否正确访问到admin服务




运行dev环境：

```bash
npm run dev
```

运行dev环境(H5)：

```bash
npm run dev:h5
```
