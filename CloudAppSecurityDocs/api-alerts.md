---
title: Cloud App Security Alerts API
description: この記事では、Alerts API の使用方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 0363d275c764d1e92d8d3f295de82e0c5bd2143a
ms.sourcegitcommit: 286f8d5d940d1bb9a09daa3070ac4fc3768208f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84505441"
---
# <a name="alerts-api"></a>Alerts API

*適用対象:Microsoft Cloud App Security*

Alerts API を使用すると、Cloud App Security によって特定された、注意が必要な緊急リスクに関する情報を取得できます。 アラートは、不審な使用パターンや、会社のポリシーに違反するコンテンツを含むファイルから生成される可能性があります。

サポートされている要求は次のとおりです。

- [アラートの一覧表示](api-alerts-list.md)
- [一括無視](api-alerts-bulk-dismiss.md)
- [一括解決](api-alerts-bulk-resolve.md)
- [アラートのフェッチ](api-alerts-fetch.md)
- [アラートの無視](api-alerts-dismiss.md)
- [アラートを既読としてマークする](api-alerts-mark-read.md)
- [アラートを未読としてマークする](api-alerts-mark-unread.md)

## <a name="filters"></a>フィルタ

フィルターの動作の詳細については、「[フィルター](api-introduction.md#filters)」を参照してください。

サポートされているフィルターを次の表に示します。

| フィルター | Type | 演算子 | [説明] |
| --- | --- | --- | --- |
| entity.entity | entity pk | eq、neq | 指定したファイルに関連するアラートをフィルター処理します。 例: `[{ "id": "entity-id", "saas": 11161, "inst": 0 }]` |
| entity.ip | string | eq、neq | 指定した IP アドレスに関連するアラートをフィルター処理します |
| entity.service | integer | eq、neq | 指定したサービス appId に関連するアラートをフィルター処理します。例:11770 |
| entity.instance | integer | eq、neq | 指定したインスタンスに関連するアラートをフィルター処理します。例:11770、1059065 |
| entity.policy | string | eq、neq | 指定したポリシーに関連するアラートをフィルター処理します |
| entity.file | string | eq、neq | 指定したファイルに関連するアラートをフィルター処理します |
| severity | integer | eq、neq | 重要度でフィルター処理します。 次の値を指定できます。<br /><br />**0**:低<br />**1**:中間<br/>**2**:高 |
| resolutionStatus | integer | eq、neq | アラートの解決状態でフィルター処理します。次の値を指定できます。<br /><br />**0**:オープン<br />**1**:破棄<br />**2**:解決済み |
| read | boolean | eq | "true" に設定すると、既読のアラートのみが返され、"false" に設定すると、未読のアラートのみが返されます。 |
| date | timestamp | lte、gte、range、lte_ndays、gte_ndays | アラートがトリガーされた時刻でフィルター処理します |
| resolutionDate | timestamp | lte、gte、range | アラートが解決された時刻でフィルター処理します |
| risk | integer | eq、neq | リスクでフィルター処理します |
| alertType | integer | eq、neq | アラートの種類でフィルター処理します |
| ID | string | eq、neq | アラート ID でフィルター処理します |
| ソース | string | eq | アラートの生成元 (組み込みまたはポリシー) |

[!INCLUDE [Open support ticket](includes/support.md)]
