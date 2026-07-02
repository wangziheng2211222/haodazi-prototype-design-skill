# 产品设计规范

当任务提到已知产品线、要求遵循设计规范，或没有截图/Figma 但需要产品原生视觉风格时，读取本文件。

## 选择规则

1. 如果有目标页面的 Figma 或截图证据，优先使用这些精确证据。
2. 产品设计规范用于补齐缺失的 token、组件行为、布局密度和 fallback 样式。
3. PRD 和需求文本始终是业务逻辑最高优先级来源。
4. 在 `design-tokens.json` 或最终说明中记录使用了哪个设计规范。
5. 如果使用 fallback 设计规范，要在假设或交付说明中明确说明。
6. 设计规范只解决视觉和组件风格；功能入口位置、模块归属、导航层级、Tab 关系和弹窗/抽屉承接，读取 `references/product-interaction-blueprints.md`。

## 已知产品

| 产品线索 | 设计规范参考 | 规则 |
| --- | --- | --- |
| 蝉圈圈 / Chanquanquan | `references/chanquanquan-design-system.md` | 直接加载。 |
| 蝉妈妈 / Chanmama | 暂无专属规范时使用 `references/chanquanquan-design-system.md` | 作为临时 fallback 使用，并明确标注。 |
| 蝉镜 / Chanjing | 预留未来专属规范 | 若暂无专属规范，先要求截图/Figma，或使用中性好搭子默认风格。除非用户明确允许，否则不要自动套用蝉圈圈。 |

## 输出要求

使用产品设计规范时，输出中应包含：

- `designSystem.product`：用户提供或系统推断的产品线。
- `designSystem.reference`：使用的参考文件或来源。
- `designSystem.isFallback`：是否为 fallback。
- `designSystem.fallbackReason`：fallback 原因。
- 从该设计规范提取或推导的 design tokens。

如果任务同时涉及功能落位，输出还应在 `interaction-blueprint.json` 或交付说明中记录所用产品交互蓝图；不要用设计规范推断入口层级。

## 冲突规则

- Figma 目标画框覆盖产品设计规范默认值。
- 截图视觉证据覆盖通用默认值，但不覆盖 Figma 节点证据。
- 产品设计规范覆盖通用 Element Plus 风格。
- 需求逻辑与视觉参考冲突时，业务规则服从需求。
