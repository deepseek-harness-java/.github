# deepseek-harness-java · DSH Java 场景案例库

> **一句话读懂**：本组织是 [deepseek-harness-java（DSH）](https://github.com/deepseek-harness-java/dsh-java-plugin-skills) 的**官方场景案例库** —— 每个仓库都是一个「业务应用 + 内嵌 AI 助手 + Java Native 插件」的完整可运行案例，开箱即跑、端到端验证过。

[![Java](https://img.shields.io/badge/Java-17-orange)](https://openjdk.java.net/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2-brightgreen)](https://spring.io/projects/spring-boot)
[![Cases](https://img.shields.io/badge/%E5%9C%BA%E6%99%AF%E6%A1%88%E4%BE%8B-99%20(P1~P99)-blue)](#场景总览99-个)
[![Published](https://img.shields.io/badge/%E5%B7%B2%E5%8F%91%E5%B8%83%E4%BB%93%E5%BA%93-17-8A2BE2)](#案例索引)

---

## 📖 这是什么

**DSH（deepseek-harness-java）** 是一套 Java 侧的 AI 智能体运行基座：业务应用通过 **Java Native Plugin** 机制把自己的 REST API 注册为 Agent 工具，AI 助手即可用自然语言直接操作业务系统。

本组织下的每个场景仓库都遵循统一的三层结构：

```
┌─────────────────────────────────────────────┐
│  浏览器前端页面（悬浮 AI 助手球 / SSE 流式对话）      │
├─────────────────────────────────────────────┤
│  Spring Boot 业务应用（REST API + 演示数据）        │
├─────────────────────────────────────────────┤
│  DSH Java Native 插件（把 API 注册为 AI 工具）      │
│  ↓ 安装到                                      │
│  DSH 宿主 (127.0.0.1:8090) → AI 助手调用        │
└─────────────────────────────────────────────┘
```

**插件不直连数据，全部通过 HTTP 调用业务应用**，守住安全边界；每个案例预置演示数据、内置 3~5 个 AI 工具，并附验证截图与端到端验证脚本。

---

## 🚀 快速开始

### 方式一：一句话生成（推荐）

安装技能包 [dsh-java-plugin-skills](https://github.com/deepseek-harness-java/dsh-java-plugin-skills) 后，在 WorkBuddy / CodeBuddy 里说一句话即可完成「开发 + 部署 + 启动 + 插件接入 + 验证」全链路：

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

### 方式二：手动运行任一案例

每个案例仓库内都有完整 README，标准三步：

```bash
# 1. 构建（在案例仓库根目录）
mvn clean package -DskipTests

# 2. 启动业务应用（端口见下表，各案例不同）
java -Dserver.port=18094 -jar e-app/target/e-app-1.0.0-SNAPSHOT.jar

# 3. 把插件安装到 DSH 宿主
bash install_plugin.sh e-plugin/target/e-plugin-1.0.0-SNAPSHOT.jar \
  express-copilot 1.0.0-SNAPSHOT e-plugin-1.0.0-SNAPSHOT.jar "AI 快递助手"

# 4. 打开页面即可使用
open http://127.0.0.1:18094/
```

> 前置条件：JDK 17+、Maven 3.8+、本地已运行 DSH 宿主（`127.0.0.1:8090`）。

---

## 📚 案例索引（已发布仓库，点击即入）

### 🔧 基座与技能

| 仓库 | 说明 |
|---|---|
| [dsh-java-plugin-skills](https://github.com/deepseek-harness-java/dsh-java-plugin-skills) | **DSH Java 技能包**：一句话生成业务应用与 Java Native 插件，含 99 案例话术库（`references/prompt-recipes.md`） |

### 🛒 商城零售与生活电商

| 仓库 | 场景 | 插件 ID | 端口 |
|---|---|---|---|
| [digital-mall](https://github.com/deepseek-harness-java/digital-mall) | P1 虚拟数码商城 · AI 购物助手（商品/订单/物流） | — | — |
| [fresh-group-buy](https://github.com/deepseek-harness-java/fresh-group-buy) | P2 生鲜社区团购 · AI 买菜助手（拼团/自提点/订单） | — | — |
| [personal-ledger](https://github.com/deepseek-harness-java/personal-ledger) | P3 个人记账助手 · 流水/预算/月报/消费结构分析 | — | — |
| [credit-simulator](https://github.com/deepseek-harness-java/credit-simulator) | P4 小额信贷模拟器 · 等额本息/本金试算 + AI 产品推荐 | — | — |
| [takeout-platform](https://github.com/deepseek-harness-java/takeout-platform) | P6 外卖订餐平台 · AI 美食助手（菜单/凑单/骑手模拟） | `takeout-assistant` | 18082 |
| [shop-review](https://github.com/deepseek-harness-java/shop-review) | P7 周边探店点评 · AI 探店助手（按场景推荐/两店对比） | `review-scout` | 18086 |
| [marketing-factory](https://github.com/deepseek-harness-java/marketing-factory) | P9 营销活动工厂 · AI 营销助手（活动/ROI 复盘/券运营） | `marketing-copilot` | 18088 |
| [points-mall](https://github.com/deepseek-harness-java/points-mall) | P54 会员积分商城 · AI 积分助手（账户/兑换推荐/流水） | `points-copilot` | 18090 |

### 🚕 出行 · 物流 · 酒旅 · 文旅

| 仓库 | 场景 | 插件 ID | 端口 |
|---|---|---|---|
| [trip-planner](https://github.com/deepseek-harness-java/trip-planner) | P5 城市出行规划 · 地铁/公交/打车三方案推荐 | `trip-assistant` | 18081 |
| [hotel-booking](https://github.com/deepseek-harness-java/hotel-booking) | P44 酒店民宿预订 · AI 订房助手（房态/价格日历/预订） | `hotel-copilot` | 18095 |
| [express-tracking](https://github.com/deepseek-harness-java/express-tracking) | P43 快递查寄台 · AI 快递助手（轨迹/运费/下单/网点/异常） | `express-copilot` | 18094 |
| [scenic-guide](https://github.com/deepseek-harness-java/scenic-guide) | P57 景区智慧导览 · AI 导览台（拥挤度/路线/演出索道/避堵） | `scenic-copilot` | 18093 |

### 🍽️ 生活服务与门店经营

| 仓库 | 场景 | 插件 ID | 端口 |
|---|---|---|---|
| [online-clinic](https://github.com/deepseek-harness-java/online-clinic) | P11 在线问诊导诊 · 症状推科室/排班/预约（AI 仅导诊不诊断） | — | — |
| [restaurant-ops](https://github.com/deepseek-harness-java/restaurant-ops) | P56 餐饮门店经营台 · AI 店长台（桌台/毛利/点单/结账） | `restaurant-copilot` | 18092 |

### 💼 工作协作与内容

| 仓库 | 场景 | 插件 ID | 端口 |
|---|---|---|---|
| [team-kanban](https://github.com/deepseek-harness-java/team-kanban) | P8 团队项目看板 · AI 看板助手（进度/移卡/建卡/周报） | `kanban-copilot` | 18087 |
| [community-plaza](https://github.com/deepseek-harness-java/community-plaza) | P10 兴趣社区广场 · AI 社区助手（话题/热榜/观点总结/代发帖） | `plaza-copilot` | 18089 |
| [livestream-review](https://github.com/deepseek-harness-java/livestream-review) | P55 直播带货复盘台 · AI 复盘助手（指标/商品漏斗/流量节奏） | `live-copilot` | 18091 |

> 「—」表示该仓库为早期案例，插件 ID 与端口请见仓库内 README。

---

## 🗂️ 场景总览（99 个：P1 ~ P99）

技能库共沉淀 **99 个场景案例**，按 16 个大类组织。已发布的仓库见上表，其余案例通过技能包一句话即可生成。

<details>
<summary><b>▶ 展开完整 99 案例清单</b></summary>

| 大类 | 场景 |
|---|---|
| **商城零售与生活电商** | P1 虚拟数码商城 · P2 生鲜社区团购 · P6 外卖订餐平台 · P7 周边探店点评 · P9 营销活动工厂 |
| **金融与支出管理** | P3 个人记账助手 · P4 小额信贷模拟器 · P46 保险理赔工作台 · P20 个人订阅管理 |
| **出行 · 物流 · 酒旅** | P5 出行规划 · P43 快递物流查件台 · P44 酒店民宿预订 |
| **生活服务与智能硬件** | P23 智能家居中控台 · P48 物业报修服务台 · P49 宠物医院管理台 · P50 汽车养护预约台 |
| **医疗健康** | P11 在线问诊预约 · P12 健身打卡私教 · P40 医生门诊工作站 ⚠️只整理不诊断 |
| **教育学习** | P13 在线课程平台 · P14 单词背诵 · P35 教师教学工作台 · P36 数学思维 · P37 语文读写 · P38 英语听说 · P17 研学旅游营地 · P18 阅读笔记社区 |
| **工作协作与内容** | P8 团队项目看板 · P19 团队决议纪要 · P15 IT 咨询工单 · P10 兴趣社区广场 · P22 财经资讯早报台 · P21 私人音乐歌单馆 · P24 自媒体创作工作台 |
| **产研测运维（工程效能）** | P28 Redis 运维监控台 · P29 ES 集群运维台 · P30 发布上线监控台 · P34 生产值班巡检台 · P31 研发协作工具台 · P32 测试用例工作台 · P33 产品需求工作台 · P27 AI 应用运行监控台 |
| **角色工作台** | P39 销售 CRM 工作台 · P41 律师办案工作台 ⚠️不输出法律意见 · P42 HR 招聘工作台 |
| **政务 · 公益 · 行业纵深** | P16 政务办事大厅 · P26 碳普惠生活平台 · P25 智慧农场管理台 · P47 智能制造 MES · P45 企业财务报销台 · P51 供应链采购对账台 · P52 房产中介房源工作台 |
| **消费与文旅扩展** | P53 二手闲置交易 · P54 会员积分商城 · P55 直播带货复盘台 · P56 餐厅门店经营台 · P57 景区智慧导览 · P58 婚庆策划工作台 · P59 民宿房东经营台 · P60 城市演出票务台 |
| **出行与能源扩展** | P61 充电站运营台 · P62 车队调度台 · P63 光伏电站运维台 · P64 航班动态助手 |
| **金融与家庭扩展** | P65 股票基金自选看板 ⚠️不构成投资建议 · P66 家庭资产配置台 · P67 众筹项目台 |
| **健康与教育扩展** | P68 体检报告管理台 · P69 慢病管理助手 · P70 心理咨询预约台 · P71 校园教务排课台 · P72 企业培训考试台 · P73 留学申请进度台 |
| **企业与政务扩展** | P74 企业知识库 · P75 OKR 目标管理台 · P76 IT 资产管理台 · P77 合同台账 · P78 舆情监测台 · P79 招投标管理台 · P80 电商客服质检台 · P81 政务热线分析台 · P82 社区网格员工作台 · P83 志愿者活动台 |
| **垂直行业与更多角色** | P84 ESG 报告工作台 · P85 实验室样本管理台 · P86 建筑工地安全巡检台 · P87 冷链仓储监控台 · P88 水质环境监测台 · P89 导游带团工作台 · P90 房东租务管理台 · P91 营养师工作台 · P92 自由职业结算台 · P93 电竞战队复盘台 · P94 琴行教务台 · P95 宠物寄养平台 · P96 装修报价工作台 · P97 社区团购团长台 · P98 图书馆座位预约台 · P99 摄影约拍平台 |

</details>

> 完整案例话术与 AI 能力亮点见技能仓库：[dsh-java-plugin-skills/references/prompt-recipes.md](https://github.com/deepseek-harness-java/dsh-java-plugin-skills)

---

## 🏗️ 案例仓库的统一结构

每个场景仓库都遵循同一套结构，看懂一个就能看懂全部：

```
<case-name>/
├── pom.xml                  # 父 pom（Maven 多模块）
├── x-app/                   # Spring Boot 业务应用
│   ├── Controller.java      #   REST API
│   ├── Store.java           #   预置演示数据
│   └── AssistantController.java  # AI 助手 SSE（透传 DSH）
├── x-plugin/                # DSH Java Native 插件
│   ├── XxxPlugin.java       #   3~5 个 AI 工具
│   └── META-INF/plugin.yaml #   插件声明
└── docs/
    ├── 使用说明.md
    └── images/              # 界面与验证截图
```

**每个案例 README 都包含**：项目组成 → 插件工具清单 → REST API 表 → 快速开始 → 端到端验证（`agent_stream.sh` 实测对话）→ 技术要点 → 目录结构。

---

## 🤝 如何参与

- **想跑某个场景**：从[案例索引](#-案例索引已发布仓库点击即入)点进对应仓库，按 README 快速开始。
- **想做清单里还没有的场景**：安装[技能包](https://github.com/deepseek-harness-java/dsh-java-plugin-skills)，用 Prompt 结构公式一句话生成，生成后欢迎 PR 回收案例。
- **想了解 DSH 宿主与插件协议**：见技能包仓库的技能文档与 `install_plugin.sh` 用法。

## 📮 相关链接

- 技能包（99 案例话术库）：https://github.com/deepseek-harness-java/dsh-java-plugin-skills
- 全部仓库列表：https://github.com/orgs/deepseek-harness-java/repositories
