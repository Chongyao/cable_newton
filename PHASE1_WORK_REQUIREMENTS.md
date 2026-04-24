# Phase 1 工作内容要求

## 1. 阶段目标
Phase 1 聚焦 **cables（1D deformables / VBD）**，目标是为 NVIDIA Newton 物理引擎交付可直接使用的、**Newton-ready** 的 cable 资产与相关求解能力。

核心目标包括：
- 基于 NVIDIA cable taxonomy 完成各类 cable 资产制作
- 使资产的几何、参数化与 Newton VBD solver 兼容
- 为不同 cable 类型标定各向异性刚度参数
- 为每类资产提供至少一个验证场景，证明其行为合理
- 在 Newton 现有 rod solver 不足时，补充定制 Newton / Warp plugin solver
- 最终形成可交付的资产包、插件、文档与阶段总结

## 2. Phase 1 资产范围
依据合同附件与 cable taxonomy，Phase 1 覆盖以下 cable 类别：

1. Electrical wire
2. Electrical cable
3. Ribbon cable
4. Flex cable
5. Coaxial cable
6. Industrial hoses
7. Tensile / tendon cables
8. Cable bundles

其中 taxonomy 文档还额外提到：
- Miscellaneous / Bowden cables

但当前正式 SOW 明确要求交付的主范围为前述 8 类 cable 资产。

## 3. 每类资产的交付要求
对每一种 cable class，需满足以下要求：

### 3.1 资产与几何
- 交付可用于 Newton 的 cable 资产
- 几何与参数化方式需兼容 Newton VBD solver
- 资产几何应适合公司自动化资产管线
- 几何通常应从 centerline 与 material frame 生成

### 3.2 数据与格式
- 交付 Open USD 资产文件
- 资产需带有正确的 Newton API annotations

### 3.3 物理参数标定
- 为每类 cable 标定各向异性刚度参数
- 参数至少覆盖：
  - bending-Y
  - bending-Z
  - torsion
  - axial ±
- 参数特性需与 taxonomy 中描述的材料/结构行为一致

### 3.4 验证场景
- 每类资产至少提供 1 个验证场景
- 验证场景应展示可信、可解释的行为
- 验证内容可包括 routing、insertion，或与该类型 cable 相符的典型使用场景

## 4. 定制求解器 / 插件要求
当 Newton 现有 rod solver 不能满足需求时，需要补充定制 Newton / Warp plugin solver，特别适用于以下可能需要非各向同性行为的类别：
- ribbon cable
- flex cable
- tensile / tendon cables
- cable bundles
- 以及其他 Newton 默认 rod solver 无法准确表达的 cable 类型

对应要求包括：
- 设计并实现 custom solver / plugin components
- 与 Newton / Warp 集成
- 输出书面 solver / plugin design document，内容应包括：
  - 架构设计
  - Newton / Warp 集成方式
  - 性能目标
- 提供可运行的 plugin 实现，并在对应 cable class 上完成验证

## 5. 交付打包要求
最终交付不仅是单个资产，还应形成可直接使用的整体包：
- 每个 custom solver / plugin 需与对应资产一并打包
- 下游用户应能够使用公司提供的 plugin 直接运行公司提供的资产
- 所有 solver / plugin 代码、设计文档、资产与相关工件均归公司所有

## 6. 明确不在本阶段范围内的内容
依据 SOW，以下内容不属于本次 Phase 1 / 4-week trial 的交付范围：
- plastic deformation、crease、crack 等材料级薄片变形行为
- 与 thin / surface deformables 相关的工作
- 与 3D volumetric deformables 相关的工作
- Phase 2、Phase 3 的正式交付内容

## 7. 协作与沟通要求
Phase 1 除资产与技术交付外，还包含明确的协作要求：

- 参与固定状态会议：每周 3 次
- 日常通过公司指定渠道协作（如 Slack）
- 提交每周书面进展更新，内容包括：
  - 已完成工作
  - 当前阻塞项
  - 下一步计划
- 如果发现 Newton 本身存在限制，应先向公司方（Steven Ren / Krish Mehta）反馈，由公司决定是否与 NVIDIA Newton 团队沟通
- 未经公司书面同意，不应直接向 NVIDIA 或第三方共享公司 solver 设计或 plugin 实现

## 8. 工具与环境要求
工作环境与技术栈包括：
- NVIDIA Newton physics engine / Warp
- Open USD
- Python
- C++
- CUDA（按需）
- 公司控制的 git 仓库，所有代码在合并前需经过 review

## 9. 里程碑要求
## 9.1 来自岗位说明（Phase 1 原始分段）
- **Week 1**：
  - Newton / VBD 开发环境搭建完成
  - pipeline design doc 完成
  - 首 2 类 cable 资产完成
- **Week 2**：
  - 再完成 4 类 cable 资产
  - 对应 validation scenes 完成
- **Week 3**：
  - 最后 2 类 cable 资产完成
  - 输出 Phase 1 asset pack
  - 完成交付文档并移交 NVIDIA / 项目方

## 9.2 来自正式 SOW（4-week trial，优先按此执行）
- **Week 1**：
  - Newton / Warp / VBD 开发环境可用
  - cable asset pipeline 设计文档完成
  - solver / plugin 设计文档首版完成
  - 前 2 类适合 Newton 现有 rod solver 的 cable 资产交付（例如 electrical wire、electrical cable）
- **Week 2**：
  - 新增 cable classes 与对应 validation scenes 交付
  - custom plugin solver scaffold 完成，并在一个 non-isotropic cable class 上验证
- **Week 3**：
  - 剩余 cable classes 交付
  - custom solver 用于更多 non-isotropic cable classes（例如 ribbon cable、flex cable、tensile/tendon cables、cable bundles）
- **Week 4**：
  - consolidated cable asset pack 完成
  - custom plugin solver(s) 完成
  - supporting documentation 完成
  - 提交书面 retrospective，总结 solver 稳定性、真实工作量、后续建议，以及后续 Statement of Work 的建议范围

## 10. 验收标准
正式验收以公司内部验证和批准为准，且公司拥有最终裁量权。若交付未达到验收标准，需要按要求进行合理修改直至通过。

可归纳的核心验收要求如下：
- 全部目标 cable classes 已按要求完成
- 资产为 Newton-ready，并能在目标管线中使用
- Open USD 与 Newton annotations 完整正确
- 刚度参数与 taxonomy 预期一致
- 每类资产至少有一个可信验证场景
- 对于必要类别，custom plugin solver 已可工作并完成验证
- 最终提交完整资产包、插件、文档与阶段总结

## 11. 建议的实际执行重点
结合三份材料，Phase 1 的工作重点可归纳为：

1. **先搭建环境与资产管线**：优先完成 Newton / Warp / VBD 环境和资产生成流程。
2. **先做 rod solver 可覆盖的简单类别**：例如 electrical wire、electrical cable。
3. **尽早识别需要 custom solver 的类别**：尤其是 ribbon、flex、tensile/tendon、bundle 等非各向同性或结构特殊类型。
4. **资产与 solver 同步验证**：不要只生成资产文件，必须同时准备 validation scenes。
5. **按最终打包思路推进**：资产、插件、文档要能组合成交付包，而不是分散的实验结果。
6. **保留 trial retrospective 所需素材**：包括稳定性问题、工作量评估、后续范围建议。

## 12. 文档依据
本文件基于以下材料整理：
- Contractor Job Spec — Chongyao Zhao (Newton Deformables)
- Chongyao_Consulting_Agreement_v2（含 Exhibit A / Statement of Work）
- Cable Taxonomy

若不同材料之间存在差异，建议以 **正式签署的 Consulting Agreement + Exhibit A (SOW)** 为主，岗位说明中的 3-week 分解可作为早期参考版本。
