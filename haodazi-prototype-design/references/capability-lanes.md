# 能力分流

用本参考文件把好搭子原型设计工作组织成用户能理解的业务能力，而不是内部 agent 工种。

## 能力路由

| 输入或请求 | 能力通道 | 主要产物 |
| --- | --- | --- |
| 模糊想法、短需求、不知道怎么描述 | 主动假设补全 | `assumption-card.json`、`page-map.json`、`requirements-map.json`、评审假设 |
| PRD、需求纪要、产品想法 | 需求生成原型 | `page-map.json`、`requirements-map.json`、`interaction-blueprint.json`、高保真页面 |
| 用户要求先看模块、方案、页面组或拆解 | 模块评审确认 | `module-review-state.json`、`page-map.json`、`requirements-map.json` |
| 一张或多张截图 | 截图风格复刻 | `visual-dna.json`、`design-tokens.json`、视觉 QA 说明 |
| Figma 文件/画框 | Figma 还原 | `figma-restoration-context.json`、画框截图、资产清单、视觉 QA 说明 |
| 生成后的用户反馈 | 原型评审修复 | `review-issues`、`repair-plan`、修复后页面、`repair-history.json` |
| 设计/开发/Figma 交付 | 交付资产 | `component-inventory.json`、`implementation-notes.md`、`figma-redraw-brief.md` |

## 需求生成原型

默认能力。完整原型任务都要经过这条能力。

内部产物：

- `inputSummary`
- `pageMap`
- `pageIds`
- `moduleCoverage`
- `interactionBlueprint`
- `assumptionCard`
- `requirementsMap`
- 可选 `moduleReviewState`
- `highFidelityPages`
- `coverageWarnings`

规则：

- 输入不完整时先主动补齐合理业务闭环，不要把用户拉进长问卷。
- 理解需求后直接生成完整高保真页面。
- 保留模块拆解和 `pageId` 推理，但不要强迫用户先选择模块。
- 同一评审面内的列表、详情、新增/编辑弹窗、抽屉和局部状态，要绑定到同一个 `pageId`。
- 需求卡必须连接原始文本和生成覆盖情况。
- 用户明确要求先确认模块或方案时，先进入模块评审确认，不要直接越过用户确认。

## 主动假设补全

用户只给一句想法、需求明显不完整，或不知道怎么描述需求时使用。目标是帮用户把需求先变成可生成版本，而不是把问题抛回用户。

输出：

- `assumptionCard`
- `assumptions`
- `inferredRoles`
- `inferredCoreFlow`
- `inferredPages`
- `inferredStates`
- `blockingQuestion`，仅在确实无法继续时输出

规则：

- 默认不提问，先生成主动假设卡。
- 主动假设卡写成“我将按以下方向生成”，不要写成问卷。
- 每张假设卡最多包含 5 项：产品类型、主要角色、核心流程、页面范围、关键状态/规则。
- 假设要具体到能改变页面结构，例如“销售团队客户管理工作台”，不要写“后台系统”这种空泛描述。
- 用户不回复时，按假设继续生成，并把假设写入需求卡、页面地图和评审说明。
- 用户纠正时，只改对应假设和受影响 `pageId`，不要推倒全部结果。

只有三类情况先问一个阻塞问题：

- 业务类型完全无法判断。
- 平台形态会显著影响布局和组件，但输入没有线索。
- 输入互相冲突，导致核心方向无法选择。

## 模块评审确认

用户要求查看拆解、选择方案、确认页面组、优化此组、追加拆解，或任务复杂到必须先确认页面边界时使用。

输出：

- `moduleGroups`
- `modules`
- `schemes`
- `pageIds`
- `coverageWarnings`
- `moduleReviewState`

规则：

- 模块评审的目标是确认需求理解、页面边界和方案选择，不是预览视觉稿。
- 每个模块记录标题、描述、优先级、变更类型、所属 `pageId`、关键字段、状态、流程、权限、异常和覆盖风险。
- 同 `pageId` 下的列表、详情、弹窗、抽屉、表单和状态模块要联动选择。
- “优化此组”必须携带当前 `pageId`、该页面组全部模块、原始需求、截图/Figma/知识库上下文和用户反馈重新分析。
- 页面边界变化时，可以返回新的 `pageId`，但必须重新生成或校验交互蓝图。
- 被跳过、被替换、被用户确认的模块都要记录，供后续高保真使用。

## 截图风格复刻

用户提供截图、已有页面、产品参考或视觉样例时使用。

输出：

- `styleSummary`
- `visualDna`
- `designTokens`
- `componentPatterns`
- `layoutPatterns`
- `densityRules`
- `assetHints`
- `avoidances`
- 如果可对比生成预览，则输出 `visualDiffs`

规则：

- 默认把截图当作视觉证据，不再问“参考还是复用”。
- 多截图时，选择主参考、辅助参考，并记录冲突点。
- 提取布局密度、导航形态、信息层级、组件风格、颜色、字体、圆角、阴影、描边、间距和状态处理。
- 截图有明确视觉语言时，不要退回通用蓝白后台。
- 截图视觉与需求冲突时，业务逻辑服从需求，视觉语言参考截图。

## Figma 还原

用户提供 Figma 链接、具体画框、node ID、file key、Figma 导出上下文，或要求 Figma 还原时使用。

输出：

- `figmaFileSummary`
- `targetFrames`
- `nodeTreeSummary`
- `autoLayoutRules`
- `figmaDesignTokens`
- `componentInstances`
- `assetManifest`
- `frameScreenshots`
- `figmaRestorationContext`
- `visualDiffs`

规则：

- 优先使用具体 frame/node 证据，而不是截图猜测或产品设计规范默认值。
- 解析 Figma URL 意图：file key、node ID、选中画框和权限约束。
- 如果文件很大且没有指定目标画框，先让用户选择目标画框，不要试图一次还原全部。
- 在可用时读取或保留 Auto Layout、约束、尺寸、颜色、字体、圆角、阴影、描边、透明度、组件、实例和资产。
- 尽量导出或使用目标画框截图作为视觉 QA 基准。
- 不要把 Figma 1:1 还原简化成截图风格复刻。
- 不要让 Element Plus 默认样式覆盖 Figma 视觉目标；Element Plus 只是运行时组件，布局和视觉意图仍要贴近 Figma。

## 原型评审修复

已有高保真结果后，或用户要求修改原型时使用。

先分类反馈：

- 需求缺口：缺规则、页面、角色、字段、流程或状态。
- 视觉偏差：布局、颜色、字体、间距、圆角、阴影、组件或资产不匹配。
- 交互问题：导航、弹窗/抽屉行为、确认、反馈、禁用态或表单校验。
- 字段/状态问题：命名不一致、枚举不一致、状态流转、权限、空/错/加载态。
- 缺失页面：需要新增页面或路由。
- 交付资产需求：用户需要交付材料，而不是改页面代码。

修复规则：

- 只修最小受影响页面、区域、交互或 token。
- 保留无关页面和业务逻辑。
- 如果修复影响共享导航、共享字段或共享状态枚举，要同步更新受影响页面。
- 记录 `repairPlan`、`patchedPages` 和 `repairHistory`。

## 交付资产

当用户需要设计继续改、Figma 重绘、开发估算、评审材料或原型之外的交付内容时使用。

输出：

- 设计风格摘要。
- 设计 token：颜色、字体、间距、圆角、阴影、组件、状态、图标、资产。
- 组件清单：按钮、表格、卡片、表单、弹窗、抽屉、标签、导航、图表、空/错/加载态。
- 页面结构和流程。
- 开发说明：数据对象、API 假设、状态枚举、权限、交互说明、风险和未决问题。
- Figma 重绘说明，或后续 Figma 插件/导入使用的中间节点描述。

规则：

- 除非用户只要规划，否则交付资产应在原型之后生成。
- 交付资产要足够结构化，方便设计和研发复用。
- 解释关键设计选择的原因，而不是只给代码。

## 视觉 QA

提供截图/Figma，或用户质疑视觉还原度时使用。

输出：

- `quality-report.json`
- `visual-diffs`
- 如果用户要求可见评分，则给相似度评分
- 定向修复建议

规则：

- 使用最具体的视觉基准：Figma frame 优先，其次截图，再其次产品设计规范。
- 检查布局、层级、颜色、字体、间距、圆角、阴影、组件缺失、资产缺失和密度。
- 分数可作为内部判断；只有用户要求或评分能解释质量门槛时，才展示给用户。
