---
title: Cloud App Security が Office 365 環境の保護にどのように役立つか
description: この記事では、Office 365 アプリを Cloud App Security に接続する利点について説明します。 API コネクタを使用して、使用状況を表示したり制御したりすることができます。
author: shsagir
ms.author: shsagir
ms.service: cloud-app-security
ms.topic: article
ms.date: 12/04/2019
ms.collection: M365-security-compliance
ms.openlocfilehash: 40105f8e4a43f61d5f5c00c3fab1c6b58b03e940
ms.sourcegitcommit: db5ec79d219dd6674939c872ace7cd2ca80860a4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75190152"
---
# <a name="how-cloud-app-security-helps-protect-your-office-365-environment"></a>Cloud App Security が Office 365 環境の保護にどのように役立つか

*適用対象: Microsoft Cloud App Security*

クラウドファイルストレージ、コラボレーション、BI、CRM ツールを提供する主要な生産性スイートである Office 365 を使用すると、ユーザーは組織やパートナー全体でドキュメントを効率的かつ効率的な方法で共有できます。 Office 365 を使用すると、内部的にだけでなく外部コラボレーターにも機密データが公開され、さらには共有リンク経由で公開されるようになります。 このようなインシデントは、悪意のあるアクターが原因で発生する可能性があります。 Office 365 では、生産性を向上させるために、大規模なサードパーティ製のアプリのエコシステムも提供しています。 これらのアプリを使用すると、悪意のあるアプリや過剰なアクセス許可を持つアプリを使用するリスクに組織をさらす可能性があります。

Office 365 を Cloud App Security に接続すると、ユーザーのアクティビティに関する洞察が向上し、機械学習ベースの異常検出、情報保護検出 (外部情報共有の検出など) を使用して脅威検出を行うことができます。) によって、自動修復コントロールが有効になり、組織内の有効なサードパーティアプリからの脅威が検出されます。

Office 365 コネクタを使用すると、次の製品が保護されます。

- Office 365
- Dynamics 365 CRM
- Exchange
- OneDrive
- Power BI
- SharePoint
- 担当

## <a name="main-threats"></a>主な脅威

- 侵害されたアカウントと内部の脅威
- データ漏えい
- セキュリティ意識の不足
- 悪意のあるサードパーティ製アプリ
- マルウェア
- 対策
- 攻撃
- 管理されていない独自のデバイスの持ち込む (BYOD)

## <a name="how-cloud-app-security-helps-to-protect-your-environment"></a>Cloud App Security が環境の保護にどのように役立つか

- [クラウドの脅威、侵害されたアカウント、悪意のある内部関係者の検出](best-practices.md#detect-cloud-threats-compromised-accounts-malicious-insiders-and-ransomware)
- [クラウドに格納されている規制対象の機密データを検出、分類、ラベル付け、保護する](best-practices.md#discover-classify-label-and-protect-regulated-and-sensitive-data-stored-in-the-cloud)
- [環境にアクセスできる OAuth アプリを検出して管理する](manage-app-permissions.md)
- [クラウドに格納されているデータに DLP ポリシーとコンプライアンスポリシーを適用する](best-practices.md#enforce-dlp-and-compliance-policies-for-data-stored-in-the-cloud)
- [共有データの公開を制限し、コラボレーションポリシーを適用する](best-practices.md#limit-exposure-of-shared-data-and-enforce-collaboration-policies)
- [フォレンジック調査のためにアクティビティの監査証跡を使用する](best-practices.md#use-the-audit-trail-of-activities-for-forensic-investigations)

## <a name="control-office-365-with-built-in-policies-and-policy-templates"></a>組み込みのポリシーとポリシーテンプレートを使用して Office 365 を管理する

次の組み込みポリシーテンプレートを使用して、潜在的な脅威についての検出と通知を行うことができます。

| 種類 | 名前 |
| ---- | ---- |
| 組み込みの異常検出ポリシー | [匿名 IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-anonymous-ip-addresses)<br />[頻度の低い国からのアクティビティ](anomaly-detection-policy.md#activity-from-infrequent-country)<br />[不審な IP アドレスからのアクティビティ](anomaly-detection-policy.md#activity-from-suspicious-ip-addresses)<br />[あり得ない移動](anomaly-detection-policy.md#impossible-travel)<br />[終了したユーザーによって実行されるアクティビティ](anomaly-detection-policy.md#activity-performed-by-terminated-user)(AAD は IdP として必要)<br />[マルウェアの検出](anomaly-detection-policy.md#malware-detection)<br />[複数回失敗したログイン試行](anomaly-detection-policy.md#multiple-failed-login-attempts)<br />[ランサムウェアの検出](anomaly-detection-policy.md#ransomware-activity)<br />[疑わしいメール削除アクティビティ (プレビュー)](anomaly-detection-policy.md#suspicious-email-deletion-activity-preview)<br />[疑わしい受信トレイ転送](anomaly-detection-policy.md#suspicious-inbox-forwarding)の[異常なファイル削除アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[通常とは異なるファイル共有アクティビティ](anomaly-detection-policy.md#unusual-activities-by-user)<br />[通常とは異なる複数ファイルのダウンロードアクティビティ](anomaly-detection-policy.md#unusual-activities-by-user) |
| アクティビティポリシーテンプレート | Logon from a risky IP address (危険な IP アドレスからのログオン)<br />Mass download by a single user (1 人のユーザーによる大量ダウンロード)<br />ランサムウェア アクティビティの可能性 |
| ファイルポリシーテンプレート | 承認されていないドメインで共有されているファイルを検出する<br />個人用電子メールアドレスで共有されるファイルを検出する<br />PII/PCI/PHI を使用したファイルの検出 |
| OAuth アプリの異常検出ポリシー | [紛らわしい OAuth アプリ名](app-permission-policy.md#oauth-app-anomaly-detection-policies)<br />[OAuth アプリの発行者名の誤用](app-permission-policy.md#oauth-app-anomaly-detection-policies) |

ポリシーの作成の詳細については、「[ポリシーを作成する](control-cloud-apps-with-policies.md#create-a-policy)」を参照してください。

## <a name="automate-governance-controls"></a>ガバナンスコントロールの自動化

潜在的な脅威を監視するだけでなく、次の Office 365 ガバナンスアクションを適用して自動化し、検出された脅威を修復することができます。

| 種類 | 操作 |
| ---- | ---- |
| データガバナンス | **OneDrive:**<br /> -親フォルダーのアクセス許可を継承する<br /> -ファイル/フォルダーをプライベートにする<br /> -ファイル/フォルダーを管理者検疫に配置します<br /> -ファイル/フォルダーをユーザー検疫に配置します<br /> -ファイル/フォルダーをごみ箱に入れます。<br /> -特定のコラボレーターを削除します<br /> -ファイル/フォルダーの外部コラボレーターを削除します<br /> -分類ラベルを適用 Azure Information Protection<br /> -Azure Information Protection 分類ラベルを削除します<br /> **SharePoint**<br /> -親フォルダーのアクセス許可を継承する<br /> -ファイル/フォルダーをプライベートにする<br /> -ファイル/フォルダーを管理者検疫に配置します<br /> -ファイル/フォルダーをユーザー検疫に配置します<br /> -ファイル/フォルダーをユーザー検疫に配置し、所有者のアクセス許可を追加します。<br /> -ファイル/フォルダーをごみ箱に入れます。<br /> -ファイル/フォルダーの外部コラボレーターを削除します<br /> -特定のコラボレーターを削除します<br /> -分類ラベルを適用 Azure Information Protection<br /> -Azure Information Protection 分類ラベルを削除します |
| ユーザーガバナンス | -警告をユーザーに通知する (Azure AD 経由)<br /> -ユーザーにもう一度サインインするように要求します (Azure AD 経由)<br /> -ユーザーの中断 (Azure AD 経由) |
| OAuth アプリガバナンス | -OAuth アプリのアクセス許可を取り消す |

アプリからの修復脅威の詳細については、「[接続されているアプリの管理](governance-actions.md)」を参照してください。

## <a name="protect-office-365-in-real-time"></a>Office 365 をリアルタイムで保護する

[外部ユーザーとのセキュリティ保護とコラボレーション](best-practices.md#secure-collaboration-with-external-users-by-enforcing-real-time-session-controls)に関するベストプラクティスを確認し、[機密データのダウンロードをアンマネージまたは危険なデバイスにブロックして保護](best-practices.md#block-and-protect-download-of-sensitive-data-to-unmanaged-or-risky-devices)します。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Office 365 を Microsoft Cloud App Security に接続する方法](connect-office-365-to-microsoft-cloud-app-security.md)