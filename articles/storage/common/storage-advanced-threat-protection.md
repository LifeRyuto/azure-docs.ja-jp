---
title: Advanced Threat Protection の構成
titleSuffix: Azure Storage
description: アカウント アクティビティの異常を検出するように、ご利用のアカウントへの害を及ぼす可能性のあるアクセス試行が通知されるように、Advanced Threat Protection for Azure Storage を構成します。
services: storage
author: tamram
ms.service: storage
ms.topic: conceptual
ms.date: 02/04/2020
ms.author: tamram
ms.reviewer: cbrooks
ms.openlocfilehash: d97b63aa87bfd8cf8ca1a3f5b213d6b16ca066df
ms.sourcegitcommit: f15f548aaead27b76f64d73224e8f6a1a0fc2262
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77616858"
---
# <a name="configure-advanced-threat-protection-for-azure-storage"></a>Advanced Threat Protection for Azure Storage を構成する

Advanced Threat Protection for Azure Storage では、ストレージ アカウントに対する通常と異なる潜在的に有害なアクセスの試行すなわちストレージ アカウントの悪用を検出するセキュリティ インテリジェンス レイヤーが追加されます。 この保護レイヤーにより、セキュリティの専門家でなくても、セキュリティ監視システムを管理しなくても、脅威に対処することができます。

セキュリティ アラートは、アクティビティで異常が発生したときにトリガーされます。 これらのセキュリティ アラートは [Azure Security Center](https://azure.microsoft.com/services/security-center/) と統合されます。さらに、不審なアクティビティの詳細と、脅威の調査や修復方法に関する推奨事項と共に、サブスクリプション管理者にメールで送信されます。

> [!NOTE]
> Advanced Threat Protection for Azure Storage は、現時点では BLOB ストレージでのみ使用できます。 Azure Government およびソブリン クラウド リージョンでは利用できません。 30 日間の無料試用など、価格の詳細については、[Azure Security Center の価格ページ]( https://azure.microsoft.com/pricing/details/security-center/)を参照してください。

Advanced Threat Protection for Azure Storage では、脅威の検出のため、BLOB ストレージに対する読み取り要求、書き込み要求、削除要求の診断ログが取り込まれます。 Advanced Threat Protection からのアラートを調査するために、Storage Analytics Logging を使用して関連するストレージのアクティビティを確認することができます。 詳細については、「[Azure portal でのストレージ アカウントの監視](storage-monitor-storage-account.md#configure-logging)」の「**ログの構成**」を参照してください。

## <a name="set-up-advanced-threat-protection"></a>Advanced Threat Protection の設定

Advanced Threat Protection は、次のセクションで説明するいくつかの方法で構成することができます。

### <a name="portal"></a>[ポータル](#tab/azure-portal)

1. [Azure ポータル](https://portal.azure.com/)を開きます。
1. ご利用の Azure Storage アカウントに移動します。 **[設定]** で **[高度なセキュリティ]** を選択します。
1. 高度なセキュリティの構成ページで、 **[設定]** リンクを選択します。
1. **[高度なセキュリティ]** を **[オン]** に設定します。
1. **[保存]** をクリックして、新しいポリシーまたは更新されたポリシーを保存します。

    ![Azure Storage Advanced Threat Protection をオンにする](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-turn-on.png)

### <a name="azure-security-center"></a>[Azure Security Center](#tab/azure-security-center)

Azure Security Center で Standard レベルにサブスクライブすると、Advanced Threat Protection がご利用のすべてのストレージ アカウントで自動的に設定されます。 次のようにして、特定のサブスクリプションのストレージ アカウントで Advanced Threat Protection を有効または無効にすることができます。

1. [Azure portal](https://portal.azure.com) で **Azure Security Center** を起動します。
1. メイン メニューで、 **[Pricing & settings]\(価格と設定\)** をクリックします。
1. ストレージ アカウントの脅威の防止を有効または無効にするサブスクリプションをクリックします。

    ![サブスクリプションの選択](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-subscription.png)

1. **[価格レベル]** をクリックします。
1. **[リソースの種類ごとに価格レベルを選択]** セクションの **[ストレージアカウント]** 行で、 **[有効]** または **[無効]** をクリックします。

    ![Security Center で ATP を有効にする](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-pricing2.png)
1. **[保存]** をクリックします。

### <a name="template"></a>[テンプレート](#tab/template)

Azure Resource Manager テンプレートを使用して、Advanced Threat Protection が有効になっている Azure Storage アカウントをデプロイします。 詳細については、[Advanced Threat Protection でのストレージ アカウント](https://azure.microsoft.com/resources/templates/201-storage-advanced-threat-protection-create/)に関するページを参照してください。

### <a name="azure-policy"></a>[Azure Policy](#tab/azure-policy)

特定のサブスクリプションまたはリソース グループ内のストレージ アカウント全体で Advanced Threat Protection を有効にするには、Azure Policy を使用します。

1. Azure の **[ポリシー - 定義]** ページを起動します。

1. **[ストレージ アカウントで Advanced Threat Protection をデプロイします]** ポリシーを探します。

     ![ポリシーを探す](./media/storage-advanced-threat-protection/storage-atp-policy-definitions.png)

1. Azure サブスクリプションまたはリソース グループを選択します。

    ![サブスクリプションまたはグループを選択する](./media/storage-advanced-threat-protection/storage-atp-policy2.png)

1. ポリシーを割り当てます。

    ![[ポリシー定義] ページ](./media/storage-advanced-threat-protection/storage-atp-policy1.png)

### <a name="rest-api"></a>[REST API](#tab/rest-api)

Rest API のコマンドを使用して、特定のストレージ アカウントの Advanced Threat Protection 設定を作成、更新、または取得します。

* [Advanced Threat Protection - 作成](https://docs.microsoft.com/rest/api/securitycenter/advancedthreatprotection/create)
* [Advanced Threat Protection - 取得](https://docs.microsoft.com/rest/api/securitycenter/advancedthreatprotection/get)

### <a name="powershell"></a>[PowerShell](#tab/azure-powershell)

次の PowerShell コマンドレットを使用します。

* [Advanced Threat Protection を有効にする](https://docs.microsoft.com/powershell/module/az.security/enable-azsecurityadvancedthreatprotection)
* [Advanced Threat Protection を取得する](https://docs.microsoft.com/powershell/module/az.security/get-azsecurityadvancedthreatprotection)
* [Advanced Threat Protection を無効にする](https://docs.microsoft.com/powershell/module/az.security/disable-azsecurityadvancedthreatprotection)

---

## <a name="explore-security-anomalies"></a>セキュリティ異常を調べる

ストレージ アクティビティの異常が発生すると、疑わしいセキュリティ イベントに関する情報を含む通知が電子メールで送信されます。 イベントの詳細には、次のものが含まれます。

* 異常の種類
* ストレージ アカウント名
* イベント時間
* ストレージの種類
* 考えられる原因
* 調査手順
* 修復手順

電子メールには、潜在的な脅威の考えられる原因と調査や緩和のための推奨されるアクションについての詳細も含まれます。

![Azure Storage Advanced Threat Protection のアラート メール](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-alert-email.png)

Azure Security Center の [[セキュリティ アラート]](../../security-center/security-center-managing-and-responding-alerts.md) タイルから、現在のセキュリティ アラートを確認して管理することができます。 特定のアラートをクリックすると、詳細な情報と、現在の脅威を調査し、今後の脅威に対処するためのアクションが表示されます。

![Azure Storage Advanced Threat Protection のアラート メール](./media/storage-advanced-threat-protection/storage-advanced-threat-protection-alert.png)

## <a name="security-alerts"></a>セキュリティのアラート

アラートは、ストレージ アカウントへの通常とは異なる、害を及ぼす可能性のあるアクセス試行やストレージ アカウントの悪用が発生すると、生成されます。 Azure Storage のアラートの一覧については、[Azure Security Center でのデータ サービスの脅威の防止](https://docs.microsoft.com/azure/security-center/alerts-reference#alerts-azurestorage)に関するページの、**ストレージ**に関するセクションを参照してください。

## <a name="next-steps"></a>次のステップ

* [Azure Storage アカウントのログ](/rest/api/storageservices/About-Storage-Analytics-Logging)に関する詳細を確認する
* [Azure Security Center](../../security-center/security-center-intro.md) の詳細について参照してください
