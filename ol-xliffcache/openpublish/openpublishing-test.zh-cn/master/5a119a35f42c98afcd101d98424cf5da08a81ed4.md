---
description: na
experiment: true
keywords: na
pagetitle: Install ATA
search: na
ms.custom: 
  - ATA
ms.date: na
ms.prod: identity-ata
ms.technology: 
  - security
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.author: 5f6e9ed0-302d-496f-873c-7a2b94e50410
---
# 安装 ATA
若要获取 ATA 部署、 配置，并且正在运行所需的步骤如下。

若要配置 ATA，请按照下列步骤 ︰

- [预安装步骤](#Preinstallsteps)

- [步骤 1。 下载并安装 ATA 中心](#InstallATACtr)

- [步骤 3。 配置 ATA 网关域的连接设置](#ConfigConSettings)

- [步骤 4。 下载 ATA 网关安装包](#DownloadATA)

- [第 5 步。 ATA 网关安装](#InstallATAGW)

- [步骤 6。 配置 ATA 网关设置](#ConfigATAGW)

- [步骤 7。 配置 VPN 子网和蜜标的用户](#ATAvpnHoneytokensetting)

## <a name="Preinstallsteps"></a>安装前步骤

1. 如果您安装 ATA 公共预览版本，请参阅 [ATA 发行说明](./small.md) 有关卸载 ATA 预览版本的帮助。

2. ATA 中心服务器上安装 KB2934520 并在开始安装前 ATA 网关服务器上，否则为 ATA 安装将安装此更新需要中间 ATA 安装重新启动。

## <a name="InstallATACtr"></a>步骤 1。 下载并安装 ATA 中心
验证服务器满足要求后，您可以继续进行 ATA 中心安装。

ATA 中心服务器上执行以下步骤。

1. 下载从 ATA [TechNet 评估中心](http://www.microsoft.com/en-us/evalcenter/)。

2. 登录的用户是本地管理员组的成员。

3. 从提升的命令提示符处，运行 Microsoft ATA 中心 Setup.EXE 并按照安装向导。

4. 在 **欢迎** 页上，选择您的语言，请单击 **下一步**。

5. 阅读最终用户许可协议，如果您接受这些条款，请单击 **下一步**。

6. 在 **中心配置** 页上，输入基于您的环境的以下信息 ︰

   |字段 <br /> <br />|描述 <br /> <br />|注释 <br /> <br />|
   |---------|---------------|------------|
   |安装路径 <br /> <br />|这是将在其中安装 ATA 中心的位置。 默认情况下，这是 %programfiles%\Microsoft 高级威胁 Analytics\Center <br /> <br />|保留默认值 <br /> <br />|
   |数据库数据路径 <br /> <br />|这是 MongoDB 数据库文件将位于的位置。 默认情况下，这是 %programfiles%\Microsoft 高级威胁 Analytics\Center\MongoDB\bin\data <br /> <br />|将位置更改为必须根据您调整大小的增长空间的位置。 **注意：** <ul><li>在生产环境中应使用具有足够的空间根据容量规划的驱动器。 </li><li>对于大型部署数据库应在单独的物理磁盘上。 </li> </ul>请参阅 [ATA 容量规划](./small.md) 的大小调整的信息。 <br />|
   |数据库日志路径 <br /> <br />|这是数据库日志文件将位于的位置。 默认情况下，这是 %programfiles%\Microsoft 高级威胁 Analytics\Center\MongoDB\bin\data\journal <br /> <br />|对于大型部署，数据库日志应该位于单独的物理磁盘从数据库和系统驱动器上。 将位置更改为一个位置，必须为您的数据库日志留出空间。 <br /> <br />|
   |ATA 中心服务 IP 地址 ︰ 端口 <br /> <br />|这是 ATA 中心服务将侦听来自 ATA 网关的通信的 IP 地址。 <br /> <br />**默认端口 ︰** 443 <br /> <br />|单击向下箭头选择 ATA 中心服务要使用的 IP 地址。 <br /> <br />IP 地址和端口的 ATA Center 服务不能为相同的 IP 地址和端口 ATA 控制台。 请务必更改 ATA 控制台的端口。 <br /> <br />|
   |ATA 中心服务 SSL 证书 <br /> <br />|这是 ATA 中心服务将使用的证书。 <br /> <br />|单击密钥图标以选择安装的证书或在实验室环境中部署时检查自签名的证书。 <br /> <br />|
   |ATA 控制台的 IP 地址 <br /> <br />|这是为 ATA 控制台将由 IIS 使用的 IP 地址。 <br /> <br />|单击向下箭头选择 ATA 控制台所用的 IP 地址。 **注意 ︰** 记下此 IP 地址来更轻松地从 ATA 网关访问 ATA 控制台。 <br />|
   |ATA 控制台 SSL 证书 <br /> <br />|这是由 IIS 使用的证书。 <br /> <br />|单击密钥图标以选择安装的证书或在实验室环境中部署时检查自签名的证书。 <br /> <br />|
   ![](./Image/ATA_Center_Configuration.JPG)

7. 单击 **安装** 安装 ATA 及其组件并创建 ATA 中心和 ATA 控制台之间的连接。

8. 安装完成后，单击 **启动**  为连接到 ATA 控制台。

   安装和 ATA 中心在安装期间配置以下组件 ︰

   - Internet 信息服务 (IIS)

   - MongoDB

   - ATA Center 服务和 ATA 控制台 IIS 网站

   - 自定义性能监视器数据收集组

   - 自签名的证书 （如果在安装期间选择）

> [!NOTE]
> 为了帮助进行故障排除和产品增强功能，建议您安装工具是 MongoVue 和任何其他 MongoDB 外接程序，或您选择的任何其他第三方工具。 工具是 MongoVue 要求.Net Framework 3.5 安装。

### 验证安装

1. 检查以了解 Microsoft 高级威胁分析中心服务正在运行。

2. 在桌面上单击 Microsoft 高级威胁分析快捷方式以连接到 ATA 控制台。 登录相同的用户凭据用来安装 ATA 中心。 第一次登录到您将会自动向返回 ATA 控制台 **域连接设置** 页后，可以继续配置和部署的 ATA 网关。

3. 查看中的错误文件 **Microsoft.Tri.Center Errors.log** 文件，可以在以下默认位置中找到 ︰ %programfiles%\Microsoft 高级威胁 Analytics\Center\Logs。

## <a name="ConfigConSettings"></a>步骤 2。 配置 ATA 网关域的连接设置
在域连接设置部分中的设置适用于所有 ATA 网关管理的数据中心。

若要将域配置为连接设置 ATA 中心服务器上执行以下步骤。

1. 打开 ATA 控制台并以用户身份登录。 有关说明，请参阅 [使用 ATA 控制台](./small.md)。

2. 第一次后 ATA Center 已安装，请登录到 ATA Console 您将自动进入 ATA 网关配置页。 如果您需要修改任何设置之后，单击设置图标并选择 **配置**。

   ![](./Image/ATA_config_icon.JPG)

3. 在 **网关** 页上，单击 **域连接设置**, ，输入以下信息，请单击 **保存**。

   |字段 <br /> <br />|注释 <br /> <br />|
   |---------|------------|
   |**用户名** （必需） <br /> <br />|输入的只读的用户名，例如 ︰ **user1**。 <br /> <br />|
   |**密码** （必需） <br /> <br />|密码为只读的用户输入，例如 ︰ **Pencil1**。 **注意 ︰** 请确保该密码是否正确。 如果保存了错误的密码，ATA 服务将停止 ATA 网关服务器上运行。 <br />|
   |**域** （必需） <br /> <br />|例如，对于只读的用户，输入域 **contoso.com**。 **注意 ︰** 很重要，输入用户所在的域的完整的 FQDN。 例如，如果用户的帐户是 corp.contoso.com 域中，您需要输入 `corp.contoso.com` 不 contoso.com <br />|
   ![](./Image/ATA_Domain_Connectivity_User.JPG)

## <a name="DownloadATA"></a>步骤 3。 下载 ATA 网关安装包
在配置域连接设置之后，您可以下载 ATA 网关安装程序包。

若要下载 ATA 网关数据包 ︰

1. 在 ATA 网关计算机上，打开浏览器并输入为 ATA 控制台的 ATA 中心中配置的 IP 地址。 当 ATA 控制台打开后时，单击设置图标并选择 **配置**。

   ![](./Image/ATA_config_icon.JPG)

2. 在 **ATA 网关** 选项卡上，单击 **下载 ATA 网关安装**。

3. 保存包本地。

Zip 文件包含下列内容 ︰

- ATA 网关安装程序

- 具有连接到数据中心所需的信息的配置设置文件

## <a name="InstallATAGW"></a>步骤 4。 安装数据网关
在安装之前 ATA 网关，来验证正确配置端口镜像和 ATA 网关，可以看到从域控制器之间的流量。 请参阅 [验证端口镜像](./small.md) 有关详细信息。

> [!IMPORTANT]
> 请确保 [KB2919355](http://support.microsoft.com/kb/2919355/) 是否已安装。  运行下面的 PowerShell cmdlet，以检查是否安装了修补程序 ︰
> 
> `Get-HotFix -Id kb2919355`

ATA 网关服务器上执行以下步骤。

1. 从 zip 文件中提取文件。

2. 从提升的命令提示符下，运行 Microsoft ATA 网关 Setup.exe，然后按照安装向导。

3. 在 **欢迎** 页上，选择您的语言，请单击 **下一步**。

4. 在下  **ATA 网关配置**, ，输入以下信息根据您的环境 ︰

   ![](./Image/ATA_Gateway_Configuration.JPG)

   |字段 <br /> <br />|描述 <br /> <br />|注释 <br /> <br />|
   |---------|---------------|------------|
   |安装路径 <br /> <br />|这是 ATA 网关的安装位置。 默认情况下，这是 %programfiles%\Microsoft 高级威胁 Analytics\Gateway <br /> <br />|保留默认值 <br /> <br />|
   |ATA 网关服务 SSL 证书 <br /> <br />|这是 ATA 网关将使用的证书。 <br /> <br />|用于实验室环境仅使用自签名的证书。 <br /> <br />|
   |ATA 网关注册 <br /> <br />|输入用户名和 ATA 管理员的密码。 <br /> <br />|对于 ATA 网关注册 ATA 中心，请输入用户名和密码的用户的安装 ATA 中心。 此用户必须是某个 ATA 中心上的以下本地组的成员。 <br /> <br /><ul><li>管理员 </li><li>Microsoft 高级威胁分析管理员 </li> </ul> **注意 ︰** 这些凭据仅用于注册并且不会存储在 ATA。 <br />|
   安装和 ATA 网关在安装期间配置以下组件 ︰

   - KB 3047154

      > [!IMPORTANT]
      > - 不要在虚拟化主机上安装 KB 3047154。 这可能导致端口镜像无法正常工作。
      > - 不要在 ATA 网关上安装 Message Analyzer、 Wireshark 或其他网络捕获软件。 如果您需要捕获网络流量，安装并使用 Microsoft 网络监视器 3.4。

   - ATA 网关服务

   - Microsoft Visual c + + 2013 可再发行组件

   - 自定义性能监视器数据收集组

5. 安装完成后，单击 **启动**  打开您的浏览器并登录到 ATA 控制台中。

### <a name="ConfigATAGW"></a>第 5 步。 配置 ATA 网关设置
安装数据网关后，执行以下步骤以配置 ATA 网关的设置。

1. 在 ATA 网关计算机上，在 ATA 控制台中，单击 **配置** ，然后选择 **ATA 网关** 页。

2. 输入以下信息。

   |字段 <br /> <br />|描述 <br /> <br />|注释 <br /> <br />|
   |---------|---------------|------------|
   |描述 <br /> <br />|输入 ATA 网关 （可选） 的说明。 <br /> <br />||
   |**域控制器** （必需） <br /> <br />有关列表的控制器的其他信息，请参阅下文。 <br /> <br />|输入你的域控制器的完整的 FQDN，然后单击加号以将其添加到列表。 例如，  **dc01.contoso.com** <br /> <br />![](./Image/ATAGWDomainController.png) <br /> <br />|在列表中的第一个域控制器中的对象将同步通过 LDAP 查询。 具体取决于域的大小，这可能需要一些时间。 **注意：** <ul><li>请确保第一个域控制器是 **不** 只读的。   读取只有只在初始同步完成后，才应该添加控制器的域。 </li> </ul> <br />|
   |**捕获网络适配器** （必需） <br /> <br />|选择的网络适配器连接到交换机配置为目标镜像端口以接收域控制器的通信。 <br /> <br />|选择捕获网络适配器。 <br /> <br />|
   ![](./Image/ATA_Config_GW_Settings.jpg)

3. 单击 **保存**。

   > [!NOTE] 它将需要几分钟 ATA 网关服务来启动第一次，因为它生成的网络的高速缓存 ATA 网关用来捕获分析器。

以下信息适用于在中输入的服务器 **域控制器** 列表。

- 在列表中的第一个域控制器将由 ATA 网关，用于同步通过 LDAP 查询域中的对象。 具体取决于域的大小，这可能需要一些时间。

- 其流量是否正在由 ATA 网关通过端口镜像监视的所有域控制器必须都列在 **域控制器** 列表。 如果域控制器未列在 **域控制器** 列表中，检测到可疑活动可能无法按预期运行。

- 请确保第一个域控制器是 **不** 只读域控制器 (RODC)。

   读取只有只在初始同步完成后，才应该添加控制器的域。

- 列表中的至少一个域控制器是全局编录服务器。 这将使 ATA 若要解决在林中其他域中的计算机和用户对象。

配置更改将应用于在下一步计划 ATA 网关和数据中心之间同步 ATA 网关。

### 验证安装 ︰
要验证已成功部署 ATA 网关，请检查下列方面 ︰

1. 检查 Microsoft 高级威胁分析网关服务正在运行。 在保存 ATA 网关设置后，可能需要几分钟时间以启动该服务。

2. 如果该服务未启动，请查看位于以下默认文件夹中的"Microsoft.Tri.Gateway Errors.log"文件"%programfiles%\Microsoft 高级威胁 Analytics\Gateway\Logs"，搜索与"传输"或"服务启动"的条目。

3. 检查下列 Microsoft ATA 网关的性能计数器 ︰

   - **NetworkListener 捕获消息 / 秒**︰ 此计数器可跟踪每秒 ATA 正在捕获的消息数。 此值应 mid 数百到数千具体取决于被监视的域控制器的数量和每个域控制器有多忙。 单引号或双引号的数字值与镜像配置的端口表明存在问题。

   - **EntityTransfer 活动传输次数/秒**︰ 此值应为范围内的几百每隔几秒。

4. 如果这是安装的第一个 ATA 网关，几分钟后登录到 ATA 控制台，并通过轻扫右侧的打开屏幕打开通知窗格。 您应看到一份 **实体最近学习了** 控制台右侧的通知栏中。

5. 若要验证安装成功完成 ︰

   在控制台中，搜索的搜索栏，例如，用户或组在您的域中的某些内容。

   打开性能监视器。 在性能树中，单击 **性能监视器** ，然后单击加号图标到 **添加计数器**。 展开 **Microsoft ATA 网关** 和向下滚动到 **每秒的网络侦听器捕获消息** 并将其添加。 然后，确保关系图上查看活动。

   ![](./Image/ATA_performance_monitoring_add_counters.png)

### <a name="ATAvpnHoneytokensetting"></a>步骤 6。 配置短期租约子网和蜜标用户
短期租约子网是子网中 IP 地址分配发生迅速更改-秒或几分钟内。 例如，IP 地址用于您的 Vpn 和 Wi-fi IP 地址。 若要输入您的组织中使用的短期租约子网的列表，请按照下列步骤 ︰

1. 从 ATA 网关计算机上的 ATA 控制台中，单击设置图标并选择 **配置**。

   ![](./Image/ATA_config_icon.JPG)

2. 在下 **检测**, ，输入以下内容的短期租约子网。 输入短期租约使用子网斜线记数法格式，例如 ︰  `192.168.0.0/24` ，然后单击加号。

3. 蜜标帐户 Sid，请输入中将没有网络活动，然后单击加号可对用户帐户的 SID。 例如：`S-1-5-21-72081277-1610778489-2625714895-10511`。

   > [!NOTE] 若要查找用户的 SID，请运行以下 Windows PowerShell cmdlet `Get-ADUser UserName`。

4. 配置排除项 ︰ 您可以配置要从特定的可疑活动中排除的 IP 地址。 请参阅 [使用 ATA 检测设置](./small.md) 有关详细信息。

5. 单击 **保存**。

![](./Image/ATA_VPN_Subnets.JPG)

祝贺您，您已成功部署 Microsoft 高级威胁分析 ！

检查攻击时间线，以查看检测到可疑活动和搜索用户或计算机以及查看他们的配置文件。

请记住，它采用对于 ATA 来建立行为的配置文件，以便在第一个三周期间您将看不到任何可疑行为的活动的第三周最少。

## 另请参阅
[有关支持，请查看我们的论坛 ！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
[配置事件收集](./small.md)
[ATA 系统必备组件](./small.md)



<!--HONumber=May16_HO4-->


