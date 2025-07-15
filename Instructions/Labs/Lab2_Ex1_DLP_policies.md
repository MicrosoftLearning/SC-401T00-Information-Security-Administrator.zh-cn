---
lab:
  title: 练习 1 - 实现和管理 DLP 策略
  module: Module 2 - Implement Data Loss Prevention
---
## WWL 租户 - 使用条款

如果在讲师引导式培训过程中向你提供租户，请注意，提供租户旨在支持讲师引导式培训中的动手实验室。

租户不应共享或用于动手实验室以外的用途。 本课程使用的租户为试用租户，课程结束后无法使用或访问，不符合扩展条件。

租户不得转换为付费订阅。 在本课程中获得的租户仍然是 Microsoft Corporation 的财产，我们保留随时获取访问权限和收回的权利。

# 实验室 2 - 练习 1 - 实现和管理 DLP 策略

Contoso Ltd. 新雇用的信息安全管理员 Joni Sherman 被要求配置数据丢失防护 (DLP) 策略，以帮助保护Microsoft 365 中的敏感客户数据。 在此实验室中，你将使用 Microsoft Purview 和 Microsoft Defender 来创建和管理 DLP 策略，以检测和限制敏感信息（如信用卡号和员工 ID）的共享。

**任务**：

1. 在模拟模式下创建 DLP 策略
1. 修改 DLP 策略
1. 在 PowerShell 中创建 DLP 策略
1. 在模拟模式下激活策略
1. 修改策略优先级
1. 在 Microsoft 365 Defender 中启用文件检查
1. 为 Microsoft 365 Defender 创建文件策略

## 任务 1 - 在模拟模式下创建 DLP 策略

在此任务中，你将在模拟模式下创建 DLP 策略，以 Teams 消息中的信用卡号为目标。 策略将在用户尝试共享敏感内容时通知用户，并允许他们以理由替代。

1. 使用 **SC-401-CL1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)。

1. 在 Microsoft Edge 中，导航到 `https://purview.microsoft.com` ，并以 Joni Sherman 的身份登录到 Microsoft Purview 门户  。 以 `JoniS@WWLxZZZZZZ.onmicrosoft.com` 身份登录（其中 ZZZZZZ 是实验室托管提供程序提供的唯一租户 ID）。 Joni 的密码是在上一练习中设置的。

1. 选择“**解决方案**” > “**数据丢失防护**” > “**策略**”。

1. 在“**策略**”页中，选择“**+创建策略**”以启动用于创建新数据丢失防护策略的配置。

1. 在“**从模板开始或创建自定义策略**”页上，选择“**自定义**”作为类别，然后选择“**法规**”下的“**自定义策略**”。

1. 选择**下一步**。

1. 在“为 DLP 策略命名”页面上输入****：

   - **名称**：`DLP - Credit Card Protection`
   - **说明**：`Detect and restrict sharing of credit card numbers in Teams messages.`

1. 选择**下一步**。

1. 在“分配管理单元”**** 页上，选择“下一步”****。

1. 在“**选择应用策略的位置**”页上，仅启用“**Teams 聊天和频道消息**”位置。 如果已选择任何其他位置，请取消选择。

1. 选择**下一步**。

1. 在“定义策略设置”页上，选择“创建或自定义高级 DLP 规则”，然后选择“下一步”************。

1. 在“自定义高级 DLP 规则”页面上选择“+ 创建规则” 。

1. 在“**创建规则**”浮出控件中：
    - 在“名称”字段中，输入 `Credit card information`。

1. 在“**条件**”下，选择“**+ 添加条件**” > “**从 Microsoft 365 共享内容**”。

1. 在“**从 Microsoft 365 共享内容**”部分中：
    - 为**组织外部的人员**选择该选项。

1. 选择“**+ 添加条件**” > “**内容包含**”。

1. 在新的“**内容包含**”部分中：
    - 选择“**添加**” > “**敏感信息类型**”。
    - 在“**敏感信息类型**”页上，搜索并选择 `Credit Card Number`，然后选择“**添加**”。

1. 在“**操作**”下，选择“**+ 添加操作**” > “**限制访问或加密 Microsoft 365 位置中的内容**”。

1. 在“**限制访问或加密内容**”部分中：
    - 选择“**仅阻止组织外部的人员**”。

1. 在“**用户通知**”下：
    - 打开切换“**使用通知来通知用户，并帮助引导他们正确使用敏感信息**”。
    - 选中“**使用策略提示在 Office 365 服务中通知用户**”复选框。

1. 在“**用户替代**”下：
    - 选中复选框“**允许用户替代策略限制**”(Fabric, Exchange, SharePoint, OneDrive, and Teams)。
    - 选中“**需要业务理由才可替代**”复选框。

1. 在“**事件报告**”中的“**在管理员警报和报告中使用此严重性级别**”下拉菜单中：
    - 选择“**低**”。

1. 在“**创建规则**”浮出面板的底部，选择“**保存**”。

1. 返回到“**自定义高级 DLP 规则**”页，选择“**下一步**”。

1. 在“**策略模式**”页上，选择“**在模拟模式下运行策略**”，并选择“**在处于模拟模式时显示策略提示**”复选框。

1. 选择**下一步**。

1. 在“**查看并完成**”页上查看设置，然后选择“**提交**”。

1. 在“新策略已创建”页上，选择“完成” 。

你已创建 DLP 策略，用于扫描 Teams 内容的信用卡号并允许使用业务理由进行替代。

## 任务 2 - 修改 DLP 策略

在此任务中，你将扩展现有 DLP 策略的范围以包含 Exchange 电子邮件。 这有助于确保跨其他通信通道的一致保护。

1. 你仍应使用 **SC-401-CL1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)，并且应以 **Joni Sherman** 的身份登录到 Microsoft 365。

1. 你应仍位于 Microsoft Purview 的“**策略**”页上。 如果没有，请打开 **Microsoft Edge** 并导航到 `https://purview.microsoft.com`。 选择“**解决方案**” > “**数据丢失防护**” > “**策略**”。

1. 在“**策略**”页上，选中最近创建的“**DLP - 信用卡保护**”的复选框，然后选择“**编辑策略**”以打开策略配置。

1. 在“**命名 DLP 策略**”页上，将说明编辑为 `Detect and restrict sharing of credit card numbers in Teams and Exchange messages.`

1. 选择**下一步**。

1. 在“分配管理单元”**** 页上，选择“下一步”****。

1. 在“**选择要应用策略的位置**”页上，选中“**Exchange 电子邮件**”复选框，将此位置添加到 DLP 策略。

1. 选择“**下一步**”，直到到达“**查看并完成**”页面。

1. 选择“**查看并完成**”页上的“**提交**”以应用对策略做出的修改。

1. 更新策略后，选择“**策略已更新**”页上的“**完成**”。

已成功更新策略，以扫描电子邮件以及 Teams 消息。

## 任务 3 - 在 PowerShell 中创建 DLP 策略

在此任务中，你将使用 PowerShell 创建 DLP 策略，以阻止通过电子邮件共享员工 ID。 此方法演示如何通过脚本定义和强制实施策略设置。

1. 你仍然应该会使用 **SC-401-CL1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)。

1. 右键单击任务栏中的“**开始**”按钮，然后选择“**终端 (管理员)**”，打开提升的 PowerShell 窗口。

1. 运行 **Connect-IPPSSession** cmdlet 以连接到安全性和合规性 PowerShell：

    ```powershell
    Connect-IPPSSession
    ```

1. 在“**登录到帐户**”弹出窗口中，以 **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com`（其中 ZZZZZZ 是实验室托管提供程序提供的唯一租户 ID）的身份登录。 Joni 的密码是在上一练习中设置的。

1. 运行 **New-DlpCompliancePolicy** cmdlet 以创建扫描所有 Exchange 邮箱的 DLP 策略：

    ```powershell
    New-DlpCompliancePolicy -Name "EmployeeID DLP Policy" -Comment "This policy blocks sharing of Employee IDs" -ExchangeLocation All
    ```

1. 运行 **New-DlpComplianceRule** cmdlet，将 DLP 规则添加到在上一步中创建的 DLP 策略。 此策略使用在上一练习中创建的“**Contoso 员工 ID**”敏感信息类型：

    ```powershell
    New-DlpComplianceRule -Name "EmployeeID DLP rule" -Policy "EmployeeID DLP Policy" -BlockAccess $true -ContentContainsSensitiveInformation @{Name="Contoso Employee IDs"}
    ```

1. 运行 **Get-DLPComplianceRule** cmdlet 以查看 **EmployeeID DLP 规则**：

    ```powershell
    Get-DLPComplianceRule -Identity "EmployeeID DLP rule"
    ```

已成功使用 PowerShell 创建阻止员工 ID 共享的 DLP 策略。

## 任务 4 – 在模拟模式下激活策略

在模拟中测试 DLP 策略后，将激活该策略以开始强制执行其操作。

1. 你仍应使用 **SC-401-CL1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)，并且应以 **Joni Sherman** 的身份登录到 Microsoft 365。

1. 在 **Microsoft Edge** 中导航到 DLP 策略，方法是前往“`https://purview.microsoft.com`” > “**解决方案**” > “**数据丢失防护**”，然后从左侧边栏中选择“**策略**”。

1. 在“**策略**”页上，选择“**DLP - 信用卡保护**”策略。

1. 在右侧浮出控件的底部，选择“**查看模拟**”。

1. 在模拟页上，花点时间探索：

   - “**模拟概述**”选项卡，其中按位置显示扫描进度、总匹配项和扫描状态。
   - **审阅选项卡项**，其中任何预测匹配项将在可用后显示。
   - **警报选项卡**，其中将列出模拟模式下触发的任何警报。

1. 在模拟模式下浏览见解后，选择“**打开策略**”，然后选择“**确认**”以激活 DLP 策略。

   将显示一个确认浮出控件，指示策略已成功发布。

该策略现在处于活动状态，并强制限制 Teams 和 Exchange 中的信用卡信息。

## 任务 5 - 修改策略优先级

当存在多个策略时，其优先级确定哪一个策略首先适用。 在此任务中，你将员工 ID 策略移动到最高优先级。

1. 你仍应使用 **SC-401-CL1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)，并且应以 **Joni Sherman** 的身份登录到 Microsoft 365。

1. 在 **Microsoft Edge** 中，Microsoft Purview 门户选项卡的“**策略**”页应该仍处于打开状态。 如果没有，请打开 **Microsoft Edge** 并导航到 `https://purview.microsoft.com`。 选择“**解决方案**” > “**数据丢失防护**” > “**策略**”。

1. 在“**策略**”页上，选择“**EmployeeID DLP 策略**”。

1. 从顶部导航功能区中选择“**调整优先级**”，然后选择“**移动到顶部(最高优先级)**”。

1. 在“数据丢失防护”窗口中，选择“刷新”，然后查看策略表的“顺序”列中的优先级  。

1. 选择右上角 Joni 的图标以退出登录她的帐户，然后选择“**退出登录**”。

你已更新策略优先级，以使员工 ID 策略优先于其他人。

## 任务 6 - 在 Microsoft 365 Defender 中启用文件检查

某些文件策略需要访问以检查受保护文件的内容。 在此任务中，你将授予必要的权限，以允许 Microsoft Defender 扫描 OneDrive 和 SharePoint 文件的内容以获取敏感信息。

1. 你仍应使用 **SC-401-CL1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)，并以 Joni Sherman 的身份登录。

1. 在 **Microsoft Edge** 中，转到 `https://security.microsoft.com` 以导航到 Microsoft Defender。 以 **MOD 管理员** `admin@WWLxZZZZZZ.onmicrosoft.com`（其中 ZZZZZZ 是实验室托管提供程序提供的唯一租户 ID）的身份登录。 管理员的密码应由实验室托管提供程序提供。

1. 在左侧边栏中，展开“**系统**” > “**设置**”，然后选择“**云应用**”。

1. 在“**云应用**”窗口的左窗格中，向下滚动到“**信息保护**”部分。 在“**检查受保护的文件**”下，选择“**授予权限**”以启用文件检查。

1. 按照提示在 Microsoft Entra ID 中允许所需的权限，随后应会在 Microsoft Defender for Cloud Apps 中看到文件检查处于“**活动状态**”。

1. 选择右上角的“**MA**”图标以退出登录 MOD 管理员帐户，选择“**退出登录**”，然后关闭浏览器窗口。

现在，Defender 中启用了文件检查，允许文件策略扫描敏感内容。

## 任务 7 - 为 Microsoft 365 Defender 创建文件策略

在此任务中，你将在 Microsoft Defender 中创建文件策略，用于标识和隔离包含 OneDrive 和 SharePoint 中的信用卡号的文件。

1. 你仍然应该会使用 **SC-401-CL1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)。

1. 打开 **Microsoft Edge**，导航到 **`https://security.microsoft.com`** 并以 **Joni Sherman** 的身份 `JoniS@WWLxZZZZZZ.onmicrosoft.com`（其中 ZZZZZZ 是实验室托管提供程序提供的唯一租户 ID）登录到 Microsoft Defender 门户。 Joni 的密码是在上一练习中设置的。

1. 在 **Microsoft Defender** 门户的左侧导航中，选择“**云应用**” > “**策略**”，然后选择**策略管理**”。

1. 在“**策略**”页面上，展开“**+ 创建策略**”，然后选择“**文件策略**”。

1. 在“**创建文件策略**”页上，配置：

   - **策略名称**：`Credit card information for files`
   - **策略严重性**：**低**
   - **类别**：**DLP**
   - **说明**：`Protect credit card numbers from being shared in files.`
   - 在“**符合以下所有部分的文件**”中：
      - 对于第一个筛选器，请将下拉列表配置为：“**访问级别等于公共（Internet）、外部、公共**”并添加“**内部**”
      - 对于第二个筛选器，请将下拉列表配置为：“**上次修改后（日期）**”并使用今天的日期

          ![显示文件匹配下拉列表的屏幕截图，其中添加了内部选项。](../Media/files-matching-internal.png)

   - 在“检查方法”下拉菜单中，选择“数据分类服务”********。
   - 在“选择检查类型…”下拉菜单中，选择“敏感信息类型…” 。
   - 在“**选择敏感信息类型**”对话框中，搜索并选中 `Credit Card Number` 复选框。
      - 在“**选择敏感信息类型**”对话框右上角，选择“**完成**”。

   - 在**治理操作**下，展开 **Microsoft OneDrive for Business**：
      - 选中“**放入用户隔离**”复选框
   - 对 **Microsoft Office SharePoint Online** 重复相同的流程
      - 选中“**放入用户隔离**”复选框

1. 选择页面底部的“**创建**”，以创建文件策略。

你已成功创建一个文件策略，用于检测和隔离包含敏感信用卡数据的文件。
