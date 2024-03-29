---
title: 软考笔记 - 系统测试与维护
date: 2023-04-09 15:00:00 +0800
categories: 软考
---
2022年5月左右的预测。

![2022-May-system-test-and-maintenance.png](https://s2.loli.net/2023/04/09/YKdm6Ggiurxh5cS.png)

## 软件测试分类与方法

软件应尽早测试、不断测试。程序员避免测试自己的程序。代码修改后应进行回归测试。对一个程序而言，尚未发现的错误数量与该程序已发现错误数成正比。

- 动态测试，计算机运行，分为：黑盒、白盒、灰盒测试；
- 静态测试，纯人工，分为：桌前检查（自己review）、代码审查（交叉review）、代码走查（团体review，闻讯形式）。

黑盒测试（功能测试）：等价类划分、边界值分析、错误推测、因果图；

白盒测试：基本路径、循环覆盖、逻辑覆盖。

## 软件测试阶段

- 单元测试：模块测试，模块功能、性能、接口等
- 集成测试：模块间的接口
- 系统测试：真实环境下，验证完整的软件配置项能否和系统正确连接
- 确认测试：验证软件与需求的一致性。内部确认测试、Alpha、Beta、验收测试（其中Alpha和Beta针对软件产品来测试）
- 回归测试：测试软件变更之后，变更部分的正确性对变更需求的符合性。

集成测试策略：一次性组装，增量式组装。其中增量式组装分为自顶向下（需要桩模块）、自底向上（需要驱动模块）和混合式（都需要）。

系统测试：主要有功能测试和性能测试。性能测试可以进一步分为：负载测试、压力测试、强度测试、容量测试（并发测试）好可靠性测试。

- 负载测试：各种工作负载下的性能
- 压力测试：系统的瓶颈或不可接受的性能点，极限点
- 强度测试：系统在资源特别的低的环境下运行
- 容量测试：同时在线的用户数
- 可靠性测试：MTTF之类参数

## 面向对象测试

分为下面四个层次：

- 算法层（单元测试）：包括等价类划分测试、组合功能测试（基于判定表的测试）、递归函数测试和多态消息测试
- 类层（模块测试）：包括不变式边界测试、模态类测试和非模态类测试
- 模板层/类树层（集成测试）：包括多态服务测试和展平测试
- 系统层（系统测试）

## 软件测试与调试

软件调试的方法：

- 蛮力法：主要思想是“通过计算机找错"，低效，耗时
- ﻿回溯法：从出错处人工沿控制流程往回追踪，直至发现出错的根源。复杂程序由于回溯路径多，难以实施
- 原因排除法：主要思想是演绎和归纳，用二分法实现

|                       软件测试                       |                软件调试                |
| :--------------------------------------------------: | :------------------------------------: |
|                    找出存在的错误                    |      定位错误并修改程序以修正错误      |
| 从已知条件开始，<br />有预知的结果<br />（测试用例） | 从未知条件开始，<br />结束过程不可预计 |
|     测试过程可以事先设计，<br />进度可以事先确定     |         不能描述过程或持续时间         |

## 遗留系统处置问题

![legacy-system-problem.png](https://s2.loli.net/2023/04/10/o8cufBYdD7PO9Nj.png)

## 新旧系统转换策略

- 直接转换：老系统停，新系统上，风险高
- 并行转换：两个系统在转换期同时运行一段时间，成本高，风险降低
- 分段转换：部分子系统直接转换，分段进行；分地区转换；

### 数据转换与迁移

包括三步：抽取、转换、装载。

- 系统切换前通过工具迁移
- 系统切换前采用手工录入
- 系统切换后通过新系统生成

## 系统维护

- 正确性维护：改正尚未发现的错误
- 适应性维护：使软件适应环境变化（外部环境、数据环境）
- 完善性维护：扩充功能和改善性能
- 预防性维护：适应未来的软硬件环境
