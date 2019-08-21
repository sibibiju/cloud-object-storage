---

copyright:
  years: 2017, 2018, 2019
lastupdated: "2019-03-19"

keywords: glossary, getting started, terms

subcollection: cloud-object-storage

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:download: .download} 

# 主要术语
{: #terminology}

## 服务 (Service)
{: #terminology-service}

{{site.data.keyword.cloud}} Platform 独有的组件（例如，{{site.data.keyword.cos_full}}、Cloudant、Functions 等）。

## 资源 (Resource)
{: #terminology-resource}

您在 {{site.data.keyword.cloud_notm}} 中已创建的任何内容。资源可以是服务的实例、Kubernetes 集群、Object Storage 存储区、Cloud Foundry 应用程序或 {{site.data.keyword.cloud_notm}} Platform 中创建的其他几乎任何内容。对资源的访问使用 Identity and Access Management 策略进行控制。

## 资源实例/服务实例 (Resource instance/Service instance)
{: #terminology-service-instance}

云服务的实例。根据服务，这可能是多租户服务 ({{site.data.keyword.cos_short}}) 中的唯一实例或帐户。

## 资源实例标识/服务实例标识 (Resource instance ID/Service instance ID)
{: #terminology-service-instance-id}

创建或供应服务实例时，将按云资源名称 (CRN) 格式为该实例分配唯一标识：

```
crn:v1:bluemix:public:<service-name>:<region>:a/<account-id>:<resource-instance-GUID>:<resource-type>:<resource>
```

对于 {{site.data.keyword.cos_short}} 的实例，这可能类似于：

```
crn:v1:bluemix:public:cloud-object-storage:global:a/3bf0d9003abfb5d29761c3e97696b71c:d6f04d83-6c4f-4a62-a165-696756d63903::
```

## 服务凭证 (Service credential)
{: #terminology-service-credential}

服务凭证是开发者用于将应用程序连接到 Object Storage 实例的重要信息集合：

```json
{
  "apikey": "<apikey>",
  "endpoints": "https://control.cloud-object-storage.cloud.ibm.com/v2/endpoints",
  "iam_apikey_description": "<auto-generated-apikey-description>",
  "iam_apikey_name": "<auto-generated-apikey-description>",
  "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:<role>",
  "iam_serviceid_crn": "crn:v1:staging:public:iam-identity::a/<account-id>::serviceid:ServiceId-<GUID>",
  "resource_instance_id": "crn:v1:bluemix:public:cloud-object-storage:global:a//<account-id>:<resource-instance-GUID>::"
}
```

## 服务标识 (Service ID)
{: #terminology-service-id}

服务标识是一个抽象的用户，旨在供开发者用于标识访问 Object Storage 资源的应用程序（或应用程序的组件）。可以像对其他任何用户一样，为服务标识授予对资源的 IAM 角色。

## IAM 角色 (IAM roles)
{: #terminology-roles}

IAM 角色表示给定主体应该对给定资源具有的访问级别。有两种类型的角色：
  - 平台角色：使用 {{site.data.keyword.cloud_notm}} Platform 本身（管理帐户，创建实例，编写 IAM 策略）。
  - 服务角色：使用特定于服务的资源（访问存储区和对象）。

## 身份端点 (Identity endpoint)
{: #terminology-identity}

IAM 端点 (`iam.cloud.ibm.com`) 用于访存访问令牌以交换 API 密钥。此令牌在发送到 {{site.data.keyword.cos_short}} 服务端点的所有 REST API 请求的 `Authorization` 头中使用。

## 服务端点 (Service endpoints)
{: #terminology-service-endpoint}
[服务端点](/docs/services/cloud-object-storage?topic=cloud-object-storage-endpoints#endpoints)（例如，`s3.us-south.cloud-object-storage.appdomain.cloud`）是用于发送与数据交互的 API 请求的基本 URL。

## {{site.data.keyword.cos_short}} 存储区位置 (Object Storage bucket location)
{: #terminology-location}

{{site.data.keyword.cos_short}} 中的所有存储区的作用域均限定为一个位置。这是一个区域（例如，`us-south` 或 `us-east`）或者地理位置（例如，`eu-geo` 或 `us-geo`）。在此位置中，会对对象切片并将其分散在三个不同的物理位置。

## 区域 (Regions)
{: #terminology-region}
区域和位置通常可互换使用，但与 {{site.data.keyword.cloud_notm}} Platform 中提供的大部分服务不同，{{site.data.keyword.cos_short}} 是一个“全局”服务。{{site.data.keyword.cloud_notm}} Platform 存在于不同区域（例如，`美国南部`或`英国`）中，并且某些服务的作用域限定为其创建位置。虽然每个 {{site.data.keyword.cos_short}} 实例都会视为“全局”，但每个存储区都采用了位置、弹性和存储类的特定组合。

## {{site.data.keyword.cos_short}} 弹性 (Object Storage Resiliency)
{: #terminology-resiliency}

弹性是指在其中分布数据的地理区域的范围和规模。_跨区域_弹性是在多个大城市区域中分布数据，_区域_弹性是在单个大城市区域中分布数据。

## {{site.data.keyword.cos_short}} S3 密钥与 IAM API 密钥 (Object Storage S3 Keys vs. IAM API Key)
{: #terminology-auth}

作为 IaaS 供应的 {{site.data.keyword.cos_short}} 实例使用访问密钥和私钥对（称为 HMAC 密钥），而不是 {{site.data.keyword.cloud_notm}} IAM API 密钥。这些密钥对支持创建 AWS V4 签名以用于认证和授权，而不是创建 {{site.data.keyword.cloud_notm}} IAM 使用的 OAuth2 不记名令牌。虽然 IAM API 密钥支持的访问控制在强度和细颗粒度方面要高得多，但要使用与 S3 兼容的工具和网关（例如，AWS CLI 或 Cyberduck），需要 HMAC 密钥。