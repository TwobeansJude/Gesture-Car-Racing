# 🏎️ Gesture Car Racing

> **用手势开赛车！** 打开摄像头，双手倾斜控制方向，躲避车流，挑战最高分。

A browser-based racing game controlled entirely by hand gestures. Powered by **MediaPipe Hands** and **Canvas API** — no keyboard, no mouse, just your hands.

---

> 打开浏览器 → 允许摄像头 → 双手放入画面 → 开始飙车！

---

## ✨ Features

- **🖐️ 手势操控** — 通过双手倾斜角度实时控制赛车转向，自然直观的人机交互
- **📷 实时摄像头** — 基于 Google MediaPipe Hands，毫秒级手部关键点检测
- **🎯 非线性操控曲线** — 小幅倾斜被阻尼（防止误触），大幅倾斜被放大（紧急避让），手感更加自然
- **🛣️ 渐进式难度** — 四层递进：车流汇入 → 高速路段 → 疯狂早高峰 → 超越极限
- **💻 零依赖开箱即用** — 单 HTML 文件，浏览器打开即玩，无需安装任何东西
- **🎨 完整 UI 体验** — 教程引导、实时 HUD、结束结算，以及右下角摄像头画中画

---

## 🚀 Quick Start

### 方式一：直接打开（推荐）

1. 下载 `index.html`
2. 用浏览器打开
3. 允许摄像头权限
4. 🏁 开始游戏！

### 方式二：本地服务器

```bash
# Python
python -m http.server 8000

# Node.js
npx serve .

# VS Code
# 安装 Live Server 插件，右键 → Open with Live Server
```

然后访问 `http://localhost:8000`

> ⚠️ **注意**：由于浏览器安全策略，摄像头 API 需要在 `localhost` 或 HTTPS 环境下才能使用。直接用 `file://` 协议打开可能无法获取摄像头权限。

---

## 🕹️ How to Play

| 手势 | 效果 |
|------|------|
| 双手水平 | 直行 🏁 |
| 左手高、右手低 | 左转 ⬅️ |
| 右手高、左手低 | 右转 ➡️ |
| 单手/无手 | 方向自动回正 |

1. 将双手放入摄像头画面中
2. 像握方向盘一样，倾斜双手来控制赛车方向
3. 躲避路上的障碍车辆
4. 行驶越远，分数越高，难度越大！

---

## 🧠 How It Works

```
摄像头采集 → MediaPipe Hands 手部关键点检测
    ↓
提取双手食指根部坐标 → 计算双手连线角度
    ↓
非线性映射 (sign(x) × |x|¹·⁸) → 转向信号
    ↓
Canvas 实时渲染 → 玩家赛车移动 ← 碰撞检测
    ↓
分数 & 难度更新 → 障碍物生成
```

- **手势识别**：MediaPipe Hands 21-point hand landmark detection
- **信号处理**：`atan2` 计算双手倾斜角 → 非线性响应曲线 → 阻尼衰减（无手时自动回正）
- **游戏渲染**：原生 Canvas 2D API，60fps requestAnimationFrame 游戏循环
- **难度系统**：基于行驶距离的四档递进，动态调整车速和障碍物密度

---

## 🏗️ Tech Stack

| 领域 | 技术 |
|------|------|
| 手势识别 | MediaPipe Hands (@mediapipe/hands) |
| 视频采集 | WebRTC (Navigator.mediaDevices) |
| 游戏渲染 | HTML5 Canvas 2D API |
| 前端 | Vanilla HTML + CSS + JavaScript |
| 依赖管理 | jsDelivr CDN (零 npm 依赖) |

---

## 📁 Project Structure

```
Gesture-Car-Racing/
└── index.html          # 所有代码（HTML + CSS + JS）都在这里
```

是的，整个项目只有一个文件！🎉

---

## 🎯 难度等级

| 等级 | 分数门槛 | 名称 | 变化 |
|------|----------|------|------|
| 1 | 0 | 市区行驶 | 初始速度，低密度 |
| 2 | >10 | 车流汇入 | 速度 ↑，密度 ↑ |
| 3 | >30 | 高速路段 | 速度 ↑↑，密度 ↑↑ |
| 4 | >60 | 疯狂早高峰 | 速度 ↑↑↑，密度 ↑↑↑ |
| 5 | >100 | 超越极限 | 最高速度 & 密度 |

---

## 🔧 Browser Compatibility

| 浏览器 | 支持情况 |
|--------|----------|
| Chrome 88+ | ✅ 完美支持 |
| Edge 88+ | ✅ 完美支持 |
| Firefox 99+ | ✅ 支持 |
| Safari 15+ | ✅ 支持 |
| 移动端浏览器 | ⚠️ 摄像头可用但双手操作不便 |

---

## 📝 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 👤 Author

**Jude ZHAO** ([@TwobeansJude](https://github.com/TwobeansJude))

---

## ⭐ Acknowledgments

- [MediaPipe](https://mediapipe.dev/) — Google's open-source machine learning pipeline for hand tracking
- Canvas API — MDN Web Docs

---

> 🏎️ *Put your hands in the air, and drive like you just don't care!*
