# V2Ray Worker

An all-in-one toolkit for running V2Ray on Cloudflare Workers. Create VLESS and Trojan configs and serve subscription links straight from your own Worker, with all settings kept in Cloudflare KV.

基于 Cloudflare Workers 的 V2Ray 一站式解决方案。可在你自己的 Worker 上生成 VLESS 和 Trojan 配置并提供订阅链接，所有设置均保存在 Cloudflare KV 中。

[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/0xdolus/v2ray-worker?style=flat)](https://github.com/0xdolus/v2ray-worker/stargazers)
[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/0xdolus/v2ray-worker)

---

### Features / 功能特性

- Generates **VLESS** configs out of the box / 内置 **VLESS** 配置生成器
- Generates **Trojan** configs out of the box / 内置 **Trojan** 配置生成器
- Provides subscription links for V2Ray clients / 支持 V2Ray 客户端订阅链接
- Persists settings in Cloudflare **KV** / 设置保存在 Cloudflare **KV** 中
- One-click deploy via GitHub Actions / 通过 GitHub Actions 一键部署
- Written entirely in **TypeScript** / 全部使用 **TypeScript** 编写

---

### Compatible clients / 兼容客户端

Any client that handles VLESS or Trojan over WebSocket and can import subscription links should work.

任何支持 WebSocket 传输的 VLESS / Trojan 并可导入订阅链接的客户端均可使用。

| Platform / 平台 | Client / 客户端 |
| --- | --- |
| Android | [v2rayNG](https://github.com/2dust/v2rayNG) |
| Windows / Linux / macOS | [v2rayN](https://github.com/2dust/v2rayN) |
| iOS / macOS | Shadowrocket, Streisand, V2Box |

#### v2rayNG

A V2Ray client for Android, supporting [Xray core](https://github.com/XTLS/Xray-core) and [v2fly core](https://github.com/v2fly/v2ray-core).

适用于 Android 的 V2Ray 客户端，支持 [Xray core](https://github.com/XTLS/Xray-core) 和 [v2fly core](https://github.com/v2fly/v2ray-core)。

- **Download / 下载：** https://github.com/2dust/v2rayNG/releases
- **Geoip / Geosite：** the `geoip.dat` and `geosite.dat` files are located in `Android/data/com.v2ray.ang/files/assets` (the path may differ on some devices). The built-in download feature fetches enhanced versions from [v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat) and requires a working proxy.
  `geoip.dat` 和 `geosite.dat` 位于 `Android/data/com.v2ray.ang/files/assets`（部分设备路径可能不同）。内置下载功能会从 [v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat) 获取增强版本，需要可用的代理。
- **GPG verification / GPG 签名校验：** release files are signed with GPG to verify authenticity and integrity and to help prevent mirror, ISP, or CDN hijacking.
  发布文件已使用 GPG 签名，可用于校验真实性与完整性，预防镜像站、运营商或 CDN 劫持。

  Fingerprint / 公钥指纹：
  ```
  7694 5E9F 3E9A 168F 8070 F195 805D 661C
  134D FAF6 8903 C199 463C 31E5 AE90 3AE0
  ```

More in the [v2rayNG wiki](https://github.com/2dust/v2rayNG/wiki) / 更多内容请见 [v2rayNG wiki](https://github.com/2dust/v2rayNG/wiki)。

---

### Deploy / 部署

1. Fork this repository and enable GitHub Actions.
   Fork 本仓库并启用 GitHub Actions。
2. In Cloudflare, create a KV namespace named `settings` and copy its ID.
   在 Cloudflare 中创建名为 `settings` 的 KV 命名空间，并复制其 ID。
3. In your fork, go to **Settings → Secrets and variables → Actions** and add a secret named `KV_NAME` with the namespace ID as its value.
   在你的仓库中进入 **Settings → Secrets and variables → Actions**，添加名为 `KV_NAME` 的 secret，值为该命名空间 ID。
4. Edit `README.md`, find the button URL below, and replace `https://github.com/USER/REPO_NAME` with your own repository URL.
   编辑 `README.md`，找到下方按钮链接，将 `https://github.com/USER/REPO_NAME` 替换为你自己的仓库地址。
5. Click **Deploy with Workers** and follow the prompts.
   点击 **Deploy with Workers** 并按提示操作。

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/USER/REPO_NAME)

---

### Usage / 使用方法

1. Open your Worker URL. / 打开你的 Worker 地址。
2. Set your UUID / password in the panel. / 在面板中设置 UUID / 密码。
3. Copy the subscription link. / 复制订阅链接。
4. Import it into your client (for example, v2rayNG or v2rayN). / 将其导入客户端（例如 v2rayNG 或 v2rayN）。

---

### Proxy IPs / 代理 IP

A list of proxy IPs is available at / 代理 IP 列表：  
https://rentry.co/CF-proxyIP

---

### Development guide / 开发指南

#### Note / 提示

- Clone the repository and run `npm install` to set up dependencies.
  克隆仓库并运行 `npm install` 安装依赖。
- Start a local dev server with `npx wrangler dev`.
  使用 `npx wrangler dev` 启动本地开发服务器。
- Build and deploy manually with `npx wrangler deploy`.
  使用 `npx wrangler deploy` 手动构建并部署。
- Make sure the `settings` KV namespace is bound in `wrangler.toml`.
  确保 `wrangler.toml` 中已绑定 `settings` KV 命名空间。

---

### Credits / 致谢

- The VLESS generator is adapted from [Zizifn Edge Tunnel](https://github.com/zizifn/edgetunnel) and rewritten in TypeScript.
  VLESS 生成器改编自 [Zizifn Edge Tunnel](https://github.com/zizifn/edgetunnel)，并使用 TypeScript 重写。
- The Trojan generator is adapted from [ca110us/epeius](https://github.com/ca110us/epeius/tree/main) and rewritten in TypeScript.
  Trojan 生成器改编自 [ca110us/epeius](https://github.com/ca110us/epeius/tree/main)，并使用 TypeScript 重写。

---

### Disclaimer / 免责声明

This project is intended for educational and personal use. You are responsible for following Cloudflare's Terms of Service and the laws that apply where you live.

本项目仅供学习和个人使用。请自行遵守 Cloudflare 服务条款及所在地区的法律法规。

---

### Feedback / 反馈

Spotted a bug or have a suggestion? [Open an issue](https://github.com/0xdolus/v2ray-worker/issues).

发现问题或有建议？欢迎 [提交 issue](https://github.com/0xdolus/v2ray-worker/issues)。

---

**About**  
A complete solution for V2Ray configs on Cloudflare Workers.  
基于 Cloudflare Workers 的 V2Ray 配置完整解决方案。

**Repository**: https://github.com/0xdolus/v2ray-worker  
**License**: GPL-3.0
