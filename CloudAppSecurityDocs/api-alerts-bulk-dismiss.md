---
title: 一括無視 - Alerts API
description: この記事では、Cloud App Security の Alerts API の一括無視要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 7caef6711d8e8dd526e0c684cdec72bce785db93
ms.sourcegitcommit: 286f8d5d940d1bb9a09daa3070ac4fc3768208f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84505571"
---
# <a name="bulk-dismiss---alerts-api"></a>一括無視 - Alerts API

*適用対象:Microsoft Cloud App Security*

指定したフィルターと一致する複数のアラートを無視する POST 要求を実行します。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/alerts/dismiss_bulk/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| filters | 要求に対してすべての検索フィルターを使用してオブジェクトをフィルター処理します。詳細については、[アラートのフィルター](api-alerts.md#filters)に関するページを参照してください |
| コメント | アラートが無視される理由に関するコメント |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:<your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/alerts/dismiss_bulk/" -d '{
  "comment": "Irrelevant",
  "filters": {
    "id": {
      "eq": [
        "55af7415f8a0a7a29eef2e1f",
        "55af741cf8a0a7a29eef2e20"
      ]
    }
  }
}'
```

[!INCLUDE [Open support ticket](includes/support.md)]
