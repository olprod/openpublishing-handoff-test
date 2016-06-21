---
uid: graph.windows.net/myorganization/Contacts/1.6
title: 对联系人的 azure AD Graph API 操作
ms.TocTitle: Operations on contacts
ms.ContentId: 477161a7-aebf-4d4b-981d-fcbc148e25c1
ms.topic: reference (API)
ms.date: 01/26/2016
sections:
  - graph.windows.net/myorganization/Contacts/1.6/get contacts
  - graph.windows.net/myorganization/Contacts/1.6/get contact by id
  - graph.windows.net/myorganization/Contacts/1.6/update contact
  - graph.windows.net/myorganization/Contacts/1.6/delete contact
  - graph.windows.net/myorganization/Contacts/1.6/get contact manager link
  - graph.windows.net/myorganization/Contacts/1.6/update contact manager
  - graph.windows.net/myorganization/Contacts/1.6/get contact direct reports links
  - graph.windows.net/myorganization/Contacts/1.6/get contact memberOf links
---

# 对联系人的操作 |Graph API 参考


 _**适用于 ︰** API 的关系图 |Azure Active Directory_


<a id="Overview"> </a>
本主题讨论如何执行对组织使用 Azure Active Directory (AD) Graph API 的联系人的操作。 组织联系人通常表示对贵公司或组织外部的用户。 它们是不同于 O365 Outlook 个人联系人。 借助 Azure AD Graph API 中，您可以阅读组织的联系信息以及它们与其他目录对象，如它们的管理器、 组成员身份和直接下属的关系。 编写组织联系人的能力仅限于那些当前尚未从内部部署目录同步的联系人 ( **dirSyncEnabled** 属性是  **null** 或 **false**)。 为此类联系人，可以更新或删除联系人本身或其 manager 属性。 不能使用 Graph API 创建组织的联系人。 有关组织的联系人，包括如何在你的租户中创建的详细信息请参阅 [联系人]。

Graph API 是一个基于 REST 的 API，提供对在 Azure Active Directory，如用户、 组、 组织联系人和应用程序的目录对象的编程访问。

> [!IMPORTANT] 它也可通过 azure AD Graph API 功能 [Microsoft Graph](https://graph.microsoft.io/), ，如 Outlook、 OneDrive、 OneNote、 计划者和 Office 关系图中，通过使用单个访问令牌的单个终结点访问所有服务的一个统一的 API，它还包括来自其他 Microsoft Api。

## 对联系人执行 REST 操作

若要执行对组织联系人使用 Graph API 的操作，您向发送 HTTP 请求使用支持的方法 （GET、 POST、 PATCH、 PUT、 或 DELETE） 了面向联系人资源集合、 特定联系人、 联系人、 或函数的导航属性的终结点或可以对联系人调用的操作。

Graph API 请求使用的以下基本 URL:
```no-highlight
https://graph.windows.net/{tenant_id}/{resource_path}?{api_version}[odata_query_parameters]
```

> [!IMPORTANT]
> 发送到 Graph API 的请求必须是格式良好，目标的有效的终结点和 Graph API 版本，而执行从 Azure AD 中获得一个有效的访问令牌及其 `Authorization` 标头。 有关如何创建请求和接收响应使用 Graph API 的更多详细信息，请参阅 [操作概述]。

您指定 `{resource_path}` 以不同的方式取决于是否在你的租户、 单个联系人或特定联系人的导航属性目标的所有联系人的集合。

- `/contacts` 以联系人资源集合为目标。 此资源路径可用于在你的租户中读取所有联系人的筛选的列表。
- `/contacts/{object_id}` 针对你的租户中的单个联系人。 使用其对象 ID (GUID) 指定的目标联系人。 您可以使用此资源路径来获取联系人的声明的属性。 对于尚未从本地目录同步的联系人，您可以使用此资源路径，若要修改的联系人、 声明的属性或删除联系人。
- `/contacts/{object_id}/{nav_property}` 针对指定的导航属性的联系人。 可用于返回对象或由指定联系人的目标导航属性引用的对象。 **请注意**︰ 读取的这种形式的寻址才可用。
- `/contacts/{object_id}/$links/{nav_property}` 针对指定的导航属性的联系人。 这种形式的寻址可用于读取和修改导航属性。 对于读取，为响应正文中的一个或多个链接返回该属性引用的对象。 可以修改仅管理器导航属性的未从本地目录同步的联系人。 该管理器指定为请求正文中的链接。

例如，以下请求将返回链接到指定的联系人管理器 ︰

```no-highlight
GET https://graph.windows.net/myorganization/contacts/a2fb3752-08b4-413d-af6f-1d99c4c131d9/$links/manager?api-version=1.6
```

## 对联系人的基本操作 <a id="BasicContactOperations"> </a>
通过定向联系人资源集合或特定联系人，可以执行对联系人进行读取的操作。 您可以更新并面向特定联系人从本地目录中删除不同步的联系人。 Graph API 不支持创建联系人。 也不支持更新或删除从本地目录同步的联系人 ( **dirSyncEnabled** 属性是 **true**)。 以下主题演示如何对联系人执行基本操作。

****

---
uid: graph.windows.net/myorganization/Contacts/1.6/get 联系 codeGenerator: true
---

### 获取联系人 <a id="GetContacts"> </a>
获取联系人的集合。 您可以对要进行筛选、 排序和分页响应的请求添加 OData 查询参数。 有关详细信息，请参阅 [支持查询、 筛选和分页选项]。

在成功时返回的集合 [联系人] 对象; 否则，响应正文将包含错误的详细信息。 有关错误的详细信息，请参阅 [错误代码和错误处理]。

****

---
uid ︰ 通过 id codeGenerator graph.windows.net/myorganization/Contacts/1.6/get 联系人 ︰ true
---

###获取联系人 <a id="GetAContact"> </a>

获取指定的联系人。 您可以使用对象 ID (GUID) 来标识目标联系人。

在成功时返回 [联系] 对象为指定联系人; 否则为响应正文包含错误的详细信息。 有关错误的详细信息，请参阅 [错误代码和错误处理]。

****
---
uid: graph.windows.net/myorganization/Contacts/1.6/update 联系人
---

### 更新联系人 <a id="UpdateContact"> </a>

更新联系人的属性。 指定任何可写 [联系人] 请求正文中的属性。 更改仅您指定的属性。 您可以更新未从本地目录同步的联系人 ( **dirSyncEnabled** 属性是 **null** 或 **false**)。

如果成功，则返回没有响应正文;否则，响应正文将包含错误的详细信息。 有关错误的详细信息，请参阅 [错误代码和错误处理]。

****
---
uid: graph.windows.net/myorganization/Contacts/1.6/delete 联系人
---
### 删除联系人 <a id="DeleteContact"> </a>

删除联系人。 可以从本地目录中删除不同步的联系人 ( **dirSyncEnabled** 属性是 **null** 或  **false**)。

如果成功，则返回没有响应正文;否则，响应正文将包含错误的详细信息。 有关错误的详细信息，请参阅 [错误代码和错误处理]。

****

## 对联系人导航属性操作 <a id="ContactNavigationOps"> </a>

联系人和联系人管理器、 直接组成员身份和直接报告等目录中的其他对象之间的关系是通过导航属性公开。 您可以阅读然后，针对在请求中的这些导航属性，在某些情况下，修改这些关系。

---
uid: graph.windows.net/myorganization/Contacts/1.6/get 联系人管理器链接 codeGenerator: true
---

### 获取一个联系人管理器 <a id="GetContactsManager"> </a>

获取从的联系人的经理 **manager** 导航属性。

成功时，将返回到链接 [用户] 或 [联系] 分配作为联系人的经理; 否则为响应正文包含错误的详细信息。 有关错误的详细信息，请参阅 [错误代码和错误处理]。

**请注意**︰ 您可以从要返回的 URL 中删除"$links"段 [用户] 或 [联系人] 对象而不是一个链接。

****

---
uid: graph.windows.net/myorganization/Contacts/1.6/update 联系人管理器
---
### 分配的联系人管理器 <a id="AssignContactsManager"> </a>

将分配一个联系人管理器通过 **manager** 属性。 被授予用户或联系人。 请求正文包含一个指向 [用户] 或 [联系人] 分配。 您可以更新未从本地目录同步的联系人的经理 ( **dirSyncEnabled** 属性是 **null** 或 **false**)。

如果成功，则返回没有响应正文;否则，响应正文将包含错误的详细信息。 有关错误的详细信息，请参阅 [错误代码和错误处理]。

****
---
uid: graph.windows.net/myorganization/Contacts/1.6/get 联系人的直接下属的链接 codeGenerator: true
---
### 获取联系人的直接下属 <a id="GetContactsDirectReports"> </a>

获取从联系人的直接下属 **directReports** 导航属性。

在成功时返回到链接的集合 [用户]的和 [联系]的针对其该联系人进行了更新管理器为已分配的; 否则为响应正文包含错误的详细信息。 有关错误的详细信息，请参阅 [错误代码和错误处理]。

**请注意**︰ 您可以从要返回的 URL 中删除"$links"段  [DirectoryObject]s 的用户和联系人而不是链接。

****
---
uid: graph.windows.net/myorganization/Contacts/1.6/get 联系人 memberOf 链接 codeGenerator: true
---
### 获取联系人的组成员身份 <a id="GetContactsMemberships"> </a>

获取从联系人的组成员身份 **memberOf** 导航属性。

此属性返回联系人是直接成员的组。 若要获取所有联系人都有直接或间接成员身份的组，请调用 [getMemberGroups] 函数。

在成功时返回到链接的集合 [组]s 此联系人的成员; 否则，响应正文将包含错误的详细信息。 有关错误的详细信息，请参阅 [错误代码和错误处理]。

**请注意**︰ 您可以从要返回的 URL 中删除"$links"段 [DirectoryObject]s 的组，而不是链接。

****
## 功能和对联系人的操作 <a id="ContactFunctions"> </a>
您可以对联系人调用以下任何功能。

### 检查 （可传递） 的特定组成员身份
您可以调用 [isMemberOf] 函数来检查特定组中的成员身份。 检查是可传递。

### 检查列表中的组 （可传递） 的成员身份
您可以调用 [checkMemberGroups] 函数来检查列表中的组的成员身份。 检查是可传递。

### 获取所有组成员身份 （可传递）
您可以调用 [getMemberGroups] 函数以返回联系人是其成员的所有组。 检查是可传递，与不同的是读取 [memberOf](#GetContactsMemberships) 导航属性，用于返回联系人是直接成员的组。

****

##其他资源

- 了解有关 Graph API 的详细信息支持的功能、 功能和 [Graph API 概念] 中的预览功能


[应用程序]: ./entity-and-complex-type-reference.md#ApplicationEntity
[AppRoleAssignment]: ./entity-and-complex-type-reference.md#AppRoleAssignmentEntity
[联系人]: ./entity-and-complex-type-reference.md#ContactEntity
[协定]: ./entity-and-complex-type-reference.md#ContractEntity
[设备]: ./entity-and-complex-type-reference.md#DeviceEntity
[DirectoryLinkChange]: ./entity-and-complex-type-reference.md#DirectoryLinkChangeEntity
[DirectoryObject]: ./entity-and-complex-type-reference.md#DirectoryObjectEntity
[DirectoryRole]: ./entity-and-complex-type-reference.md#DirectoryRoleEntity
[DirectoryRoleTemplate]: ./entity-and-complex-type-reference.md#DirectoryRoleTemplateEntity
[域 （预览版）]: ./entity-and-complex-type-reference.md#DomainEntity
[DomainDnsRecord]: ./entity-and-complex-type-reference.md#DomainDnsRecordEntity
[DomainDnsCnameRecord]: ./entity-and-complex-type-reference.md#DomainDnsCnameRecordEntity
[DomainDnsMxRecord]: ./entity-and-complex-type-reference.md#DomainDnsMxRecordEntity
[DomainDnsSrvRecord]: ./entity-and-complex-type-reference.md#DomainDnsSrvRecordEntity
[DomainDnsTxtRecord]: ./entity-and-complex-type-reference.md#DomainDnsTxtRecordEntity
[DomainDnsUnavailableRecord]: ./entity-and-complex-type-reference.md#DomainDnsUnavailableRecordEntity
[ExtensionProperty]: ./entity-and-complex-type-reference.md#ExtensionPropertyEntity
[组]: ./entity-and-complex-type-reference.md#GroupEntity
[OAuth2PermissionGrant]: ./entity-and-complex-type-reference.md#OAuth2PermissionGrantEntity
[服务主体]: ./entity-and-complex-type-reference.md#ServicePrincipalEntity
[SubscribedSku]: ./entity-and-complex-type-reference.md#SubscribedSkuEntity
[TenantDetail]: ./entity-and-complex-type-reference.md#TenantDetailEntity
[用户]: ./entity-and-complex-type-reference.md#UserEntity

[AlternativeSecurityId]: ./entity-and-complex-type-reference.md#AlternativeSecurityIdType
[AppRole]: ./entity-and-complex-type-reference.md#AppRoleType
[AssignedLicense]: ./entity-and-complex-type-reference.md#AssignedLicenseType
[AssignedPlan]: ./entity-and-complex-type-reference.md#AssignedPlanType
[KeyCredential]: ./entity-and-complex-type-reference.md#KeyCredentialType
[LicenseUnitsDetail]: ./entity-and-complex-type-reference.md#LicenseUnitsDetailType
[OAuth2Permission]: ./entity-and-complex-type-reference.md#OAuth2PermissionType
[PasswordCredential]: ./entity-and-complex-type-reference.md#PasswordCredentialType
[PasswordProfile]: ./entity-and-complex-type-reference.md#PasswordProfileType
[ProvisionedPlan]: ./entity-and-complex-type-reference.md#ProvisionedPlanType
[ProvisioningError]: ./entity-and-complex-type-reference.md#ProvisioningErrorType
[RequiredResourceAccess]: ./entity-and-complex-type-reference.md#RequiredResourceAccessType
[ResourceAccess]: ./entity-and-complex-type-reference.md#ResourceAccessType
[ServicePlanInfo]: ./entity-and-complex-type-reference.md#ServicePlanInfoType
[ServicePrincipalAuthenticationPolicy]: ./entity-and-complex-type-reference.md#ServicePrincipalAuthenticationPolicyType
[VerifiedDomain]: ./entity-and-complex-type-reference.md#VerifiedDomainType

[在 Azure 上 Azure.com 上的 graph API 快速入门]: https://azure.microsoft.com/documentation/articles/active-directory-graph-api-quickstart/

<!--HONumber=May16_HO4-->


