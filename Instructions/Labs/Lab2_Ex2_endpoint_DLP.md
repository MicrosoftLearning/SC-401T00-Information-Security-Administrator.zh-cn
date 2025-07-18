---
lab:
  title: 练习 2 - 实现和管理终结点 DLP
  module: Module 2 - Implement Data Loss Prevention
---

# 实验室 2 - 练习 2 - 实现和管理终结点 DLP

Contoso Ltd. 新聘请的信息安全管理员 Joni Sherman 被要求加强对公司设备上的 DLP 控制。 一些员工一直在将敏感的客户信息复制到 USB 驱动器，增加了数据泄露的风险。 在此实验室中，Joni 将配置终结点 DLP 策略来阻止这些传输。

**任务**：

1. 为终结点 DLP 载入设备
1. 创建终结点 DLP 策略
1. 配置终结点 DLP 设置
1. 配置 Microsoft Purview 扩展

## 任务 1 - 为终结点 DLP 加入设备

在本任务中，你将加入 Windows 11 设备，使其得到终结点 DLP 策略的保护。

1. 使用 **SC-401-cl2\admin** 帐户登录到**客户端 2 VM (SC-401-CL2)**。

1. 打开 Microsoft Edge，导航到 **`https://purview.microsoft.com`**，以 **Joni Sherman** 的身份登录到 Microsoft Purview 门户。 以 `JoniS@WWLxZZZZZZ.onmicrosoft.com` 身份登录（其中 ZZZZZZ 是实验室托管提供程序提供的唯一租户 ID）。 Joni 的密码是在上一练习中设置的。

1. 从左侧边栏中选择“**设置**”。

1. 在左侧边栏上，展开“**设备加入**”，然后选择“**加入**”。

1. 在“**加入**”页上，在“**部署方法**”下拉菜单中，选择“**本地脚本(最多可用于 10 台计算机)**”，然后选择“**下载包**”。

1. 在“**下载**”对话框中，将鼠标悬停在下载上方，然后选择文件夹图标以“**在文件夹中显示**”。

1. 将 Zip 文件解压缩至 SC-401-CL1 的“**桌面**”。 应该会看到名为 DeviceComplianceLocalOnboardingScript.cmd 的脚本。

1. 在桌面上，右键单击刚刚解压的 **DeviceComplianceLocalOnboardingScript.cmd** 文件，然后选择“**显示更多选项**”，再选择“**属性**”。

1. 在属性窗口的“**常规**”选项卡底部，选择“**安全**”部分中的“**取消阻止**”，然后选择“**确定**”以保存此设置。

1. 返回桌面，右键单击 **DeviceComplianceLocalOnboardingScript.cmd** 文件，然后选择“**以管理员身份运行**”。 在“**用户帐户控制**”对话框中，选择“**是**”。

1. 在“命令提示符”屏幕中键入 Y 以进行确认，然后按 Enter 键 。

1. 脚本完成后，将收到成功消息和“**按任意键继续**”提示。 按任意键关闭命令窗口。 完成此加入可能需要一分钟时间。

1. 打开“开始”菜单并搜索 `Access work or school`。 在“**最佳匹配**”下选择“**访问工作或学校**”。

1. 在“**添加工作或学校帐户**”的“**访问工作或学校**”窗口中，选择“**连接**”。

1. 在“**设置工作或学校帐户**”对话框中，选择“**让此设备加入 Microsoft Entra ID**”链接，并以 **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com`（其中 ZZZZZZ 是实验室托管服务提供商提供的唯一租户 ID）的身份登录。 Joni 的密码是在上一练习中设置的。

1. 在“请确认这是你的组织”对话框中查看租户 URL 并选择“加入”。********  

1. 设备连接后，在“**你已完成所有设置!**”屏幕上选择“**完成**” 。

1. 重启客户端 2 VM (SC-401-CL2)。

1. 重新登录到客户端 1 VM (SC-401-CL1)。

1. Microsoft Purview 窗口应仍在显示“**设备**”页。 刷新此页面并验证设备是否已成功加入。

已成功加入设备并将其加入到 Microsoft Entra ID。 它现在可以受终结点 DLP 策略的保护。

## 任务 2 - 创建终结点 DLP 策略

在此任务中，你将创建一个 DLP 策略，该策略阻止将敏感信息传输到 USB 驱动器。 这有助于在不授权的情况下降低数据被带离现场的风险。

1. 使用 SC-401-CL1\admin 帐户登录到客户端 1 VM (SC-401-CL1)。

1. 你应仍位于 Microsoft Purview 门户中的“**设备**”页，并以 Joni Sherman 的身份登录。

1. 在 Microsoft Purview 门户中，选择“**解决方案**” > “**数据丢失防护**”。

1. 在左侧导航面板中，选择“**策略**”，然后选择“**+ 创建管理**”。

1. 在“从模板开始或创建自定义策略”页面上，依次选择“自定义”、“自定义策略”和“下一步”****************。

1. 在“**为 DLP 策略命名**”页上输入：

    - **名称**：`Block USB transfers`
    - **说明**：`Prevent transferring sensitive data to USB devices.`

1. 在“分配管理单元”**** 页面上，选择“下一步”****。

1. 在“**选择应用策略的位置**”页上，确保仅选择“**设备**”这一位置。 如果已选择任何其他位置，请确保将其取消选中，然后选择“**下一步**”。

1. 在“定义策略设置”页面上，选择“创建或自定义高级 DLP 规则”，然后选择“下一步”************。

1. 在“自定义高级 DLP 规则”页面上选择“+ 创建规则” 。

1. 在“创建规则”**** 页面上，输入：

    - **名称**：`USB transfer rule`
    - **说明**：`Block USB transfers of sensitive data.`

1. 在“**条件**”下选择“**+ 添加条件**”，然后选择“**内容包含**”。

1. 在新的“**内容包含**”部分中：
    - 选择“**添加**” > “**敏感信息类型**”。
    - 在“**敏感信息类型**”页上，搜索这些敏感信息类型：
       - `Credit Card Number`
       - `U.S. Social Security Number (SSN)`
       - `U.S. Driver's License Number`
       - `Contoso Employee IDs`

1. 在“**操作**”下，选择“**+ 添加操作**” > “**审核或限制设备上的活动**”。

1. 在新的“**审核或限制设备上的活动**”部分中：
    - 在“**所有应用的文件活动**”部分中，确保已选择“**复制到可移动的 USB 设备**”。
    - 选择“**复制到可移动 USB 设备**”左侧的下拉列表，将操作从“**仅审核**”更改为“**阻止**”。

1. 在“**用户通知**”下：
    - **打开**切换“**使用通知来通知用户，并帮助引导他们正确使用敏感信息**”。
    - 选中“**当限制活动时向用户显示策略提示通知**”复选框。

1. 在“**创建规则**”浮出控件的底部，选择“**保存**”。

1. 返回到“**自定义高级 DLP 规则**”页，选择“**下一步**”。

1. 在“**策略模式**”页上，选择“**在模拟模式下运行策略**”。
   - 选中复选框，以“**在模拟模式下显示策略提示**”。
   - 此外，请选中复选框“**如果在模拟后的 15 天内未编辑策略，请打开**”。

1. 选择**下一步**。

1. 在“查看并完成”页面上，查看策略设置，然后选择“提交”******** 以创建策略。

1. 创建策略后，请在“**已创建新策略**”页上选择“**完成**”。

你已成功在模拟模式下创建 DLP 策略，阻止 USB 传输敏感数据。 如果未编辑策略，则会在 15 天后自动打开该策略。

## 任务 3 – 配置终结点 DLP 设置

在此任务中，你将通过排除本地文件夹、设置浏览器限制和阻止云域来微调终结点 DLP 设置。

1. 你仍应使用 **SC-401-cl1\admin** 帐户登录到客户端 1 VM (SC-401-CL1)，并且应以 **Joni Sherman** 的身份登录到 Microsoft 365。

1. 在 Microsoft Purview 中，从左侧导航窗格中，选择“**设置**” > “**数据丢失防护**”。

1. “**数据丢失防护设置”** 页应在显示“**终结点 DLP 设置**”。

1. 在“终结点 DLP 设置”页面上，展开“Windows 的文件路径排除”，并选择“+ 添加文件路径排除”************。

1. 在“**从 Windows 设备中排除这些文件路径**”浮出控件页上的“**文件路径排除**”字段中，输入 `C:\FilePathExclusionTest`，然后选择右侧的“**+**”按钮。 选择“保存”以保存此输入****。

1. 返回到“终结点 DLP 设置”页面，展开“敏感数据的浏览器和域限制”，并选择“+ 添加或编辑不允许的浏览器”。************

1. 在“**添加不允许的浏览器**”浮出控件页中，选中“**Google Chrome**”对应的复选框，然后选择“**保存**”。

1. 返回到“**终结点 DLP 设置**”页，选择“**服务域**”下拉列表，并将其从“**关闭**”更改为“**阻止**”。

1. 在“更新云应用模式”对话框中，选择“是”以激活阻止模式********。

1. 在“服务域”下，选择“+ 添加云服务域”。********

1. 在“**添加云服务域**”浮出控件页上的“**域**”字段中输入 `dropbox.com`，然后选择“**+**”（加号）图标，以添加路径。 选择“保存”以保存此设置。

你已应用自定义终结点 DLP 设置来优化策略的行为，包括排除、浏览器限制和阻止对特定域的访问。

## 任务 4 - 配置 Microsoft Purview 扩展

在此任务中，你将在 Google Chrome 中安装 Microsoft Purview 扩展，以在受支持的浏览器中测试终结点 DLP 策略行为。

1. 从任务栏中打开 Edge 浏览器。

1. 通过 `https://chrome.google.com` 导航到 Google Chrome 下载。

1. 选择“**下载 Chrome**”，然后选择“**下载**”通知中的“**打开文件**”，以打开“**ChromeSetup.exe**”。

1. 在“用户帐户控制”对话框中选择“是”以安装 Chrome 浏览器 。

1. 安装完成后，在“**登录 Chrome**”屏幕上，选择“**不，谢谢**”或“**不登录**”。

1. 在“**设置默认浏览器**”页上选择“**跳过**”。

1. 当新安装的 Chrome 浏览器窗口打开时，导航到 **Chrome Web Store** 中的 **Microsoft Purview 扩展**，网址为：

   `https://chrome.google.com/webstore/detail/microsoft-purview-extensi/echcggldkblhodogklpincgchnpgcdco`

1. 确认你位于正确的扩展页上，然后选择“**添加到 Chrome**”。

1. 在“**添加“Microsoft Purview 扩展”上?** 窗口中，选择“**添加扩展**”。

1. 关闭关于正在添加到 Chrome 的扩展的通知，然后导航到 **`chrome://extensions`**。

1. 验证“Microsoft Purview 扩展”是否可见并是否已激活。

1. 关闭 Chrome 浏览器窗口。

你已成功安装了 Chrome 并添加了 Microsoft Purview 扩展。 设备现在支持在 Edge 和 Chrome 中强制实施 DLP 策略。
