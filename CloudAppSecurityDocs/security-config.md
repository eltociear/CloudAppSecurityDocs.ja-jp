---
title: Azure のセキュリティ構成に関する推奨事項を取得する - Cloud App Security | Microsoft Docs
description: この記事では、Azure Security Center と統合することによって Cloud App Security のセキュリティ構成に関する推奨事項を取得する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 8/1/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: e7acfac8168057b66e7c0295211ef0f29315600e
ms.sourcegitcommit: 6eff466c7a6817b14a60d8c3b2c201c7ae4c2e2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74720997"
---
# <a name="security-configuration-for-azure"></a>Azure のセキュリティ構成

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security では、お客様の Azure 環境のセキュリティ構成の評価を得ることができます。 この評価では、Azure Security Center を利用して、不足している構成とセキュリティ制御に関する推奨事項が提供されます。

## <a name="enable-security-configuration-recommendations"></a>セキュリティ構成に関する推奨事項を有効にする

この機能を使用するには、Azure AD と Azure portal での適切なアクセス許可が必要です。 既定では、Azure AD グローバル管理者のロールでは、Azure サブスクリプションにはアクセスできません。 自分や他のユーザーに対して Azure サブスクリプションへのアクセスを許可するには、ご自分のアクセス許可を昇格させます。

> [!IMPORTANT]
> 次のプロセスを完了した後は、この昇格を無効にすることをお勧めします。

Microsoft Cloud App Security でセキュリティ構成に関する推奨事項を有効にするには、次を実行します。

1. <a href="https://docs.microsoft.com/azure/security-center/security-center-management-groups" target="_blank">Azure Security Center に対するテナント全体の可視性を確保します</a>。 このプロセスには次のものが含まれます。

    - 自分自身と、このページへのアクセスを許可する他のすべての Microsoft Cloud App Security 管理者に対して、すべてのサブスクリプションの閲覧者のロールを付与する。
    - Azure Security Center のルート管理グループにロールを割り当てる
    - ご自分の Azure AD グローバル管理者を昇格させて、Azure サブスクリプションへのアクセスを許可する。
    - この記事では、セキュリティ管理者になるためのプロセスについて説明しています。 この統合を機能させるために必要な最小限のアクセス許可は、**閲覧者**です。

1. 変更を有効にするために、<a href="https://ms.portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/0" target="_blank">Azure Security Center</a> を必ず開いてください。

1. Cloud App Security で、 **[調査]**  >  **[セキュリティの構成]** の順に参照し、 **[Azure]** タブを選択します。

    - Microsoft Cloud App Security では、上位 50 件のサブスクリプションに対してのみ、推奨事項が提供されます。
    - 変更が有効になるまでに最大 15 分かかる場合があります。

    ![セキュリティの構成メニュー](media/security-configuration-menu.png)

1. 推奨事項は、種類、リソース、サブスクリプションごとにフィルター処理できます。 また、[セキュリティの構成] アイコン ![ASC アイコン](media/asc-icon.png) をクリックして Azure Security Center で推奨事項を開いて詳細情報を確認し、推奨事項についてさらに詳しく調べることができます。

セキュリティに関する推奨事項の実装方法の詳細については、[Azure Security Center でのセキュリティに関する推奨事項の管理](https://docs.microsoft.com/azure/security-center/security-center-recommendations)に関するページを参照してください。

![セキュリティの構成](media/security-configuration-azure.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
