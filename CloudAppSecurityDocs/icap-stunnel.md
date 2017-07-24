---
title: "Cloud App Security の安全な ICAP による外部 DLP 統合 | Microsoft Docs"
description: "このトピックでは、Cloud App Security と stunnel セットアップで ICAP 接続を構成するために必要な手順について説明します。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/16/2017
ms.topic: article
ms.prod: 
ms.service: cloud-app-security
ms.technology: 
ms.assetid: 9656f6c6-7dd4-4c4c-a0eb-f22afce78071
ms.reviewer: reutam
ms.suite: ems
ms.openlocfilehash: ccc2197943c81b1a871375d4134c5aaf01876345
ms.sourcegitcommit: ae4c8226f6037c5eb286eb27142d6bbb397609e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2017
---
# <a name="external-dlp-integration"></a>外部 DLP 統合

> [!NOTE] 
> この機能はプレビュー段階です。 この機能をお客様のテナントで試すには、< mcaspreview@microsoft.com > にお問い合わせください。

Cloud App Security は既存の DLP ソリューションと統合し、コントロールをクラウドに拡張できます。同時に、オンプレミスとクラウドを問わず、アクティビティ全体で一貫性のある統合ポリシーが維持されます。 このプラットフォームは、REST API や ICAP など、使いやすいインターフェイスをエクスポートします。Symantec Data Loss Prevention (以前の Vontu Data Loss Prevention) や Forcepoint DLP など、コンテンツ分類システムと統合できます。 

統合は標準 ICAP プロトコルを利用して行われます。これは [RFC 3507](https://tools.ietf.org/html/rfc3507) に説明のある http 型のプロトコルです。 ICAP のデータ転送を守るために、DLP ソリューションと Cloud App Security の間に安全な SSL トンネル (stunnel) を構築する必要があります。 stunnel を構築することで、DLP サーバーと Cloud App Security の間で送信されるデータが TLS で暗号化されます。 

本ガイドでは、Cloud App Security と stunnel セットアップで ICAP 接続を構成し、通信を保護するために必要な手順について説明します。

## <a name="architecture"></a>アーキテクチャ
Cloud App Security はクラウド環境をスキャンします。ファイル ポリシー構成に基づき、内部 DLP エンジンと外部 DLP のいずれを利用してファイルをスキャンするのか決定します。 外部 DLP スキャンが適用される場合、ファイルは安全なトンネルを経由して顧客環境に送信され、顧客環境で ICAP アプライアンスに中継され、DLP 判定が行われます (許可またはブロック)。 応答は stunnel 経由で Cloud App Security に返されます。このとき、ポリシーを利用し、通知、隔離、共有コントロールなど、後続のアクションが決定されます。

![stunnel アーキテクチャ](./media/icap-architecture-stunnel.png)

Cloud App Security は Azure で実行されます。Azure での展開により高いパフォーマンスが一時停止されます。 ただし、他のクラウドやオンプレミスでの展開など、他の選択肢もあります。 他の環境で展開する場合、待機時間が長く、スループットが低いため、パフォーマンスが低下することがあります。 トラフィックを暗号化するために、ICAP サーバーと stunnel を同じネットワークに展開する必要があります。

## <a name="prerequisites"></a>前提条件
Cloud App Security で stunnel 経由でデータを ICAP サーバーに送信するには、Cloud App Security で使用される外部 IP アドレスに DMZ ファイアウォールを開きます。このとき、動的ソース ポート番号を使用します。 

1.  ソース アドレス: [「前提条件」の「アプリを接続する」](enable-instant-visibility-protection-and-governance-actions-for-your-apps.md#prerequisites)を参照
2.  ソース TCP ポート: 動的
3.  宛先アドレス: 後続の手順で構成する外部 ICAP サーバーに接続されている stunnel の 1 または 2 つの IP アドレス
4.  宛先 TCP ポート: ネットワークに定義されている宛先 TCP ポート

## <a name="step-1--set-up-icap-server"></a>手順 1: ICAP サーバーを設定する

ICAP サーバーを設定します。ポート番号を書き留め、**[モード]** を **[ブロック]** に設定します。 ブロック モードでは、分類判定を Cloud App Security に戻すように ICAP サーバーが設定されます。

この方法については、外部 DLP 製品のマニュアルを参照してください。 たとえば、「[付録 A: ForcePoint ICAP サーバー セットアップ](#forcepoint)」を参照してください。

## <a name="step-2--set-up-your-stunnel-server"></a>手順 2: stunnel サーバーを設定する 

この手順では、ICAP サーバーに接続される stunnel を設定します。 

>[!NOTE]
> この手順は強く推奨されますが、任意です。テスト ワークロードでは省略できます。 

### <a name="install-stunnel-on-a-server"></a>サーバーに stunnel をインストールする

**前提条件**

- **サーバー** - Windows Server または Linux サーバー (メジャー ディストリビューション)。

stunnel インストール対応のサーバーの種類については、[stunnel Web サイト](https://www.stunnel.org/index.html)をご覧ください。 Linux を使用している場合、Linux ディストリビューション マネージャーでインストールできます。

#### <a name="install-stunnel-on-windows"></a>Windows に stunnel をインストールする

1. [最新の Windows Server インストールをダウンロードします](https://www.stunnel.org/downloads.html) (これは最近のあらゆる版の Windows Server で可能になっています)。
(既定のインストール)

2. インストール中、新しい自己署名証明書を作成しないでください。証明書は後の手順で作成します。

3. **[Start server after installation]\(インストール後にサーバーを起動する\)** をクリックします。

4. 次のいずれかの方法で証明書を作成します。

   -    証明書管理サーバーを利用し、ICAP サーバーで SSL 証明書を作成し、stunnel インストールのために用意したサーバーにキーをコピーします。
   -    あるいは、stunnel サーバーで、次の OpenSSL コマンドを利用して秘密キーと自己署名証明書を生成します。 次の変数を置き換えます。
       -    **key.pem** を秘密キーの名前に変更
       -    **cert.pem** を証明書の名前に変更
       -    **stunnel-key** を新しく作成したキーの名前に変更

5. stunnel インストール パスの下で、config ディレクトリを開きます。 既定では、c:\Program Files (x86)\stunnel\config\ です。
6. 管理者アクセス許可で次のコマンド ラインを実行します。     `..\bin\openssl.exe genrsa -out ey.pem 2048 `
      
     ` ..\bin\openssl.exe  req -new -x509 -config ".\openssl.cnf" -key key.pem -out .\cert.pem -days 1095`

8. cert.pem と key.pem を連結し、ファイルに保存します。 `cat cert.pem key.pem >> stunnel-key.pem`

9. [公開キーをダウンロードし](https://adaprodconsole.blob.core.windows.net/icap/publicCert.pem)、**C:\Program Files (x86)\stunnel\config\CAfile.pem** に保存します。

10. Windows ファイアウォールでポートを開くための次の規則を追加します。

        rem Open TCP Port 11344 inbound and outbound
        netsh advfirewall firewall add rule name="Secure ICAP TCP Port 11344" dir=in action=allow protocol=TCP localport=11344
        netsh advfirewall firewall add rule name=" Secure ICAP Port 11344" dir=out action=allow protocol=TCP localport=11344

11. `c:\Program Files (x86)\stunnel\bin\stunnel.exe` を実行し、stunnel アプリケーションを開きます。 

12. **[構成]** をクリックし、**[構成の編集]** をクリックします。

   ![Windows Server 構成を編集する](./media/stunnel-windows.png)
 
13. ファイルを開き、次のサーバー構成行を貼り付けます。ここで、**ICAP Server IP** は ICAP サーバーの IP アドレスです。**stunnel-key** は前の手順で作成したキーです。**CAfile** は Cloud App Security stunnel の公開証明書です。 また、サンプルがあればそれを削除し (例では Gmail テキストを確認できます)、次をファイルにコピーします。

        [microsoft-Cloud App Security]
        accept = 0.0.0.0:11344
        connect = **ICAP Server IP**:1344
        cert = C:\Program Files (x86)\stunnel\config\**stunnel-key**.pem
        CAfile = C:\Program Files (x86)\stunnel\config\**CAfile**.pem
        TIMEOUTclose = 0

12. ファイルを保存し、**[構成の再読み込み]** をクリックします。

13. 予想どおり動作していることを確認するには、コマンド プロンプトから次を実行します。 `netstat -nao  | findstr 11344`
 

#### <a name="install-stunnel-on-ubuntu"></a>Ubuntu に stunnel をインストールする

次の例は Ubuntu サーバー インストールに基づきます。ルート ユーザーとしてサインインしています。他のサーバーの場合、並列コマンドを使用します。 

用意したサーバーに最新版の stunnel をダウンロードし、インストールします。Ubuntu サーバーで次のコマンドを実行すると、stunnel と OpenSSL の両方がインストールされます。

    apt-get update
    apt-get install openssl -y
    apt-get install stunnel4 -y
コンソールから次のコマンドを実行し、stunnel がインストールされていることを確認します。 バージョン番号と構成オプションの一覧が表示されるはずです。

    stunnel-version

### <a name="generate-certificates"></a>証明書を生成する

ICAP サーバーと Cloud App Security では、stunnel 全体でのサーバーの暗号化と認証に秘密キーと公開証明書が使用されます。 stunnel をバックグラウンド サービスとして実行できるように、パス フレーズなしで秘密キーを作成してください。 また、ファイルのアクセス許可を、stunnel 所有者は**読み取り可能**に、その他のユーザーは**なし**に設定してください。

次のいずれかの方法で証明書を作成できます。
-   証明書管理サーバーを利用し、ICAP サーバーで SSL 証明書を作成し、stunnel インストールのために用意したサーバーにキーをコピーします。 
-   あるいは、stunnel サーバーで、次の OpenSSL コマンドを利用して秘密キーと自己署名証明書を生成します。 次の変数を置き換えます。
    - **“key.pem”** を秘密キーの名前に変更
    - **“cert.pem”** を証明書の名前に変更
    - **“stunnel-key”** を新しく作成したキーの名前に変更
       
            openssl genrsa -out key.pem 2048
            openssl req -new -x509 -key key.pem -out cert.pem -days 1095
            cat key.pem cert.pem >> /etc/ssl/private/stunnel-key.pem

### <a name="download-the-cloud-app-security-stunnel-client-public-key"></a>Cloud App Security stunnel クライアントの公開キーをダウンロードする

https://adaprodconsole.blob.core.windows.net/icap/publicCert.pem から公開キーをダウンロードし、**/etc/ssl/certs/CAfile.pem** に保存します。

### <a name="configure-stunnel"></a>stunnel を構成する 

stunnel 構成は stunnel.conf ファイルで設定されます。

1. 次のディレクトリで stunnel.conf ファイルを作成します。 **vim /etc/stunnel/stunnel.conf**

3.  ファイルを開き、次のサーバー構成行を貼り付けます。**DLP Server IP** は ICAP サーバーの IP アドレスです。**stunnel-key** は前の手順で作成したキーです。**CAfile** は Cloud App Security stunnel の公開証明書です。

        [microsoft-Cloud App Security]
         accept = 0.0.0.0:11344
         connect = **ICAP Server IP**:1344
          cert = /etc/ssl/private/**stunnel-key**.pem
          CAfile = /etc/ssl/certs/**CAfile**.pem
          TIMEOUTclose = 1

> [!NOTE] 
> 既定では、stunnel ポート番号は 11344 に設定されます。 これは必要に応じて別のポートに変更できますが、新しいポート番号を必ず書き留めてください。次の手順で入力する必要があります。

### <a name="update-your-ip-table"></a>IP テーブルを更新する
次のルート ルールで IP アドレス表を更新します。
   
    iptables -I INPUT -p tcp --dport 11344 -j ACCEPT

IP 表の更新を永続にするには、次のコマンドを使用します。

     sudo apt-get install iptables-persistent
     sudo /sbin/iptables-save > /etc/iptables/rules.v4
 

### <a name="run-stunnel"></a>stunnel を実行する
1.  stunnel サーバーで、次のコマンドを実行します。

        vim /etc/default/stunnel4

2.  変数 ENABLED を 1 に変更します。

        ENABLED=1

3.  サービスを再起動し、構成を有効にします。

        /etc/init.d/stunnel4 restart

4.  次のコマンドを実行し、stunnel が正しく動作していることを確認します。

        ps -A | grep stunnel

    次のコマンドを実行し、正しいポートで待機していることを確認します。

        netstat -anp | grep 11344

5. stunnel サーバーが展開されたネットワークが前述のネットワーク前提条件に一致していることを確認します。 これは、Cloud App Security から入ってくる接続がサーバーに届くための前提条件です。

プロセスが終わらない場合、[stunnel マニュアル](https://www.stunnel.org/docs.html)を参照して問題を解決してください。


## <a name="step-3--connect-to-cloud-app-security"></a>手順 3:  Cloud App Security に接続する

1. Cloud App Security の **[設定]** で、**[セキュリティ拡張機能]** を選択し、**[外部 DLP]** タブを選択します。

2. プラス記号をクリックし、新しい接続を追加します。 

3. **[Add new external DLP]\(新しい外部 DLP の追加\)** ウィザードに **[接続名]** を入力します (たとえば、「My Forcepoint connector」と入力します)。この名前はコネクタの識別に利用されます。

4. **[接続の種類]** を選択します。
    - **Symantec Vontu** – Vontu DLP アプライアンスにカスタマイズ統合を利用するにはこれを選択します。
    - **Forcepoint DLP** – Forcepoint DLP アプライアンスにカスタマイズ統合を利用するにはこれを選択します。
    - **Generic ICAP – REQMOD** - [要求変更](https://tools.ietf.org/html/rfc3507)を利用するその他の DLP アプライアンスの場合
    - **Generic ICAP – RESPMOD** - [応答変更](https://tools.ietf.org/html/rfc3507)を利用するその他の DLP アプライアンスの場合
    ![Cloud App Security ICAP 接続](./media/icap-wizard1.png)

4. [参照] をクリックし、stunnel への接続に使用する、stunnel のパブリック ルート CA を選択し、**[次へ]** をクリックします。

   > [!NOTE]
   > **[Use secure ICAP]\(安全な ICAP を使用する\)** ボックスを選択し、stunnel ゲートウェイを暗号化することが推奨されます。 テスト目的であれば、あるいは stunnel サーバーがない場合、この選択を外し、DLP サーバーと直接統合します。 

5. **[サーバー構成]** 画面で、手順 2 で設定した stunnel サーバーの **[IP アドレス]** と **[ポート]** を指定します。 負荷分散を目的とする場合、追加のサーバーの **[IP アドレス]** と **[ポート]** を構成できます。 指定する IP アドレスは、サーバーの外部静的 IP アドレスになります。

   ![Cloud App Security ICAP 接続](./media/icap-wizard2.png)
6. **[次へ]**をクリックします。 Cloud App Security により、構成したサーバーへの接続がテストされます。 エラーが発生した場合、マニュアルとネットワーク設定を見直してください。 正常に接続されたら、**[終了]** をクリックします。

7. 次に、この外部 DLP サーバーにトラフィックを送るために、**ファイル ポリシー**の作成の **[コンテンツ検査方法]** で、先ほど作成した接続を選択します。 ファイル ポリシーの作成方法については[こちら](data-protection-policies.md)をご覧ください。


## 付録 A: ForcePoint ICAP サーバー セットアップ <a name="forcepoint"></a>

ForcePoint で、次の手順でアプライアンスを設定します。

1.  DLP アプライアンスで、**[展開]** > **[システム モジュール]** の順に移動します。 

    ![ICAP 展開](./media/icap-system-modules.png)

2.  **[全般]** タブで **[ICAP サーバー]** が **[有効]** になっていること、**[ポート]** が **[1344]** に設定されていることを確認します。 また、**[Allow connection to this ICAP Server from the following IP addresses]\(次の IP アドレスからこの ICAP サーバーへの接続を許可する\)** で **[任意の IP アドレス]** を選択します。
 
    ![ICAP 構成](./media/icap-ip-address.png)

3.  HTTP/HTTPS タブで、**[モード]** を **[ブロック]** に設定します。
 
    ![ICAP ブロック](./media/icap-blocking.png)
 



