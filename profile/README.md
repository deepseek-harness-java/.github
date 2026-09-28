# deepseek-harness-java · DSH Java 智能体生态

> **一句话读懂**：本组织是 [deepseek-harness-java（DSH）](https://github.com/deepseek-harness-java/dsh-java-plugin-skills) 的官方仓库群 —— **1 个技能包 + 27 个独立 AI 产品 + 74 个行业场景案例**，全部基于 DSH Java Native Plugin 机制，开箱即跑、端到端验证过。

[![Java](https://img.shields.io/badge/Java-17-orange)](https://openjdk.java.net/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2-brightgreen)](https://spring.io/projects/spring-boot)
[![Products](https://img.shields.io/badge/%E7%8B%AC%E7%AB%8B%20AI%20%E4%BA%A7%E5%93%81-27-8A2BE2)](#-27-个独立-ai-产品)
[![Cases](https://img.shields.io/badge/%E5%9C%BA%E6%99%AF%E6%A1%88%E4%BE%8B-74-blue)](#-74-个行业场景案例)

---

## 📖 这是什么

**DSH（deepseek-harness-java）** 是一套 Java 侧的 AI 智能体运行基座：业务应用通过 **Java Native Plugin** 机制把自己的 REST API 注册为 Agent 工具，AI 助手即可用自然语言直接操作业务系统。

组织内仓库分两大形态，遵循同一套技术底座：

| 形态 | 说明 | 结构 |
|---|---|---|
| **独立 AI 产品**（`dsh-java-*`） | 本身就是一个完整可用的生产力工具/管理后台，AI 是"熟练操作员" | `*-app`（独立后台/UI）+ `*-plugin`（DSH 插件） |
| **场景案例**（行业名命名） | 「业务应用 + 内嵌 AI 助手」的完整可运行案例 | 同左，外加演示数据与验证截图 |

统一三层结构：

```
┌─────────────────────────────────────────────┐
│  浏览器前端页面（工作台 / AI 对话 / SSE 流式）        │
├─────────────────────────────────────────────┤
│  Spring Boot 业务应用（REST API + 演示数据）        │
├─────────────────────────────────────────────┤
│  DSH Java Native 插件（把 API 注册为 AI 工具）      │
│  ↓ 安装到                                      │
│  DSH 宿主 (127.0.0.1:8090) → AI 助手调用        │
└─────────────────────────────────────────────┘
```

**插件不直连数据，全部通过 HTTP 调用业务应用**，守住安全边界。两类仓库的共同交付标准：

- ✅ 可运行 app + 插件（3~6 个 AI 工具）+ README
- ✅ 端到端验证脚本（E2E 全部断言通过）
- ✅ 3 张标准截图（01-首页 / 02-AI 调用工具实测 / 03-安全红线拒绝）
- ✅ **安全红线内置**：每个产品/案例都有明确的"AI 绝不做"清单（只读边界、不外发、不替代专业判断等）

---

## 🚀 快速开始

### 方式一：一句话生成（推荐）

安装技能包 [dsh-java-plugin-skills](https://github.com/deepseek-harness-java/dsh-java-plugin-skills) 后，在 [WaLiCode](https://walicode.xiaofuge.cn/) / Codex / WorkBuddy / CodeBuddy 里说一句话即可完成「开发 + 部署 + 启动 + 插件接入 + 验证」全链路：

| 说法 | 效果 |
|---|---|
| 「就做 P6」 / 「做外卖订餐平台」 | 按该案例一句话完成开发 + 部署 + 启动 |
| 「P57 是什么」 | 展示该案例的应用形态与 AI 能力亮点 |
| 「做一个宠物寄养平台」 | 库外领域，按同结构即时生成新案例并开工 |

库外领域的 **Prompt 结构公式**：

```
开发一个 PC 端 <领域应用>，
含 <核心功能 3~4 项>，预置 <演示数据规模>；
AI <角色名>助手能 <3 个跨工具的智能能力>，
<以插件接入 DSH 运行 / 启动运行给我地址>。
```

### 方式二：手动运行任一仓库

每个仓库内都有完整 README，标准三步：

```bash
# 1. 构建（在仓库根目录）
mvn clean package -DskipTests

# 2. 启动业务应用（端口见各仓库 README）
java -Dserver.port=18094 -jar e-app/target/e-app-1.0.0-SNAPSHOT.jar

# 3. 把插件安装到 DSH 宿主
bash install_plugin.sh e-plugin/target/e-plugin-1.0.0-SNAPSHOT.jar \
  express-copilot 1.0.0-SNAPSHOT e-plugin-1.0.0-SNAPSHOT.jar "AI 快递助手"

# 4. 打开页面即可使用
open http://127.0.0.1:18094/
```

> 前置条件：JDK 17+、Maven 3.8+、本地已运行 DSH 宿主（`127.0.0.1:8090`）。

---

## 🧰 基座与技能

| 仓库 | 说明 |
|---|---|
| [dsh-java-plugin-skills](https://github.com/deepseek-harness-java/dsh-java-plugin-skills) | **DSH Java 技能包**：一句话生成业务应用与 Java Native 插件，含场景话术库与全链路验证脚本 |

---

## 🧩 27 个独立 AI 产品

工具优先——每个产品解决一类真实工作流（开发/数据/运维/写作），AI 能组合多工具完成"一句话任务"；数据本地优先（`~/.dsh-java-<name>/`），无外部 SaaS 依赖。

### 🔧 开发者工具

| 仓库 | 产品 · 能力 |
|---|---|
| [dsh-java-git](https://github.com/deepseek-harness-java/dsh-java-git) | Git Story Studio · git 历史分析/变更摘要/回滚建议（不改写历史） |
| [dsh-java-log](https://github.com/deepseek-harness-java/dsh-java-log) | Log Lens · 日志筛选/模式聚类/异常定位 |
| [dsh-java-api](https://github.com/deepseek-harness-java/dsh-java-api) | API Sketch · API 接口草图/OpenAPI 生成/字段校验 |
| [dsh-java-cron](https://github.com/deepseek-harness-java/dsh-java-cron) | Cron Forge · cron 表达式解析/触发时间/校验 |
| [dsh-java-env](https://github.com/deepseek-harness-java/dsh-java-env) | Env Doctor · 环境一致性体检/密钥脱敏扫描 |
| [dsh-java-dep](https://github.com/deepseek-harness-java/dsh-java-dep) | Dependency Radar · 依赖雷达/版本冲突/CVE 提示 |
| [dsh-java-diff](https://github.com/deepseek-harness-java/dsh-java-diff) | Diff Narrator · 代码变更叙事/风险扫描/回滚计划 |
| [dsh-java-regex](https://github.com/deepseek-harness-java/dsh-java-regex) | Regex Forge · 正则解释/测试/生成/优化 |
| [dsh-java-shell](https://github.com/deepseek-harness-java/dsh-java-shell) | Shell Buddy · 命令解释/风险提示/安全替代建议 |
| [dsh-java-json](https://github.com/deepseek-harness-java/dsh-java-json) | JSON Lens · JSON 解析/校验/对比/路径查询 |

### 📊 数据与效率

| 仓库 | 产品 · 能力 |
|---|---|
| [dsh-java-csv](https://github.com/deepseek-harness-java/dsh-java-csv) | CSV Studio · CSV 清洗/转换/校验/统计 |
| [dsh-java-markdown](https://github.com/deepseek-harness-java/dsh-java-markdown) | Markdown Doctor · 文档体检/结构修复/链接检查 |
| [dsh-java-meeting](https://github.com/deepseek-harness-java/dsh-java-meeting) | Meeting Digest · 会议纪要/行动项提取/跟进 |
| [dsh-java-inbox](https://github.com/deepseek-harness-java/dsh-java-inbox) | Inbox Triage · 邮件分诊/优先级/归档建议（不代发邮件） |
| [dsh-java-backlog](https://github.com/deepseek-harness-java/dsh-java-backlog) | Backlog Shaper · 需求整理/用户故事/优先级矩阵（不代替拍板） |
| [dsh-java-glossary](https://github.com/deepseek-harness-java/dsh-java-glossary) | Term Atlas · 团队中英术语典/文档挖词/双语卡片（不改他人释义） |
| [dsh-java-recall-deck](https://github.com/deepseek-harness-java/dsh-java-recall-deck) | Recall Deck · 记忆卡工坊/SM-2 间隔重复/学习统计（不删学习进度） |
| [dsh-java-style](https://github.com/deepseek-harness-java/dsh-java-style) | Tone Tuner · 文风画像/改写建议/可读性/术语校对（不动原稿） |
| [dsh-java-faq](https://github.com/deepseek-harness-java/dsh-java-faq) | FAQ Builder · 客服记录聚类/FAQ 草稿/覆盖缺口（不臆造政策答复） |
| [dsh-java-storymap](https://github.com/deepseek-harness-java/dsh-java-storymap) | Story Mapper · 用户旅程画板/痛点扫描/情绪曲线（不替代用户研究） |
| [dsh-java-release](https://github.com/deepseek-harness-java/dsh-java-release) | Release Notes Hub · 发布中枢/渠道文案变体/时间线（不直接对外发布） |

### 🛡️ 安全与运维

| 仓库 | 产品 · 能力 |
|---|---|
| [dsh-java-secret](https://github.com/deepseek-harness-java/dsh-java-secret) | Secret Sweeper · 密钥泄漏扫描/熵检查/轮换清单（明文脱敏） |
| [dsh-java-docker](https://github.com/deepseek-harness-java/dsh-java-docker) | Docker Lens · 镜像容器清单/瘦身/dockerfile lint（不 stop/rm 容器） |
| [dsh-java-nginx](https://github.com/deepseek-harness-java/dsh-java-nginx) | Nginx Composer · 配置解析/路由表/错误 lint（不写回不 reload） |
| [dsh-java-ssh-fleet](https://github.com/deepseek-harness-java/dsh-java-ssh-fleet) | SSH Fleet Notes · 服务器舰队手册/巡检清单（不发起真实连接） |
| [dsh-java-firewall-plan](https://github.com/deepseek-harness-java/dsh-java-firewall-plan) | Port Guard · 端口快照/冲突诊断/防火墙建议（不 kill 进程） |
| [dsh-java-backup-audit](https://github.com/deepseek-harness-java/dsh-java-backup-audit) | Backup Auditor · 备份健康检查/3-2-1 策略评估（不删不改备份） |

---

## 🏭 74 个行业场景案例

每个案例 = 「业务应用 + 内嵌 AI 助手 + Java Native 插件」的完整可运行仓库，覆盖零售、出行、生活服务、教育、工作协作等行业。

### 🛒 商城零售与生活电商

| 仓库 | 场景 |
|---|---|
| [digital-mall](https://github.com/deepseek-harness-java/digital-mall) | P1 虚拟数码商城 · AI 购物助手 |
| [fresh-group-buy](https://github.com/deepseek-harness-java/fresh-group-buy) | P2 生鲜社区团购 · AI 买菜助手 |
| [takeout-platform](https://github.com/deepseek-harness-java/takeout-platform) | P6 外卖订餐平台 · AI 美食助手 |
| [shop-review](https://github.com/deepseek-harness-java/shop-review) | P7 周边探店点评 · AI 探店助手 |
| [marketing-factory](https://github.com/deepseek-harness-java/marketing-factory) | P9 营销活动工厂 · AI 营销助手 |
| [points-mall](https://github.com/deepseek-harness-java/points-mall) | 会员积分商城 · AI 积分助手 |
| [coffee-ordering](https://github.com/deepseek-harness-java/coffee-ordering) | 咖啡下单管家 · AI 点单助手 |
| [tea-shop](https://github.com/deepseek-harness-java/tea-shop) | 茶饮点单管家 · AI 茶饮助手 |
| [veggie-box](https://github.com/deepseek-harness-java/veggie-box) | P81 净菜周配管家台 |
| [breakfast-club](https://github.com/deepseek-harness-java/breakfast-club) | P97 早餐鲜配 · AI 管家 |

### 💰 金融与个人事务

| 仓库 | 场景 |
|---|---|
| [personal-ledger](https://github.com/deepseek-harness-java/personal-ledger) | P3 个人记账助手 · 流水/预算/月报 |
| [credit-simulator](https://github.com/deepseek-harness-java/credit-simulator) | P4 小额信贷模拟器 · 试算 + AI 推荐 |
| [insurance-claims](https://github.com/deepseek-harness-java/insurance-claims) | P58 保险理赔助手台 · 核验/测算/审核 |
| [expense-reimburse](https://github.com/deepseek-harness-java/expense-reimburse) | P57 费控报销助手台 · 合规校验/审批 |

### 🚕 出行 · 物流 · 酒旅 · 文旅

| 仓库 | 场景 |
|---|---|
| [trip-planner](https://github.com/deepseek-harness-java/trip-planner) | P5 城市出行规划 · 三网聚合三方案 |
| [express-tracking](https://github.com/deepseek-harness-java/express-tracking) | 快递查寄台 · 轨迹/运费/下单/异常预警 |
| [hotel-booking](https://github.com/deepseek-harness-java/hotel-booking) | 酒店预订管家 · 房态日历/二次确认下单 |
| [scenic-guide](https://github.com/deepseek-harness-java/scenic-guide) | 景区智慧导览 · 客流避堵/路线规划 |
| [zoo-tour](https://github.com/deepseek-harness-java/zoo-tour) | P85 动物园导览管家台 |
| [yacht-rental](https://github.com/deepseek-harness-java/yacht-rental) | P84 游艇租赁管家台 |
| [car-rental](https://github.com/deepseek-harness-java/car-rental) | 租车管家 · 车辆/门店/订单/维保 |

### 🏠 生活服务与门店经营

| 仓库 | 场景 |
|---|---|
| [online-clinic](https://github.com/deepseek-harness-java/online-clinic) | P11 在线问诊导诊 · AI 仅导诊不诊断 |
| [dental-clinic](https://github.com/deepseek-harness-java/dental-clinic) | 牙科诊所助手台 · 排班/挂号/病历 |
| [doctor-outpatient](https://github.com/deepseek-harness-java/doctor-outpatient) | P40 医生门诊工作站 · 病历摘要 |
| [pet-clinic](https://github.com/deepseek-harness-java/pet-clinic) | 宠物医院助手 · 兽医排班/档案 |
| [vet-clinic-af](https://github.com/deepseek-harness-java/vet-clinic-af) | 安心宠物疫苗驱虫门诊 |
| [pet-board](https://github.com/deepseek-harness-java/pet-board) | 宠物寄养连锁管家 |
| [pet-boarding](https://github.com/deepseek-harness-java/pet-boarding) | P87 宠物寄养管家台 |
| [pet-grooming](https://github.com/deepseek-harness-java/pet-grooming) | P100 毛孩子美容会所 |
| [gym-membership](https://github.com/deepseek-harness-java/gym-membership) | P68 健身房会籍管家 |
| [gym-coach](https://github.com/deepseek-harness-java/gym-coach) | P86 健身私教管家台 |
| [swimming-pool](https://github.com/deepseek-harness-java/swimming-pool) | P78 游泳培训管家 |
| [housekeeping-cleaning](https://github.com/deepseek-harness-java/housekeeping-cleaning) | P69 家政保洁管家 |
| [errand-service](https://github.com/deepseek-harness-java/errand-service) | P77 跑腿代办管家 |
| [moving-service](https://github.com/deepseek-harness-java/moving-service) | 搬家服务连锁管家 |
| [laundry-service](https://github.com/deepseek-harness-java/laundry-service) | 连锁洗衣管家 |
| [laundry-room](https://github.com/deepseek-harness-java/laundry-room) | P88 洗衣管家台 |
| [hair-salon](https://github.com/deepseek-harness-java/hair-salon) | 连锁美发沙龙管家 |
| [appliance-repair](https://github.com/deepseek-harness-java/appliance-repair) | 家电维修连锁管家 |
| [photography-studio](https://github.com/deepseek-harness-java/photography-studio) | P75 摄影预约管家 |
| [kids-photo](https://github.com/deepseek-harness-java/kids-photo) | P89 亲子摄影管家台 |
| [flower-subscription](https://github.com/deepseek-harness-java/flower-subscription) | 鲜花订阅管家 |
| [car-care](https://github.com/deepseek-harness-java/car-care) | 汽车养护门店助手 · AI 不做故障诊断 |
| [restaurant-ops](https://github.com/deepseek-harness-java/restaurant-ops) | 餐饮门店经营台 · AI 店长台 |
| [property-service](https://github.com/deepseek-harness-java/property-service) | P60 智慧物业管家台 |
| [library-seat](https://github.com/deepseek-harness-java/library-seat) | P61 图书馆自习室管家台 |
| [study-room](https://github.com/deepseek-harness-java/study-room) | 静光社区自习室 |
| [tool-shed](https://github.com/deepseek-harness-java/tool-shed) | 万能社区工具棚 · 共享租借 |
| [community-kitchen](https://github.com/deepseek-harness-java/community-kitchen) | 邻里香社区共享厨房 |
| [eldercare-center](https://github.com/deepseek-harness-java/eldercare-center) | 夕阳暖老年日间照料中心 |
| [smart-farm](https://github.com/deepseek-harness-java/smart-farm) | 云上田园智慧农场 |
| [kids-club](https://github.com/deepseek-harness-java/kids-club) | P96 童萌团儿童托管班 |
| [wedding-planner](https://github.com/deepseek-harness-java/wedding-planner) | P98 花好月圆婚礼策划 |
| [badminton-hall](https://github.com/deepseek-harness-java/badminton-hall) | P99 飞扬羽毛球馆 |
| [tutoring-book](https://github.com/deepseek-harness-java/tutoring-book) | 家教预约管家 |
| [xylophone-class](https://github.com/deepseek-harness-java/xylophone-class) | P83 马林巴课程顾问台 |
| [water-purifier](https://github.com/deepseek-harness-java/water-purifier) | P82 净水器租赁管家台 |
| [umbrella-share](https://github.com/deepseek-harness-java/umbrella-share) | P80 共享雨伞管家台 |
| [smart-mes](https://github.com/deepseek-harness-java/smart-mes) | P59 智能制造 MES 生产助手台 |

### 💼 工作协作与内容

| 仓库 | 场景 |
|---|---|
| [team-kanban](https://github.com/deepseek-harness-java/team-kanban) | P8 团队项目看板 · AI 看板助手 |
| [community-plaza](https://github.com/deepseek-harness-java/community-plaza) | P10 兴趣社区广场 · AI 社区助手 |
| [livestream-review](https://github.com/deepseek-harness-java/livestream-review) | 直播带货复盘台 · AI 复盘助手 |

### 🖥️ 产研测运维工作台

| 仓库 | 场景 |
|---|---|
| [deploy-monitor](https://github.com/deepseek-harness-java/deploy-monitor) | P30 发布上线监控台 · GO-NO-GO/一键回滚 |
| [dev-collab](https://github.com/deepseek-harness-java/dev-collab) | P31 研发协作工具台 · MR 评审/技术债 |
| [test-workbench](https://github.com/deepseek-harness-java/test-workbench) | P32 测试用例工作台 · 追溯矩阵/漏测分析 |
| [pm-workbench](https://github.com/deepseek-harness-java/pm-workbench) | P33 产品需求工作台 · 优先级/PRD/排期 |
| [duty-desk](https://github.com/deepseek-harness-java/duty-desk) | P34 生产值班巡检台 · 值班/告警/交接班 |

### 🎓 教育学习

| 仓库 | 场景 |
|---|---|
| [teacher-workbench](https://github.com/deepseek-harness-java/teacher-workbench) | P35 教师教学工作台 · 学情/教案/批改 |
| [math-think](https://github.com/deepseek-harness-java/math-think) | P36 数学思维训练 · 错因/变式题组 |
| [chinese-writing](https://github.com/deepseek-harness-java/chinese-writing) | P37 语文阅读写作 · 书单/作文批改 |
| [english-listening](https://github.com/deepseek-harness-java/english-listening) | P38 英语听说训练 · 跟读评分 |

### 👥 角色工作台

| 仓库 | 场景 |
|---|---|
| [sales-crm](https://github.com/deepseek-harness-java/sales-crm) | P39 销售 CRM · 客户 360/商机漏斗 |
| [lawyer-case](https://github.com/deepseek-harness-java/lawyer-case) | P41 律师办案助手 · 不构成法律意见 |
| [hr-recruit](https://github.com/deepseek-harness-java/hr-recruit) | HR 招聘助手 · AI 不做录用决定 |

---

## 🏗️ 统一仓库结构

看懂一个就能看懂全部：

```
<repo-name>/
├── pom.xml                  # 父 pom（Maven 多模块）
├── x-app/                   # Spring Boot 业务应用
│   ├── Controller.java      #   REST API
│   ├── Service/Store.java   #   业务逻辑 + 预置演示数据
│   ├── AssistantController.java  # AI 助手 SSE（透传 DSH 宿主）
│   └── static/              #   前端页面（工作台 + AI 对话）
├── x-plugin/                # DSH Java Native 插件
│   ├── XxxPlugin.java       #   3~6 个 AI 工具（AbstractHarnessPlugin）
│   └── META-INF/plugin.yaml #   插件声明
├── *_e2e.py                 # 端到端验证脚本（REST + SSE 全链路）
├── screenshots/             # 01-home / 02-ai-drawer / 03-safety
└── README.md                # 工具清单/API 表/快速开始/验证
```

**SPI 契约**：`META-INF/services/...JavaHarnessPlugin` + `plugin.yaml`；工具以 `plugin__<pluginId>__<tool>` 暴露给 AI；E2E 通过 app 的 SSE 端点验证 AI 真实调用了插件工具（且在红线用例上正确拒绝）。

---

## 🤝 如何参与

- **想跑某个产品/场景**：从上面的索引点进对应仓库，按 README 快速开始。
- **想要清单里还没有的场景**：安装[技能包](https://github.com/deepseek-harness-java/dsh-java-plugin-skills)，用 Prompt 结构公式一句话生成，生成后欢迎 PR 回收案例。
- **想了解 DSH 宿主与插件协议**：见技能包仓库的技能文档与 `install_plugin.sh` 用法。

## 📮 相关链接

- 技能包（场景话术库 + 全链路验证）：https://github.com/deepseek-harness-java/dsh-java-plugin-skills
- 全部仓库列表：https://github.com/orgs/deepseek-harness-java/repositories
