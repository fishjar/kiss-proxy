# KISS-PROXY

基于 `cloudflare workers` 的简单接口代理，可用于 [KISS Translator](https://github.com/fishjar/kiss-translator) 翻译服务。

## 1、准备

- 一个 cloudflare（https://www.cloudflare.com/） 帐号
- 一个可以访问的域名（需要域名是因为默认的 `*.workers.dev` 无法访问）

## 2、部署

```sh
git clone https://github.com/fishjar/kiss-proxy.git
cd kiss-proxy
yarn install
yarn deploy
```

## 3、设置自定义域名

- 登录 cloudflare
- 找到刚才部署的 worker
  - 触发器 > 添加自定义域

## 4、最终接口地址

- 谷歌翻译: `https://<设置的域名地址>/gt`
- OpenAI: `https://<设置的域名地址>/openai`

## 5、添加更多代理

找到源代码，修改这一段：

```js
const sites = {
  "/gt": {
    method: "GET",
    url: "https://translate.googleapis.com/translate_a/single",
  },
  "/openai": {
    method: "POST",
    url: "https://api.openai.com/v1/chat/completions",
  },
};
```

然后重新部署：

```sh
yarn deploy
```
