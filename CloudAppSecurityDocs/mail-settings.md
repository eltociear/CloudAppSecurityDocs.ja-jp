---
title: "電子メールの通知の基本設定 |Microsoft Docs"
description: "この記事では、Cloud App Security によって送信された電子メール通知を個人用に設定する方法について情報を提供します。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: cloud-app-security
ms.technology: 
ms.assetid: 8402cdc9-4969-4150-b567-ccc9d75e5370
ms.reviewer: reutam
ms.suite: ems
ms.openlocfilehash: ce24e4c25ab4d8b85e4ddb6d6d574dd29b8c2003
ms.sourcegitcommit: 2f4474084c7e07ac4853945ab5aa1ea78950675d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2017
---
##  <a name="mailsettings"></a> 電子メールの通知の基本設定  
メニュー バーで設定アイコン ![設定アイコン](./media/settings-icon.png "設定アイコン") をクリックして [**メールの設定**] を選択し、Cloud App Security から管理者に送信されるアラート要求の電子メール通知、および関与している支社についてエンド ユーザーに送信される通知のパラメーターを設定できます。  
  
![[メールの設定] メニュー](./media/mail-setting-menu.png "[メールの設定] メニュー")  
  
次を構成します。  
  
1.  **From email address (電子メール アドレスから)**: 通知の送信に使用する電子メール アカウント。  
  
     **From display name (表示名から)**: 電子メール メッセージの [**From**] フィールドに表示する名前。  
  
     **返信用メール アドレス**: メッセージの返信に使用される電子メール アカウント。  
  
     ![[メールの設定] の構成](./media/mail-settings-config.png "[メールの設定] の構成")  

  >[!NOTE]
  >**[送信元メール アドレス]** フィールドを独自のドメインに変更する方法については、[こちら](https://mandrill.zendesk.com/hc/articles/205582277-How-do-I-add-DNS-records-for-my-sending-domains-)の指示を参照してください。
  
2.  [**メールのデザイン**] では、HTML ファイルを使用すると、システムから送信される電子メール メッセージのカスタマイズやデザインを行えます。 テンプレートに使用される HTML ファイルには次の項目が含まれます。  
  
    -   すべてのテンプレートの CSS は、テンプレート内でインラインである必要があります。  
  
    -   テンプレートには編集不可能なプレースホルダーが 3 つ含まれます。  
  
         %%logo%% - [全般設定] ページでアップロードされた企業のロゴの URL。  
  
         %%title%% - ポリシーにより設定された電子メールのタイトルのプレースホルダー。  

         %%content%% - ポリシーにより設定されたエンド ユーザー向けコンテンツのプレースホルダー。  
     
3.  [**テンプレートのアップロード**] をクリックして、作成したファイルを選択します。 

4. 次に、[**テスト メールの送信**] をクリックしてテスト メールを自分自身に送信し、作成したテンプレートの例を確認します。 電子メールは、ポータルへのログインに使用されたアカウントに送信されます。 テスト メールでは、メタデータ フィールド、テンプレート、電子メールの件名、電子メール本文のタイトルと内容を確認できます。  電子メール テンプレートのサンプルを次に示します。 



```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
  <html>  
       <head>  
            <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>  
            <meta name="viewport" content="width=device-width, initial-scale=1.0"/>  
          </head>  
          <body class="end-user">  
          <table border="0" cellpadding="20%" cellspacing="0" width="100%" id="background-table">  
            <tr>  
              <td align="center">  
                <!--[if (gte mso 9)|(IE)]>  
                <table width="600" align="center" cellpadding="0" cellspacing="0" border="0">  
                  <tr>  
                    <td>  
                <![endif]-->  
                <table bgcolor="#ffffff" align="center" border="0" cellpadding="0" cellspacing="0" style="padding-bottom: 40px;" id="container-table">  
                  <tr>  
                    <td align="right" id="header-table-cell">  
                      <img src="%%logo%%" alt="Microsoft Cloud App Security" id="org-logo" />  
                    </td>  
                  </tr>  
                  <tr>  
                    <td style="padding-top: 58px;" align="center" valign="top">  
                      <table width="100%" cellpadding="12">  
                        <tr>  
                          <td align="center" class="round-title">  
                            %%title%%  
                          </td>  
                        </tr>  
                      </table>  
                    </td>  
                  </tr>  
                  <tr>  
                    <td style="padding: 0 40px 79px 40px;" class="content-table-cell" align="left" valign="top">  
                        %%content%%  
                    </td>  
                  </tr>  
                  <tr>  
                    <td class="last-row"></td>  
                  </tr>  
                </table>  
                <!--[if (gte mso 9)|(IE)]>  
                </td>  
                </tr>  
                </table>  
                  <![endif]-->  
              </td>  
              </tr>  
          </table>  
            </body>  
          </html>  
   ```
  

  
  

  
    
## <a name="see-also"></a>参照  
[Cloud Discovery のセットアップ](set-up-cloud-discovery.md)   
[テクニカル サポートが必要な場合は、Cloud App Security のサポート ページをご利用ください。](http://support.microsoft.com/oas/default.aspx?prid=16031)   
[Premier サポートをご利用のお客様は、Premier ポータルから直接 Cloud App Security を選択することもできます。](https://premier.microsoft.com/)  
  
  