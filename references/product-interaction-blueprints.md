# 产品交互蓝图

当任务提到已知产品线、需要判断功能入口位置、页面归属、导航层级、Tab 关系、弹窗/抽屉入口或原系统交互习惯时，读取本文件。

## 选择规则

1. 需求文档仍是业务逻辑最高优先级来源。
2. 交互蓝图用于判断功能应该放在哪个模块、从哪个入口进入、是否同级导航切换、是否用弹窗/抽屉承接。
3. 设计规范用于视觉样式，交互蓝图用于产品结构；二者不能互相替代。
4. 如果有目标页面截图或 Figma，优先使用截图/Figma 的精确入口证据。
5. 如果使用交互蓝图，要在 `interaction-blueprint.json` 或交付说明中记录引用来源。
6. 蓝图仅代表已采集范围；未采集入口不能推断为已有功能。

## 已知产品

| 产品线索 | 交互蓝图参考 | 规则 |
| --- | --- | --- |
| 蝉圈圈 / 圈圈 / Chanquanquan | `references/chanquanquan-interaction-blueprint.md` | 直接加载，用于模块落位、入口位置、导航关系和功能区域判断。 |
| 蝉妈妈 / Chanmama | 暂无专属交互蓝图 | 可临时参考蝉圈圈的业务结构，但必须标注为 fallback，并避免照搬模块名。 |
| 蝉镜 / Chanjing | 预留未来专属交互蓝图 | 若暂无专属蓝图，先依赖需求、截图或 Figma；不要自动套用蝉圈圈。 |

## 输出要求

使用产品交互蓝图时，输出中应包含：

- `interactionBlueprint.source.product`：产品线。
- `interactionBlueprint.source.reference`：使用的交互蓝图文件。
- `interactionBlueprint.source.isFallback`：是否为 fallback。
- `interactionBlueprint.source.usedFor`：模块落位、入口位置、导航关系、Tab 层级、弹窗/抽屉等。
- 未确认入口或缺失采集范围要写入评审问题。

## 冲突规则

- 需求明确指定入口时，优先服从需求，并在说明中标注偏离蓝图。
- Figma 或截图出现真实入口位置时，优先服从截图/Figma。
- 交互蓝图只补齐产品结构，不覆盖视觉设计规范。
- 蓝图未采集的入口不得作为原系统已有能力输出。
