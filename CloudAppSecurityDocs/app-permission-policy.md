---
title: Cloud App Security で OAuth アプリを制御するポリシーを作成する
description: この記事では、Microsoft Cloud App Security でアプリのアクセス許可ポリシーを作成し、操作するための手順について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 11/27/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 25809c1ace00b31df32c225f6b72a2b4e98a70d8
ms.sourcegitcommit: 826d2ec022647bce6c3135c115a41ee894ff8ecd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84800726"
---
# <a name="oauth-app-policies"></a>OAuth アプリに関するポリシー

*適用対象:Microsoft Cloud App Security*

ご利用の環境に接続されている [OAuth アプリの既存の調査](manage-app-permissions.md)に加え、OAuth アプリが特定の条件を満たした場合に自動通知を受け取るようにアクセス許可ポリシーを設定することができます。 たとえば、高いアクセス許可レベルを必要とし、50 人を超えるユーザーによって承認されたアプリがある場合、自動的にアラートを受け取ることができます。

OAuth アプリに関するポリシーでは、Office 365、G Suite、Salesforce について、各アプリで要求されたアクセス許可とそれを承認したユーザーを調査することができます。 これらのアクセス許可は、承認されているものまたは禁止されているものとしてマークすることもできます。 禁止されているものとしてマークすると、アプリを承認した各ユーザーのそれぞれのアプリのアクセス許可が取り消されます。

## <a name="create-a-new-oauth-app-policy"></a>新しい OAuth アプリ ポリシーを作成する

新しい OAuth アプリ ポリシーを作成するには、2 つの方法があります。 1 番目の方法は **[調査]** の下で行われ、2 番目の方法は **[コントロール]** の下で行われます。

新しい OAuth アプリ ポリシーを作成するには:

1. **[調査]** で、**[OAuth アプリ]** を選択します。

1. 必要に応じてアプリをフィルター処理します。たとえば、**メールボックスの予定表を変更**するための**アクセス許可**を要求するすべてのアプリを表示することができます。
1. **[検索に基づく新しいポリシー]** ボタンをクリックします。
    ![検索に基づく新しいポリシー](media/app-permissions-filter.png)
1. **[コミュニティの利用状況]** フィルターを使用して、アプリに対するアクセス許可が一般的であるか、一般的でないか、あるいはまれであるかに関する情報を取得することができます。 このフィルターは、珍しいアプリで、重大度レベルが高いアクセス許可か、多くのユーザーからのアクセス許可を要求する場合に便利です。
1. アプリを承認したユーザーのグループ メンバーシップに基づいてポリシーを設定できます。 たとえば、管理者は、アクセス許可を承認したユーザーが Administrators グループのメンバーである場合にのみ、一般的ではないアプリが高いアクセス許可を要求した場合にそれらを失効させるポリシーを設定することができます。

また、**[コントロール]**、**[ポリシー]** の順にクリックして、ポリシーを作成することもできます。 その後、**[ポリシーの作成]**、**[OAuth app policy]\(OAuth アプリ ポリシー\)** の順にクリックします。

   ![新しい OAuth アプリ ポリシー](media/app-permissions-policy.png)

## <a name="oauth-app-anomaly-detection-policies"></a>OAuth アプリの異常検出ポリシー

作成できる OAuth アプリポリシーに加えて、次のようなすぐに使用できる異常検出ポリシーがあります。これは、悪意のある可能性があるものを識別するために OAuth アプリのメタデータをプロファイルします。

| ポリシー名 | [ポリシーの説明] |
| --- | --- |
| 紛らわしい OAuth アプリ名 | 環境に接続されている OAuth アプリをスキャンし、誤った名前のアプリが検出されたときにアラートをトリガーします。 ラテン文字に似た形式でない名前は、悪意のあるアプリを既知の信頼できるアプリとして偽装しようとしている可能性があります。 |
| OAuth アプリの発行者名の誤用 | 環境に接続されている OAuth アプリをスキャンし、発行者名が誤っているアプリが検出されたときにアラートをトリガーします。 ラテン文字に似た外部文字などの正規の発行者名は、信頼されている既知の発行元からのアプリとして悪意のあるアプリを偽装しようとしている可能性があります。 |
| 悪意のある OAuth アプリの同意 | 環境に接続されている OAuth アプリをスキャンし、悪意のある可能性があるアプリが承認されたときにアラートをトリガーします。 悪意のある OAuth アプリは、ユーザーを侵害するために、フィッシングキャンペーンの一部として使用することができます。 この検出では、Microsoft のセキュリティ研究と脅威インテリジェンスの専門知識が利用されて、悪意のあるアプリが特定されます。 |

<!--
| OAuth apps authorized by external users | Scans OAuth apps connected to your environment and triggers an alert when an app was authorized by an external user. |
| OAuth apps with high permissions and rare community use – Google | Scans OAuth apps connected to your environment and triggers an alert for apps with high permissions and rare community use in Google. |
| OAuth apps with high permissions and rare community use – Office | Scans OAuth apps connected to your environment and triggers an alert for apps with high permissions and rare community use in Office. |
| OAuth apps with rare community use - Salesforce | Scans OAuth apps connected to your environment and triggers an alert for apps with rare community use in Salesforce. |
-->

> [!NOTE]
> 異常検出ポリシーは、Azure Active Directory で承認されている OAuth アプリでのみ使用できます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [データ保護ポリシー](data-protection-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
