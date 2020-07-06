---
title: フェッチ - Activities API
description: この記事では、Cloud App Security の Activities API のフェッチ要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 17e5d65219e883b5c89f5c799cf02e9825d20dc5
ms.sourcegitcommit: 286f8d5d940d1bb9a09daa3070ac4fc3768208f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84505641"
---
# <a name="fetch---activities-api"></a>フェッチ - Activities API

*適用対象:Microsoft Cloud App Security*

指定した主キーと一致するアクティビティをフェッチする GET 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
GET /api/v1/activities/<pk>/
```

## <a name="request-url-parameters"></a>要求 URL のパラメーター

| パラメーター | [説明] |
| --- | --- |
| pk | アクティビティの ID |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:<your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/activities/<pk>/"
```

### <a name="response"></a>[応答]

指定したアクティビティを JSON 形式で返します。

```json
{
  // activity record
}
```

[!INCLUDE [Open support ticket](includes/support.md)]
