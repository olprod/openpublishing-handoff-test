---
title: Azure AD Graph API 实体和复杂类型引用
ms.TocTitle: Entity and complex type reference
ms.ContentId: 88f6e187-70db-4d90-b3b6-b8702bad1220
ms.topic: reference (API)
ms.date: 01/26/2016
---


# 实体和复杂类型引用 |Graph API 参考 

    
 _**适用于 ︰** API 的关系图 |Azure Active Directory_


<a id="Overview"> </a>
本主题讨论的实体和关系图 API 公开的复杂类型。

Graph API 是一个 OData 3.0 符合 REST API，它提供对在 Azure Active Directory，如用户、 组、 组织联系人和应用程序的目录对象的编程访问。 

> [!IMPORTANT] 它也可通过 azure AD Graph API 功能 [Microsoft Graph](https://graph.microsoft.io/), ，如 Outlook、 OneDrive、 OneNote、 计划者和 Office 关系图中，通过使用单个访问令牌的单个终结点访问所有服务的一个统一的 API，它还包括来自其他 Microsoft Api。

## 实体引用

### 应用程序实体 <a id="ApplicationEntity"> </a>
表示一个应用程序。 将身份验证外包给 Azure AD 的任何应用程序都必须在目录中进行注册。 这涉及告诉 Azure AD 关于你的应用程序，包括它具有处的位置，要将回复发送身份验证后，要确定您的应用程序及更多内容的 URI 的 URL 的 URL。  有关详细信息，请参阅 [基础知识的应用程序注册 Azure AD 中](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-scenarios/#basics-of-registering-an-application-in-azure-ad)。 继承自 [DirectoryObject]。

#### 属性
**声明的属性**

|  Name |  类型 |  创建 (POST) |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| 应用程序 Id | 版本 1.5 中的 Edm.String<br/><br/> 以前的版本中的 Edm.Guid | 否 | 可筛选 | 否 | 应用程序的唯一标识符。 |
| 实体的 {3>approles | 集合 ([AppRole]) | 可选 | 是 | 是 | 应用程序可能会声明的应用程序角色的集合。 这些角色可以分配给用户、 组或服务主体。<br/><br/> **说明**︰ 需要版本 1.5，不可为 null。 |
| availableToOtherTenants | Edm.Boolean | 可选 | 可筛选 | 是 | **true** 应用程序是否与其他租户共享; 否则为 **false**。 |
| deletionTimestamp | Edm.DateTime | 否 | 是 | 否 | 应用程序已删除从租户的时间。 如果还未删除该应用程序，将返回 **null**。 已删除的应用程序可以从读取 `/deletedApplications` 资源集合。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| displayName | Edm.String | 必需 | 是 | 是 | 应用程序的显示名称。 |
| errorUrl | Edm.String | 可选 | 是 | 是 |  |
| groupMembershipClaims | Edm.String | 可选 | 是 | 是 | 位掩码，用于配置的用户或应用程序需要的 OAuth 2.0 访问令牌中颁发的"groups"声明。 位掩码值为 ︰ 0 ︰ 无、 1 ︰ 安全组和 Azure AD 角色，2 ︰ 和非保留，4 ︰ 保留。 将位掩码设置为 7 将获得的所有安全组、 通讯组和登录的用户所在的 Azure AD 目录角色。<br/><br/> **说明**︰ 需要 1.5 版。 |
| 主页 | Edm.String | 可选 | 是 | 是 | 应用程序的主页的 URL。 |
| identifierUris | Collection （edm.string) | 可选 | 可筛选 | 是 | 用于标识应用程序的 Uri。 有关详细信息，请参阅 [应用程序对象和服务主体对象](https://azure.microsoft.com/en-us/documentation/articles/active-directory-application-objects/)。<br/><br/> **说明**︰ 不可为 null， **任何** 操作员是必需的筛选器表达式多值属性; 有关详细信息，请参阅 [支持查询、 筛选和分页选项]。 |
| 实体的 {3>keycredentials | 集合 ([KeyCredential]) | 可选 | 是 | 是 | 与应用程序相关联的密钥凭据的集合<br/><br/> **说明**︰ 不可为 null |
| knownClientApplications | Collection(Edm.Guid) | 可选 | 是 | 是 | 绑定到此资源应用程序的客户端应用程序。 同意任何已知的客户端应用程序中将会隐式同意资源应用程序通过组合的同意对话框 （显示客户端和资源所需的 OAuth 权限作用域）。<br/><br/> **说明**︰ 需要版本 1.5，不可为 null。 |
| 注销 Url | Edm.String | 可选 | 是 | 是 |  |
| mainLogo | Edm.Stream | 可选 | 是 | 是 | 主徽标的应用程序。<br/><br/> **说明**︰ 不可为 null |
| oauth2AllowImplicitFlow | Edm.Boolean | 可选 | 是 | 是 | 指定此 web 应用程序是否可以请求 OAuth2.0 隐式流令牌。 默认值是 **false**。<br/><br/> **说明**︰ 需要版本 1.5，不可为 null。 |
| oauth2AllowUrlPathMatching | Edm.Boolean | 可选 | 是 | 是 | 指定是否作为 OAuth 2.0 令牌请求的一部分，Azure AD 将允许对应用程序的重定向 URI 路径匹配 **replyUrls**。 默认值是 **false**。<br/><br/> **说明**︰ 需要版本 1.5，不可为 null。 |
| oauth2Permissions | 集合 ([OAuth2Permission]) | 可选 | 是 | 是 | Web API （资源） 应用程序向客户端应用程序公开的 OAuth 2.0 权限作用域的集合。 同意过程，可能向客户端应用程序授予这些权限作用域。<br/><br/> **说明**︰ 需要版本 1.5，不可为 null。 |
| oauth2RequiredPostResponse | Edm.guid 更新 | 可选 | 是 | 是 | 指定是否作为 OAuth 2.0 令牌请求的一部分，Azure AD 将允许与 GET 请求相反的 POST 请求。 默认值为 false，它指定将允许仅 GET 请求。<br/><br/> **说明**︰ 需要版本 1.5，不可为 null。 |
| objectId | Edm.guid 更新 | 否 | 是 | 否 | 应用程序的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一 |
| 对象类型 | Edm.String | 否 | 是 | 否 | 一个字符串，标识对象类型。 对于应用程序的值始终是"应用程序"。 继承自 [DirectoryObject]。 |
| 实体的 {3>passwordcredentials | 集合 ([PasswordCredential]) | 可选 | 是 | 是 | 与应用程序关联的密码凭据的集合。<br/><br/> **说明**︰ 不可为 null |
| publicClient | Edm.Boolean | 可选 | 是 | 否 | 指定此应用程序是否为公共客户端 （如安装的应用程序在移动设备上运行）。 默认值是 **false**。 |
| replyUrls | Collection （edm.string) | 可选 | 是 | 是 | 指定的登录，将用户令牌发送到的 Url 或 Uri OAuth 2.0 授权代码和访问令牌发送到重定向。<br/><br/> **说明**︰ 不可为 null |
| requiredResourceAccess | 集合 ([RequiredResourceAccess]) |  | 是 |  | 指定此应用程序需要访问的组的 OAuth 权限作用域和应用程序角色的每个这些资源下它需要的资源。 所需的资源访问权限的这种预先配置驱动了同意体验。<br/><br/> **说明**︰ 需要版本 1.5，不可为 null。 |
| samlMetadataUrl | Edm.String | 可选 | 是 | 是 | 应用程序的 SAML 元数据 URL。 |

**导航属性**   

|  Name |  源多重性 |  收件人 |  目标多重性 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| extensionProperties | \* | [ExtensionProperty] | \* | 与应用程序关联的扩展属性。 需要 1.5 或更高版本。 |
| 所有者 | \* | [DirectoryObject] | \* | 应用程序的所有者的目录对象。 所有者是一组非管理员用户，他们有权修改此对象。 需要 2013年-11-08 版或更高版本。 继承自 [DirectoryObject]。 |
**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对应用程序 （HTTP 方法列在括号中） 支持以下操作 ︰

- 创建 (CREATE)
- 读取 （读取）
- 更新 (PATCH)
- 删除 (DELETE)

对应用程序导航属性支持以下操作。 并非所有操作可能都支持每个导航属性。

- 读取 （读取）
- 更新 (POST)
- 删除 (DELETE)

不能对应用程序调用以下操作。

- [还原] 还原已删除的应用程序。 需要版本 1.5 或更高版本。

---

### AppRoleAssignment 实体 <a id="AppRoleAssignmentEntity"> </a>
用于记录当用户或组分配到应用程序。 在这种情况下，该角色分配将导致应用程序磁贴显示在用户的应用程序访问面板。 此实体也可用于授予对资源应用程序属于特定角色的另一个应用程序 （建模为服务主体） 访问权限。 您可以创建、 读取、 更新和删除角色分配。 继承自 [DirectoryObject]。

**重要**︰ 版本 1.5 中引入。
#### 属性
**声明的属性**

|  Name |  类型 |  创建 (POST) |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| creationTimestamp | Edm.DateTime | 否 | 是 | 否 | 当创建程序集的授予的时间。 |
| deletionTimestamp | Edm.DateTime | 否 | 是 | 否 | 此属性不是有效的应用程序角色分配，并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| id | Edm.guid 更新 | 必需 | 是 | 是 | 分配给此主体角色 id。 此角色必须由目标资源应用程序声明 **resourceId** 中其 **appRoles** 属性。 如果资源未声明的任何权限，则必须指定默认 id (零 GUID)。<br/><br/> **说明**︰ 不可为 null。  |
| principalDisplayName | Edm.String | 否 | 是 | 否 | 已授予访问权限的主体的显示名称。 |
| objectId | Edm.String | 否 | 是 | 否 | 应用程序角色分配的的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 否 | 是 | 否 | 一个字符串，标识对象类型。 对于应用程序角色分配的值始终为"AppRoleAssignment"。 继承自 [DirectoryObject]。 |
| principalId | Edm.guid 更新 | 必需 | 是 | 是 | 唯一标识符 (**objectId**) 被授予访问权限的主体。<br/><br/> **说明**︰ 必需。  |
| principalType | Edm.String | 否 | 是 | 否 | 主体的类型。 这可能是"用户"、"Group"或"ServicePrincipal"。 |
| resourceDisplayName | Edm.String | 否 | 是 | 否 | 对其进行分配的资源显示名称。 |
| resourceId | Edm.guid 更新 | 必需 | 是 | 是 | 唯一标识符 (**objectId**) 为其进行分配的目标资源 （服务主体）。 |
**导航属性**   
无。

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

---

### 联系人实体 <a id="ContactEntity"> </a>
表示组织的联系人。 继承自 [DirectoryObject]。

组织联系人代表用户不在你公司的目录中。 它们是已启用邮件的实体，通常表示对贵公司或组织外部的人员。 无法使用 Azure AD 身份验证组织的联系人，也可以将它们分配许可证。 

可以在通过与使用 Azure AD Connect，一个在本地目录同步你的租户中创建组织的联系人或要通过 Exchange Online 的管理门户或 Exchange Online PowerShell cmdlet 之一创建它们。 有关 Azure AD Connect 的详细信息，请参阅 [与 Azure Active Directory 集成本地标识](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect/)。 有关 Exchange Online 管理工具的详细信息，请参阅 [Exchange Online 设置和管理](https://technet.microsoft.com/en-us/library/exchange-online-administration-and-management.aspx#BKMK_ExchangeAdministrationCenter)。 

不能使用 Graph API 创建组织的联系人。 可以但是，更新和删除当前未同步的联系人从本地目录;也就是说，联系以获取该 **dirSyncEnabled** 属性是 **null** 或 **false**。 无法更新或删除联系人为其 **dirSyncEnabled** 属性是 **true**。

**请注意**︰ 组织联系人是表示外部用户的 directory 实体。 他们不应该与 O365 Outlook 个人联系人相混淆。 
 
#### 属性
**声明的属性**

|  Name |  类型 |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| city | Edm.String | 可筛选 | 是 | 联系人所在的城市。 |
| country | Edm.String | 可筛选 | 是 | 联系人所在国家/地区。 |
| deletionTimestamp | Edm.DateTime | 是 | 否 | 此属性对于联系人，并始终返回无效 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| department | Edm.String | 可筛选 | 是 | 联系人工作的部门的名称。 |
| dirSyncEnabled | Edm.Boolean | 可筛选 | 否 | **true** 如果从本地目录; 同步此对象 **false** 如果此对象最初从本地目录同步，但不能再同步; **null** 如果永远不会从本地目录 （默认值） 同步此对象。 |
| displayName | Edm.String | 可筛选 | 是 | 联系人的显示名称。 |
| facsimileTelephoneNumber | Edm.String | 是 | 是 | 联系人的业务传真机的电话号码。 |
| givenName | Edm.String | 可筛选 | 是 | 给定名称 （名字） 的联系人。 |
| jobTitle | Edm.String | 可筛选 | 是 | 联系人的职务。 |
| lastDirSyncTime | Edm.DateTime | 可筛选 | 否 | 指示对象上次同步与在本地目录的最后一个时间。 |
| mail | Edm.String | 可筛选 | 否 | 该联系人，例如"jeff@contoso.onmicrosoft.com"SMTP 地址。 |
| mailNickname | Edm.String | 可筛选 | 是 | 联系人的邮件别名。 |
| mobile | Edm.String | 是 | 是 | 联系人的主移动电话号码。 |
| objectId | Edm.String | 是 | 否 | 联系人的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 是 | 否 | 一个字符串，标识对象类型。 联系人的值始终是"Contact"。 继承自 [DirectoryObject]。 |
| physicalDeliveryOfficeName | Edm.String | 是 | 是 | 中的业务联系人营业场所的办公地点。 |
| postalCode | Edm.String | 是 | 是 | 联系人通信地址的邮政编码。 特定于联系人的国家/地区的邮政编码。 在美国，此属性包含邮政编码。 |
| 实体的 {4>provisioningerrors | 集合 ([ProvisioningError]) | 是 | 否 | 成功设置阻止该联系人的错误详细信息的集合。<br/><br/> **注意 ︰** 不可为 null  |
| proxyAddresses | Collection （edm.string) | 可筛选 | 否 | **注意 ︰** 唯一，不可为 null， **任何** 操作员是必需的筛选器表达式多值属性; 有关详细信息，请参阅 [支持查询、 筛选和分页选项]。  |
| sipProxyAddress | Edm.String | 是 | 否 | 指定语音的联系人的 IP (VOIP) 会话发起协议 (SIP) 地址。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| state | Edm.String | 可筛选 | 是 | 省市自治区中联系人的地址。 |
| streetAddress | Edm.String | 是 | 是 | 业务联系人营业场所的街道地址。 |
| surname | Edm.String | 可筛选 | 是 | 联系人的姓氏 （家族名称或姓）。 |
| telephoneNumber | Edm.String | 是 | 是 | 业务联系人营业场所的主电话号码。 |
| thumbnailPhoto | Edm.Stream | 是 | 是 | 要为联系人显示的缩略图照片。<br/><br/> **注意 ︰** 不可为 null  |

**导航属性**  
 
|  Name |  源多重性 |  收件人 |  目标多重性 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| manager | \* | [DirectoryObject]<br/><br/> (仅 [用户] 和 [联系人] 支持对象。) | 0..1 | 用户或是此联系人的经理的联系人中。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ GET、 PUT、 DELETE |
| directReports | \* | [DirectoryObject]<br/><br/> (仅 [用户] 和 [联系人] 支持对象。) | \* | 联系人的直接下属。 （用户和具有其 manager 属性设置为该联系人的联系人。）继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ 获取 |
| memberOf | \* | [DirectoryObject]<br/><br/> (仅 [组] 支持对象。) | \* | 此联系人所在的组。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ 获取 |

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对联系人 （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰ 

- 读取 (GET)
- 更新 (PATCH): 未从本地目录同步仅联系人 (**dirSyncEnabled** 是 **null** 或 **false**)。
- 删除 (DELETE)

对联系人导航属性; 支持以下操作并非所有操作可能都支持每个导航属性。

- 读取 (GET)
- 更新 (PUT): **manager** 属性，仅针对未从本地目录同步的联系人 (**dirSyncEnabled** 是 **null** 或 **false**)。
- 删除 (DELETE): **manager** 属性，仅针对未从本地目录同步的联系人 (**dirSyncEnabled** 是 **null** 或  **false**)。

可对联系人调用以下操作和函数 ︰

- [checkMemberGroups]: 检查联系人的列表中的组的成员身份。 检查是可传递。
- [getMemberGroups] 以返回联系人是其成员的组的列表。 检查是可传递。
- [isMemberOf]: 检查联系人是否为指定组的成员。 检查是可传递。

#### 备注
联系人是已启用邮件的实体，并且不能通过使用 Graph API 创建。 它们可以更新;不过，更新仅支持对联系人，并带有 **dirSyncEnabled** 属性集 **null** 或 **false**。 可以删除联系人。

---

### 联系人实体 <a id="ContractEntity"> </a>
仅用于合作伙伴租户中存在。 合作伙伴租户是属于 Microsoft 合作伙伴都是 Office 365 联合、 Microsoft 云解决方案提供商联系或 Microsoft 顾问合作伙伴计划的一部分的 Azure AD 租户。 表示与客户租户合作伙伴租户具有现有的合作关系。 只读。 继承自 [DirectoryObject]。

**重要**︰ 版本 1.5 中引入。
#### 属性
**声明的属性**

| Name | 类型 | Read(GET) | 描述 |
|:----|:----|:----|:----|
| customerContextId | Edm.guid 更新 | 可筛选 | 客户租户引用该合作关系的唯一标识符。 对应于 **objectId** 客户租户属性 [TenantDetail] 对象。 |
| defaultDomainName | Edm.String | 可筛选 | 一份客户租户的默认域的名称。 在建立与客户合作关系时，生成的副本。 它不会自动更新如果更改了客户租户的默认域的名称。 |
| deletionTimestamp | Edm.DateTime | 是 | 此属性不是有效的协定，并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| displayName | Edm.String | 可筛选 | 一份客户租户的显示名称。 在建立与客户合作关系时，生成的副本。 它不会自动更新如果更改了客户租户的显示名称。 |
| 对象类型 | Edm.String | 是 | 一个字符串，标识对象类型。 此值始终是"协定"。 继承自 [DirectoryObject]。 |
| objectId | Edm.String | 是 | 合作关系的唯一标识符。 继承自 [DirectoryObject]。 <br/> <br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。 |

**导航属性**   
无。

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对协定 （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰ 

- 读取 (GET)


---

### 设备实体 <a id="DeviceEntity"> </a>
表示的目录中注册的设备。 继承自 [DirectoryObject]。


#### 属性
**声明的属性**

|  Name |  类型 |  创建 (POST) |  读取 (GET) |  更新 (PATCH) |   描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| accountEnabled | Edm.Boolean | 可选 | 可筛选 | 是 |  |
| alternativeSecurityIds | 集合 ([AlternativeSecurityId]) | 可选 | 可筛选 | 是 | **说明**︰ 不可为 null， **任何** 操作员是必需的筛选器表达式多值属性; 有关详细信息，请参阅 [支持查询、 筛选和分页选项]。  |
| approximateLastLogonTimeStamp | Edm.DateTime | 可选 | 是 | 是 |  |
| deletionTimestamp | Edm.DateTime | 否 | 是 | 否 | 此属性不是有效的设备，并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| deviceId | Edm.guid 更新 | 必需 | 可筛选 | 是 |  |
| deviceObjectVersion | Edm.Int32 | 可选 | 是 | 是 |  |
| deviceOSType | Edm.String | 必需 | 是 | 是 | 在设备上的操作系统的类型。 |
| deviceOSVersion | Edm.String | 必需 | 是 | 是 | 在设备上的操作系统的版本 |
| devicePhysicalIds | Collection （edm.string) | 可选 | 可筛选 | 是 | **说明**︰ 不可为 null  |
| dirSyncEnabled | Edm.Boolean | 否 | 可筛选 | 否 | **true** 如果从本地目录; 同步此对象 **false** 如果此对象最初从本地目录同步，但不能再同步; **null** 如果永远不会从本地目录 （默认值） 同步此对象。 |
| displayName | Edm.String | 必需 | 可筛选 | 是 | 设备显示名称。 |
| isCompliant | Edm.Boolean | 可选 | 是 | 是 | **true** 如果设备符合移动设备管理 (MDM) 策略; 否则为 **false**。 |
| IsManaged | Edm.Boolean | 可选 | 是 | 是 | **true** 设备是否正由 Intune 之类的移动设备管理 (MDM) 应用程序管理; 否则为 **false**。 |
| lastDirSyncTime | Edm.DateTime | 否 | 可筛选 | 否 | 上次时间从该处对象上次与本地目录同步。 |
| objectId | Edm.String | 否 | 是 | 否 | 设备的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一  |
| 对象类型 | Edm.String | 否 | 是 | 否 | 一个字符串，标识对象类型。 设备的此值始终是"设备"。 继承自 [DirectoryObject] |

**导航属性**
  
|  Name |  源多重性 |  收件人 |  目标多重性 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| registeredOwners | \* | [用户] | \* | 注册的所有者的设备的用户。 |
| registeredUsers | \* | [用户] | \* | 注册用户的设备用户的用户。 |

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
（HTTP 方法列在括号中） 的设备上支持以下操作 ︰

- 创建 (CREATE)
- 读取 （读取）
- 更新 (PATCH)
- 删除 (DELETE)

支持以下操作对设备导航属性。 并非所有操作可能都支持每个导航属性。

- 读取 （读取）
- 更新 (PUT)
- 删除 (DELETE)

在设备上支持任何函数或操作。

---

### DirectoryLinkChange 实体 <a id="DirectoryLinkChangeEntity"> </a>
一个 **DirectoryLinkChange** 返回对象，指示差异查询结果集中的联系人、 用户、 属性或链接表示一组自上次差异查询以来已更改。  **DirectoryLinkChange** 对象将表示更改到的用户或联系人的 **manager** 属性或对一组更改 **成员** 属性。 有关差异查询的详细信息，请参阅 [差异查询]。 继承自 [DirectoryObject]。
#### 属性
**声明的属性**

|  Name |  类型 |  读取 (GET) |  描述 |
|:-------|:-------|:-------|:-------|
| associationType | Edm.String | 是 | 一个字符串，标识要应用更改的关联类型。 值为"成员"或"Manager"。 |
| deletionTimestamp | Edm.DateTime | 是 | 此属性不是有效的目录链接更改对象，并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| objectId | Edm.String | 是 | 唯一标识符目录链接更改对象。 有关 **DirectoryLinkChange** 对象时，此值始终是 00000000-0000-0000-0000-000000000000。 继承自 [DirectoryObject]。<br/><br/> **注意 ︰ 密钥** 不可变，不可为 null，唯一  |
| 对象类型 | Edm.String | 是 | 一个字符串，标识对象类型。 有关 **DirectoryLinkChange** 对象时，此值始终是"DirectoryLinkChange"。 [DirectoryObject] |
| sourceObjectId | Edm.String | 是 | 源对象中; 的对象 ID例如，"7373b0af-d462-406e-ad26-f2bc96d823d8"。 |
| sourceObjectType | Edm.String | 是 | 一个字符串，标识源对象类型;这将是以下项之一:"组"、"用户"或"Contact"。 |
| sourceObjectUri | Edm.String | 是 | 源对象中; 的 URI例如， `"https://graph.windows.net/contoso.com/groups/7373b0af-d462-406e-ad26-f2bc96d823d8"`。 |
| targetObjectId | Edm.String | 是 | 目标对象; 对象 ID例如，"dca803ab-bf26-4753-bf20-e1c56a9c34e2"。 |
| targetObjectType | Edm.String | 是 | 一个字符串，标识源对象类型;这将是以下项之一:"组"、"用户"或"Contact"。 |
| targetObjectUri | Edm.String | 是 | 目标对象中; 的 URI例如， `"https://graph.windows.net/contoso.com/users/dca803ab-bf26-4753-bf20-e1c56a9c34e2"`。 |

**导航属性**   
无。

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

---

### DirectoryObject 实体 <a id="DirectoryObjectEntity"> </a>
表示 Azure Active Directory 对象。  **DirectoryObject** 类型是大部分其他目录实体类型的基类型。
#### 属性
**声明的属性**

|  Name |  类型 |  创建 (POST) |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| deletionTimestamp | Edm.DateTime | 否 | 是 | 否 | 从该处删除目录对象的时间。 它仅适用于可以还原的那些目录对象。 当前仅支持已删除 [应用程序] 对象; 所有其他实体返回 **null** 此属性。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| objectId | Edm.String | 否 | 是 | 否 | 一个对象; 的唯一标识符的 Guid例如，12345678-9abc-def0-1234年-56789abcde。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 否 | 是 | 否 | 一个字符串，标识对象类型。 例如，对于组的值始终是"Group"。 |

**导航属性**   

|  Name |  源多重性 |  收件人 |  目标多重性 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| {1>createdobjects | \* | DirectoryObject | \* | 创建当前对象的目录对象。 只读属性。 需要 2013年-11-08 版或更高版本。 |
| createdOnBehalfOf | \* | DirectoryObject | 0..1 | 目录对象，代表其创建此对象。 只读属性。 需要 2013年-11-08 版或更高版本。 |
| manager | \* | DirectoryObject | 0..1 | 此对象管理器。 对用户和联系人有效。 返回用户或联系人。  |
| directReports | \* | DirectoryObject | \* | 用户和向该对象报告的联系人。 对用户和联系人有效。 返回用户和联系人。 只读属性。 |
| 成员 | \* | DirectoryObject | \* | 此对象的成员的对象。 对组和角色有效。 在组上，返回联系人、 用户和组。 对于角色，将返回用户和服务主体。 |
| memberOf | \* | DirectoryObject | \* | 此对象属于的对象。 对联系人、 组、 服务主体和用户有效。 在联系人上，将返回组。 在组上，将返回组。 在用户上，返回组和角色。 对服务主体返回角色。 只读属性。<br/><br/> 该属性是不可传递。 例如，如果用户 A 是组 B 的成员，而组 B 是组 C 的成员，用户 A 的 memberOf 属性将不返回组 c。 |
| {1>ownedobjects | \* | DirectoryObject | \* | 拥有当前对象的目录对象。 只读属性。 需要 2013年-11-08 版或更高版本。 |
| 所有者 | \* | DirectoryObject | \* | 目录对象的所有者的当前对象。 所有者是一组非管理员用户，他们有权修改此对象。 需要 2013年-11-08 版或更高版本。 |

**注意 ︰** 并不是所有导航属性都是继承的实体类型上一定有效 **DirectoryObject**。 如果发送针对特定实体无效属性的请求， **400 错误的请求** 返回响应。 有关哪些导航属性就是在特定实体上有效的详细信息，请参考该实体类型的文档。 

#### 支持的操作
完整的目录对象支持的操作集如下 （用于每种的 HTTP 方法位于括号中） ︰ 创建 (POST)、 读取 (GET)、 更新 (PATCH) 和删除 (DELETE)。 但是，并非所有这些操作是在每个实体类型上支持。 目录对象的声明的属性是只读的;创建或更新操作不能在指定它们。

在每个导航属性上支持的操作的潜在一组包括 ︰ 

- **{1>createdobjects**︰ 读取 (GET)。
- **createdOnBehalfOf**︰ 读取 (GET)。
- **管理器**︰ 读取 (GET)、 更新 (PUT) 和删除 (DELETE)。
- **directReports**︰ 读取 (GET)。 
- **成员**︰ 读取 (GET)、 更新 (POST) 和删除 (DELETE)。
- **memberOf**︰ 读取 (GET)。
- **{1>ownedobjects**︰ 读取 (GET)。
- **所有者**︰ 读取 (GET)、 更新 (POST) 和删除 (DELETE)。

每个实体类型，也不是为每个实体类型必须支持导航属性的潜在操作的一套一定支持并不是所有导航属性。

特定的目录对象是否支持特定的操作或函数取决于目录对象的类型 ( **objectType** 属性)。 信息有关哪些对象类型支持哪些函数或操作，请参阅特定对象，例如，用户、 组、 等等，或某个特定函数的文档。

请查阅有关支持的实体操作的信息的特定实体类型的文档。

---

### DirectoryRole 实体 <a id="DirectoryRoleEntity"> </a>
表示 Azure AD 目录角色。 Azure AD 目录角色实参也称为 *管理员角色*。 有关目录 （管理员） 角色的详细信息，请参阅 [在 Azure AD 中分配管理员角色](http://azure.microsoft.com/documentation/articles/active-directory-assign-admin-roles/)。

使用 Graph API 中，可以将用户和服务主体分配给目录角色，以授予他们的目标角色的权限。 你可以读取目录角色对象并更新 **成员** 目录角色，但您的导航属性不能删除目录角色或更新其声明的属性。 继承自 [DirectoryObject]。 

若要读取目录角色，或更新其成员，它必须首先激活在租户中。 在版本 1.5 中，默认情况下激活所有目录角色。 从 1.5 版开始，仅 **公司管理员** 目录角色激活默认情况下。 若要激活其他可用的目录角色发送 POST 请求 **objectId** 的 [DirectoryRoleTemplate] 目录角色所基于的。 请参阅 **支持的操作** 和 **备注** 有关详细信息。

**重要**︰ 从版本 1.5，开始 **角色** 实体类型已重命名为 **DirectoryRole**。
#### 属性
**声明的属性**

| Name | 类型 | 创建 (POST)| 读取 (GET) | 描述 |
|:-------|:-------|:-------|:-------|:-------|
| deletionTimestamp | Edm.DateTime | 否 | 是 | 此属性不是对目录角色，并始终返回有效 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| description | Edm.String | 否 | 是 | 对目录角色的说明。 |
| displayName | Edm.String | 否 | 是 | 目录角色的显示名称。  |
| isSystem | Edm.Boolean | 否 | 是 | **true** 如果角色是一种系统角色; 否则为 **false**。  |
| objectId | Edm.String | 否 | 是 | 目录角色的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 否 | 是 | 一个字符串，标识对象类型。 对于目录角色值始终为"DirectoryRole"。 继承自 [DirectoryObject]。<br/><br/> **请注意**︰ 在低于 1.5 的版本，值将为"角色"。  |
| roleDisabled | Edm.Boolean | 否 | 是 | **true** 目录角色是否已禁用; 否则为 **false**。  |
| roleTemplateId | 字符串 | 必需 | 是 |   **ObjectId** 的 [DirectoryRoleTemplate] 在基于此角色。 <br/><br/> **说明**︰ 在 1.5 版之前的版本，该属性为只读模式。 在版本 1.5 和更高版本中，必须激活目录角色租户中具有的 POST 操作时指定的属性。 在激活目录角色后，该属性是只读的。  |

**导航属性**   

|  Name |  源多重性 |  收件人 |  目标多重性 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| 成员 | \* | [DirectoryObject]<br/><br/> ([用户] 和 [ServicePrincipal] 支持。 | \* | 用户和服务主体是此目录角色的成员。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ GET、 POST、 删除 |

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对目录角色 （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰ 

- 创建 (POST): 在 1.5 和更高版本中受支持。 激活中使用的租户的目录角色 [DirectoryRoleTemplate] 由指定 **roleTemplateId** 在请求中的属性。 目录角色激活后，您可以添加和从角色删除用户和服务主体。
- 读取 (GET)

对目录角色导航属性支持以下操作 ︰ 

- 读取 (GET)
- 更新 (POST)
- 删除 (DELETE)

对目录角色; 可能会调用任何函数或操作但是，你可以在调用 [getMemberObjects] [用户] 或 [ServicePrincipal] 以确定其目录角色成员。 请注意，对于用户，此函数也会返回其直接和可传递组成员身份。

#### 备注
- 在 1.5 版和更高版本，仅 **公司管理员** 角色是激活的 （并且是可见的） 默认情况下租户中。 使用创建 (POST) 操作来激活其他目录角色。 此操作指定 **roleTemplateId** 在请求中的属性。 此属性包含 **objectId** 的 [DirectoryRoleTemplate] 对应于您想要激活的角色的实例。 目录角色激活后可以添加和删除用户和服务主体它使用 Graph API。 在低于 1.5，所有目录角色的版本 (由表示 **角色** 实体) 激活默认情况下和在创建 (POST) 不支持操作。
- 不能使用 Graph API 删除目录角色。 支持更新 **成员** 仅导航属性。 添加和删除支持此属性上。
- 对目录角色不支持查询筛选器表达式。

---

### DirectoryRoleTemplate 实体 <a id="DirectoryRoleTemplateEntity"> </a>
表示目录角色模板。 目录角色模板指定的目录角色的属性值 ([DirectoryRole])。 没有为每个可能在租户中激活目录角色相关联的目录角色模板对象。 继承自 [DirectoryObject]。

若要读取目录角色，或更新其成员，它必须首先激活在租户中。 在版本 1.5 中，默认情况下激活所有目录角色。 从 1.5 版开始，仅 **公司管理员** 目录角色激活默认情况下。 若要激活其他可用的目录角色应将 POST 请求发送到的 /directoryRoles 端点 **objectId** 中指定的目录角色模板目录角色所基于的 **roleTemplateId** 请求的参数。 有关详细信息，请参阅 [DirectoryRole]。

**请注意**︰ 目录角色模板将公开以 **用户** 目录角色。  **用户** 目录角色是隐式和对目录客户端是不可见。 每个 [用户] 租户中分配给此角色由基础结构。 已激活该角色。 不要使用此模板。

**重要**︰ 版本 1.5 中引入。

#### 属性
**声明的属性**

| Name | 类型 | 读取 (GET) | 描述 |
|:-------|:-------|:-------|:-------|
| description | Edm.String | 是 | 要设置目录角色的说明。 |
| deletionTimestamp | Edm.DateTime | 是 | 此属性不是对目录角色模板，并始终返回有效 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| displayName | Edm.String |  是  | 要设置目录角色的显示名称。 |
| objectId | Edm.String |  是  | 模板的的唯一标识符。 继承自 [DirectoryObject]。 在版本 1.5 和更高版本中，您指定 **objectId** 目录角色模板的 **roleTemplateId** POST 请求中的属性激活 [DirectoryRole] 租户中。 <br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String |  是  | 一个字符串，标识对象类型。 对于角色模板值始终为"RoleTemplate"。 继承自 [DirectoryObject]。 |

**导航属性**   
无。

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
在目录角色模板 （HTTP 方法列在括号中） 上支持以下操作 ︰

- 读取 (GET)

---

###域实体 （预览版） <a id="DomainEntity"> </a> 表示与租户相关联的域。

**重要**︰ 仅在 beta 版中可用。
####属性 **声明属性**

| Name | 类型 | 创建<br/>(POST) | 读取<br/>(GET) | 更新<br/>(PATCH) | 描述 |
| -----|------|--------------|-----------|---------------|------------- |
| authenticationType | Edm.String | 否 | 是 |  | 指示域配置为使用什么身份验证类型。 值为"已托管"或"联合"。 |
| availabilityStatus | Edm.String | 否 | 是  | | 此属性始终为 null，除非使用操作 [验证]。 当使用操作，[验证] **域** 响应中返回实体。  **AvailabilityStatus** 属性 **域** 在响应中的实体为"AvailableImmediately"或"EmailVerifiedDomainTakeoverScheduled"。 |
| isAdminManaged | Edm.Boolean | 否 | 是 |  | **false**, ，如果域的 DNS 记录管理委派给 Office 365。 否则为 **true**。<br/><br/>**说明**︰ 不可为 null |
| isDefault | Edm.Boolean | 否 | 是 | 是 | 指示这是用于创建用户的默认域。 没有每家公司只有一个默认域。<br/><br/>**说明**︰ 不可为 null |
| isInitial | Edm.Boolean | 否 | 是 |  | 指示这是由 Microsoft 在线服务 (companyname.onmicrosoft.com) 创建的初始域。 没有每家公司只有一个初始域。<br/><br/>**说明**︰ 不可为 null |
| isRoot | Edm.Boolean | 否 | 是 |  | 对于子域而言，这表示根级域。 只能使用根域需要进行验证，并且将自动验证所有子域。<br/><br/>**说明**︰ 不可为 null |
| isVerified | Edm.Boolean | 否 | 是 |  | 指示此域是否已完成域所有权验证。<br/><br/>**说明**︰ 不可为 null |
| name | Edm.String | 必需 | 可筛选 |  | 域的完全限定的名称。<br/><br/>**说明**︰ 密钥不可变，不可为 null，唯一 |
| supportedServices | Collection （edm.string) | 否 | 是 | 是 | 分配给域的功能。 可以包括 0、 1 或多个下列值 ︰<ul><li>"电子邮件"</li><li>""Sharepoint</li><li>""EmailInternalRelayOnly</li><li>""OfficeCommunicationsOnline</li><li>""SharePointDefaultDomain</li><li>""FullRedelegation</li><li>""SharePointPublic</li><li>""OrgIdAuthentication</li><li>""Yammer</li><li>""Intune</li></ul><br/><br/>这些值中的大多数都是只读的。 其中您可以添加/删除使用 Graph API 的值包括 ︰<ul><li>"电子邮件"</li><li>""OfficeCommunicationsOnline</li><li>""Yammer</li></ul><br/><br/>**说明**︰ 不可为 null |

**导航属性**

Name | 源多重性 | 收件人 | 目标多重性 | 描述
-----|-----|-----|-----|-----
serviceConfigurationRecords | * | [DomainDnsRecord] | * | 客户端之前要添加到域的 DNS 区域文件可由 Microsoft Online services 域的 DNS 记录。
verificationDnsRecords | * | [DomainDnsRecord] | * | 客户所具有的客户可以完成与 Azure AD 域所有权验证之前，将添加到域的 DNS 区域文件的 DNS 记录。

---
 
###DomainDnsRecord 实体 （预览版） <a id="DomainDnsRecordEntity"> </a> 对于租户中每个域，您可能需要以之前可以由 Microsoft 在线服务使用域将 DNS 记录添加到域的 DNS 区域文件。   **DomainDnsRecord** 实体用于提供这种 DNS 记录。 基实体 [DomainDnsCnameRecord], ，[DomainDnsMxRecord], ，[DomainDnsSrvRecord] 和 [DomainDnsSrvRecord] 实体。

**重要**︰ 仅在 beta 版中可用。
####属性 **声明属性**

Name | 类型 | 读取<br/>(GET) | 描述
-----|-----|-----|-----
dnsRecordId | Edm.guid 更新 | 是 | 分配给此实体的唯一标识符。<br/><br/>**说明**︰ 不可为 null
步骤可选 | Edm.Boolean | 是 | 指示是否必须由 Microsoft Online Services 的域和正常运行的 DNS 主机上的客户配置此记录。<br/><br/>**说明**︰ 不可为 null
标签 | Edm.String | 是 | 指示在 DNS 主机上配置的 DNS 记录的名称时要使用的值。
recordType | Edm.String | 是 | 指示此实体所表示的 DNS 记录何种类型。 值可以是以下项之一 ︰<ul><li>""CName</li><li>""Mx</li><li>""Srv</li><li>""Txt</li></ul><br/><br/>**说明**︰ 键
supportedService | Edm.String | 是 | 指示哪个 Microsoft 联机服务或功能具有此 DNS 记录的依赖项。 可以是下列值之一 ︰<ul><li>**空**</li><li>"电子邮件"</li><li>""Sharepoint</li><li>""EmailInternalRelayOnly</li><li>""OfficeCommunicationsOnline</li><li>""SharePointDefaultDomain</li><li>""FullRedelegation</li><li>""SharePointPublic</li><li>""OrgIdAuthentication</li><li>""Yammer</li><li>""Intune</li></ul>
ttl | Edm.Int32 | 是 |  指示在 DNS 主机上配置的 DNS 记录的生存时间 (ttl) 属性时要使用的值。<br/><br/>**说明**︰ 不可为 null

---
 
###DomainDnsCnameRecord 实体 （预览版） <a id="DomainDnsCnameRecordEntity"> </a> 表示一条 CNAME 记录，需要对其添加到租户中对特定域的 DNS 区域文件。 继承自 [DomainDnsRecord] 实体。

**重要**︰ 仅在 beta 版中可用。
####属性 **声明属性**

Name | 类型 | 读取<br/>(GET) | 描述
-----|-----|-----|-----
canonicalName | Edm.String | 是 | 指示在 DNS 主机上配置的 CNAME 记录的规范名称时要使用的值。
dnsRecordId | Edm.guid 更新 | 是 | 分配给此实体的唯一标识符。<br/><br/>**说明**︰ 不可为 null
步骤可选 | Edm.Boolean | 是 | 指示是否必须由 Microsoft Online Services 的域和正常运行的 DNS 主机上的客户配置此 CNAME 记录。<br/><br/>**说明**︰ 不可为 null
标签 | Edm.String | 是 | 指示在 DNS 主机上配置的 CNAME 记录的名称时要使用的值。
recordType | Edm.String | 是 | 指示此实体所表示的 DNS 记录何种类型。 此值始终是"CName"。<br/><br/>**说明**︰ 键
supportedService | Edm.String | 是 | 指示哪个 Microsoft 联机服务或功能程序依赖于此 CNAME 记录。 可以是下列值之一 ︰<ul><li>**空**</li><li>"电子邮件"</li><li>""Sharepoint</li><li>""EmailInternalRelayOnly</li><li>""OfficeCommunicationsOnline</li><li>""SharePointDefaultDomain</li><li>""FullRedelegation</li><li>""SharePointPublic</li><li>""OrgIdAuthentication</li><li>""Yammer</li><li>""Intune</li></ul>
ttl | Edm.Int32 | 是 | 指示在 DNS 主机上配置的 CNAME 记录的生存时间 (ttl) 属性时要使用的值。<br/><br/>**说明**︰ 不可为 null

---
 
###DomainDnsMxRecord 实体 （预览版） <a id="DomainDnsMxRecordEntity"> </a> 表示 MX 记录，需要对其添加到租户中对特定域的 DNS 区域文件。 继承自 [DomainDnsRecord] 实体。

**重要**︰ 仅在 beta 版中可用。
####属性 **声明属性**

Name | 类型 | 读取<br/>(GET) | 描述
-----|-----|-----|-----
dnsRecordId | Edm.guid 更新 | 是 | 分配给此实体的唯一标识符。<br/><br/>**说明**︰ 不可为 null
步骤可选 | Edm.Boolean | 是 | 指示是否必须由 Microsoft Online Services 的域和正常运行的 DNS 主机上的客户配置此 MX 记录。<br/><br/>**说明**︰ 不可为 null
标签 | Edm.String | 是 | 在 DNS 主机上配置的 MX 记录的别名/主机/Name 属性时要使用的值。
mailExchange | Edm.String | 是 | 在 DNS 主机上配置该答案/目标/值的 MX 记录时要使用的值。
recordType | Edm.String | 是 | 指示此实体所表示的 DNS 记录何种类型。 此值始终是"Mx"。<br/><br/>**说明**︰ 键
首选项 | Edm.Int32 | 是 | 在 DNS 主机上配置的 MX 记录的首选项/优先级属性时要使用的值。
supportedService | Edm.String | 是 | 指示哪个 Microsoft 联机服务或功能程序依赖于此 CNAME 记录。 可以是下列值之一 ︰<ul><li>**空**</li><li>"电子邮件"</li><li>""Sharepoint</li><li>""EmailInternalRelayOnly</li><li>""OfficeCommunicationsOnline</li><li>""SharePointDefaultDomain</li><li>""FullRedelegation</li><li>""SharePointPublic</li><li>""OrgIdAuthentication</li><li>""Yammer</li><li>""Intune</li></ul>
ttl | Edm.Int32 | 是 | 在 DNS 主机上配置的 MX 记录的生存时间 (ttl) 属性时要使用的值。<br/><br/>**说明**︰ 不可为 null

---
 
###DomainDnsSrvRecord 实体 （预览版） <a id="DomainDnsSrvRecordEntity"> </a> 表示 SRV 记录，需要对其添加到租户中对特定域的 DNS 区域文件。 继承自 [DomainDnsRecord] 实体。

**重要**︰ 仅在 beta 版中可用。
####属性 **声明属性**

Name | 类型 | 读取<br/>(GET) | 描述
-----|-----|-----|-----
dnsRecordId | Edm.guid 更新 | 是 | 分配给此实体的唯一标识符。<br/><br/>**说明**︰ 不可为 null
步骤可选 | Edm.Boolean | 是 | 指示是否必须由 Microsoft Online Services 的域和正常运行的 DNS 主机上的客户配置此 SRV 记录。<br/><br/>**说明**︰ 不可为 null
标签 | Edm.String | 是 | 值配置时要使用 **名称** SRV 记录的 DNS 主机的属性。
nameTarget | Edm.String | 是 | 值配置时要使用 **目标** SRV 记录的 DNS 主机的属性。
端口 | Edm.Int32 | 是 | 值配置时要使用 **端口** SRV 记录的 DNS 主机的属性。
优先级 | Edm.Int32 | 是 | 值配置时要使用 **优先级** SRV 记录的 DNS 主机的属性。
协议 | Edm.String | 是 | 值配置时要使用 **协议** SRV 记录的 DNS 主机的属性。
recordType | Edm.String | 是 | 指示此实体所表示的 DNS 记录何种类型。 此值始终是"Srv"。<br/><br/>**说明**︰ 键
服务 | Edm.String | 是 | 值配置时要使用 **服务** SRV 记录的 DNS 主机的属性。
supportedService | Edm.String | 是 | 指示哪个 Microsoft 联机服务或功能具有此 SRV 记录的依赖项。 可以是下列值之一 ︰<ul><li>**空**</li><li>"电子邮件"</li><li>""Sharepoint</li><li>""EmailInternalRelayOnly</li><li>""OfficeCommunicationsOnline</li><li>""SharePointDefaultDomain</li><li>""FullRedelegation</li><li>""SharePointPublic</li><li>""OrgIdAuthentication</li><li>""Yammer</li><li>""Intune</li></ul>
ttl | Edm.Int32 | 是 | 值配置时要使用 **生存时间** SRV 记录的 DNS 主机的属性。<br/><br/>**说明**︰ 不可为 null
权重 | Edm.Int32 | 是 | 值配置时要使用 **权重** SRV 记录的 DNS 主机的属性。

---
 
###DomainDnsTxtRecord 实体 （预览版） <a id="DomainDnsTxtRecordEntity"> </a> 表示 TXT 记录，需要对其添加到租户中对特定域的 DNS 区域文件。 继承自 [DomainDnsRecord] 实体。

**重要**︰ 仅在 beta 版中可用。
####属性 **声明属性**

Name | 类型 | 读取<br/>(GET) | 描述
-----|-----|-----|-----
dnsRecordId | Edm.guid 更新 | 是 | 分配给此实体的唯一标识符。<br/><br/>**说明**︰ 不可为 null
步骤可选 | Edm.Boolean | 是 | 指示是否必须由 Microsoft Online Services 的域和正常运行的 DNS 主机上的客户配置此 MX 记录。<br/><br/>**说明**︰ 不可为 null
标签 | Edm.String | 是 | 在 DNS 主机上配置的 MX 记录的别名/主机/Name 属性时要使用的值。
recordType | Edm.String | 是 | 指示此实体所表示的 DNS 记录何种类型。 此值始终是"Mx"。<br/><br/>**说明**︰ 键
supportedService | Edm.String | 是 | 指示哪个 Microsoft 联机服务或功能程序依赖于此 CNAME 记录。 可以是下列值之一 ︰<ul><li>**空**</li><li>"电子邮件"</li><li>""Sharepoint</li><li>""EmailInternalRelayOnly</li><li>""OfficeCommunicationsOnline</li><li>""SharePointDefaultDomain</li><li>""FullRedelegation</li><li>""SharePointPublic</li><li>""OrgIdAuthentication</li><li>""Yammer</li><li>""Intune</li></ul>
文本 | Edm.String | 是 |  |        
ttl | Edm.Int32 | 是 | 值 （以秒为单位） 的 DNS 主机配置 TXT 记录的生存时间属性时使用。<br/><br/>**说明**︰ 不可为 null


---
 
###DomainDnsUnavailableRecord 实体 （预览版） <a id="DomainDnsUnavailableRecordEntity"> </a> 继承自 [DomainDnsRecord] 实体。 在查询的导航属性 **serviceConfigurationRecords** 为 [域] 实体，可能会收到一个或多个 [DomainDnsCnameRecord], ，[DomainDnsMxRecord], ，[DomainDnsSrvRecord] 和/或 [DomainDnsTxtRecord] 实体。 这些实体表示之前，必须添加到区域文件的域名，可以由 Microsoft 在线服务使用域的 DNS 记录。 不能生成此类实体时 **DomainDnsUnavailableRecord** 改为返回实体。 

**重要**︰ 仅在 beta 版中可用。
####属性 **声明属性**

Name | 类型 | 读取<br/>(GET) | 描述
-----|-----|-----|-----
description | Edm.String | 是 | 为什么提供原因 **DomainDnsUnavailableRecord** 实体，并返回。

---

### ExtensionProperty 实体 <a id="ExtensionPropertyEntity"> </a>
允许应用程序来定义和使用的一组可以不需要外部数据存储区的应用程序将添加到目录对象 （用户、 组、 租户详细信息、 设备、 应用程序和服务主体） 的其他属性。 有关扩展属性的详细信息，请参阅 [Directory 架构扩展]。 继承自 [DirectoryObject]。

**重要**: **ExtensionProperty** 版本 1.5 中引入。

#### 属性
**声明的属性**

|  Name |  类型 |  创建 (POST) |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| appDisplayName | Edm.String | 否 | 是 | 否 |  |
| 数据类型 | Edm.String | 可选 | 是 | 是 | 指定要添加的目录扩展属性的类型。 支持的类型包括 ︰ 整数、 LargeInteger、 DateTime （必须在指定 ISO 8601-DateTime 以 UTC 存储）、 二进制、 布尔值和字符串。 |
| deletionTimestamp | Edm.DateTime | 否 | 是  | 否 | 此属性不是有效的扩展属性，并始终返回 **null**。 继承自 [DirectoryObject]。  |
| objectId | Edm.String | 否 | 是 | 否 | 权限作用域的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 否 | 是 | 否 | 一个字符串，标识对象类型。 对于扩展属性的值始终为"ExtensionProperty"。 继承自 [DirectoryObject]。 |
| name | Edm.String | 可选 | 是 | 是 | 指定的目录扩展属性的显示名称。<br/><br/> **说明**︰ 不可为 null。  |
| isSyncedFromOnPremises | Edm.Boolean | 否 | 是 | 否 | 指示是否已从本地目录同步的扩展属性。<br/><br/> **说明**︰ 不可为 null。  |
| targetObjects | Collection （edm.string) | 可选 | 是 | 是 | 目录扩展属性添加到目录对象。 可以扩展的支持的目录实体包括:"用户"、"组"、"TenantDetail"、"设备"、"应用程序"和"ServicePrincipal"<br/><br/> **说明**︰ 不可为 null。  |

**导航属性**   
无。

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

---

### 组实体 <a id="GroupEntity"> </a>
表示 Azure Active Directory 组。 继承自 [DirectoryObject]。
#### 属性
**声明的属性**

|  Name |  类型 |  创建 (POST) |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| deletionTimestamp | Edm.DateTime | 否 | 是 | 否 | 此属性不是有效的组，并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| description | Edm.String | 可选 | 是 | 是 | 组的可选说明。 |
| dirSyncEnabled | Edm.Boolean | 否 | 可筛选  | 否 | **true** 如果从本地目录; 同步此对象 **false** 如果此对象最初从本地目录同步，但不能再同步; **null** 如果永远不会从本地目录 （默认值） 同步此对象。 |
| displayName | Edm.String | 必需 | 可筛选  | 是 | 组的显示名称。 此属性是必需的当创建一个组，而且不能在更新过程中清除它。  |
| lastDirSyncTime | Edm.DateTime | 否 | 可筛选  | 否 | 指示对象上次同步与在本地目录的最后一个时间。 |
| mail | Edm.String | 否 | 可筛选  | 否 | 对于组，例如，"serviceadmins@contoso.onmicrosoft.com"SMTP 地址。 |
| mailEnabled | Edm.Boolean | 必需 | 是 | 是 | 指定是否已启用邮件的组。 如果 **securityEnabled** 属性也是 **true**, ，则该组是一个已启用邮件的安全组; 否则，组是 Microsoft Exchange 分发组。 可以使用 Azure AD Graph 创建只有 （纯） 安全组。 对于这一原因，该属性必须设置 **false** 时创建组和它不能更新使用 Azure AD Graph。 |
| mailNickname | Edm.String | 必需 | 可筛选  | 是 | 组的邮件别名。 创建组时，必须指定此属性。 |
| objectId | Edm.String | 否 | 是 | 否 | 组的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 否 | 是 | 否 | 一个字符串，标识对象类型。 对于组，该值始终为"Group"。 继承自 [DirectoryObject]。 |
| onPremisesSecurityIdentifier | 字符串 |  | 是 |  | 从本地同步到云的组包含在本地安全标识符 (SID)。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| 实体的 {4>provisioningerrors | 集合 ([ProvisioningError]) | 否 | 是 | 否 | 正在阻止成功设置此组的错误详细信息的集合。<br/><br/> **说明**︰ 不可为 null。  |
| proxyAddresses | Collection （edm.string) | 否 | 可筛选  | 否 | <br/><br/> **说明**︰ 不可为 null， **任何** 操作员是必需的筛选器表达式多值属性; 有关详细信息，请参阅 [支持查询、 筛选和分页选项]。  |
| securityEnabled | Edm.Boolean | 必需 | 可筛选  | 是 | 指定组是否为安全组。 如果 mailEnabled 属性也是如此，组是已启用邮件的安全组;否则，它是一个安全组。 可以使用 Azure AD Graph 创建只有 （纯） 安全组。 对于这一原因，该属性必须设置 **true** 创建组时。 |

**导航属性**   

|  Name |  源多重性 |  收件人 |  目标多重性 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| 成员 | \* | [DirectoryObject]<br/><br/> (仅 [联系人], ，[组], ，[ServicePrincipal], ，和 [用户] 支持对象) | \* | 用户、 联系人、 组和作为此组的成员的服务主体。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ GET （适用于所有组），POST （适用于安全组和已启用邮件的安全组），DELETE （仅适用于安全组） |
| memberOf | \* | [DirectoryObject]<br/><br/> (仅 [组] 支持对象) | \* | 此组所在的组。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ GET （适用于所有组）  |
| 所有者 | \* | [DirectoryObject] | \* | 组的所有者。 所有者是一组非管理员用户，他们有权修改此对象。 需要 2013年-11-08 版或更高版本。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ GET （适用于所有组），POST （适用于安全组和已启用邮件的安全组），DELETE （仅适用于安全组） |
| appRoleAssignments | \* | [DirectoryObject] | \* | 包含一组分配给应用程序组。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| extensionProperties | \* | [DirectoryObject] | \* | 包含与应用程序关联的扩展属性。 <br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对用户 （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰ 

- 创建 (POST): 仅适用于安全组。
- 读取 (GET): 适用于所有组。
- 更新 (PATCH): 仅适用于安全组和已启用邮件的安全组。 并非所有属性都可以进行都更新。
- 删除 (DELETE): 仅适用于安全组。

对组导航属性支持以下操作 ︰ 

- 读取 (GET): 适用于所有组。
- 更新 (POST): 仅适用于安全组和已启用邮件的安全组。 （成员并且仅限于所有者。）
- 删除 (DELETE): 仅适用于安全组。 （成员并且仅限于所有者。）

可能会对组调用以下操作和函数 ︰

- [checkMemberGroups] 来检查列表中的组的组的成员身份。 检查是可传递。
- [getAvailableExtensionProperties] 返回为一组已注册的扩展属性的列表。 需要版本 1.5 或更高版本。
- [getMemberGroups] 返回一组的成员组的列表。 检查是可传递。
- [isMemberOf]: 检查组是否为指定组的成员。 检查是可传递。

#### 备注

- 有三种类型的组 ︰ 邮件分发组 (**mailEnabled** 属性 **true** 和 **securityEnabled** 属性 **false**); 已启用邮件的安全组 (**mailEnabled** 属性 **true** 和 **securityEnabled** 属性 **true**); 和 （纯） 安全组 (**mailEnabled** 属性 **false** 和 **securityEnabled** 属性 **true**)。
- 您只能创建安全组使用 Graph API （您不能创建已启用邮件的安全组或邮件分发组）。 出于此原因 **mailEnabled** 属性必须设置 **false** 和 **securityEnabled** 属性必须设置 **true** 创建组时。
- 创建安全组使用 Graph API 时，必须指定标记为必需的所有属性。 这些属性是 ︰ **displayName**, ，**mailNickname**, ，**mailEnabled** (**false**)， **securityEnabled** (**true**)。
- 无法更新到已启用邮件的安全组或邮件分发组使用 Graph API 的安全组的组。

---

### OAuth2PermissionGrant 实体 <a id="OAuth2PermissionGrantEntity"> </a>
表示对用户或管理员同意过程的一部分 （由服务主体） 的应用程序已被授予的 OAuth 2.0 委托权限作用域。 

**重要**︰ 从版本 1.5，开始 **权限** 实体类型已重命名为 **OAuth2PermissionGrant**。 在版本 1.5 中，同意过程中创建的权限添加到 **权限** 属性的用户或服务主体。
#### 属性
**声明的属性**

| 属性 | 类型 | 创建 (POST) | 读取 (GET) | 更新 (PATCH) | 描述 |
|:-----|:-----|:-----|:-----|:-----|:-----|
| clientId | Edm.String | 可选 | 是 | 否 | 指定 **objectId** 的服务主体授予同意模拟用户在访问资源时 (由表示 **resourceId**)。 |
| {1>consenttype | Edm.String | 可选 | 是 | 否 | 指定许可由管理员代表组织提供的还是由个人提供。 可能的值为"AllPrincipals"Principal"。 |
| expiryTime | Edm.DateTime | 可选 | 是 | 是 | ±ЈБф。 返回 **null**。 请勿使用。 |
| objectId | Edm.String | 否 | 是 | 否 | 权限作用域的唯一标识符。<br/><br/> **说明**: **密钥**, ，不可为 null。  |
| principalId | Edm.String | 可选 | 是 | 否 | 如果 **{1>consenttype** 为"AllPrincipals"此值为 null，并且同意将应用于组织中的所有用户。 如果 **{1>consenttype** 为"Principal"，则此属性指定 **objectId** 授予许可，并且只适用于该用户的用户。 |
| resourceId | Edm.String | 可选 | 是 | 否 | 指定 **objectId** 向其授予访问权限的资源服务主体。 |
| 作用域 | Edm.String | 可选 | 是 | 是 | 在 OAuth 2.0 访问令牌中指定的资源应用程序应期望的作用域声明的值。 |
| startTime | Edm.DateTime | 可选 | 是 | 否 | ±ЈБф。 返回 **null**。 请勿使用。 |

**导航属性**   
无。

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对权限作用域 （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰ 

- 创建 (POST)
- 读取 (GET)
- 更新 (PATCH): **范围** 只属性。
- 删除 (DELETE)

可以对权限作用域调用任何函数或操作。
####备注
- 在 1.5 版和更高版本， **oauth2PermissionGrants** 导航属性 **用户** 实体和 **ServicePrincipal** 实体返回 **OAuth2PermissionGrant** 与用户或服务主体关联的对象。
- 在版本 1.5 之前, **权限** 导航属性 **用户** 实体和 **ServicePrincipal** 实体返回 **权限** 与用户或服务主体关联的对象。

---

### 服务主体实体 <a id="ServicePrincipalEntity"> </a>
表示一个目录中的应用程序的实例。 继承自 [DirectoryObject]。
#### 属性
**声明的属性**

|  Name |  类型 |  创建 (POST) |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| accountEnabled | Edm.Boolean | 可选 | 可筛选 | 是 | **true** 服务主体帐户，则启用; 否则为如果 **false**。  |
| appDisplayName | Edm.String | 否 | 是 | 否 | 关联的应用程序公开的显示名称。 |
| 应用程序 Id | Edm.guid 更新 | 必需 | 可筛选 | 是 | 关联的应用程序的唯一标识符 (其 **appId** 属性)。 |
| appOwnerTenantId | Edm.guid 更新 | 否 | 是 | 否 |  |
| {1>approleassignmentrequired | Edm.Boolean | 可选 |  | 是 | 指定是否 **AppRoleAssignment** 给用户或组之前需要 Azure AD 将向应用程序颁发用户或访问令牌。<br/><br/> **说明**︰ 需要 1.5 版或更高版本，不可为 null。  |
| 实体的 {3>approles | 集合 ([AppRole]) |  | 是 |  | 关联的应用程序公开的应用程序角色。 有关详细信息请参阅 **appRoles** 上的属性定义 [应用程序] 实体<br/><br/> **说明**︰ 需要 1.5 版或更高版本，不可为 null。  |
| authenticationPolicy |  [ServicePrincipalAuthenticationPolicy]  |  | 是 |  | 保留仅供内部使用。 请勿使用。 版本 1.5 中删除。<br/><br/> **说明**︰ 在仅限版本 2013年-11-08 中可用。  |
| deletionTimestamp | Edm.DateTime | 否 | 是 | 否 | 此属性不是有效的服务主体，并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| displayName | Edm.String | 可选 | 可筛选 | 是 | 服务主体的显示名称。 |
| errorUrl | Edm.String | 可选 | 是 | 是 |  |
| 主页 | Edm.String | 可选 | 是 | 是 | 关联应用程序主页的 URL。 |
| 实体的 {3>keycredentials | 集合 ([KeyCredential]) | 可选 |  | 是 | 与服务主体相关联的密钥凭据的集合。<br/><br/> **说明**︰ 不可为 null。  |
| 注销 Url | Edm.String | 可选 | 是 | 是 |  |
| oauth2Permissions | 集合 ([OAuth2Permission]) | 否 | 是 | 否 | 关联的应用程序公开的 OAuth 2.0 权限。 有关详细信息请参阅 **oauth2Permissions** 上的属性定义 [应用程序] 实体。<br/><br/> **说明**︰ 需要 1.5 版或更高版本，不可为 null。  |
| objectId | Edm.String | 否 | 是 | 否 | 服务主体的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 否 | 是 | 否 | 一个字符串，标识对象类型。 对于服务主体值始终为"ServicePrincipal"。 继承自 [DirectoryObject]。 |
| 实体的 {3>passwordcredentials | 集合 ([PasswordCredential]) | 可选 | 是 | 是 | 与服务主体关联的密码凭据的集合。<br/><br/> **说明**︰ 不可为 null。  |
| preferredTokenSigningKeyThumbprint | Edm.String | 是 | 是 | 是 | 保留仅供内部使用。 不要编写或依赖于此属性。 可能在将来版本中删除。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| publisherName | Edm.String | 可选 | 可筛选 | 是 | 在其中指定关联的应用程序的租户的显示名称。 |
| replyUrls | Collection （edm.string) | 可选 | 是 | 是 | 将用户令牌发送到的登录关联的应用程序或重定向 Uri OAuth 2.0 授权代码和访问令牌发送到关联的应用程序的 Url。<br/><br/> **说明**︰ 不可为 null。  |
| samlMetadataUrl | Edm.String | 可选 | 是 | 是 |  |
| servicePrincipalNames | Collection （edm.string) | 可选 | 可筛选  | 是 | 用于标识关联的应用程序的 Uri。 有关详细信息，请参阅 [应用程序对象和服务主体对象](https://msdn.microsoft.com/en-us/library/azure/dn132633.aspx)。<br/><br/> **说明**︰ 不可为 null， **任何** 操作员是必需的筛选器表达式多值属性; 有关详细信息，请参阅 [支持查询、 筛选和分页选项]。  |
| 标记 | Collection （edm.string) | 可选 | 可筛选  | 是 | <br/><br/> **说明**︰ 不可为 null。  |

**导航属性**   

|  Name |  源多重性 |  收件人 |  目标多重性 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| appRoleAssignedTo | \* | [AppRoleAssignment] | \* | 主体 （用户、 组和服务主体） 分配给此服务主体。 需要版本 1.5 或更高版本。 |
| appRoleAssignments | \* | [AppRoleAssignment] | \* | 服务主体分配到的应用程序。 需要版本 1.5 或更高版本。 |
| {1>createdobjects | \* | [DirectoryObject] | \* | 创建的此服务主体的目录对象。 继承自 [DirectoryObject]。 需要 2013年-11-08 版或更高版本。 |
| memberOf | \* | [DirectoryObject]<br/><br/> (仅 [DirectoryRole] 和 [组] 支持对象) | \* | 角色和组，此服务主体是直接的成员。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ 获取 |
| oauth2PermissionGrants | \* |  [OAuth2PermissionGrant]  | \* | 与此服务主体关联的用户模拟授权。 需要版本 1.5 或更高版本。 |
| {1>ownedobjects | \* | [DirectoryObject] | \* | 此服务主体所拥有的目录对象。 继承自 [DirectoryObject]。 需要 2013年-11-08 版或更高版本。 |
| 所有者 | \* | [DirectoryObject] | \* | 此服务主体所有者的目录对象。 所有者是一组非管理员用户，他们有权修改此对象。 继承自 [DirectoryObject]。 需要 2013年-11-08 版或更高版本。 |
| 权限 | \* | **权限** | \* | 重命名为 **oauth2PermissionGrants** 1.5 和更高版本中。 在早期版本中指向与服务主体关联的权限。 璝惠 **权限** 实体类型，请参阅 [OAuth2PermissionGrant]。 |

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对服务主体 （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰ 

- 创建 (POST)
- 读取 (GET)
- 更新 (PATCH)
- 删除 (DELETE)

对导航属性支持以下操作 ︰

- 读取 (GET)

可能会对组调用以下操作和函数 ︰

- [checkMemberGroups] 来检查服务主体的列表中的组的成员身份。 检查是可传递。
- [getMemberGroups] 返回服务主体的成员所属组的列表。 检查是可传递。
- [getMemberObjects] 若要返回的服务主体是其成员的组和目录角色的列表。 检查是可传递。

主体必须属于公司管理员角色才能对服务主体执行操作。 
###说明您必须设置 **appId** 属性设置为在创建服务主体的目录中的应用程序的 ID。

---

### SubscribedSku 实体 <a id="SubscribedSkuEntity"> </a>
仅读取的操作支持对订阅的 Sku;创建、 更新和删除不支持。 不支持查询筛选器表达式。 继承自 [DirectoryObject]。
#### 属性
**声明的属性**

| 属性 | 类型 | 读取 (GET) | 描述 |
|:-----|:-----|:-----|
| capabilityStatus | Edm.String | 是 |  |
| {1>consumedunits | Edm.Int32 | 是 |  |
| deletionTimestamp | Edm.DateTime | 是 | 此属性不能用于订阅的 Sku 并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| objectId | Edm.String | 是 | <br/><br/> **说明**: **密钥**, ，不可为 null  |
| prepaidUnits |  [LicenseUnitsDetail]  | 是 |  |
| servicePlans | 集合 ([ServicePlanInfo]) | 是 | <br/><br/> **说明**︰ 不可为 null  |
| skuId | Edm.guid 更新 | 是 |  |
| skuPartNumber | Edm.String | 是 |  |

**导航属性**   
无。

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对订阅的 Sku （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰

- 读取 (GET)

订阅的 Sku 不公开任何导航属性。 

可以对订阅的 Sku 调用任何函数或操作。

---

### TenantDetail 实体 <a id="TenantDetailEntity"> </a>
表示 Azure Active Directory 租户。 只能将读取和更新操作支持对租户;创建和删除不受支持。 继承 [DirectoryOjbect]。
#### 属性
**声明的属性**

|  Name |  类型 |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| 实体的 {3>assignedplans | 集合 ([AssignedPlan]) | 是 | 否 | 服务计划与租户关联的集合。<br/><br/> **说明**︰ 不可为 null。  |
| city | Edm.String |  | 否 |  |
| companyLastDirSyncTime | Edm.DateTime | 是 | 否 | 时间和日期该处租户上次上次与本地目录同步。 |
| country | Edm.String | 是 | 否 |  |
| countryLetterCode | Edm.String | 是 | 否 |  |
| deletionTimestamp | Edm.DateTime | 是 | 否 | 此属性不是有效的租户，并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| dirSyncEnabled | Edm.Boolean | 是 | 否 | **true** 如果从本地目录; 同步此对象 **false** 如果此对象最初从本地目录同步，但不能再同步; **null** 如果永远不会从本地目录 （默认值） 同步此对象。 |
| displayName | Edm.String | 是 | 否 | 个租户的显示名称。 |
| marketingNotificationEmails | Collection （edm.string)  | 是 | 可选 | <br/><br/> **说明**︰ 不可为 null。  |
| objectId | Edm.String | 是 | 否 | 租户的的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 是 | 否 | 一个字符串，标识对象类型。 租户使用的值始终为"公司"。 继承自 [DirectoryObject]。 |
| postalCode | Edm.String | 是 | 否 |  |
| preferredLanguage | Edm.String |  | 否 |  |
| 实体的 {3>provisionedplans | 集合 ([ProvisionedPlan]) | 是 | 否 | <br/><br/> **说明**︰ 不可为 null。  |
| 实体的 {4>provisioningerrors | 集合 ([ProvisioningError]) | 是 | 否 | <br/><br/> **说明**︰ 不可为 null。  |
| state | Edm.String | 是 | 否 |  |
| 街道 | Edm.String | 是 | 否 |  |
| technicalNotificationMails | Collection （edm.string) | 是 | 可选 | <br/><br/> **说明**︰ 不可为 null。  |
| telephoneNumber | Edm.String | 是 | 否 |  |
| tenantType | Edm.String | 是 | 否 | <br/><br/> **说明**︰ 版本 1.5 中已删除和更高版本。  |
| 实体的 {2>verifieddomains | 集合 ([VerifiedDomain]) | 是 | 否 | 与此 tenant 关联的域的集合。<br/><br/> **说明**︰ 不可为 null。  |

**导航属性**   
无。

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对租户 （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰ 

- 读取 (GET)
- 更新 (PATCH);仅 **{1>marketingnotificationmails** 和 **technicalNotificationMails** 属性可以使用 Graph API 进行更新。

租户不公开任何导航属性。 

可以对租户调用任何函数或操作。
####备注

- 无法创建或删除租户使用 Graph API。
- 仅 **{1>marketingnotificationmails** 和 **technicalNotificationMails** 属性可以使用 Graph API 进行更新。
- 对租户不支持查询筛选器表达式。

---

### 用户实体 <a id="UserEntity"> </a>
表示 Azure AD 用户帐户。 继承自 [DirectoryObject]。
#### 属性
**声明的属性**

|  Name |  类型 |  创建 (POST) |  读取 (GET) |  更新 (PATCH) |  描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| accountEnabled | Edm.Boolean | 必需 | 可筛选 | 是 | **true** 如果帐户是启用; 否则为 **false**。 创建用户时，此属性是必需的。  |
| assignedLicenses | 集合 ([AssignedLicense]) | 可选 | 是 | 是 | 向用户分配许可证。<br/><br/> **说明**︰ 不可为 null。  |
| 实体的 {3>assignedplans | 集合 ([AssignedPlan]) | 否 | 是 | 否 | 可分配给用户的计划。<br/><br/> **说明**︰ 不可为 null。  |
| city | Edm.String | 可选 | 可筛选 | 是 | 用户所在的城市。 |
| country | Edm.String | 可选 | 可筛选 | 是 | 国家/地区的用户所在;例如，"美国"或"UK"。 |
| deletionTimestamp | Edm.DateTime | 否 | 是 | 否 | 此属性不是有效的用户，并始终返回 **null**。 继承自 [DirectoryObject]。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| department | Edm.String | 可选 | 可筛选 | 是 | 有关用户的工作的部门名称。 |
| dirSyncEnabled | Edm.Boolean | 否 | 可筛选 | 否 | **true** 如果从本地目录; 同步此对象 **false** 如果此对象最初从本地目录同步，但不能再同步; **null** 如果永远不会从本地目录 （默认值） 同步此对象。  |
| displayName | Edm.String | 必需 | 可筛选 | 是，但不能清除 | 用户的通讯簿中显示的名称。 这通常是名字的用户、 中间名和姓的组合。 此属性是必需的当创建用户并不能在更新过程中清除。 |
| facsimileTelephoneNumber | Edm.String | 可选 | 是 | 是 | 用户的业务传真机的电话号码。 |
| givenName | Edm.String | 可选 | 可筛选  | 是 | 给定名称 （名字） 的用户。 |
| immutableId | Edm.String | 如果为 UPN 使用联合的域，必需的 | 可筛选 | 是 | 此属性用于将关联到其 Azure AD 用户对象的内部部署 Active Directory 用户帐户。 必须指定此属性，则在 Graph 中创建新的用户帐户，如果正在使用用户的联合的域时 **userPrincipalName** (UPN) 属性。<br/><br/> **重要提示 ︰**  **$** 和 **_** 指定此属性时，不能使用字符。 <br/><br/> **说明**︰ 需要 2013年-11-08 版或更高版本。  |
| jobTitle | Edm.String | 可选 | 可筛选 | 是 | 用户的职务。 |
| lastDirSyncTime | Edm.DateTime | 否 | 可筛选 | 否 | 指示对象上次同步与在本地目录中; 最后一次例如:"2013年-02-16T03:04:54Z"  |
| mail | Edm.String | 可选 | 可筛选 | 否 | 对于用户，例如"jeff@contoso.onmicrosoft.com"SMTP 地址。 |
| mailNickname | Edm.String | 必需 | 可筛选  | 是 | 用户的邮件别名。 创建用户时，必须指定此属性。 |
| mobile | Edm.String | 可选 | 是 | 是 | 用户的主移动电话号码。 |
| objectId | Edm.guid 更新 | 否 | 是 | 否 | 用户的唯一标识符。 继承自 [DirectoryObject]。<br/><br/> **说明**: **密钥**, 、 不可变，不可为 null，唯一。  |
| 对象类型 | Edm.String | 否 | 是 | 否 | 一个字符串，标识对象类型。 对于用户值始终是"User"。 继承自 [DirectoryObject]。 |
| onPremisesSecurityIdentifier | Edm.String | 否 | 是 | 否 | 包含从本地同步到云的用户在本地安全标识符 (SID)。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| otherMails | Collection （edm.string) | 可选 | 可筛选  | 是 | 为用户; 其他电子邮件地址的列表例如: ["bob@contoso.com"，"Robert@fabrikam.com"]。<br/><br/> **说明**︰ 不可为 null， **任何** 操作员是必需的筛选器表达式多值属性; 有关详细信息，请参阅 [支持查询、 筛选和分页选项]。  |
| passwordPolicies | Edm.String | 可选 | 是 | 是 | 指定用户的密码策略。 此值是一个包含一个可能的值为"DisableStrongPassword"，允许较弱的密码比默认策略指定的枚举。 此外可以指定"DisablePasswordExpiration"。 两个可能在一起; 指定例如:"DisablePasswordExpiration，DisableStrongPassword"。 |
| passwordProfile |  [PasswordProfile]  | 必需 | 是 | 是 | 指定用户的密码配置文件。 该配置文件包含用户的密码。 创建用户时，此属性是必需的。<br/><br/> 配置文件中的密码必须满足所指定的最低要求 **密码策略** 属性。 默认情况下，一个强密码是必需的。 有关强密码必须满足的约束的信息，请参阅 **密码策略** 下 [更改您的密码](http://onlinehelp.microsoft.com/office365-enterprises/ff637578.aspx) Microsoft Office 365 中帮助页。  |
| physicalDeliveryOfficeName | Edm.String | 可选 | 是 | 是 | 中的业务用户营业场所的办公地点。 |
| postalCode | Edm.String | 可选 | 是 | 是 | 用户通信地址的邮政编码。 特定于用户的国家/地区的邮政编码。 在美国，此属性包含邮政编码。 |
| preferredLanguage | Edm.String | 可选 | 是 | 是 | 用于用户的首选的语言。 应遵循 ISO 639-1 代码;例如，"EN-US"。 |
| 实体的 {3>provisionedplans | 集合 ([ProvisionedPlan]) | 否 | 是 | 否 | 可为用户设置的计划。<br/><br/> **说明**︰ 不可为 null。  |
| 实体的 {4>provisioningerrors | 集合 ([ProvisioningError]) | 否 | 是 | 否 | 正在阻止成功设置此用户的错误详细信息的集合。 |
| proxyAddresses | Collection （edm.string) | 否 | 可筛选 | 否 | 例如: ["SMTP: bob@contoso.com"，"smtp: bob@sales.contoso.com"]<br/><br/> **说明**︰ 唯一，不可为 null， **任何** 操作员是必需的筛选器表达式多值属性; 有关详细信息，请参阅 [支持查询、 筛选和分页选项]。  |
| sipProxyAddress | Edm.String | 否 | 是 | 否 | 指定语音的用户的 IP (VOIP) 会话发起协议 (SIP) 地址。<br/><br/> **说明**︰ 需要 1.5 版或更高版本。  |
| state | Edm.String | 可选 | 可筛选 | 是 | 省市自治区中用户的地址。 |
| streetAddress | Edm.String | 可选 | 是 | 是 | 业务用户营业场所的街道地址。 |
| surname | Edm.String | 可选 | 可筛选 | 是 | 用户的姓氏 （家族名称或姓）。<br/><br/> **说明**︰ 可筛选。  |
| telephoneNumber | Edm.String | 可选 | 是 | 是 | 业务用户营业场所的主电话号码。 |
| thumbnailPhoto | Edm.Stream | 可选 | 是 | 是 | 要为用户显示的缩略图照片。<br/><br/> **说明**︰ 不可为 null。  |
| usageLocation | Edm.String | 可选 | 可筛选 | 是 | 双字母国家/地区代码 (ISO 标准 3166)。 所需的用户将被分配了许可证根据法律要求，若要检查的国家/地区中的服务的可用性。 示例包括:"美国"、"JP"和"GB"。<br/><br/> **说明**︰ 不可为 null。  |
| userPrincipalName | Edm.String | 必需 | 可筛选 | 是 | 用户主体名称 (UPN) 的用户。 UPN 是由用户根据 Internet 标准 RFC 822 Internet 样式登录名。 按照约定，这应映射到用户的电子邮件名称。 常规格式为"alias@domain"，其中域必须存在于租户的已验证域的集合。 创建用户时，此属性是必需的。 <br/><br/> 可以从访问租户的已验证的域 **实体的 {2>verifieddomains** 属性 [TenantDetail]。 <br/><br/> **说明**: **密钥**, 的、 具有唯一性。  |
| userType | Edm.String | 可选 | 可筛选 | 是 | 一个字符串值，可以用于在目录中，如"成员"和"来宾"的用户类型进行分类。<br/><br/> **说明**︰ 需要 2013年-11-08 版或更高版本。  |

**导航属性**   

|  Name |  源多重性 |  收件人 |  目标多重性 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| manager | \* | [DirectoryObject]<br/><br/> (只有用户和 [联系人] 支持对象。) | 0..1 | 用户或为此用户的经理的联系人中。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ GET、 PUT、 DELETE |
| directReports | \* | [DirectoryObject]<br/><br/> (只有用户和 [联系人] 支持对象。) | \* | 用户和报告给用户的联系人中。 （用户和具有其 manager 属性设置为此用户的联系人。）继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ 获取 |
| memberOf | \* | [DirectoryObject]<br/><br/> (仅 [组] 和 [DirectoryRole] 支持对象。) | \* | 组和用户所在的目录角色中。 继承自 [DirectoryObject]。<br/><br/> HTTP 方法 ︰ 获取 |
| ownedDevices | \* |  [设备]  | \* | 由用户拥有的设备。 |
| 权限 | \* | **权限** | \* | 与用户关联的权限。 该属性已重命名为 **oauth2PermissionGrants** 和 **权限** 实体重命名为 [OAuth2PermissionGrant] 1.5 和更高版本中。 请参阅的文档 **OAuth2PermssionGrant** 有关的文档 **权限** 实体类型。<br/><br/>  |
| registeredDevices | \* |  [设备]  | \* | 注册的设备的用户。 |
| {1>createdobjects | \* |  [DirectoryObject]  | \* | 由用户创建的目录对象。 需要 2013年-11-08 版或更高版本。 |
| {1>ownedobjects | \* |  [DirectoryObject]  | \* | 由用户拥有的目录对象。 需要 2013年-11-08 版或更高版本。 |
| appRoleAssignments | \* |  [AppRoleAssignment]  | \* | 此用户分配给应用程序集。 需要版本 1.5 或更高版本。<br/><br/> HTTP 方法 ︰ GET、 POST、 删除 |
| oauth2PermissionGrants | \* |  [OAuth2PermissionGrant]  | \* | 授权同意模拟此用户的应用程序集。 需要版本 1.5 或更高版本。<br/><br/> HTTP 方法 ︰ GET、 POST、 删除 |

**注意 ︰** 不支持未列出的继承导航属性。 请求发送到不受支持的导航属性返回 **400 错误的请求**。 

#### 支持的操作
对用户 （用于每种的 HTTP 方法位于括号中） 支持以下操作 ︰ 

- 创建 (POST)
- 读取 (GET)
- 更新 (PATCH)
- 删除 (DELETE)

对用户导航属性; 支持以下操作支持对每个导航属性并不是所有操作。

- 读取 (GET)
- 更新 (PUT)
- 删除 (DELETE)

可对用户调用以下操作和函数 ︰

- [assignLicense] 来分配和/或从用户中删除指定的许可证列表。 需要 2013年-11-08 版或更高版本。
- [checkMemberGroups] 来检查用户的列表中的组的成员身份。 检查是可传递。
- [getAvailableExtensionProperties] 返回已为用户注册的扩展属性的列表。 需要版本 1.5 或更高版本。
- [getMemberGroups] 若要返回的用户所在的组列表。 检查是可传递。
- [getMemberObjects] 若要返回的组和用户所在的目录角色的列表。 检查是可传递。
- [isMemberOf] 若要检查用户是否为指定组的成员。 检查是可传递。

####备注

- 最低限度上，您必须指定以下属性创建用户时 ︰ **accountEnabled**, ，**displayName**, ，**mailNickname**, ，**passwordProfile**, ，和 **userPrincipalName**。 中指定的密码 **passwordProfile** 属性必须满足租户的密码复杂性要求。 有关详细信息，请参阅 **密码策略** 属性。
- 在 2013年-11-08 版和更高， **immutableId** 时在 Graph 中创建新的用户帐户，如果您正在使用用户的联合的域，必须指定属性 **userPrincipalName** (UPN) 属性。
-  **DisplayName** 属性不能在更新时清除。
-  **PasswordProfile** 属性始终返回 **null**。 这是为了防止显示用户的密码。 可以通过更新用户的密码重置 **passwordProfile** 属性。
- 除了标准寻址可用于所有目录实体，用户可能会解决使用 **userPrincipalName** 属性; 例如， `https://graph.windows.net/contoso.onmicrosoft.com/users/john@contoso.onmicrosoft.com?api-version=1.5`。

---

## 复杂类型引用

### AlternativeSecurityId 类型 <a id="AlternativeSecurityIdType"> </a>
包含与设备相关联的替代安全 ID。  **AlternativeSecurityIds** 属性 [设备] 实体是一套 **AlternativeSecurityId**。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| identityProvider | Edm.String |  |  |  |
| key | Edm.Binary |  |  |  |
| 类型 | Edm.Int32 |  |  |  |

---

### AppRole 类型 <a id="AppRoleType"> </a>
表示调用另一个应用程序的客户端应用程序可能请求，或者可能用于分配给用户或组指定的应用程序角色中的应用程序的应用程序角色。  **AppRoles** 属性 [ServicePrincipal] 实体和 [应用程序] 实体是一套 **AppRole**。

**重要**︰ 需要 1.5 版或更高版本。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| allowedMemberTypes | Collection （edm.string) | 不可为 null | RW | 设置"应用程序"，或者对二者同时指定此应用程序角色定义可以通过设置为"用户"或其他应用程序 （即访问此应用程序在后台服务方案中的） 分配给用户和组。 |
| description | Edm.String  |  | RW | 权限帮助文本，将出现在管理应用程序分配，并同意体验。 |
| displayName | Edm.String |  | RW | 在管理员同意和应用程序分配体验中显示的权限的显示名称。 |
| id | Edm.guid 更新 |  | RW | 唯一角色标识符 **appRoles** 集合。 |
| isEnabled | Edm.Boolean |  | RW | 当创建或更新角色定义，这必须设置为 **true** （这是默认值）。 若要删除一个角色，这必须首先将设置为 **false**。 此时，在后续调用中，可能会删除此角色。 |
| value | Edm.String |  | RW | 在身份验证和访问令牌中指定的角色声明的应用程序应期望的值。 |

---

### AssignedLicense 类型 <a id="AssignedLicenseType"> </a>
表示分配给用户的许可证。  **AssignedLicenses** 属性 [用户] 实体是一套 **AssignedLicense**。
####属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| disabledPlans | Collection(Edm.Guid) | 不可为 null | R | 已禁用的计划的唯一标识符的集合。 |
| skuId | Edm.guid 更新 |  | R | Sku 的唯一标识符。 |

---

### AssignedPlan 类型 <a id="AssignedPlanType"> </a>
 **实体的 {3>assignedplans** 属性均 [用户] 实体和 [TenantDetail] 实体是一套 **AssignedPlan**。
####属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| assignedTimestamp | Edm.DateTime |  | R | 日期和时间的分配计划时;例如 ︰ 2013年-01-02T19:32:30Z。 |
| capabilityStatus | Edm.String |  | R | 例如，"已启用"。 |
| 分析 | Edm.String |  | R | 服务; 的名称例如，"AccessControlServiceS2S"。 |
| servicePlanId | Edm.guid 更新 |  | R | 标识服务计划的 GUID。 |

---

### KeyCredential 类型 <a id="KeyCredentialType"> </a>
包含与应用程序或服务主体相关联的密钥凭据。  **实体的 {3>keycredentials** 属性 [应用程序] 和 [ServicePrincipal] 实体是一个集合 **KeyCredential**。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| customKeyIdentifier | Edm.Binary |  |  |  |
| 结束日期 | Edm.DateTime |  |  | 过期日期和时间的凭据。 |
| keyId | Edm.guid 更新 |  |  | 唯一标识符 (GUID) 的密钥。 |
| 起始日期 | Edm.DateTime |  |  | 日期和时间凭据生效。 |
| 类型 | Edm.String |  |  | 类型的密钥凭据;例如，"Symmetric"。 |
| 使用情况 | Edm.String |  |  | 一个字符串，描述的目的，可以使用该密钥;例如，"验证"。 |
| value | Edm.String |  |  |  |

---

### LicenseUnitsDetail 类型 <a id="LicenseUnitsDetailType"> </a>
 **PrepaidUnits** 属性 [SubscribedSku] 实体属于类型 **LicenseUnitsDetail**。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| 已启用 | Edm.Int32 |  |  |  |
| 挂起 | Edm.Int32 |  |  |  |
| 警告 | Edm.Int32 |  |  |  |

---

### OAuth2Permission 类型 <a id="OAuth2PermissionType"> </a>
表示一个 OAuth 2.0 委托权限作用域。 指定的 OAuth 2.0 委托的权限作用域的客户端应用程序可以请求 (通过 **requiredResourceAccess** 集合 [应用程序] 对象) 时调用资源应用程序。  **Oauth2Permissions** 属性 [ServicePrincipal] 实体和 [应用程序] 实体是一套 **OAuth2Permission**。

**重要**︰ 需要 1.5 版或更高版本。
#### 属性
|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| adminConsentDescription | Edm.String |  | RW | 在管理员同意和应用程序分配体验中显示的权限帮助文本。 |
| adminConsentDisplayName | Edm.String |  | RW | 在管理员同意和应用程序分配体验中显示的权限的显示名称。 |
| id | Edm。 Guid |  | RW | Oauth2Permissions 集合的唯一作用域权限标识符。 |
| isEnabled | Edm.Boolean | 不可为 null | RW | 当创建或更新权限时，此属性必须设置为 **true** （这是默认值）。 要删除权限，必须首先将此属性设置为 **false**。 此时，在后续调用中，可能会删除权限。 |
| 类型 | Edm.String |  | RW | 指定是否此作用域权限可以由同意最终用户，或者是否必须同意由公司管理员的租户范围权限。 可能的值为"User"或"Admin"。 |
| userConsentDescription | Edm.String |  | RW | 将出现在最终用户同意体验的权限帮助文本。 |
| userConsentDisplayName | Edm.String |  | RW | 将出现在最终用户同意体验的权限的显示名称。 |
| value | Edm.String |  | RW | 资源应用程序应在 OAuth 2.0 访问令牌中的作用域声明的值。 |

---

### PasswordCredential 类型 <a id="PasswordCredentialType"> </a>
包含与应用程序或服务主体关联的密码凭据。  **实体的 {3>passwordcredentials** 属性 [ServicePrincipal] 实体和 [应用程序] 实体是一套 **PasswordCredential**。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| customKeyIdentifier | Edm.Binary |  |  |  |
| 结束日期 | Edm.DateTime |  |  | 日期和密码的到期的时间。 |
| keyId | Edm.guid 更新 |  |  |  |
| 起始日期 | Edm.DateTime |  |  | 日期和时间密码生效。 |
| value | Edm.String |  |  |  |

---

### PasswordProfile 类型 <a id="PasswordProfileType"> </a>
包含与用户关联的密码配置文件。  **PasswordProfile** 属性 [用户] 实体是 **PasswordProfile** 对象。
####属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| password | Edm.String |  | RW | 用户的密码。 创建用户时，此属性是必需的。 可以得到更新，但用户将需要更改在下次登录密码。 <br/><br/> 密码必须满足所指定的用户的最小值要求 **密码策略** 属性。 默认情况下，一个强密码是必需的。 |
| forceChangePasswordNextLogin | Edm.Boolean |  | RW | **true** 如果用户必须更改她的密码在下次登录; 否则为 **false**。  |

---

### ProvisionedPlan 类型 <a id="ProvisionedPlanType"> </a>
 **实体的 {3>provisionedplans** 属性 [用户] 实体和 [TenantDetail] 实体是一套 **ProvisionedPlan**。
#### 属性
|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| capabilityStatus | Edm.String |  | R | 例如，"已启用"。 |
| provisioningStatus | Edm.String |  | R | 例如，"成功"。 |
| 分析 | Edm.String |  | R | 服务; 的名称例如，"AccessControlS2S" |

---

### ProvisioningError 类型 <a id="ProvisioningErrorType"> </a>
 **实体的 {4>provisioningerrors** 属性 [联系人], ，[用户], ，和 [组] 实体是一个集合 **ProvisioningError**。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| errorDetail | Edm.String |  | R | 错误的说明。 |
| 已解决 | Edm.Boolean |  | R | **true** 如果错误是解析; 否则为 **false**。  |
| 服务实例 | Edm.String |  | R | 服务实例发生错误。  |
| timestamp | Edm.DateTime |  | R | 日期和时间出现了错误。 |

---

### RequiredResourceAccess 类型 <a id="RequiredResourceAccessType"> </a>
指定 OAuth 2.0 权限作用域和应用程序需要访问的指定资源下的应用程序角色的集。 客户端应用程序可以请求指定的 OAuth 2.0 权限作用域 (通过 **requiredResourceAccess** 集合) 时调用资源应用程序。  **RequiredResourceAccess** 属性 [应用程序] 实体是一套 **ReqiredResourceAccess**。

**重要**︰ 需要 1.5 版或更高版本。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| resourceAppId | Edm.String |  | RW | 应用程序需要访问资源的唯一标识符。 这应该等于 **appId** 目标资源应用程序上声明。 |
| resourceAccess | 集合 ([ResourceAccess]) | 不可为 null | RW | OAuth2.0 权限作用域和应用程序需要从指定的资源的应用程序角色的列表。 |

---

### ResourceAccess 类型 <a id="ResourceAccessType"> </a>
指定的 OAuth 2.0 权限作用域或应用程序需要应用程序角色。  **ResourceAccess** 属性 [RequiredResourceAccess] 类型是一套 **ResourceAccess**。

**重要**︰ 需要 1.5 版或更高版本。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| id | Edm.guid 更新 | 不可为 null | RW | 其中一个的唯一标识符 [OAuth2Permission] 或 [AppRole] 资源应用程序公开的实例。 |
| 类型 | Edm.String  | | RW | 指定是否 **id** 属性引用 [OAuth2Permission] 或 [AppRole]。 可能值为"作用域"或"角色"。 |

---

### ServicePlanInfo 类型 <a id="ServicePlanInfoType"> </a>
包含有关与订阅的 SKU 关联的服务计划信息。  **ServicePlans** 属性 [SubscribedSku] 实体是一套 **ServicePlanInfo**。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| servicePlanId | Edm.guid 更新 |  |  | 服务计划的唯一标识符。 |
| servicePlanName | Edm.String |  |  | 服务计划的名称。 |

---

### ServicePrincipalAuthenticationPolicy 类型 <a id="ServicePrincipalAuthenticationPolicyType"> </a>
包含服务主体的身份验证策略。

**重要**︰ 仅在版本 2013年-11-08; 中可用但其保留为仅限内部使用，已在 1.5 和更高版本中删除。
#### 属性

|  Name |  类型 |  注意 |  读/写 |  描述 |
|:-------|:-------|:-------|:-------|:-------|
| defaultPolicy | Edm.String |  | R/W | 保留仅供内部使用。 请勿使用。 版本 1.5 中删除。 |
| allowedPolicies | Collection （edm.string) | 不可为 null | R/W | 保留仅供内部使用。 请勿使用。 版本 1.5 中删除。 |

---

### VerifiedDomain 类型 <a id="VerifiedDomainType"> </a>
指定租户的域。  **实体的 {2>verifieddomains** 属性 [TenantDetail] 实体是一套 **VerifiedDomain**。
####属性

|  Name |  类型 |  注意 |  读/写 |  在 bpos_api 中 |  描述 |
|:-------|:-------|:-------|:-------|:-------|:-------|
| 功能 | Edm.String |  | R | 是 | 例如，"Email"、"OfficeCommunicationsOnline"。 |
| 默认 | Edm.Boolean |  | R | 是 | **true** 如果这是默认域与租户; 否则为 **false**。  |
| id | Edm.String |  | R | 是 | 例如，"00057FFE80187238"。 |
| 初始 | Edm.Boolean |  | R | 是 |  |
| name | Edm.String |  | R | 是 | 域名;例如，"contoso.onmicrosoft.com" |
| 类型 | Edm.String |  | R | 是 | 例如，"管理"。 |

##其他资源

- 了解有关 Graph API 的详细信息支持的功能、 功能和 [Graph API 概念] 中的预览功能


[应用程序]: #ApplicationEntity
[AppRoleAssignment]: #AppRoleAssignmentEntity
[联系人]: #ContactEntity
[协定]: #ContractEntity
[设备]: #DeviceEntity
[DirectoryLinkChange]: #DirectoryLinkChangeEntity
[DirectoryObject]: #DirectoryObjectEntity
[DirectoryRole]: #DirectoryRoleEntity
[DirectoryRoleTemplate]: #DirectoryRoleTemplateEntity
[Domain]: #DomainEntity
[DomainDnsRecord]: #DomainDnsRecordEntity
[DomainDnsCnameRecord]: #DomainDnsCnameRecordEntity
[DomainDnsMxRecord]: #DomainDnsMxRecordEntity
[DomainDnsSrvRecord]: #DomainDnsSrvRecordEntity
[DomainDnsTxtRecord]: #DomainDnsTxtRecordEntity
[DomainDnsUnavailableRecord]: #DomainDnsUnavailableRecordEntity
[ExtensionProperty]: #ExtensionPropertyEntity
[组]: #GroupEntity
[OAuth2PermissionGrant]: #OAuth2PermissionGrantEntity
[服务主体]: #ServicePrincipalEntity
[SubscribedSku]: #SubscribedSkuEntity
[TenantDetail]: #TenantDetailEntity
[用户]: #UserEntity

[AlternativeSecurityId]: #AlternativeSecurityIdType
[AppRole]: #AppRoleType
[AssignedLicense]: #AssignedLicenseType
[AssignedPlan]: #AssignedPlanType
[KeyCredential]: #KeyCredentialType
[LicenseUnitsDetail]: #LicenseUnitsDetailType
[OAuth2Permission]: #OAuth2PermissionType
[PasswordCredential]: #PasswordCredentialType
[PasswordProfile]: #PasswordProfileType
[ProvisionedPlan]: #ProvisionedPlanType
[ProvisioningError]: #ProvisioningErrorType
[RequiredResourceAccess]: #RequiredResourceAccessType
[ResourceAccess]: #ResourceAccessType
[ServicePlanInfo]: #ServicePlanInfoType
[ServicePrincipalAuthenticationPolicy]: #ServicePrincipalAuthenticationPolicyType
[VerifiedDomain]: #VerifiedDomainType
    
[在 Azure 上 Azure.com 上的 graph API 快速入门]: https://azure.microsoft.com/documentation/articles/active-directory-graph-api-quickstart/


<!--HONumber=May16_HO4-->


