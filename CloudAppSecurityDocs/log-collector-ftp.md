---
title: ログ コレクターの FTP 構成
description: この記事では、Cloud App Security Cloud Discovery docker の構成を変更する手順について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 8/7/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: aba19263cafbc1d91a4a650d4cb67e9e748947db
ms.sourcegitcommit: 6eff466c7a6817b14a60d8c3b2c201c7ae4c2e2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74719907"
---
# <a name="log-collector-ftp-configuration"></a>ログ コレクターの FTP 構成

*適用対象:Microsoft Cloud App Security*

この記事では、Cloud App Security Cloud Discovery docker の構成を変更する方法について説明します。

## <a name="docker-deployment"></a>Docker のデプロイ

Cloud App Security Cloud Discovery docker の構成を変更する必要がある場合があります。

### <a name="changing-the-ftp-password"></a>FTP のパスワードの変更

1. ログ コレクターのホストに接続します。

2. `docker exec -it <collector name> pure-pw passwd <ftp user>` を実行します。

    1. 新しいパスワードを入力します。
    2. 確認のために、もう一度新しいパスワードを入力します。

3. `docker exec -it <collector name> pure-pw mkdb` を実行して、変更を適用します。

    ![FTP のパスワードの変更](media/ftp-connect.png)

### <a name="customize-certificate-files"></a>証明書ファイルのカスタマイズ

次の手順に従うと、Cloud Discovery docker へのセキュリティで保護された接続に使用する証明書ファイルをカスタマイズできます。

1. FTP クライアントを開き、ログ コレクターに接続します。

    ![FTP クライアントへの接続](media/ftp-connect.png)

2. `ssl_update` ディレクトリに移動します。
3. 新しい証明書ファイルを `ssl_update` ディレクトリにアップロードします (名前は必須です)。

    ![FTP のパスワードの変更](media/new-certs.png)

    - **FTP の場合:** 1 つファイルが必要です。 このファイルには、キーと資格証明書のデータが (この順番で) あり、**pure-ftpd.pem** という名前です。
    - **Syslog の場合:** **ca.pem**、**server-key.pem、**server-cert.pem** の 3 つのファイルが必要です。 これらのいずれかのファイルが見つからない場合、更新はされません。

4. ターミナルで実行する場合: `docker exec -t <collector name> update_certs` このコマンドを実行すると、次のスクリーンショットのような出力が生成されます。

    ![FTP のパスワードの変更](media/update-certs.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Cloud Discovery の展開](set-up-cloud-discovery.md)

[!INCLUDE [Open support ticket](includes/support.md)]
