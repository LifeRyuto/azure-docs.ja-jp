---
title: Azure Pipelines と Azure Application Insights による DevOps リリース パイプラインの継続的監視 | Microsoft Docs
description: Application Insights で行う継続的な監視を迅速にセットアップする手順を説明します
ms.service: azure-monitor
ms.subservice: application-insights
ms.topic: conceptual
author: mrbullwinkle
ms.author: mbullwin
ms.date: 07/16/2019
ms.openlocfilehash: c891cc7564a60dfd665d84d569e266332d255fa9
ms.sourcegitcommit: 1bd2207c69a0c45076848a094292735faa012d22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72677515"
---
# <a name="add-continuous-monitoring-to-your-release-pipeline"></a>リリース パイプラインに継続的監視を追加する

Azure Pipelines と Azure Application Insights を統合すると、ソフトウェア開発ライフ サイクルを通じて DevOps リリース パイプラインを継続的に監視できます。 

継続的な監視により、リリース パイプラインに Application Insights などの Azure リソースから監視データを組み込むことができます。 リリース パイプラインで Application Insights アラートが検出されると、アラートが解決されるまで、パイプラインによってデプロイがゲート処理またはロールバックされる可能性があります。 すべてのチェックが成功すると、展開はテストから実稼働まですべて自動で進められます。手動による介入は必要ありません。 

## <a name="configure-continuous-monitoring"></a>継続的監視を構成する

1. [Azure DevOps](https://dev.azure.com) で、組織とプロジェクトを選択します。
   
1. プロジェクト ページの左側のメニューで、 **[パイプライン]**  >  **[リリース]** を選択します。 
   
1. **[新規]** の横にあるドロップダウンの矢印を展開し、 **[新しいリリース パイプライン]** を選択します。 また、まだパイプラインがない場合は、表示されるページで **[新しいパイプライン]** を選択します。
   
1. **[テンプレートの選択]** ウィンドウで **[継続的監視を使用した Azure App Service の配置]** を探して選択し、 **[適用]** を選択します。 

   ![新しい Azure Pipelines のリリース パイプライン](media/continuous-monitoring/001.png)

1. **[ステージ 1]** ボックスで、 **[ステージ タスクを表示します]** のハイパーリンクを選択します。

   ![ステージ タスクを表示する](media/continuous-monitoring/002.png)

1. **[ステージ 1]** 構成ウィンドウで、次のフィールドを入力します。 

    | パラメーター        | 値 |
   | ------------- |:-----|
   | **ステージ名**      | ステージ名を指定するか、 **[ステージ 1]** のままにします。 |
   | **Azure サブスクリプション** | ドロップダウンを展開して、使用するリンク済み Azure サブスクリプションを選択します。|
   | **アプリの種類** | ドロップダウンを展開して、アプリの種類を選択します。 |
   | **App Service の名前** | Azure App Service の名前を入力します。 |
   | **Application Insights 用のリソース グループ名**    | ドロップダウンを展開して、使用するリソース グループを選択します。 |
   | **Application Insights のリソース名** | ドロップダウンを展開して、選択したリソース グループの Application Insights リソースを選択します。

1. 既定のアラート ルール設定でパイプラインを保存するには、Azure DevOps ウィンドウの右上にある **[保存]** を選択します。 わかりやすいコメントを入力し、 **[OK]** を選択します。

## <a name="modify-alert-rules"></a>アラート ルールを変更する

すぐに使用できる**継続的監視を使用した Azure App Service の配置**テンプレートには、4 つのアラート ルールがあります。**可用性**、**失敗した要求**、**サーバー応答時間**、**サーバーの例外**です。 サービス レベルのニーズに合わせて、ルールを追加したり、ルール設定を変更したりすることができます。 

アラート ルール設定を変更するには:

1. リリース パイプライン ページの左側のウィンドウで、 **[Configure Application Insights Alerts]\(Application Insights アラートの構成\)** を選択します。

1. **[Azure Monitor アラート]** ウィンドウで、 **[アラート ルール]** の横にある省略記号 ( **...** ) を選択します。
   
1. **[アラート ルール]** ダイアログで、アラート ルールの横にあるドロップダウン記号 ( **[可用性]** など) を選択します。 
   
1. お客様の要件に合わせて **[しきい値]** とその他の設定を変更します。
   
   ![アラートを変更する](media/continuous-monitoring/003.png)
   
1. **[OK]** を選択し、次に Azure DevOps ウィンドウの右上にある **[保存]** を選択します。 わかりやすいコメントを入力し、 **[OK]** を選択します。

## <a name="add-deployment-conditions"></a>展開の条件を追加する

リリース パイプラインに配置ゲートを追加すると、設定したしきい値を超えるアラートによって、不要なリリース プロモーションが防止されます。 アラートを解決すると、配置は自動的に進められます。

配置ゲートを追加するには:

1. メイン パイプライン ページの **[ステージ]** で、どのステージで連続監視ゲートが必要かに応じて、 **[配置前条件]** または **[配置後の条件]** シンボルを選択します。
   
   ![配置前条件](media/continuous-monitoring/004.png)
   
1. **[配置前条件]** 構成ウィンドウで、 **[ゲート]** を **[有効]** に設定します。
   
1. **[ゲートの配置]** の横にある **[追加]** を選択します。
   
1. ドロップダウン メニューから **[Azure Monitor アラートのクエリ]** を選択します。 このオプションを使用すると、Azure Monitor と Application Insights の両方のアラートにアクセスできます。
   
   ![Azure Monitor アラートのクエリ](media/continuous-monitoring/005.png)
   
1. **[評価のオプション]** で、 **[ゲートの再評価までの時間]** や **[ゲートが失敗するまでのタイムアウト]** など、設定に必要な値を入力します。 

## <a name="view-release-logs"></a>リリース ログを表示する

リリース ログで、配置ゲートの動作やその他のリリース手順を確認できます。 ログを開くには:

1. パイプライン ページの左側のメニューから **[リリース]** を選択します。 
   
1. 任意のリリースを選択します。 
   
1. **[ステージ]** で、ステージを選択してリリースの概要を表示します。 
   
1. ログを表示するには、リリースの概要で **[ログの表示]** を選択するか、任意のステージで **[成功]** または **[失敗]** のハイパーリンクを選択するか、任意のステージにカーソルを合わせて **[ログ]** を選択します。 
   
   ![リリース ログを表示する](media/continuous-monitoring/006.png)

## <a name="next-steps"></a>次の手順

Azure Pipelines の詳細については、[Azure Pipelines のドキュメント](https://docs.microsoft.com/azure/devops/pipelines)を参照してください。
