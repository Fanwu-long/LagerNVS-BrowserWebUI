# 两种 Interactive + 统一门户

## 一个网站，两个入口

统一门户（自选 Live / Offline）：

| 版本 | 打开 | 给谁 |
|---|---|---|
| **自用版** | http://127.0.0.1:8766/?v=me | 你自己演示（稳定） |
| **别人用的版** | 同一服务 `?v=share`，或 `DEMO_STATUS.txt` 里的公网链接 | 发给同学/老师临时看 |

技术原理（详细）：http://127.0.0.1:8766/07_交互式渲染演示/06_交互功能优化/tech_principles.html

```bash
# 自用（默认打开 ?v=me）
python 07_交互式渲染演示/06_交互功能优化/start_portal.py

# 分享给别人（公网隧道；域名会变，看 DEMO_STATUS.txt）
python 07_交互式渲染演示/06_交互功能优化/start_portal.py --share --tunnel

# 若 Live GPU 也在本机 8765 监听，可再给 Live 开一条隧道写入分享配置
python 07_交互式渲染演示/06_交互功能优化/start_portal.py --share --tunnel --live-tunnel
```

---

## 门户里两张卡片

| 卡片 | 稳定地址 | 说明 |
|---|---|---|
| **Live** 实时神经网络 | http://127.0.0.1:8765/ | 要 A100 作业 + SSH；分享版需 `--live-tunnel` 或 `--live-url` |
| **Offline** 离线交互 | 门户内第二张 / 同域路径 | 本机 8766 即可，样本已审计 |

状态文件：`LagerNVS/DEMO_STATUS.txt`、`portal_config.json`

`*.trycloudflare.com` 会过期，**自用永远用 127.0.0.1**。

---

## 样本数量（Offline）

| 项目 | 数量 |
|---|---|
| 场景 | **16** |
| HQ 静帧 | **5** |
| Orbit 条目 | **12** |
| 输入缩略图 | **36** |

Live：`demo` + `scene_a`（2 场景）。

---

## 有什么区别（一句话）

- **Live** = 同一 LagerNVS 网络，按你当前位姿**当场** cross-attend 出 RGB，经 WebSocket 推帧。
- **Offline** = **同一类**神经渲染结果预先算好，浏览器只做 scrub / 看静帧。

详见门户内「技术原理」页。
