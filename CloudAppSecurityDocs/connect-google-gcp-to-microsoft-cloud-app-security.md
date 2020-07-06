---
title: Google Cloud Platform を Cloud App Security に接続する
description: この記事では、API コネクタを使用して Google Cloud Platform を Cloud App Security に接続し、使用状況を表示および制御する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/16/2019
ms.topic: conceptual
ms.service: cloud-app-security
ms.collection: M365-security-compliance
ms.openlocfilehash: bf9260d0fc4c68ac27638fbefbfdd738a89ccd22
ms.sourcegitcommit: 4f3883a9e85d0aaf2802b10433b221c3f1838d88
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79285536"
---
# <a name="connect-google-cloud-platform-to-microsoft-cloud-app-security-preview"></a>Google Cloud Platform を Microsoft Cloud App Security に接続する (プレビュー)

*適用対象:Microsoft Cloud App Security*

この記事では、コネクタ API を使用して Microsoft Cloud App Security を既存の Google Cloud Platform (GCP) アカウントに接続する手順について説明します。 この接続を使用すると、GCP の使用状況を表示したり制御したりできます。 Cloud App Security で GCP を保護する方法の詳細については、[GCP の保護](protect-gcp.md)に関するページを参照してください。

> [!NOTE]
> GCP 環境に接続するための手順は、集計ログを使用するための [Google の推奨事項](https://cloud.google.com/blog/products/gcp/best-practices-for-working-with-google-cloud-audit-logging)に従っています。 統合では Google StackDriver が活用され、課金に影響する可能性のある追加のリソースが消費されます。 消費されるリソースは次のとおりです。
>
> * [集計エクスポート シンク - 組織レベル](https://cloud.google.com/logging/docs/export/aggregated_exports#concept)
> * [Pub/Sub トピック – GCP プロジェクト レベル](https://cloud.google.com/logging/docs/export/using_exported_logs#pubsub-overview)
> * [Pub/Sub サブスクリプション – GCP プロジェクト レベル](https://cloud.google.com/logging/docs/export/using_exported_logs#pubsub-overview)
>
> 現時点では、Cloud App Security では管理アクティビティの監査ログのみがインポートされます。データ アクセスとシステム イベントの監査ログはインポートされません。 GCP ログの詳細については、「[Cloud 監査ログ](https://go.microsoft.com/fwlink/?linkid=2109230)」を参照してください。

安定した統合を維持し、セットアップ プロセスが削除または変更されるのを防ぐために、統合に専用のプロジェクトを使用し、プロジェクトへのアクセスを制限することをお勧めします。 また、GCP インスタンスが、Cloud App Security に既に接続されている G Suite インスタンスの一部である場合は、GCP 接続の詳細を追加するときに、「**接続されている G Suite 組織の一部である GCP インスタンスの場合**」の手順に従うことをお勧めします。

## <a name="prerequisites"></a>[前提条件]

統合 GCP ユーザーには、次のアクセス許可が必要です。

* **IAM と管理者の編集** - 組織レベル
* **プロジェクトの作成と編集**

## <a name="configure-google-cloud-platform"></a>Google Cloud Platform の構成

* 統合 GCP ユーザー アカウントを使用して、GCP ポータルにサインインします。

### <a name="create-a-dedicated-project"></a>専用プロジェクトを作成する

組織の GCP で専用プロジェクトを作成して、統合の分離と安定性を実現します。

1. **[Create Project]\(プロジェクトの作成\)** をクリックして、新規作成を開始します。
1. **[New project]\(新しいプロジェクト\)** 画面で、プロジェクトに名前を指定し、 **[Create]** をクリックします。

    ![GCP のプロジェクトの作成ダイアログを示すスクリーンショット](media/connect-gcp-create-project.png)

### <a name="enable-the-pubsub-api"></a>Pub/Sub API を有効にする

1. 専用プロジェクトに切り替えます。
1. [Pub/Sub] タブにアクセスします。サービス アクティベーション メッセージが表示されます。

### <a name="create-a-dedicated-service-account-for-the-integration"></a>統合用の専用サービス アカウントを作成する

1. **[IAM & admin]\(IAM & 管理\)** で、 **[Service accounts]\(サービス アカウント\)** をクリックします。
1. **[CREATE SERVICE ACCOUNT]\(サービス アカウントの作成\)** をクリックして、専用のサービス アカウントを作成します。
1. アカウント名を入力し、 **[Create]\(作成\)** をクリックします。
1. **[Role]\(ロール\)** を **[Pub/Sub Admin]\(Pub/Sub 管理者\)** として指定し、 **[Save]\(保存\)** をクリックします。

    ![GCP の IAM ロールの追加機能を示すスクリーンショット](media/connect-gcp-iam-role.PNG)

1. **[Email]\(電子メール\)** の値をコピーします。この値は後で必要になります。

    ![GCP の [Service accounts]\(サービス アカウント\) ダイアログを示すスクリーンショット](media/connect-gcp-create-service-account.png)

1. **[IAM & admin]\(IAM & 管理\)** で、 **[IAM]** をクリックします。

    1. 組織レベルに切り替えます。
    1. **[ADD]** をクリックします。
    1. **[New members]\(新しいメンバー\)** ボックスに、先ほどコピーした **[Email]\(電子メール\)** の値を貼り付けます。
    1. **[Role]\(ロール\)** を **[Logs Configuration Writer]\(ログ構成ライター\)** として指定し、 **[Save]\(保存\)** をクリックします。

        ![メンバーの追加ダイアログを示すスクリーンショット](media/connect-gcp-add-member.png)

### <a name="create-a-private-key-for-the-dedicated-service-account"></a>専用サービス アカウントの秘密キーを作成する

1. プロジェクト レベルに切り替えます。
1. **[IAM & admin]\(IAM & 管理\)** で、 **[Service accounts]\(サービス アカウント\)** をクリックします。
1. 専用サービス アカウントを開き、 **[Edit]\(編集\)** をクリックします。
1. **[CREATE KEY]\(キーの作成\)** をクリックします。
1. **[Create private key]\(秘密キーの作成\)** 画面で **[JSON]** を選択し、 **[Create]\(作成\)** をクリックします。

    ![秘密キーの作成ダイアログを示すスクリーンショット](media/connect-gcp-create-private-key.png)

    > [!NOTE]
    > 後でコンピューターにダウンロードされる JSON ファイルが必要になります。

### <a name="retrieve-your-organization-id"></a>組織 ID を取得する

**組織 ID** をメモしておきます。後で必要になります。 詳細については、「[組織 ID の取得](https://cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id)」を参照してください。
    ![組織 ID ダイアログを示すスクリーンショット](media/connect-gcp-org-id.png)

## <a name="configure-cloud-app-security"></a>Cloud App Security を構成する

* Cloud App Security ポータルで、 **[調査]** 、 **[接続アプリ]** の順にクリックします。

### <a name="add-the-gcp-connection-details"></a>GCP 接続の詳細を追加する

GCP 接続の詳細を指定するには、 **[アプリ コネクタ]** で次のいずれかの操作を行います。

**接続された G Suite 組織の一部ではない GCP インスタンスの場合**

1. プラス記号をクリックし、 **[Google Cloud Platform]** をクリックします。

    ![GCP の追加メニューを示すスクリーンショット](media/connect-gcp-add.png)

1. ポップアップでコネクタの名前を指定し、 **[Connect Google Cloud Platform]\(Google Cloud Platform に接続する\)** をクリックします。

1. [Google Cloud Platform] ページで、次の操作を行います。
    1. **[Organization ID]\(組織 ID\)** ボックスに、前にメモしておいた組織を入力します。
    1. **[Private key file]\(秘密キー ファイル\)** ボックスで、前の手順でダウンロードした JSON ファイルに移動します。
    1. **[Connect Google Cloud Platform]\(Google Cloud Platform に接続する\)** をクリックします。

    > [!NOTE]
    > G Suite インスタンスを接続して、統合ユーザー管理およびガバナンスを実現することをお勧めします。 これは、G Suite 製品を使用せず、GCP ユーザーが G Suite ユーザー管理システムを介して管理されている場合でも推奨されます。

**接続されている G Suite 組織の一部である GCP インスタンスの場合**

1. 接続されているインスタンスの一覧で、G Suite コネクタが表示されている行の末尾にある 3 つのドットをクリックし、 **[Add Google Cloud Platform]\(Google Cloud Platform の追加\)** をクリックします。

1. [Google Cloud Platform] ページで、次の操作を行います。
    1. **[Organization ID]\(組織 ID\)** ボックスに、前にメモしておいた組織を入力します。
    1. **[Private key file]\(秘密キー ファイル\)** ボックスで、前の手順でダウンロードした JSON ファイルに移動します。
    1. **[Connect Google Cloud Platform]\(Google Cloud Platform に接続する\)** をクリックします。

    > [!NOTE]
    > これにより、G Suite ユーザー ID 領域を使用して、統合ユーザー管理およびガバナンスを実現できます。

### <a name="test-the-connection"></a>接続をテストする

**[API のテスト]** をクリックして、正常に接続されたことを確認します。

テストには数分かかる場合があります。 完了すると、成功または失敗の通知が表示されます。 成功の通知を受信したら、 **[完了]** をクリックします。

アプリの接続で問題が発生した場合は、[アプリ コネクタのトラブルシューティング](troubleshooting-api-connectors-using-error-messages.md)に関するページを参照してください。

## <a name="aggregated-export-sink"></a>集計エクスポート シンク

現時点では、集計エクスポート シンクの無効化は Google Cloud Shell 経由でのみ可能です。

### <a name="to-disable-aggregated-export-sink"></a>集計エクスポート シンクを無効にするには

| 手順 | スクリプト | 詳細情報 |
|-|-|-|
| 1.Google Cloud Shell セッションを開始します。 | | [Cloud Shell の使用](https://cloud.google.com/shell/docs/using-cloud-shell) |
| 2.現在のプロジェクトを設定します。 | `gcloud config set project {PROJECT_ID}` | [gcloud config set](https://cloud.google.com/sdk/gcloud/reference/config/set) |
| 3.組織レベルのシンクを一覧表示します。 | `gcloud logging sinks list --organization={ORGANIZATION_ID}` | [gcloud ログ シンクの一覧](https://cloud.google.com/sdk/gcloud/reference/logging/sinks/list) |
| 4.関連するシンクを削除します。 | `gcloud logging sinks delete {SINK_NAME} --organization={ORGANIZATION_ID}` | [gcloud ログ シンクの削除](https://cloud.google.com/sdk/gcloud/reference/logging/sinks/delete) |

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
