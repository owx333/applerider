# AppleRider

Transport management web app for bookings, drivers, vehicles, income/expense tracking, and daily closing. Single-page app (`index.html`) with **Firebase Auth**, **Firestore**, and **Storage**.

**Live:** [ride.guanzun.my](https://ride.guanzun.my)  
**Firebase project:** `applerider`

---

## 快速开始（5 分钟）

### 前置要求

- 现代浏览器（Chrome / Safari / Edge）
- 本地静态服务器（任选其一）：
  - Python 3
  - Node.js（`npx serve`）
- Firebase 账号（由管理员在 Console 创建，Email/Password 登录）

### 1. 克隆并进入仓库

```bash
git clone https://github.com/owx333/applerider.git
cd applerider
```

### 2. 启动本地预览

不要用 `file://` 直接打开 HTML（Firebase 可能异常）。用本地 HTTP 服务：

**Python 3**

```bash
python3 -m http.server 8080
```

**Node.js**

```bash
npx --yes serve -p 8080
```

浏览器打开：**http://localhost:8080**

### 3. 登录

1. 使用管理员提供的 Email / Password 登录  
2. Topbar 显示 **● Firebase Connected**（绿色）即后端正常  
3. 首个登录用户会自动成为 Admin（仅空库时）

---

## 项目结构

本仓库（GitHub Pages 前端）：

```
applerider/
├── index.html   # 完整 SPA（含 Firebase 配置）
└── CNAME        # 自定义域名 ride.guanzun.my
```

Firebase 规则与索引在**完整工作区**（与仓库同级目录），不在本 repo 内：

```
apple rider/                 # 本地完整工作区（示例路径）
├── applerider-repo/         # ← 本 Git 仓库
├── firebase.json
├── firestore.rules
├── firestore.indexes.json
├── storage.rules
└── FIREBASE_SETUP.md        # Firebase 详细配置指南
```

---

## Firebase 配置（管理员）

### Console 一次性设置

1. [Firebase Console](https://console.firebase.google.com/) → 项目 **applerider**
2. **Authentication** → 启用 **Email/Password**
3. **Firestore** → 创建数据库（Production，`asia-southeast1` 推荐）
4. **Storage** → 启用
5. **Authentication → Users** → 添加管理员账号

### 部署安全规则

在含 `firebase.json` 的目录执行（非 `applerider` 仓库根目录）：

```bash
cd "/path/to/apple rider"   # 含 firebase.json 的父目录

firebase login
firebase use applerider
firebase deploy --only firestore:rules,storage
```

登录后若出现 **Permission Denied**，通常是规则未部署。

更完整的说明（权限模型、集合、Storage 路径、FAQ）见工作区内的 `FIREBASE_SETUP.md`。

---

## 部署（GitHub Pages）

本仓库已配置 Pages：

1. Push 到 `main` 分支  
2. GitHub → Settings → Pages → 使用 `main` / root  
3. 自定义域名见 `CNAME`（`ride.guanzun.my`）

仅更新前端时，只需 push `index.html`；改 Firestore/Storage 规则需单独 `firebase deploy`。

---

## 角色与功能

| 角色 | 能力 |
|------|------|
| **Admin** | 订单、客户、司机、车辆、收支、日结、设置 |
| **Driver** | 查看/更新自己的 trips、记录 income |

App 内支持 **中文 / English** 切换（Topbar 语言按钮）。

---

## 常见问题

| 问题 | 处理 |
|------|------|
| 本地白屏或 Firebase 报错 | 用 `http://localhost` 启动，勿用 `file://` |
| Permission Denied | 部署 Firestore + Storage rules |
| 司机看不到 My Trips | 司机 Login Email 须与 Firebase Auth 账号一致 |
| 连接状态红点 | Settings → Firebase Connection → Test Connection |

---

## License

Private / internal use — contact repository owner for access.
