# VocabFlash 🚀

**A Modern, Scientific IELTS Vocabulary Learning App**

一个现代化、科学化的雅思词汇学习应用，基于 SM-2 间隔重复算法和多样化学习模式，帮助你高效掌握雅思核心词汇。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![IELTS Vocabulary](https://img.shields.io/badge/Vocabulary-3673+-blue.svg)](https://github.com/kinsung97/VocabFlash)
[![Features](https://img.shields.io/badge/Features-SM2%20%7C%204%20Modes%20%7C%20Analytics-green.svg)](https://github.com/kinsung97/VocabFlash)

***

## ✨ 核心特性

### 🧠 科学记忆系统

- **SM-2 间隔重复算法**：根据艾宾浩斯遗忘曲线动态调整复习间隔
- **智能难度分级**：5 级难度体系（基础→入门→中级→进阶→高级）
- **技能标签系统**：听力/阅读/写作/口语四维分类
- **场景化学习**：22 个雅思考试场景分类

### 📚 完整雅思词库

- **3673+ 核心词汇**：覆盖雅思听说读写全部高频词汇
- **科学分类体系**：
  - 自然地理、学校教育、科技发明、文化历史
  - 饮食健康、建筑场所、交通旅行、国家政府
  - 社会经济、法律法规、身心健康等 22 个场景
- **丰富词义信息**：音标、词性、释义、例句、同义词、反义词、常见搭配

### 🎯 多样化学习模式

| 模式       | 功能描述                        |
| -------- | --------------------------- |
| **闪卡模式** | 经典闪卡学习，点击翻转查看释义             |
| **拼写模式** | 根据释义和音标输入单词，强化拼写记忆          |
| **听力模式** | TTS 发音 + 4 选 1 选择题，提升听力辨词能力 |
| **阅读模式** | 例句填空，在语境中掌握单词用法             |

### 📊 智能进度追踪

- **学习连续天数**：🔥 火焰徽章激励持续学习
- **本周学习图表**：可视化展示 7 天学习量
- **技能分布进度**：听说读写四项技能独立统计
- **难度分布统计**：已学单词的难度等级分布
- **详细学习报告**：总复习次数、各模式正确率、最长连续天数

### 🎨 现代化 UI 设计

- **Liquid Glass 设计语言**：液体玻璃态视觉效果
- **深色模式**：护眼夜间模式，深夜学习不刺眼
- **响应式布局**：完美适配桌面端和移动端
- **主题色切换**：9 种精美主题（紫罗兰、天空蓝、薄荷绿等）
- **流畅动画**：贝塞尔曲线优化的非线性平滑过渡

***

## 🚀 快速开始

### 在线使用

**无需安装，打开即用！**

👉 **[立即体验](https://kinsung97.github.io/VocabFlash/)**

### 本地运行

```bash
# 1. 克隆仓库
git clone https://github.com/kinsung97/VocabFlash.git
cd VocabFlash

# 2. 启动本地服务器
# 使用 Python
python -m http.server 8080

# 或使用 Node.js
npx http-server -p 8080

# 3. 访问应用
# 打开浏览器访问 http://localhost:8080
```

***

## 📖 使用指南

### 基础用法

1. **开始学习**：点击"开始今天的挑战"进入闪卡模式
2. **翻看释义**：点击卡片或按 `Space` 键查看释义
3. **评级记忆**：根据记忆程度选择 Again/Hard/Good/Easy
4. **切换模式**：点击顶部标签栏切换学习模式
5. **查看进度**：点击底部"进度"标签查看详细统计

### 键盘快捷键

| 快捷键     | 功能            |
| ------- | ------------- |
| `Space` | 翻看释义          |
| `1`     | 标记为生疏 (Again) |
| `2`     | 标记为模糊 (Hard)  |
| `3`     | 标记为熟悉 (Good)  |
| `4`     | 标记为简单 (Easy)  |
| `S`     | 播放发音          |
| `F`     | 收藏单词          |
| `Enter` | 提交拼写/阅读答案     |

### 高级功能

- **切换词库**：点击分类标签选择特定场景词库
- **筛选单词**：在词库页面按难度、技能、熟练度筛选
- **导出数据**：一键导出 CSV 格式的背诵记录
- **备份恢复**：JSON 格式备份，换设备无缝衔接

***

## 🛠️ 技术架构

### 技术栈

- **Core**: 纯原生前端（HTML5 + CSS3 + Vanilla JavaScript）
- **Storage**: 浏览器 LocalStorage，100% 本地运行
- **TTS**: Web Speech API (speechSynthesis)
- **Design**: Liquid Glass 设计语言 + 响应式布局

### 核心算法

#### SM-2 间隔重复算法

```javascript
function sm2Calculate(record, quality) {
    let ef = record.easinessFactor || 2.5;
    let rep = record.repetitions || 0;
    let interval = record.interval || 0;
    
    if (quality >= 3) {
        rep++;
        if (rep === 1) interval = 1;
        else if (rep === 2) interval = 3;
        else interval = Math.round(interval * ef);
    } else {
        rep = 0;
        interval = 1;
    }
    
    ef = Math.max(1.3, ef + 0.1 - (5 - quality) * (0.08 + (5 - quality) * 0.02));
    
    return { easinessFactor: ef, repetitions: rep, interval: interval };
}
```

#### 难度计算算法

```javascript
function calcDifficulty(word) {
    // 基础难度：基于词长
    if (len <= 4) base = 1;
    else if (len <= 6) base = 2;
    else if (len <= 8) base = 3;
    else if (len <= 10) base = 4;
    else base = 5;
    
    // 学术后缀 +1
    for (suffix of academicSuffixes) {
        if (word.endsWith(suffix)) base += 1;
    }
    
    // 常见词 -1
    if (commonWords.has(word)) base -= 1;
    
    return clamp(1, 5, base);
}
```

***

## 📦 目录结构

```text
VocabFlash/
├── index.html          # 主程序文件（包含样式与逻辑）
├── words.js           # 雅思词汇数据库（3673+ 单词）
├── vocabulary.txt     # 原始词汇数据（用于转换）
├── convert.js         # 数据转换脚本
├── favicon.svg        # 网站图标
├── README.md          # 项目文档
└── LICENSE            # MIT 开源协议
```

***

## 📊 数据来源

词汇数据来自 [hefengxian/my-ielts](https://github.com/hefengxian/my-ielts) 项目，包含《雅思词汇真经》等优质雅思备考资料。

感谢原作者的整理和分享！

***

## 🎨 主题色展示

| 主题色     | 预览        |
| ------- | --------- |
| 🟣 紫罗兰  | `#6c5ce7` |
| 🔵 天空蓝  | `#3498db` |
| 🟢 薄荷绿  | `#00b894` |
| 🟠 活力橙  | `#e67e22` |
| 🟧 落霞   | `#FA7C5E` |
| 🫒 橄榄绿  | `#777926` |
| ⬛ 极简黑白  | `#1d1d1f` |
| 🌈 彩虹极光 | 多色光晕      |
| 🟢 原生极光 | 北极光绿      |

***

## 📈 学习数据统计示例

### 进度页面展示

- **总进度卡片**：已学单词数 / 总单词数 + 进度条
- **统计网格**：4 个核心指标卡片
- **本周学习图表**：7 天柱状图（CSS 实现）
- **技能分布**：4 项技能进度条（彩色区分）
- **难度分布**：5 级难度统计卡片
- **详细统计**：复习次数、正确率、最长连续等

***

## 🔒 隐私保护

- **100% 本地存储**：所有数据保存在浏览器 LocalStorage
- **零数据上传**：不收集、不上传任何用户数据
- **无需注册登录**：打开即用，无账号系统
- **完全离线可用**：首次加载后可离线使用

***

## 🤝 参与贡献

欢迎提交 **Pull Request** 或 **Issue**！

### 贡献指南

1. Fork 本仓库
2. 新建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开一个 Pull Request

### 可贡献方向

- 📝 新增词汇或优化释义
- 🎨 UI/UX 改进建议
- 🐛 Bug 修复
- 📚 新增学习模式
- 🔧 性能优化
- 🌐 国际化翻译

***

## 📄 许可证

本项目采用 [MIT License](LICENSE) 许可协议。

***

## 📱 浏览器兼容性

| 浏览器            | 最低版本 |
| -------------- | ---- |
| Chrome         | 70+  |
| Firefox        | 65+  |
| Safari         | 12+  |
| Edge           | 79+  |
| iOS Safari     | 12+  |
| Android Chrome | 70+  |

***

## 📈 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=kinsung97/VocabFlash\&type=Date)](https://star-history.com/#kinsung97/VocabFlash\&Date)

***

## 💡 备考建议

雅思不仅是单词量的积累，更是逻辑与表达能力的提升。建议：

1. **每日坚持**：利用连续天数机制，保持每天学习
2. **多模式结合**：闪卡 + 拼写 + 听力 + 阅读交替使用
3. **场景化学习**：按雅思考试场景分类突破
4. **科学复习**：遵循 SM-2 算法安排的复习时间
5. **定期复盘**：通过进度页面查看学习报告，调整策略

***

## 📞 联系方式

- **GitHub**: [@kinsung97](https://github.com/kinsung97)
- **Project Page**: [VocabFlash](https://github.com/kinsung97/VocabFlash)
- **Issues**: [问题反馈](https://github.com/kinsung97/VocabFlash/issues)

***

## 🙏 致谢

- 词汇数据来源：[hefengxian/my-ielts](https://github.com/hefengxian/my-ielts)
- SM-2 算法：[SuperMemo](https://www.super-memory.com/)
- 设计灵感：Apple/iOS 原生设计语言
