---
title: Cloud App Security でコンテンツの検査が実行される方法
description: この記事では、Cloud App Security によりクラウド内のデータの DLP コンテンツ検査が実行されるときのプロセスについて説明します。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 1/6/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: cloud-app-security
ms.technology: ''
ms.reviewer: reutam
ms.suite: ems
ms.custom: seodec18
ms.openlocfilehash: c84a6522a39a2fb57189ee2eece60f24990bd1fa
ms.sourcegitcommit: e362bf01d41e82a82f9050a064ebfeb4307b58b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/14/2020
ms.locfileid: "84758427"
---
# <a name="content-inspection"></a>コンテンツ検査

*適用対象:Microsoft Cloud App Security*

コンテンツ検査を有効にする場合、事前設定された式を使用するか、他のカスタマイズされた式を検索するかを選択できます。

正規表現を指定して、結果からファイルを除外することができます。 このオプションは、ポリシーから除外する内部分類キーワード標準がある場合に非常に便利です。

ファイルが違反と見なされる前に、一致させるコンテンツ違反の最小数を設定できます。 たとえば、10 個以上のクレジット カード番号が含まれているファイルについてアラートを発行する場合は、10 を選択できます。

選択した式に対してコンテンツが一致すると、違反テキストが "X" という文字に置き換えられます。 既定では、違反はマスクされ、違反の前後の 100 文字のコンテキストが表示されます。 式のコンテキスト内の数値は "#" という文字に置き換えられ、Cloud App Security 内には格納されません。 **[違反の最後の 4 文字のマスクを解除する]** オプションを選択すると、違反の最後の 4 文字をマスク解除できます。 正規表現で検索するデータ型 (コンテンツ、メタデータ、ファイル名) を設定する必要があります。 既定では、コンテンツとメタデータが検索されます。

## <a name="content-inspection-for-protected-files"></a>保護されたファイルのコンテンツ検査

Cloud App Security では、管理者は、暗号化されたファイルの暗号化を解除し、そのコンテンツで違反をスキャンするためのアクセス許可を、Cloud App Security に付与することができます。

Cloud App Security に必要なアクセス許可を付与するには:

1. **[設定]** に移動し、 **[Azure Information Protection]** に移動します。
2. **[保護されたファイルを検査する]** を有効にします。
3. 表示されるメッセージに従って、Azure Active Directory で必要なアクセス許可を付与します。
4. ファイル ポリシーごとに設定を構成し、保護されたファイルをスキャンするポリシーを指定することができます。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [ポリシーによるクラウド アプリの制御](control-cloud-apps-with-policies.md)

[!INCLUDE [Open support ticket](includes/support.md)]
