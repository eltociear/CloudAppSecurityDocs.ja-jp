---
title: ファイルのアップロードの最終処理 - Cloud Discovery API
description: この記事では、Cloud App Security の Cloud Discovery API の done_upload 要求について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 7013a7b079f39a88bc95d583622e2591a7c5a2af
ms.sourcegitcommit: 286f8d5d940d1bb9a09daa3070ac4fc3768208f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84505401"
---
# <a name="finalize-file-upload---cloud-discovery-api"></a>ファイルのアップロードの最終処理 - Cloud Discovery API

*適用対象:Microsoft Cloud App Security*

ファイル コンテンツのアップロードが正常に完了すると、ファイルの処理を開始するために通知されます。

## <a name="http-request"></a>HTTP 要求

```rest
POST /api/v1/discovery/done_upload/
```

## <a name="request-body-parameters"></a>要求本文のパラメーター

| パラメーター | [説明] |
| --- | --- |
| uploadUrl | ファイルのアップロードを要求する最初の呼び出しで返された URL。 |
| inputStreamName | データの受信元のデータ ソースの名前 (デバイスを表します)。 |
| uploadAsSnapshot | 継続的レポートにアップロードするのではなく、スナップショット レポートとしてデータをアップロードします。 このパラメーターが設定されている場合、inputStreamName で指定した名前を持つレポートが作成されます。 |

## <a name="example"></a>例

### <a name="request"></a>要求

要求の例を次に示します。

```rest
curl -XPOST -H "Authorization:<your_token_key>" "https://<tenant_id>.<tenant_region>.contoso.com/api/v1/discovery/done_upload/" -d "uploadUrl=<initiate_file_upload_response_url>"
```

[!INCLUDE [Open support ticket](includes/support.md)]
