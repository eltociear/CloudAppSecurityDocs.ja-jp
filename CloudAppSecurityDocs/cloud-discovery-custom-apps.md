---
title: Cloud App Security で Cloud Discovery にカスタム アプリを追加する
description: このトピックでは、シャドウ IT を監視するために Cloud App Security で Cloud Discovery にカスタム アプリを追加する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 768248178042ecc7c3af5289ea1b6c27aa92b37e
ms.sourcegitcommit: 6eff466c7a6817b14a60d8c3b2c201c7ae4c2e2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74719241"
---
# <a name="add-custom-apps-to-cloud-discovery"></a>Cloud Discovery にカスタム アプリを追加する

*適用対象:Microsoft Cloud App Security*

Cloud Discovery では、Microsoft Cloud App Security のクラウド アプリ カタログに照らしてトラフィック ログが分析されます。 クラウド アプリ カタログには、16,000 を超えるクラウド アプリが記載されています。 カタログには、Cloud App Security によって可視性とリスク情報が提供される、公開されているクラウド アプリのみが含まれています。

クラウド アプリ カタログから除外されているクラウド アプリの可視性を得るため、Cloud App Security を使用すると、組織専用に開発または割り当てられたカスタム クラウド アプリ (LOB アプリ) の使用を検出できます。

新しいカスタム クラウド アプリを追加することによって、Cloud App Security では、アップロードされたファイアウォールと、アプリへのプロキシ トラフィック ログ メッセージが照合された後、Cloud Discovery ページにおいて組織全体でのこのアプリの使用に対する可視性が提供されます (アプリを使用しているユーザーの数、それを使用している一意のソース IP アドレスの数、アプリとの間で送受信されたトラフィックの量など)。

## <a name="add-a-new-custom-cloud-app"></a>新しいカスタム クラウド アプリを追加する

1. Cloud App Security ポータルで、 **[発見]** をクリックし、 **[Cloud Discovery dashboard]\(Cloud Discovery ダッシュボード\)** をクリックします。

    ![Cloud Discovery ダッシュボード メニュー](media/cloud-discovery-dashboard-menu.png)

2. 右上隅にある 3 つのドットをクリックし、 **[カスタム アプリの新規追加]** を選択します。

    ![カスタム アプリの新規追加メニュー](media/add-custom-app-menu.png)

3. フィールドに入力して、クラウド アプリ カタログの一覧と、ファイアウォール ログでの検出後に Cloud Discovery の一覧に表示される、新しいアプリのレコードを定義します。

    ![カスタム アプリ](media/add-custom-app.png)

4. **[ドメイン]** に、カスタム アプリへのアクセス時に使用される一意のドメインを入力します。 これらのドメインは、このアプリへのトラフィック ログ メッセージを照合するために使用されます。 使用しているデータ ソースにアプリの URL の情報が含まれていない場合は、**IPv4** アドレスと **IPv6** アドレスのフィールドに入力してください。
5. **[ホスティング プラットフォーム]** と **[Azure サブスクリプション ID]** を追加します。 必要に応じて、アプリの **[部署]** を指定します。
6. リスクの **[スコア]** を割り当てて、このレコードに対する変更の追跡に役立つ **[アプリのメモ]** を追加します。
7. **[作成]** をクリックします。

アプリが作成されると、クラウド アプリ カタログで使用できるようになります。

いつでも、行の最後にある 3 つの点をクリックして、カスタム アプリを編集または削除できます。

>[!NOTE]
> 追加後のカスタム アプリには、**カスタム アプリ** タグが自動的に付けられます。 このアプリ タグを削除することはできません。
すべてのカスタム アプリを表示するには、 **[アプリ タグ]** フィルターを [カスタム アプリ] に設定します。
<!-- - By default, custom apps have a risk score of 10, but you can use the **Override app score** action to change it at any time.-->

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ユーザー アクティビティ ポリシー](user-activity-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
