---
title: Cloud Discovery エラーのトラブルシューティング - Cloud App Security
description: この記事では、Cloud Discovery の頻繁なエラーと、それぞれの推奨される解決策の一覧を示します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/19/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 5d4bff251e40954e6505c9f1633a927366d78df6
ms.sourcegitcommit: b15034dd50142afd8e95de22a9232f711b1eae6e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85624832"
---
# <a name="troubleshooting-cloud-discovery"></a>Cloud Discovery のトラブルシューティング

*適用対象:Microsoft Cloud App Security*

この記事では、Cloud Discovery のエラーと、それぞれの推奨される解決策の一覧を示します。

## <a name="microsoft-defender-atp-integration"></a>Microsoft Defender ATP の統合

Microsoft Defender ATP と Cloud App Security を統合した場合に、統合の結果が表示されません。

|問題|解決策|
|----|----|
|**Win10 エンドポイント ユーザー** レポートが一覧に表示されない|接続先のコンピューターが Windows 10 バージョン 1809 以降であり、データがアクセス可能になるまでにかかる必要な 2 時間待機したことを確認します。|
|検出レポートが空である|エンドポイント デバイスが転送プロキシの背後にある場合は、ログ コレクターを使用して、転送プロキシからログを送信できます|

## <a name="log-parsing-errors"></a>ログ解析エラー

ガバナンス ログを使用して、Cloud Discovery ログの処理を追跡できます。 この記事では、そこに表示される可能性がある各エラーに対して実行する解決アクションについて説明します。

### <a name="governance-log-errors"></a>ガバナンス ログのエラー

|エラー|[説明]|解決策|
|----|----|----|
|サポートされていないファイルの種類|アップロードされたファイルは有効なログ ファイルではありません (画像ファイルなど)。|ファイアウォールまたはプロキシから直接エクスポートされた**テキスト**、**zip、または **gzip** ファイルをアップロードします。|
|ログの形式が一致していません|アップロードしたログの形式が、このデータ ソースに予期されるログの形式と一致していません。|1.ログが破損していないことを確認します。 <br /> 2.ログを、アップロード ページに表示されるサンプル形式と比較して照合します。|
|トランザクションが 90 日以上経過しています|すべてのトランザクションが 90 日以上経過しているため、無視されます。|最新のイベントを含む新しいログをエクスポートし、再度アップロードします。|
|カタログ化されたクラウド アプリに対するトランザクションがない|認識されたクラウド アプリに対するトランザクションがログに見つかりません。|ログに送信トラフィック情報が含まれていることを確認します。|
|サポートされていないログの種類|**データソース = その他 (サポートされていない)** を選択した場合、ログは解析されません。 代わりに、レビューのために Cloud App Security テクニカル チームに送信されます。|Cloud App Security テクニカル チームは、各データ ソースごとに専用のパーサーを作成します。 最も一般的なデータ ソースは[既にサポートされています](set-up-cloud-discovery.md)。 サポートされていないデータ ソースの各アップロードは、確認され、新しいデータ ソース パーサーのパイプラインに追加されます。 新しいパーサーの通知は、Cloud App Security [リリース ノート](release-notes.md)の一部として公開されます。|

## <a name="log-collector-errors"></a>ログ コレクターのエラー

|問題|解決策|
|----|----|
|FTP 経由でログ コレクターに接続できませんでした| 1.SSH 資格情報ではなく、FTP 資格情報を使用していることを確認します。 <br />2.使用している FTP クライアントが SFTP に設定されていないことを確認します。  |
|コレクター構成の更新に失敗しました | 1.最新のアクセス トークンを入力したことを確認します。 <br />2.ファイアウォールで、ログ コレクターがポート 443 で送信トラフィックを開始できることを確認します。|
|コレクターに送信されたログがポータルに表示されません | 1.ガバナンス ログに失敗した解析タスクがあるかどうかを確認します。  <br />  &nbsp;&nbsp;&nbsp;&nbsp;その場合は、上記のログ解析エラー テーブルを使用して、エラーのトラブルシューティングを行います。<br /> 2.そうでない場合は、ポータルでデータ ソースとログ コレクターの構成を確認します。 <br /> &nbsp;&nbsp;&nbsp;&nbsp;a. [データ ソース] ページで、使用しているデータ ソースが正しく構成されていることを確認します。 <br />&nbsp;&nbsp;&nbsp;&nbsp;b. [ログ コレクター] ページで、データ ソースが適切なログ コレクターにリンクされていることを確認します。 <br /> 3.オンプレミスのログ コレクター マシンのローカル構成を確認します。  <br />&nbsp;&nbsp;&nbsp;&nbsp;a. SSH 経由でログ コレクターにログインし、collector_config ユーティリティを実行します。<br/>&nbsp;&nbsp;&nbsp;&nbsp;b. 定義したプロトコル (Syslog/TCP、Syslog/UDP、または FTP) を使用して、ファイアウォールまたはプロキシがログ コレクターにログを送信していること、およびそれらを正しいポートとディレクトリに送信していることを確認します。<br /> &nbsp;&nbsp;&nbsp;&nbsp;c. コンピューターで netstat を実行し、ファイアウォールまたはプロキシから着信接続を受信することを確認します <br /> 4. ログ コレクターがポート 443 で送信トラフィックを開始できることを確認します。 |
|ログ コレクターの状態:作成日 | ログ コレクターのデプロイが完了しませんでした。 デプロイ ガイドに従って、オンプレミスのデプロイ手順を完了します。|
|ログ コレクターの状態:切断 | リンクされたどのデータ ソースからも過去 24 時間でデータを受信していません。 |
|最新のコレクターイメージのプルに失敗した| Docker のデプロイ中にこのエラーが発生した場合、ホスト マシンに十分なメモリがない可能性があります。 これを確認するには、ホストで `docker pull microsoft/caslogcollector` コマンドを実行します。 それによって、エラー `failed to register layer: Error processing tar file(exist status 1): write /opt/jdk/jdk1.8.0_152/src.zip: no space left on device` が返された場合、ホスト マシンの管理者に、領域を増やすように問い合わせてください。|

## <a name="discovery-dashboard-errors"></a>Discovery ダッシュボードのエラー

|問題|解決策|
|----|----|
|Discovery データが正常にアップロードされ、解析されましたが、Cloud Discovery ダッシュボードが空のように見えます|ダッシュボードは、ログに記録されていないデータでフィルター処理されているため、表示するデータがない可能性があります。 Cloud Discovery ダッシュボードでフィルターを変更して、さまざまな種類のデータを表示し、結果を確認してみてください。|

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [クラウド環境を保護するための日常的な作業](daily-activities-to-protect-your-cloud-environment.md)

[!INCLUDE [Open support ticket](includes/support.md)]
