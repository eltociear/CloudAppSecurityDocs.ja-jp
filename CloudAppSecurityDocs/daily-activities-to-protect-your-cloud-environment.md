---
title: Cloud App Security ダッシュボードの操作
description: この記事では、Cloud App Security ダッシュボードの基本的な使用方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: c5c5dfb141347b1a08f850335c82e54393bbf4c6
ms.sourcegitcommit: 7b6124e5ecb3fa8fc1176d89e06b052f2a53a310
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83854254"
---
# <a name="working-with-the-dashboard"></a>ダッシュボードの操作

*適用対象:Microsoft Cloud App Security*

この記事では、Cloud App Security で日常行う必要があることについて説明します。  

## <a name="check-the-dashboard"></a>ダッシュボードを確認する

ダッシュボードに表示される情報は、組織に関するすべての最も重要な情報の概要です。 各情報カードには、表示された情報をより詳細に調査するためのリンクがあります。 また、指定されたフィルターを使用して、特定のアプリのダッシュボード情報を表示するように選択することもできます。

![Cloud App Security ダッシュボード](media/dashboard-enhanced.png)

### <a name="what-can-you-expect-to-see-in-the-dashboard"></a>ダッシュボードに表示される情報

- **オープン アラート**  
オープン アラートの数、アラートの状態の分布を示すグラフ、および最近のアラートが表示されます

- **検出されたアプリ**  
検出されたアプリの数、アプリのリスク分布のグラフ、およびトラフィックごとの上位のアプリ カテゴリが表示されます。
- **Top users to investigate** (調査対象の上位ユーザー)  
調査対象のユーザーの数、および調査の優先順位が最も高いユーザーが表示されます。
- **アプリの条件付きアクセス制御**  
アプリの条件付きアクセス制御によって保護されているアプリの数、および過去 30 日間の保護されたセッションとアクションの数が表示されます。
- **アプリ コネクタの状態**  
API で接続されたアプリ インスタンスの数とその状態が表示されます。
- **Files infected with malware** (マルウェアに感染したファイル)  
マルウェアに感染したファイルの数が表示されます。
- **Privileged Office 365 OAuth apps** (特権付きの Office 365 OAuth アプリ)  
非常に高い権限のアクセス許可を付与された、使用頻度の低い OAuth アプリの数が表示されます。
- **Azure のセキュリティ構成**  
Azure のセキュリティ構成に関するレコメンデーションの数と重要度が表示されます。
- **AWS のセキュリティ構成**  
AWS のセキュリティ構成に関するレコメンデーションの数と重要度が表示されます。
- **DLP アラート**  
過去 30 日間の DLP アラートのグラフが表示されます。
<!-- - **Activity map**  
Shows the global spread of activities performed by users over the last 30 days. -->

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [アラートの調査](investigate.md)

[!INCLUDE [Open support ticket](includes/support.md)]
