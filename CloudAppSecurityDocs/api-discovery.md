---
title: Cloud App Security Cloud Discovery API
description: この記事では、Cloud Discovery API の使用方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/27/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: cloud-app-security
ms.suite: ems
ms.openlocfilehash: 647570edd98fd1fd4977a9096fcf475f3ee09a8e
ms.sourcegitcommit: 286f8d5d940d1bb9a09daa3070ac4fc3768208f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84505251"
---
# <a name="cloud-discovery-api"></a>Cloud Discovery API

*適用対象:Microsoft Cloud App Security*

Cloud Discovery を使用すると、ユーザーから提供されたシステム ログを解析し、クラウド環境内の新規および不明なアプリケーションを検出できます。 会社の検出ログ ファイルのアップロードを自動化するには、Cloud Discovery API を使用します。 ファイルのアップロード プロセスは、連続して呼び出す必要がある 3 つの API 呼び出しで構成されています。

さらに、Cloud App Security を使用すると、既存のオンプレミスのセキュリティ アプライアンスを使用して、承認されていないアプリへのアクセスをブロックできます。 専用のブロック スクリプトを取得し、アプライアンスにインポートするには、ブロック スクリプトの生成呼び出しを使用します。

サポートされている要求は次のとおりです。

- [ファイルのアップロードの開始](api-discovery-initiate.md)
- [ファイルのアップロードの実行](api-discovery-perform.md)
- [ファイルのアップロードの最終処理](api-discovery-finalize.md)
- [ブロック スクリプトの生成](api-discovery-script.md)

[!INCLUDE [Open support ticket](includes/support.md)]
