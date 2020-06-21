---
title: Microsoft Power automation を Microsoft Cloud App Security と統合して、カスタムアラートの自動化を実現する
description: この記事では、Microsoft Power automation と Cloud App Security を統合することによって、カスタムアラートの自動化を実現する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.openlocfilehash: f63e873d2b65781a3bca7209c020696bf2957171
ms.sourcegitcommit: 4e2b905c8770d411df68372c29154d30b2cf195e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2020
ms.locfileid: "85123245"
---
# <a name="integrate-with-microsoft-power-automate-for-custom-alert-automation"></a>カスタムアラートの自動化のための Microsoft Power automation との統合

*適用対象:Microsoft Cloud App Security*

Cloud App Security は[Microsoft Power](https://docs.microsoft.com/flow/getting-started) automation と統合して、カスタムアラートの自動化とオーケストレーションのプレイブックを提供します。 Power の自動化で利用できる[コネクタのエコシステム](https://docs.microsoft.com/connectors/)を使用することにより、Cloud App Security がアラートを生成するときにプレイブックのトリガーを自動化できます。 たとえば、[ServiceNow コネクタ](https://docs.microsoft.com/connectors/service-now/)を使用してチケット発行システムで問題を自動的に作成したり、Cloud App Security でアラートがトリガーされたときに、カスタム ガバナンス アクションを実行するための承認メールを送信します。

## <a name="prerequisites"></a>前提条件

- 有効な[Microsoft Power 自動自動化プラン](https://flow.microsoft.com/pricing)が必要です

## <a name="how-it-works"></a>しくみ

Cloud App Security は、ポリシーを定義するときに、ユーザーの中断やファイルのプライベート作成など、事前に定義されたガバナンスオプションを提供します。 Cloud App Security コネクタを使用して Power 自動でプレイブックを作成することによって、ポリシーに対してカスタマイズされたガバナンスオプションを有効にするワークフローを作成できます。 Power の自動化でプレイブックを作成したら、それを Cloud App Security のポリシーに関連付けて、Power の自動化にアラートを送信するだけです。 Microsoft Power の自動化では、組織に合わせてカスタマイズしたワークフローを作成するためのコネクタと条件がいくつか提供されています。

Power の自動化の[Cloud App Security コネクタ](https://docs.microsoft.com/connectors/cloudappsecurity/)は、自動化されたトリガーとアクションをサポートしています。 Cloud App Security によってアラートが生成されると、電源自動化が自動的にトリガーされます。 アクションには、Cloud App Security でのアラートの状態の変更が含まれます。

## <a name="how-to-create-playbooks-with-power-automate"></a>パワー自動化を使用してプレイブックを作成する方法

1. Cloud App Security で [API トークンを作成](api-tokens.md)します。

2. [Power オートメーションポータル](https://flow.microsoft.com)に移動し、[**マイフロー**] を選択して [**新規作成**] を選択し、ドロップダウンから [**自動-空白から**] を選択します。

    ![Power オートメーションによる新しいフローの作成](media/flow-create-new.png)

3. フローの名前を指定し、[**フローのトリガーを選択**してください] に**Cloud App Security**を入力し、[**アラートの生成時**] を選択します。

    ![アラートが生成されたときの電源自動化](media/flow-when-alert.png)

4. **[認証設定]** の下に、手順 1 の API トークンを貼り付けます。

5. Cloud App Security でポリシーがアラートを生成するときにトリガーされる必要があるワークフローを定義します。 アクション、論理条件を追加し、スイッチ ケースの条件、またはループを追加して、プレイブックを保存できます。

    ![Power の自動化のワークフロー](media/flow-workflow.png)

6. Cloud App Security ポータルで、[**ポリシー** ] に移動し、電源自動化に転送するアラートがあるポリシーの行で、3つのドットをクリックし、[**設定**] を選択します。
7. [**アラート**] で、[ **Power の自動化にアラートを送信する**] を選択し、ドロップダウンメニューからプレイブックの名前を選択します。

    ![Cloud App Security ポータルでの電源自動化の有効化](media/flow-mcas-config.png)

8. 作成済みまたはアクセス権が付与されている Cloud App Security プレイブックは、[**セキュリティ拡張機能**] 画面に表示されます。

    ![Cloud App Security でプレイブックを表示する](media/flow-extensions.png)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
