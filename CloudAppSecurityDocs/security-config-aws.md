---
title: AWS のセキュリティ構成に関する推奨事項を取得する
description: この記事では、アマゾン ウェブ サービスと統合することによって Cloud App Security のセキュリティ構成に関する推奨事項を取得する方法について説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/28/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: 904dc2c6a86d135502c81fd3037b9b8ca4459d99
ms.sourcegitcommit: b15034dd50142afd8e95de22a9232f711b1eae6e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85625014"
---
# <a name="security-configuration-for-aws"></a>AWS のセキュリティ構成

*適用対象:Microsoft Cloud App Security*

Microsoft Cloud App Security では、お客様のアマゾン ウェブ サービス環境のセキュリティ構成の評価を得ることができます。 この評価では、AWS の Center for Internet Security (CIS) ベンチマークに基づく基本的なセキュリティに関する推奨事項が提供されます。

## <a name="prerequisites"></a>[前提条件]

- AWS Security Hub は、すべての AWS アカウント リージョンに対して設定する必要があります。 詳細については、「[AWS Security Hub のセットアップ](https://go.microsoft.com/fwlink/?linkid=2100208)」を参照してください。
    > [!NOTE]
    > 初めて Security Hub を有効にする場合、初期データが使用可能になるまでに数時間かかることがあります。
- ご自分のアマゾン ウェブ サービスが Cloud App Security に接続されている必要があります。 詳細については、「[AWS を Microsoft Cloud App Security に接続する](connect-aws-to-microsoft-cloud-app-security.md)」を参照してください。

## <a name="how-to-view-aws-security-recommendations"></a>AWS のセキュリティに関する推奨事項を表示する方法

1. Cloud App Security で、 **[調査]**  >  **[セキュリティの構成]** の順に参照し、 **[アマゾン ウェブ サービス]** タブを選択します。

    > [!NOTE]
    > 変更が有効になるまでに最大 15 分かかる場合があります。

    ![セキュリティの構成メニュー](media/security-configuration-menu.png)

1. 推奨事項は、種類、リソース、アカウントごとにフィルター処理できます。 また、[セキュリティの構成] アイコン ![ASC アイコン](media/asc-icon.png) をクリックして Amazon Security Hub で推奨事項を開いて詳細情報を確認し、推奨事項についてさらに詳しく調べることができます。

    ![セキュリティの構成](media/security-configuration-aws.png)

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
