---
lab:
  title: 练习 1 - 配置保留策略
  module: Module 5 - Implement and manage retention
---

## WWL 租户 - 使用条款

如果在讲师引导式培训过程中向你提供租户，请注意，提供租户旨在支持讲师引导式培训中的动手实验室。

租户不应共享或用于动手实验室以外的用途。 本课程使用的租户为试用租户，课程结束后无法使用或访问，不符合扩展条件。

租户不得转换为付费订阅。 在本课程中获得的租户仍然是 Microsoft Corporation 的财产，我们保留随时获取访问权限和收回的权利。

# 实验室 5 - 练习 1 - 实现和管理保留

你是 Contoso Ltd 的合规性管理员 Joni Sherman。该公司正在收紧其数据安全策略，以减少与财务数据和特权通信相关的风险暴露。 你被要求配置 Microsoft Purview 保留解决方案，这些解决方案支持审核就绪情况、限制不必要的数据保留，并确保对敏感通信进行适当的监督。

**任务**：

1. 创建保留标签
1. 发布保留标签
1. 创建自动应用保留标签策略
1. 创建静态的保留策略
1. 创建自适应范围
1. 创建自适应保留策略
1. 恢复 SharePoint 内容

## 任务 1 - 创建保留标签

在此任务中，你将为需要保留的敏感财务数据创建保留标签，以便进行审核和调查。

1. 使用 **SC-401-cl1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)。

1. 在 Microsoft Edge 中，导航到 `https://purview.microsoft.com` 并以 **Joni Sherman** 的身份 `JoniS@WWLxZZZZZZ.onmicrosoft.com` （其中 ZZZZZZ 是实验室托管提供程序提供的唯一租户 ID）登录到 Microsoft Purview 门户。 Joni 的密码是在上一练习中设置的。

1. 导航到“**解决方案**” > “**数据生命周期管理**” > “**保留标签**”。

1. 在“**标签**”页上，选择“**创建标签**”。

1. 在“**命名保留标签**”页上，输入：

   - **名称**：`Sensitive Financial Records`
   - **** 面向用户的说明：`Use for financial files with sensitive data that must be retained for audit or security purposes.`
   - **** 面向管理员的说明：`Retains high-impact financial data for 5 years to support audits and security investigations.`

1. 选择**下一步**。

1. 在“定义标签设置”页面上，选择“将项永远保留或保留特定时间段”，然后选择“下一步”  。

1. 在“**定义时间段**”页上，确保为保留期配置输入设置这些值：

    - **保留期有多长？**：5 年
    - **此时间段应从何时开始?**：修改项时

1. 选择**下一步**。

1. 在“**选择保留期后会发生什么情况**”页上，选择“**自动删除项**”，然后选择“**下一步**”。

1. 在“查看并完成”页上，选择“创建标签” 。

1. 在“**已创建保留标签**”页上，选择“**不执行任何操作**”选项，然后选择“**完成**”。

你创建了一个保留标签，该标签将财务内容保留五年，并随后将其删除，以减少数据泄露。

## 任务 2 - 发布保留标签

在此任务中，你将发布保留标签，以便用户可以将其应用于 Exchange、SharePoint 和 OneDrive 等 Microsoft 365 服务。

1. 在 Microsoft Purview 中，导航到“**解决方案**” > “**数据生命周期管理**” > “**保留标签**”。

1. 选中“**敏感财务记录**”标签旁边的复选框，然后选择“**发布标签**”图标（![发布标签图标](../Media/publish-labels-icon.png)）以发布此保留标签。

1. 在“**选择要发布的标签**”页上，验证是否已选择“**敏感财务记录**”标签，然后选择“**下一步**”。

1. 在“策略范围”页上选择“下一步”********。

1. 在“选择要创建的保留策略的类型”页上选择“静态”，然后选择“下一步”  。

1. 在“**选择标签发布位置**”页上选择“**让我选择特定位置**”，然后选择：

    - Exchange 邮箱
    - SharePoint 经典和通信站点
    - OneDrive 帐户
    - 取消选择所有其他位置

1. 选择**下一步**。

1. 在“**为策略命名**”页上输入：

    - **名称**：`Sensitive Financial Data Retention`
    - **说明**：`Makes the 'Sensitive Financial Records' label available to users in Exchange, SharePoint, and OneDrive.`

1. 选择**下一步**。

1. 在“**完成**”页上选择“**提交**”。  

1. 在“**已发布保留标签**”页上，选择“**完成**”。

已发布保留标签，使用户可以在关键 Microsoft 365 服务中应用。

## 任务 3 - 创建自动应用保留标签策略。

在此任务中，你将配置自动将保留标签应用于包含个人财务信息的内容的策略。

1. 在 Microsoft Purview 中，导航到“**解决方案**” > “**数据生命周期管理**” > “**策略**” > “**标签策略**”。

1. 在“**标签策略**”页上，选择“**自动应用标签**”以启动标签配置。

1. 在“**开始**”页上，输入：

   - **名称**：`Auto-apply Personal Financial PII`
   - **说明**：`Applies this label to personal financial data to help meet audit and investigation requirements. Retains content for 3 years.`

1. 选择**下一步**。

1. 在“**选择要将此标签应用到的内容类型**”页上，选择“**将标签应用到包含敏感信息的内容**”，然后选择“**下一步**”。

1. 在“**包含敏感信息的内容**”页上，选择“**财务**”类别，然后选择**美国《格雷姆-里奇-比利雷法案》 (GLBA)** 法规，然后选择“**下一步**”。

1. 在“**定义包含敏感信息的内容**”页上，选择“**下一步**”。

1. 在“策略范围”页上，选择“下一步”。

1. 在“选择要创建的保留策略的类型”页面上，选择“静态” 。

1. 在“**选择标签发布位置**”页上选择“**让我选择特定位置**”，然后选择：

    - Exchange 邮箱
    - SharePoint 经典和通信站点
    - OneDrive 帐户
    - 取消选择所有其他位置

1. 在“**选择要自动应用的标签**”页上，选择“**添加标签**”。

1. 在“**选择标签**”浮出控件上，选择“**个人财务 PII**”，然后选择“**添加**”。

1. 返回“**选择要自动应用的标签**”页，选择“**下一步**”。

1. 在“**决定是测试还是运行策略**”上，选择“**在运行策略之前测试策略**”，然后选择“**下一步**”。

1. 在“**查看并完成**”页上，选择“**提交**”，然后在“**已创建自动标记策略**”页上选择“**完成**”。

你已创建一个自动应用策略，用于标识个人财务数据并自动应用保留标签。

## 任务 4 - 创建保留策略

在此任务中，你将为 Microsoft Teams 内容创建静态保留策略，以帮助降低长期数据风险。

1. 在 Microsoft Purview 中，导航到“**解决方案**” > “**数据生命周期管理**” > “**策略**” > “**保留策略**”。

1. 在“**保留策略**”页上，选择“**新建保留策略**”。

1. 在“**命名保留策略**”页上输入：

   - **名称**：`Teams Retention`
   - **说明**：`Retains Teams chats and channel messages for 3 years, then deletes them to reduce long-term data risk.`

1. 选择**下一步**。

1. 在“策略范围”页上，选择“下一步”。

1. 在“选择要创建的保留策略的类型”页上，选择“静态”，然后选择“下一步”  。

1. 在“**选择应用策略的位置**”页上，启用：

   - Teams 渠道消息
   - Teams 聊天
   - 将所有其他位置保留为禁用状态。

1. 选择**下一步**。

1. 在“**决定是否要保留内容、删除内容或二者均可**”页上，确保为保留配置设置以下值：

   - 选择“**将项保留特定时间段**”。
   - 在“**将项保留特定时间段**”下，从下拉列表中选择“**自定义**”
   - 将“年数”字段更改为 `3`
   - 保留期开始依据：上次修改项的时间
   - 保留期结束时：自动删除项

1. 选择**下一步**。

1. 在“**查看并完成**”页上，选择“**提交**”，然后在“**已成功创建保留策略**”页上选择“**完成**”。

你已配置静态保留策略，该策略会在自动删除 Teams 消息之前保留三年。

<!------ Commenting out until tenant bug issues are resolved
## Task 5 – Create an adaptive scope

In this task, you'll define an adaptive scope that targets Microsoft 365 groups associated with leadership and operations roles.

1. In Microsoft Purview, **Settings** > **Roles and scopes** > **Adaptive scopes**.

1. On the **Adaptive scopes** page select **+ Create scope**.

1. On the **Name your adaptive policy scope** page enter:

    - **Name**: `Leadership and Ops Groups`
    - **Description**: `Targets Leadership and Operations M365 groups with privileged access to sensitive data.`

1. Select **Next**.

1. On the **Assign admin unit** page select **Next**.

1. On the **What type of scope do you want to create?** page select **Users**, then select **Next**.

1. On the **Create the query to define users** page, in the **User attributes** section, ensure these values are selected for the user attribute configuration:

   - Select the **Attribute** dropdown then select **Department**
   - Leave the default **is equal to** value in the next field
   - Enter `Leadership` as the **Value**

1. Add a second attribute by selecting **+ Add attribute** on the **Create the query to define users** page. In the new field under the one we just configured, configure these values:

   - Select the dropdown for the query operator and update it from And to **Or**
   - Select the **Attribute** dropdown then select **Department**
   - Leave the default **is equal to** value in the next field
   - Enter `Operations` as the **Value**

1. Select **Next**.

1. On the **Review and finish** page select **Submit**.

1. Once your adaptive scope is created select **Done** on the **Your scope was created** page.

You've created an adaptive scope to support targeted retention for privileged groups in the organization.

## Task 6 – Create an adaptive retention policy

In this task, you'll use the adaptive scope you created to configure a retention policy for Microsoft 365 groups with sensitive responsibilities.

1. In Microsoft Purview, navigate to **Solutions** > **Data Lifecycle Management** > **Policies** >  **Retention policies**.

1. On the **Retention policies** page, select **+ New retention policy**.

1. On the **Name your retention policy** page enter:

    - **Name**: `Privileged Group Retention`
    - **Description**: `Retains content from Leadership and Operations groups for 5 years to support audit and investigation.`

1. Select **Next**.

1. On the **Policy Scope** page select **Next**.

1. On the **Choose the type of retention policy to create** page select **Adaptive** then select **Next**.

1. On the **Choose adaptive policy scopes and locations** page select **+ Add scopes**.

1. On the **Choose adaptive policy scopes** flyout panel select the checkbox for **Leadership and Ops Groups** then select **Add** at the bottom of the panel.

1. Back on the **Choose locations to apply the policy** enable:

    - Microsoft 365 Group mailboxes & sites
    - Leave all other locations disabled.

1. Select **Next**.

1. On the **Decide if you want to retain content, delete it, or both** page, ensure these values are set for the retention configuration:

   - Select **Retain items for a specific period**.
   - Under **Retain items for a specific period**, select **5 years** from the dropdown list
   - **Start the retention period based on**: When items were last modified
   - **At the end of the retention period**: Delete items automatically

1. Select **Next**.

1. On the **Review and finish** page select **Submit**.

1. Select **Done** once the policy is created.

You've created a retention policy that applies to content owned by privileged groups, retaining it for five years before deletion.
-->

## 任务 5 – 恢复 SharePoint 内容

在此任务中，你将模拟从 SharePoint 网站还原已删除的文档，以验证恢复选项。

1. 使用 **SC-401-cl1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)。

1. 在 Microsoft Edge 中，导航到 `https://www.office.com` 并以 Joni Sherman 的身份登录到 Microsoft 365  。

1. 在 Microsoft Office 365 登陆页面上，选择左上角的“应用启动器”（网格图标），然后从子菜单中选择 **SharePoint**。

   ![显示省略号位置的屏幕截图，以显示操作菜单。](../Media/show-more-actions-sharepoint.png)

1. 在 SharePoint 登陆页面上，搜索“`Benefits`”，然后从搜索结果中选择“**Benefits @ Contoso**”。

1. 在左侧边栏中，选择“**文档**”。

1. 在“**文档**”页上，选中“**Vacation Policies.pptx**”复选框，然后在操作栏中选择“**删除**”。

1. 在“**删除?**”对话框中，选择“**删除**”。

1. 在左侧边栏中选择“**回收站**”。

1. 在“**回收站**”页上，右键单击“**Vacation Policies.pptx**”，然后选择“**还原**”。

1. 在左侧边栏中，选择“**文档**”并注意文件已还原。

你已经成功从 SharePoint 网站恢复了已删除的文档。
