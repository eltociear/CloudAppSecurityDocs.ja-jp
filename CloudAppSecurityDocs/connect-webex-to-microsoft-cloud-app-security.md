---
title: Webex を Cloud App Security に接続する
description: この記事では、お使いの Webex アプリを、使用状況を表示および制御する API コネクタを使用して、Cloud App Security に接続する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: f50ff4ae3b3a5a04ab9ffe052b0fb1e8ecdb2f7d
ms.sourcegitcommit: 00599ac6c64a4c62ed9ebdda3edb58f90f92c24d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "76912163"
---
# <a name="connect-cisco-webex-to-microsoft-cloud-app-security"></a>Cisco Webex を Microsoft Cloud App Security に接続する

*適用対象:Microsoft Cloud App Security*

この記事では、コネクタ API を使用して Microsoft Cloud App Security を既存の Cisco Webex アカウントに接続する方法を説明します。 この接続を使用すると、Webex のユーザー、アクティビティ、ファイルについて、表示したり制御したりできます。 Cloud App Security での Cisco Webex の保護方法の詳細については、[Cisco Webex の保護](protect-webex.md)に関する記事を参照してください。

## <a name="prerequisites"></a>[前提条件]

- 接続専用のサービス アカウントを作成することをお勧めします。 これにより、Webex で送信されたメッセージの削除など、Webex で実行されるガバナンス アクションがこのアカウントから実行されていることを確認できます。 それ以外の場合は、Webex に Cloud App Security を接続した管理者の名前が、アクションを実行したユーザーとして表示されます。
- Webex において、完全な権限を持つ管理者**および**コンプライアンス管理者のアクセス許可を持っている必要があります。

## <a name="how-to-connect-webex-to-cloud-app-security"></a>Webex を Cloud App Security に接続する方法

1. Cloud App Security コンソールで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

1. **[アプリ コネクタ]** ページで、[+] ボタン、 **[Cisco Webex]** の順にクリックします。

    ![WebEx の接続](media/cisco-webex.png "WebEx の接続")

1. ポップアップで、このコネクタのインスタンス名を入力します。

1. **[Connect Cisco Webex]\(Cisco Webex を接続する\)** をクリックします。 Webex のサインイン ページが開きます。 ご自分の資格情報を入力して、Cloud App Security によるチームの Webex インスタンスにアクセスできるようにします。

1. Webex に、Cloud App Security があなたのチームの情報やアクティビティ ログにアクセスし、チーム メンバーとしてアクティビティを実行することを許可するかどうかを確認するメッセージが示されます。 続行するには、 **[許可]** をクリックします。

1. Cloud App Security コンソールに戻ると、Webex と正常に接続されたことを示すメッセージが届きます。

1. **[API のテスト]** をクリックして、正常に接続されたことを確認します。

    テストには数分かかる場合があります。 成功の通知を受信したら、 **[閉じる]** をクリックします。

Webex に接続すると、接続前の 7 日間のイベントを受け取ります。 Cloud App Security では、イベントが過去 3 か月にわたってスキャンされます。 これを増やすには、Cisco Webex の Pro ライセンスを所有し、Cloud App Security サポートでチケットを開く必要があります。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
