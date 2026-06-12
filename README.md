# DocQuiz

> 一款支持多种文档格式导入的智能刷题 Android 应用，将 Word/PDF/Markdown 题库一键转换为交互式答题卡片。

## 功能特性

### 文档导入
- **DOCX** — 基于 Apache POI 解析 Word 文档，支持段落与表格内容提取
- **PDF** — 基于 PDFBox 提取文本，自动排序保持阅读顺序
- **Markdown** — 原生 .md 文件支持，识别标准题目标记格式

### 题目解析
- 自动识别五种题型：**单选** / **多选** / **判断** / **填空** / **简答**
- 智能解析题干、选项（A-E）、答案、解析、标签
- 支持嵌入式答案检测（选项与答案同行场景）
- 导入时可自定义题库名称，已导入题库支持重命名

### 刷题模式
- **顺序刷题** / **随机刷题** 一键切换
- **错题重刷** — 自动收集错题，支持独立错题专练模式
- 实时答题统计：已答数、正确数、错题集
- 刷题进度持久化存储，关闭应用后自动恢复

### AI 答疑
- 接入兼容 OpenAI API 的 LLM 服务，支持流式输出
- 对话式交互：AI 逐选项分析，解答题目思路
- 可自定义 API 地址、模型名称与密钥

### 交互设计
- Material3 设计语言，支持亮色 / 暗色主题
- 自适应布局：手机端底部导航栏，平板端侧栏常驻
- 刷题完成页分数汇总，百分比 + 图表式呈现

## 截图

<!-- 截图占位，后续补充 -->
<!-- ![刷题界面](screenshots/quiz.png) -->
<!-- ![得分页](screenshots/score.png) -->

## 技术栈

| 类别 | 技术 |
|------|------|
| 语言 | Kotlin |
| UI 框架 | Jetpack Compose + Material3 |
| 架构 | MVVM (ViewModel + StateFlow) |
| 持久化 | Room Database + Gson |
| 文档解析 | Apache POI (DOCX) / PDFBox (PDF) |
| 网络 | OkHttp (SSE 流式对话) |
| 依赖注入 | 手动 DI (AppContainer) |

## 项目结构

```
app/src/main/java/com/example/docquiz/
├── ai/
│   └── AiChatService.kt          # AI 对话服务（流式 SSE）
├── data/
│   ├── db/
│   │   ├── AppDatabase.kt        # Room 数据库
│   │   ├── Daos.kt               # 题库 & 答题记录 DAO
│   │   ├── QuizBankEntity.kt     # 题库持久化实体
│   │   └── QuizRecordEntity.kt   # 答题记录实体
│   ├── datastore/
│   │   └── AIConfigDataStore.kt  # AI 配置持久化
│   ├── parser/
│   │   ├── DocxParser.kt         # DOCX 文本提取
│   │   ├── PdfParser.kt          # PDF 文本提取
│   │   ├── MdParser.kt           # Markdown 文本读取
│   │   └── MarkdownParser.kt     # 题目结构化解析引擎
│   └── repository/
│       └── QuizRepository.kt     # 数据仓库层
├── di/
│   └── AppContainer.kt           # 依赖容器
├── model/
│   └── Model.kt                  # 数据模型（Question/QuizBank/QuestionType 等）
├── ui/
│   ├── ai/
│   │   └── AIChatDialog.kt       # AI 对话浮层
│   ├── quiz/
│   │   └── QuestionCard.kt       # 答题卡片（单选/多选/填空/判断/简答）
│   ├── score/
│   │   └── ScoreOverlay.kt       # 刷题完成得分页
│   ├── sidebar/
│   │   ├── AIConfigSection.kt    # AI 配置面板
│   │   ├── ControlPanel.kt       # 刷题控制面板（模式切换/错题重刷）
│   │   ├── ImportZone.kt         # 文件导入区域
│   │   ├── SidebarColumn.kt      # 侧栏布局（平板端）
│   │   └── StatsPanel.kt         # 答题统计面板
│   ├── theme/
│   │   └── Color.kt              # 主题色定义
│   └── MainScreen.kt             # 主界面（手机+平板自适应）
├── viewmodel/
│   └── QuizViewModel.kt          # 核心状态管理
├── DocQuizApp.kt                 # Application 入口
└── MainActivity.kt               # Activity 入口
```

## 快速开始

### 环境要求

- Android Studio Hedgehog (2023.1.1) 或更高版本
- JDK 17
- Gradle 8.7
- Android SDK 34 (compileSdk)
- 最低支持 Android 8.0 (API 26)

### 构建运行

```bash
# 克隆项目
git clone <repo-url>
cd DocQuiz

# 构建 Debug APK
./gradlew assembleDebug

# 安装到设备
adb install app/build/outputs/apk/debug/app-debug.apk
```

### AI 功能配置

1. 进入应用设置页
2. 填写 LLM API 地址（如 `https://api.openai.com`）
3. 填写 API Key 和模型名称（如 `gpt-4o-mini`）
4. 保存后在刷题界面点击「AI 解答」即可使用

## 作者

**qingzhou**

## 许可证

MIT License

