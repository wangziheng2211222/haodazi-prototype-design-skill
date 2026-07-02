# 输出协议

当任务需要明确产物、需求追踪或可复用评审输出时，使用这些结构。

## 产物集合

完整原型设计任务可按需要产出以下文件：

- `prototype.html` 或仓库原生页面文件：可运行的高保真评审原型。
- `page-map.json`：页面 ID、页面名、路由标签、页面职责和评审目的。
- `requirements-map.json`：需求卡、原文位置、解析意图和生成覆盖。
- `module-review-state.json`：模块分组、方案选择、页面组确认和用户修改意见。
- `interaction-blueprint.json`：跨页面流程、状态流转、弹窗、抽屉和关键交互。
- `visual-dna.json`：截图/风格分析，包括主参考、辅助参考、冲突点和 avoidances。
- `figma-restoration-context.json`：使用 Figma 时记录画框、节点、token、资产和截图上下文。
- `review-notes.md`：假设、未覆盖问题、覆盖警告和建议评审议程。
- `quality-report.json`：需求覆盖、运行时、视觉 QA 和修复状态。
- `acceptance-summary.json`：从用户任务角度归纳覆盖模块、未覆盖模块、评审风险和下一步。
- `repair-history.json`：修复计划、修复页面和修复原因。
- `agent-runs.json`：阶段状态、降级、重试、质量结果和修复次数。
- `design-tokens.json`：从截图或 Figma 推导出的颜色、字体、圆角、阴影、密度、间距和组件模式。
- `component-inventory.json`：生成组件清单和可复用模式。
- `design-system-used.md`：使用的产品设计规范、fallback 状态和偏离点。
- `delivery-notes.md`：设计和研发后续使用的实现备注。
- `implementation-notes.md`：开发估算、数据对象、API 假设、状态枚举、权限和风险。
- `figma-redraw-brief.md`：后续 Figma 重绘或插件导入使用的结构化设计说明。

轻量聊天任务可直接在回复中概括这些部分，不一定写文件。

## 页面地图 Schema

```json
{
  "productName": "string",
  "reviewGoal": "string",
  "pages": [
    {
      "pageId": "overview",
      "name": "总览",
      "purpose": "说明评审者可在此页验证什么。",
      "routeLabel": "总览",
      "primaryObjects": ["object"],
      "states": ["default", "empty", "loading", "error"],
      "contains": ["table", "filters", "detail-drawer", "create-dialog"],
      "requirementsCovered": ["R1", "R2"]
    }
  ],
  "flows": [
    {
      "name": "主流程",
      "steps": ["overview", "list", "detail"],
      "successState": "string",
      "failureStates": ["string"]
    }
  ]
}
```

## 需求地图 Schema

```json
{
  "sourceDocuments": [
    {
      "sourceId": "prd-main",
      "title": "需求文档",
      "type": "prd|notes|figma|screenshot|user-message",
      "sourcePointer": "文件、URL、章节、页码或消息引用"
    }
  ],
  "requirementCards": [
    {
      "requirementId": "REQ-001",
      "title": "需求卡标题",
      "summary": "一句话概括解析后的需求。",
      "sourceId": "prd-main",
      "sourcePointer": "第 2.1 节 / 第 3 页 / 第 4 段",
      "sourceExcerpt": "短原文摘录或来源线索。",
      "parsedIntent": "产品必须支持什么。",
      "acceptanceCriteria": ["评审者可以验证的条件。"],
      "impactedPageIds": ["lead-workbench"],
      "impactedStates": ["empty", "error", "permission-denied"],
      "openQuestions": ["如有未决问题，写在这里。"],
      "coverageStatus": "covered|partial|open"
    }
  ]
}
```

## 模块评审状态 Schema

```json
{
  "moduleGroups": [
    {
      "groupId": "lead-workbench-group",
      "pageId": "lead-workbench",
      "title": "线索工作台",
      "description": "同一真实页面内的列表、筛选、详情抽屉和新建弹窗。",
      "linkedSelection": true,
      "modules": ["MOD-001", "MOD-002"],
      "coverageWarnings": ["缺少批量操作规则"]
    }
  ],
  "modules": [
    {
      "moduleId": "MOD-001",
      "title": "线索列表",
      "description": "展示线索、状态和负责人。",
      "changeType": "create|update|remove|unknown",
      "priority": "P0|P1|P2|P3",
      "pageId": "lead-workbench",
      "fields": ["线索名称", "状态", "负责人"],
      "states": ["empty", "loading", "error", "permission-denied"],
      "flows": ["筛选线索", "打开详情"],
      "schemes": [
        {
          "schemeId": "A",
          "title": "表格 + 详情抽屉",
          "tradeoff": "适合高密度运营工作台。"
        }
      ],
      "sourceRequirementIds": ["REQ-001"]
    }
  ],
  "userSelections": {
    "selectedModuleIds": ["MOD-001"],
    "selectedSchemes": {
      "MOD-001": "A"
    },
    "skippedModuleIds": [],
    "notes": ["用户希望先保留详情抽屉。"]
  },
  "pageBoundaryStatus": "confirmed|needs-review|changed"
}
```

## 交互蓝图 Schema

```json
{
  "productPositioning": "string",
  "navigationModel": {
    "type": "left-sidebar|top-nav|tabs|breadcrumb|mixed",
    "items": [
      {
        "label": "线索",
        "pageId": "lead-workbench"
      }
    ]
  },
  "pageHierarchy": [
    {
      "pageId": "lead-workbench",
      "parentPageId": "",
      "level": 1,
      "role": "primary-workbench"
    }
  ],
  "criticalFlows": [
    {
      "name": "新建线索并跟进",
      "steps": [
        {
          "pageId": "lead-workbench",
          "action": "点击新建"
        }
      ]
    }
  ],
  "crossPageActions": [
    {
      "fromPageId": "overview",
      "toPageId": "lead-workbench",
      "trigger": "点击待处理线索"
    }
  ],
  "commonInteractionRules": [
    "删除前二次确认",
    "保存成功后使用 ElMessage 提示"
  ],
  "stateRules": [
    {
      "state": "empty",
      "displayRule": "解释空状态原因并提供主操作"
    }
  ],
  "visualConstraints": ["紧凑表格", "右侧详情抽屉"],
  "fallback": {
    "isDegraded": false,
    "reason": ""
  }
}
```

## 设计 Token Schema

```json
{
  "sourcePriority": ["requirements", "figma", "screenshots", "inference"],
  "designSystem": {
    "product": "蝉圈圈",
    "reference": "references/chanquanquan-design-system.md",
    "isFallback": false,
    "fallbackReason": ""
  },
  "styleSummary": "string",
  "colors": {
    "background": "#ffffff",
    "surface": "#ffffff",
    "text": "#111827",
    "mutedText": "#6b7280",
    "primary": "#2563eb",
    "border": "#e5e7eb",
    "danger": "#dc2626"
  },
  "typography": {
    "fontFamily": "system-ui",
    "pageTitle": "20px",
    "body": "14px",
    "caption": "12px"
  },
  "shape": {
    "radius": "8px",
    "shadow": "subtle",
    "borderWidth": "1px"
  },
  "density": {
    "table": "compact",
    "form": "comfortable",
    "navigation": "dense"
  },
  "componentPatterns": [
    "left-sidebar navigation",
    "filter toolbar above table",
    "detail drawer for row inspection"
  ],
  "avoidances": [
    "generic marketing hero",
    "decorative gradients without product evidence"
  ]
}
```

## 视觉 DNA Schema

```json
{
    "primaryReference": "截图 1 或产品设计规范",
  "auxiliaryReferences": ["screenshot-2"],
  "conflicts": [
    {
      "sourceA": "screenshot",
      "sourceB": "requirements",
      "resolution": "业务逻辑服从需求；视觉语言参考截图。"
    }
  ],
  "styleSummary": "string",
  "layoutDensity": "compact|comfortable|spacious",
  "navigationPattern": "string",
  "componentPatterns": ["table toolbar", "detail drawer"],
  "colorNotes": ["string"],
  "typographyNotes": ["string"],
  "avoidances": ["generic blue-white admin"]
}
```

## Figma 还原上下文 Schema

```json
{
  "figmaFileSummary": "string",
  "targetFrames": [
    {
      "frameName": "string",
      "fileKey": "string",
      "nodeId": "string",
      "frameScreenshot": "可用时填写路径或 URL"
    }
  ],
  "nodeTreeSummary": "string",
  "autoLayoutRules": ["string"],
  "figmaDesignTokens": {},
  "componentInstances": ["string"],
  "assetManifest": [
    {
      "assetId": "string",
      "type": "image|svg|icon",
      "usage": "string",
      "source": "可用时填写路径或 URL"
    }
  ],
  "restorationNotes": ["string"]
}
```

## 质量与修复 Schema

```json
{
  "qualityReport": {
    "requirementCoverage": "pass|partial|fail",
    "runtimeStatus": "pass|partial|fail",
    "visualFidelity": "pass|partial|fail|not-applicable",
    "crossPageConsistency": "pass|partial|fail",
    "openIssues": ["string"]
  },
  "visualDiffs": [
    {
      "baseline": "figma-frame|screenshot|design-system",
      "pageId": "string",
      "area": "string",
      "issue": "layout|color|typography|spacing|radius|shadow|component|asset|density",
      "severity": "P0|P1|P2|P3",
      "suggestedRepair": "string"
    }
  ],
  "repairHistory": [
    {
      "repairId": "REP-001",
      "type": "requirement-gap|visual-deviation|interaction-issue|field-state-issue|missing-page|delivery-asset",
      "affectedPageIds": ["string"],
      "changedArtifacts": ["string"],
      "reason": "string"
    }
  ]
}
```

## 验收摘要 Schema

```json
{
  "acceptanceSummary": {
    "taskGoal": "string",
    "overallStatus": "passed|partial|blocked",
    "coveredModules": ["MOD-001"],
    "uncoveredModules": [
      {
        "moduleId": "MOD-009",
        "reason": "需求缺少规则，已列为评审问题。"
      }
    ],
    "reviewRisks": [
      {
        "severity": "P0|P1|P2|P3",
        "pageId": "lead-workbench",
        "risk": "批量删除权限未明确。"
      }
    ],
    "suggestedNextActions": ["确认批量操作权限", "补充异常状态规则"]
  }
}
```

## Agent Run Schema

```json
{
  "agentRuns": [
    {
      "runId": "run-001",
      "stage": "context|decomposition|blueprint|module-review|high-fidelity|quality|acceptance|repair",
      "status": "pending|running|waiting-user|passed|degraded|failed|repaired",
      "summary": "正在整理交互蓝图。",
      "startedAt": "ISO-8601",
      "endedAt": "ISO-8601",
      "affectedPageIds": ["lead-workbench"],
      "qualityIssueIds": [],
      "repairCount": 0,
      "degradationReason": ""
    }
  ]
}
```

## 组件清单 Schema

```json
{
  "components": [
    {
      "name": "LeadTable",
      "type": "table|form|card|dialog|drawer|tag|navigation|chart|empty-state",
      "usedByPageIds": ["lead-workbench"],
      "states": ["default", "empty", "loading", "error"],
      "styleNotes": "string",
      "dataDependencies": ["Lead"]
    }
  ],
  "stateEnums": [
    {
      "name": "LeadStatus",
      "values": ["待跟进", "已转化", "已流失"]
    }
  ],
  "apiAssumptions": ["string"],
  "risks": ["string"]
}
```

## 评审说明结构

```markdown
# 评审说明

## 假设

- ...

## 需求覆盖

| 需求 | 覆盖位置 | 说明 |
| --- | --- | --- |
| ... | ... | ... |

## 待评审问题

| 优先级 | 页面 | 区域 | 问题 | 建议修复 |
| --- | --- | --- | --- | --- |
| P1 | ... | ... | ... | ... |

## 交付说明

- ...

## 视觉 QA

- 使用的基准：Figma 画框、截图、产品设计规范或无。
- 已修复视觉问题：
- 剩余视觉问题：
- 相似度评分：仅在用户要求或评分能解释质量门槛时填写。
```

## 独立 HTML 评审壳

创建独立评审原型时：

- 左侧使用固定或 sticky 的预览/内容区域。
- 右侧使用页面导航面板，包含页面列表、需求卡、状态、假设和评审问题。
- 提供需求卡详情视图：点击需求卡后展示原文位置、原文摘录、解析意图、验收标准、影响页面/状态和覆盖状态。
- 使用稳定的按钮或 tabs 切换页面。
- 不要在实际原型前面放营销落地页。
- 窄屏下导航仍应可用。

如果原型包含生成的 Vue 页面，把它们作为独立页面模块或清晰分隔的代码块嵌入。运行时边界以 `SKILL.md` 为准。
