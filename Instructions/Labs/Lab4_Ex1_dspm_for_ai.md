---
lab:
  title: 练习 1 - 保护 AI 环境中的数据
  module: Module 4 - Protect data in AI environments
---

## WWL 租户 - 使用条款

如果在讲师引导式培训过程中向你提供租户，请注意，提供租户旨在支持讲师引导式培训中的动手实验室。

租户不应共享或用于动手实验室以外的用途。 本课程使用的租户为试用租户，课程结束后无法使用或访问，不符合扩展条件。

租户不得转换为付费订阅。 在本课程中获得的租户仍然是 Microsoft Corporation 的财产，我们保留随时获取访问权限和收回的权利。

# 实验室 4 - 练习 1 - 保护 AI 环境中的数据

你是 Contoso Ltd 的信息安全管理员 Joni Sherman。随着 Microsoft Copilot 等 AI 工具更集成到日常工作流中，你的团队被要求评估和改进敏感数据的保护。 在本实验室中，你将了解适用于 AI 的 Microsoft Purview DSPM 如何通过策略强制措施、风险检测和暴露评估来帮助保护与 AI 工具的数据交互。

**任务**：

1. 使用适用于 AI 的 DSPM，为生成式 AI 站点创建 DLP 策略
1. 创建内部风险策略来检测有风险的 AI 交互
1. 阻止 Copilot 访问标记的内容
1. 运行数据评估以检测未标记的内容

## 任务 1 - 使用适用于 AI 的 DSPM 为生成式 AI 站点创建 DLP 策略

若要降低通过 AI 助手丢失数据的风险，首先使用“强化数据安全建议”创建 DLP 策略。 此策略使用自适应保护来限制将敏感数据粘贴或上传到 AI 工具，例如 Edge、Chrome 和 Firefox 中的 ChatGPT 和 Copilot。

1. 使用 **SC-401-cl1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)。

1. 在 **Microsoft Edge** 中，导航到 **`https://purview.microsoft.com`**，并以 **Joni Sherman** 的身份 `JoniS@WWLxZZZZZZ.onmicrosoft.com`（其中 ZZZZZZ 是实验室托管提供程序提供的唯一租户 ID）登录。

1. 在 Microsoft Purview 中，通过选择“**解决方案**” > “**适用于 AI 的 DSPM**” > “**建议**”，以导航到适用于 AI 的 DSPM。

1. **选择“强化数据安全**”建议。

1. 在“**AI 数据安全**”浮出控件页中，查看摘要，然后选择“**创建策略**”。 这会创建一个面向生成式 AI 站点的预配置 DLP 策略。

1. 创建策略后，选择“**查看策略**”。

1. 在“**策略详细信息**”部分中，选择“**在解决方案中编辑策略**”，以在 Microsoft Purview 中打开“**数据丢失防护**”解决方案。

1. 在“**策略**”页上，找到并选择“**适用于 AI 的 DSPM - 阻止来自 AI 站点的敏感信息**”策略。

1. 在浮出控件中，选择“**查看模拟**”。

1. 在模拟仪表板上，选择“**编辑策略**”。

1. 选择“下一步”，直到显示“选择应用策略的位置”页********。 确认策略的范围限定为“**设备**”。

1. 选择**下一步**。

1. 在“**自定义高级 DLP 规则**”页上，选择“**阻止以替代提升的风险用户**”旁边的铅笔图标，以查看规则。

1. 查看适用于 AI 的 DSPM 创建的规则的配置：
   - 在“**条件**”下，请注意包含的敏感信息类型，规则使用基于提升的风险的“**自适应保护**”。
   - 在“**操作**”下，对于“上传”和“粘贴”活动，选择**敏感服务域组限制**旁边的“**编辑**”。
   - 在服务域组配置中，确认“**生成式 AI 网站**”设置为“**阻止并替代**”。

1. 选择“**取消**”以退出规则编辑器，无需更改。

1. 返回到“自定义高级 DLP 规则”页，选择“下一步”********。

1. 在“**策略模式**”页上，选择 **“打开策略”（如果未在模拟后的 15 天内编辑策略）**，然后选择“**下一步**”。

1. 在“**查看并完成**”页上，选择“**提交**”，然后选择“**完成**”。

你创建了一个策略，该策略阻止高风险用户共享生成式 AI 网站上的敏感数据，并确认了由适用于 AI 的 DSPM 设置的策略配置。

## 任务 2 - 创建内部风险策略来检测有风险的 AI 交互

接下来，你将创建一个策略，帮助检测 Copilot 中存在风险的提示行为。

1. 在 Microsoft Purview 中，通过选择“**解决方案**” > “**适用于 AI 的 DSPM**” > “**建议**”，以导航到“**适用于 AI 的 DSPM**”。

1. 选择“**AI 应用中的检测风险交互（预览版）**”建议。

1. 在“**检测 AI 应用中的风险交互（预览版）**”浮出控件页中，查看摘要，然后选择“**创建策略**”。

1. 创建策略后，选择“**查看策略**”。

1. 在“**策略详细信息**”部分中，选择“**在解决方案中编辑策略**”，以打开 Microsoft Purview 的“**内部风险管理**”区域。

1. 在“**策略**”页上，找到并选择“**适用于 AI 的 DSPM - 检测有风险的 AI 使用情况**”策略。

1. 在浮出控件中，选择“**编辑策略**”，以查看完整的策略配置。

1. 在“**选择策略模板**”页上，观察策略使用“**有风险的 AI 使用情况（预览版）**”模板。

1. 选择“**下一步**”，直到到达**此策略页的“选择触发事件”**。
确认触发事件是“**从 Microsoft Entra ID 中删除的用户帐户**”，该 ID 表示潜在的卸载相关风险，这些风险可能先于或遵循有风险的 AI 活动。

1. 选择**下一步**。

1. 在“**指示器**”页上，展开指示器类别以查看选择哪些信号：

   - 浏览到生成式 AI 网站
   - 收到来自 Copilot 的敏感响应
   - 在 Copilot 中输入有风险的提示

1. 选择“**下一步**”，直到到达“**审阅和完成**”页面，然后选择“**取消**”以退出编辑器，而无需进行更改。

你已创建一个策略来检测有风险的 AI 交互，包括提示和响应，以帮助识别风险用户行为的早期迹象。

## 任务 3 - 阻止 Copilot 访问标记的内容

通过防止 Copilot 处理或响应受敏感度标签保护的内容，可以进一步降低风险。

1. 在 Microsoft Purview 中，通过选择“**解决方案**” > “**适用于 AI 的 DSPM**” > “**建议**”，以导航到“**适用于 AI 的 DSPM**”。

1. 选择“**保护智能 Microsoft 365 Copilot 副驾驶® 和代理引用的敏感数据（预览版）**”建议。

1. 查看此建议中提供的指南。

1. 导航到“**解决方案**” > “**数据丢失防护**” > “**策略**”。

1. 选择“**+ 创建策略**”，然后选择“**自定义策略**”。

1. 在“**为 DLP 策略命名**”页上输入：

   - **名称**：`DLP - Block Copilot access to labeled content`
   - **说明**：`Prevents Microsoft 365 Copilot from processing or responding with content labeled using sensitivity labels.`

1. 选择“下一步”，直到显示“选择应用策略的位置”页********。

1. 选择“**Microsoft 365 Copilot（预览版）**”作为策略范围，然后选择“**下一步**”，直到到达“**自定义高级 DLP 规则**”页。

1. 选择“**创建规则**”并配置：

   - **名称**：`Prevent Copilot from accessing labeled data`
   - 在“**条件**”下，选择“**添加条件**” > “**内容包含**” > “**敏感度标签**”。 添加这些敏感度标签：
     - `Trusted People`
     - `Project - Falcon`
     - `Financial Data`
   - 选择“添加”****
   - 在“**操作**”下，选择“**添加操作**” > “**阻止 Copilot 处理内容”（预览版）**”
   - 在“**创建规则**”浮出控件的底部，选择“**保存**”。

1. 返回到“自定义高级 DLP 规则”页，选择“下一步”********。

1. 在“**策略模式**”页上，选择“**立即打开策略**”，然后选择“**下一步**”。

1. 在“**查看并完成**”页上，选择“**提交**”，然后在“**已创建新策略**”页上选择“**完成**”。

1. 通过选择“**解决方案**” > “**适用于 AI 的 DSPM**” > “**建议**”，返回到“**适用于 AI 的 DSPM 建议**”。

1. 选择“**保护智能 Microsoft 365 Copilot 副驾驶® 和代理中引用的敏感数据（预览版）**”建议，然后选择“**标记为已完成**”。

你创建了一个 DLP 策略，该策略阻止在 Copilot 提示和响应中使用标记的内容。

## 任务 4 – 运行数据风险评估以检测未标记的内容

为了了解标签覆盖率的潜在差距，你将运行数据风险评估来识别没有 Copilot 可能访问的敏感度标签的文件。

1. 在“**适用于 AI 的 DSPM**”中，选择标题为“**保护 Copilot 响应和代理响应中引用的敏感数据**”的建议。

1. 在“**保护 Copilot 响应和代理响应中引用的敏感数据**”窗格中，查看摘要，然后选择“**转到评估**”。

1. 在“**数据风险评估**”页上，选择“**创建自定义评估**”

1. 在“**基本信息**”页上输入：

   - **名称**：`Unlabeled File Exposure Assessment`
   - **说明**：`Identifies files without sensitivity labels that may be exposed in Microsoft 365 Copilot responses and provides recommendations to reduce oversharing risks.`

1. 选择**下一步**。

1. 在“**添加用户**”页上，选择“**全部**”，然后选择“**下一步**”。

1. 在 **“添加数据源以评估**”页上，保留所选 **SharePoint** 的默认位置，然后选择“**下一步**”。

1. 在“**查看并运行数据评估扫描**”页上，选择“**保存并运行**”。

1. 在“**数据评估已成功创建**”页上，选择“**完成**”。

现在，你已使用适用于 AI 的 Microsoft Purview DSPM 来检测与 AI 相关的风险、强制实施策略并评估敏感数据风险，从而帮助组织安全地使用 AI。
