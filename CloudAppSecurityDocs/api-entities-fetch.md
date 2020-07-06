---
title: フェッチ - Entities API
description: この記事では、Cloud App Security の Entities API のフェッチ要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 536fe23d089d450c3ac1ce5bbfefb08dfb2ad383
ms.sourcegitcommit: 286f8d5d940d1bb9a09daa3070ac4fc3768208f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84505201"
---
# <a name="fetch---entities-api"></a>フェッチ - Entities API

*適用対象:Microsoft Cloud App Security*

> [!NOTE]
> この要求は、Office 365 Cloud App Security では使用できません。

指定した主キーと一致するエンティティをフェッチする GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/entities/<pk>/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | エンティティの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:<your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/entities/<pk>/"
```

### <a name="response"></a>[応答]

指定したエンティティを JSON 形式で返します。

```json
{
  // entity record
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
