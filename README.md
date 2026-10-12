# 乐迪机器人 · APK 存档（原厂 + 去引导改包 + 公开版 Agent）

> **二进制不放在仓库里**，全部挂在 [Releases](../../releases/latest)。本仓库只放清单、校验值与说明。
>
> 这样做的原因：单包 70–92 MB，写进 git 会永久留在历史里（每次 clone 都得拉）；
> Release 附件不计入仓库体积、单文件上限 2 GB、要撤随时撤。

---

## 1. 里面有什么

| 类别 | 文件 | 大小 (B) | 包名 |
|---|---|---|---|
| **原厂** | `xldrbt_v1.5.10.apk` | 95,913,128 | `com.auric.intell.rbt.xldrbtx` |
| **原厂** | `com.auric.intell.rbt.xldtvrbtx-1.apk` | 74,029,122 | `com.auric.intell.rbt.xldtvrbtx` |
| **原厂** | `com.auric.intell.rbt.rbtclient.apk` | 18,149,220 | `com.auric.intell.rbt.rbtclient` |
| **改包** | `xldrbt_v1.5.10-noguide.apk` | 95,957,826 | `com.auric.intell.rbt.xldrbtx`（versionCode 160） |
| **自研** | `LediAgent.public-v223.apk` | 17,756,662 | `com.ledi.agent` |

- **原厂 3 份**是厂商发布的**原始安装包，一个字节都没改**。用途：① 同型设备复活的干净基底；
  ② 协议/接口取证；③ 软件保全。
- **`xldrbt_v1.5.10-noguide.apk`** 是在原厂主 App 上打过补丁的版本（去开机引导 / 界面与图标替换 /
  指向本机后端 / 注入自启接收器），**用 platform 密钥重签**。
- **`LediAgent.public-v223.apk`** 是叠加装的独立包名 Agent（反射调用原厂引擎做动作/表情/灯光/屏幕/语音），
  与设备上的原厂 App 互不干扰。

## 2. 下载与校验

在 [Releases](../../releases/latest) 页下载附件，然后核对校验值：

```cmd
:: Windows
certutil -hashfile xldrbt_v1.5.10.apk SHA256
:: Linux / macOS
sha256sum xldrbt_v1.5.10.apk
```

| 文件 | 大小 (B) | md5 | sha256 |
|---|---|---|---|
| `xldrbt_v1.5.10.apk` | 95913128 | `8cfff20c229ad34a96c9270e6a952190` | `abd5164ebc9f2e69a8c52d136b04d52c6e20670d51f44e52b13623e713a09fc8` |
| `com.auric.intell.rbt.xldtvrbtx-1.apk` | 74029122 | `8e5179b3282386994c4922af4ae1c729` | `8aed2e0a60efc5c0b3fab377199e6b27a819cf4a713c4ba6947064182445a73e` |
| `com.auric.intell.rbt.rbtclient.apk` | 18149220 | `c3e1e4f1998016c1471af1edd9772975` | `0c0e25c5f476abb3937e076ea68f733a0ae8b83167f7140278e8194444a75c82` |
| `xldrbt_v1.5.10-noguide.apk` | 95957826 | `3f83bc651f2e7ef255f25387961feb69` | `52f3a691fd06a3497da334fad6c5b0c06ab52a4ebeb66d182d6bb6826813d3c9` |
| `LediAgent.public-v223.apk` | 17756662 | `a775f93ba4d5b99cf37721d91914699c` | `7f9cdef4e0862e7e033aeaf1e70b86af849ccb8c2f60390c2d9e8f93c263e8a5` |

## 3. 原厂包 vs 改包（别搞混）

| | 是什么 | 能不能直接装 |
|---|---|---|
| 原厂 3 份 | 未改动的原样包 | 能装，但**别用它覆盖机器上正在跑的改包** |
| `-noguide` 改包 | 在原厂包上打过补丁 | 该 ROM **只认平台签名**，用 `adb install -r` 覆盖安装 |
| `LediAgent.public` | 独立包名叠加安装 | 直接 `adb install -r` |

```bash
adb install -r xldrbt_v1.5.10-noguide.apk   # 覆盖原厂主 App
adb install -r LediAgent.public-v223.apk    # 叠加装 Agent（包名不同，可与原厂共存）
```

> ⚠️ 刷机 / 覆盖安装原厂 App 属于**不可逆且可能让设备起不来**的操作。
> 动手前先备份，并确认你手上能刷回来。

## 4. 声明

原厂包的权利归原权利人。本仓库只做保存与不修改的转发，**不对这些包授予任何许可**；
改包同样不含对原厂代码的授权。全文见 [`NOTICE.md`](NOTICE.md)。

相关仓库：接口与文档整理见 [`ledi-smart-companion-robot-basic-features`](https://github.com/beizheji/ledi-smart-companion-robot-basic-features)。
