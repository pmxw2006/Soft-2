# 固定资产管理系统 (Web 版)

> 一个基于 C# ASP.NET Web Forms + 三层架构（BLL/DAL/Mods） + SQL Server 的固定资产管理系统，实现资产入库、领用、归还、维修、报废等功能。本项目为大二上学期软件工程课程小组作业，在之前 WinForms 版的基础上重构为 Web 应用程序，架构和安全性有明显提升。

---

## 项目简介

本系统针对企业固定资产管理场景，提供资产全生命周期管理功能，包括资产信息维护、领用与归还、维修登记、报废处理、仓库信息管理以及简单的用户登录验证。系统采用 B/S 架构（浏览器/服务器），前端使用 ASP.NET Web Forms 构建动态网页，后端通过 ADO.NET 与 SQL Server 交互，并按照三层架构组织代码，提升可维护性。

**项目背景**：大二上学期软件工程课程设计，由小组成员协作完成。项目延续了大一阶段 WinForms 版的核心需求，但在技术栈上转向 Web 开发，引入了更清晰的层次划分和更安全的数据访问方式。

---

## 功能特性

- 固定资产管理：资产信息的录入、修改、删除、多条件查询
- 领用与归还：记录领用人、时间，归还后可查看归还状态
- 维修管理：资产维修登记与维修状态跟踪
- 报废管理：资产报废申请与审批记录
- 仓库信息管理：维护仓库基础数据
- 用户登录：实现简单的登录验证，区分管理员和普通用户（可通过 Session 控制访问权限）

---

## 技术栈

| 技术 | 说明 |
|------|------|
| 编程语言 | C# |
| 前端框架 | ASP.NET Web Forms (.NET Framework) |
| 数据访问 | ADO.NET（参数化查询） |
| 数据库 | SQL Server |
| 管理工具 | SQL Server Management Studio 20 (SSMS 20) |
| 架构模式 | 三层架构（表示层 / 业务逻辑层 BLL / 数据访问层 DAL + 模型层 Mods） |
| 开发工具 | Visual Studio |

---

## 项目目录结构

```
Soft-2/
├── 1、项目规格/            # 项目规格说明文档
├── ２、项目立项/          # 项目立项相关文档
├── ３、项目计划/          # 项目开发计划
├── ４、项目需求/          # 需求规格说明书
├── ５、项目设计/          # 系统设计说明书
├── 6、项目源码/            # C# 源代码
│   ├── WebApplication1/   # 表示层（ASP.NET Web Forms 页面）
│   │   ├── Login.aspx     # 登录页
│   │   ├── DengLu.aspx    # 登录处理页
│   │   ├── GuDingZiChan.aspx  # 固定资产管理页
│   │   ├── CangKuGuanLi.aspx  # 仓库管理页
│   │   ├── GuiHuan.aspx   # 归还管理页
│   │   ├── JieChu.aspx    # 借出管理页
│   │   └── ...
│   ├── BLL/               # 业务逻辑层
│   │   ├── GuDingZiChanManager.cs
│   │   ├── CangKuGuanLiManager.cs
│   │   ├── GuiHuanManager.cs
│   │   ├── JieChuManager.cs
│   │   ├── JieHuanManager.cs
│   │   └── ...
│   ├── DAL/               # 数据访问层
│   │   ├── DBHelper.cs    # 数据库连接与执行帮助类
│   │   ├── GuDingZiChanServices.cs
│   │   ├── CangKuGuanLiServices.cs
│   │   ├── GuiHuanService.cs
│   │   ├── JieChuService.cs
│   │   └── ...
│   └── Mods/              # 模型（实体）层
│       ├── GuDingZiChan.cs
│       ├── CangKuGuanLi.cs
│       ├── DengLuJieGuo.cs
│       ├── GuiHuanInfo.cs
│       ├── JieChuInfo.cs
│       └── ...
├── 8、项目答辩/            # 答辩 PPT 及相关材料
└── 9、项目总结/            # 项目总结报告
```

---

## 快速开始

### 环境要求

- Windows 操作系统
- Visual Studio 2019 或更高版本（需安装 ASP.NET 和 Web 开发组件）
- SQL Server 数据库（可通过 SSMS 20 管理）
- SQL Server Management Studio 20 (SSMS 20)

### 本地运行步骤

1. 克隆仓库
   ```bash
   git clone https://github.com/pmxw2006/Soft-2.git
   ```

2. 打开 SQL Server Management Studio 20，新建数据库（如 `Soft`），执行项目附带的数据库建表脚本（参考项目文档中提供的 SQL 脚本）。

3. 修改数据访问层 `DAL/DBHelper.cs` 中的连接字符串：
   ```csharp
   public static string connstring = "server=.;database=Soft;integrated security=true;";
   ```
   根据你的本地环境调整服务器地址、数据库名称和认证方式（若使用 SQL Server 认证，需改为 `user id=...;password=...` 格式）。

4. 使用 Visual Studio 打开 `6、项目源码/WebApplication1/WebApplication1.sln` 解决方案文件。

5. 在 Visual Studio 中按 F5 或点击“启动”按钮，系统将自动编译并在浏览器中打开登录页面。

---

## 架构说明

本项目采用三层架构（3-Tier Architecture），将代码划分为清晰的层次：

- **表示层（UI）** ：ASP.NET Web Forms 页面，负责用户交互和界面展示，调用 BLL 获取数据并呈现。
- **业务逻辑层（BLL）** ：位于 `BLL` 文件夹，封装核心业务规则，例如资产领用前的库存校验、归还状态判断等，是表示层和数据层的桥梁。
- **数据访问层（DAL）** ：位于 `DAL` 文件夹，直接与 SQL Server 交互，使用 ADO.NET 执行 SQL 命令并返回结果。所有 SQL 操作均使用参数化查询，有效防止 SQL 注入。
- **模型层（Mods）** ：位于 `Mods` 文件夹，定义了与数据库表对应的实体类，用于在各层之间传递数据。

---

## 代码安全性评估

相比 WinForms 版本（Soft-1），本项目在安全性方面有较大提升：

- **参数化查询全覆盖**：数据访问层全面使用 `SqlParameter` 进行参数化查询，有效杜绝了 SQL 注入漏洞（例如 `GuDingZiChanServices.cs` 中的模糊查询和删除操作）。
- **连接字符串仍为明文**：数据库连接字符串直接写在 `DBHelper.cs` 中，这是学生项目常见的简化处理，生产环境中应使用加密配置文件或环境变量存放。
- **用户认证简单**：系统实现了基本的登录功能，但权限管理较为基础，主要依赖 Session 判断用户身份，尚未实现细粒度的角色权限控制。
- **输入校验有待加强**：前端页面和后端代码的输入验证不够全面，部分页面可能未对空值或非法格式进行严格校验，存在数据污染风险。
- **异常处理可以更统一**：代码中部分 `catch` 块仅做简单提示，建议建立统一的异常处理与日志记录机制，避免暴露系统内部信息。

---

## 模型与设计反思

作为大二上学期的课程项目，本系统在架构和设计上比大一时有显著进步，但仍存在以下提升空间：

- **三层架构初步实践成功**：代码已经实现了表示层与业务逻辑、数据访问的分离，为后续学习和项目扩展打下良好基础。
- **耦合度可进一步降低**：部分页面代码（如 `GuDingZiChan.aspx.cs`）中仍包含直接实例化 BLL 对象的逻辑，可考虑引入依赖注入或工厂模式进一步解耦。
- **缺少接口抽象**：BLL 和 DAL 层未定义接口，导致各层之间存在具体实现依赖，不利于单元测试和替换实现。
- **数据库设计可优化**：部分表结构可能存在冗余字段或未合理使用外键约束，查询性能在数据量增大时也有优化空间。
- **前端页面体验较基础**：页面布局和样式较为简单，未使用响应式设计或前端框架，移动端访问体验有待改善。

---

## 作者与贡献

- **pmxw2006（缥缈）** - 项目主要开发者
- 小组成员共同参与需求分析、文档撰写、前后端开发与答辩准备

---

## 致谢

感谢课程指导老师在项目开发过程中给予的指导和帮助，感谢小组全体成员的协作与付出。

---

## 许可证

本项目仅用于学习交流，未经许可不得用于商业用途。

---

*最后更新：2026年5月*
