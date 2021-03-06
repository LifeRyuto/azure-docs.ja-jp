---
title: 仮想コア リソース制限 - エラスティック プール
description: このページでは、Azure SQL Database のエラスティック プールに対するいくつかの一般的な仮想コアのリソース制限について説明します。
services: sql-database
ms.service: sql-database
ms.subservice: elastic-pools
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: oslake
ms.author: moslake
ms.reviewer: carlrab, sstein
ms.date: 01/09/2020
ms.openlocfilehash: f6b7797fbebd3d1df3da3405926543d716e584f4
ms.sourcegitcommit: f53cd24ca41e878b411d7787bd8aa911da4bc4ec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75835095"
---
# <a name="resource-limits-for-elastic-pools-using-the-vcore-purchasing-model"></a>仮想コア購入モデルを使用したエラスティック プールに対するリソース制限

この記事では、仮想コア購入モデルを使用した、Azure SQL Database のエラスティック プールとプールされたデータベースに対する詳細なリソース制限について説明します。

DTU 購入モデルの制限については、[SQL Database の DTUのリソース制限 - エラスティック プール](sql-database-dtu-resource-limits-elastic-pools.md)に関する記事を参照してください。

> [!IMPORTANT]
> 場合によっては、未使用領域を再利用できるようにデータベースを縮小する必要があります。 詳細については、「[Manage file space in Azure SQL Database](sql-database-file-space-management.md)」(Azure SQL Database でファイル領域を管理する) を参照してください。

[Azure Portal](sql-database-elastic-pool-manage.md#azure-portal-manage-elastic-pools-and-pooled-databases)、[PowerShell](sql-database-elastic-pool-manage.md#powershell-manage-elastic-pools-and-pooled-databases)、[Azure CLI](sql-database-elastic-pool-manage.md#azure-cli-manage-elastic-pools-and-pooled-databases)、または [REST API](sql-database-elastic-pool-manage.md#rest-api-manage-elastic-pools-and-pooled-databases) を使って、サービス レベル、コンピューティング サイズ、ストレージ容量を設定できます。

> [!IMPORTANT]
> スケーリングのガイダンスと考慮事項については、[エラスティック プールのスケーリング](sql-database-elastic-pool-scale.md)に関するページを参照してください

## <a name="general-purpose---provisioned-compute---gen4"></a>General Purpose - プロビジョニング済みコンピューティング - Gen4

> [!IMPORTANT]
> 新しい Gen4 データベースは、オーストラリア東部とブラジル南部リージョンでサポートされなくなりました。

### <a name="general-purpose-service-tier-generation-4-compute-platform-part-1"></a>General Purpose サービス レベル:第 4 世代コンピューティング プラットフォーム (パート 1)

|コンピューティング サイズ|GP_Gen4_1|GP_Gen4_2|GP_Gen4_3|GP_Gen4_4|GP_Gen4_5|GP_Gen4_6
|:--- | --: |--: |--: |--: |--: |--: |
|コンピューティング世代|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|仮想コア|1|2|3|4|5|6|
|メモリ (GB)|7|14|21|28|35|42|
|プールあたりの最大 DB 数|100|200|500|500|500|500|
|列ストアをサポート|はい|はい|はい|はい|はい|はい|
|インメモリ OLTP ストレージ (GB)|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|データの最大サイズ (GB)|512|756|1536|1536|1536|2048|
|最大ログ サイズ|154|227|461|461|461|614|
|TempDB の最大データ サイズ (GB)|32|64|96|128|160|192|
|ストレージの種類|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|
|IO 待機時間 (概算)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|400|800|1200|1600|2000|2400|
|プールあたりの最大ログ レート (MBps)|4.7|9.4|14.1|18.8|23.4|28.1|
|プールあたりの最大同時実行ワーカー (要求) 数 ** |210|420|630|840|1050|1260|
|プールあたりの最大同時ログイン数 ** |210|420|630|840|1050|1260|
|最大同時セッション数|30,000|30,000|30,000|30,000|30,000|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0、0.25、0.5、1|0、0.25、0.5、1、2|0、0.25、0.5、1...3|0、0.25、0.5、1...4|0、0.25、0.5、1...5|0、0.25、0.5、1...6|
|レプリカの数|1|1|1|1|1|1|
|マルチ AZ|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|読み取りスケールアウト|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|含まれるバックアップ ストレージ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

### <a name="general-purpose-service-tier-generation-4-compute-platform-part-2"></a>General Purpose サービス レベル:第 4 世代コンピューティング プラットフォーム (パート 2)

|コンピューティング サイズ|GP_Gen4_7|GP_Gen4_8|GP_Gen4_9|GP_Gen4_10|GP_Gen4_16|GP_Gen4_24|
|:--- | --: |--: |--: |--: |--: |--: |
|コンピューティング世代|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|仮想コア|7|8|9|10|16|24|
|メモリ (GB)|49|56|63|70|112|159.5|
|プールあたりの最大 DB 数|500|500|500|500|500|500|
|列ストアをサポート|はい|はい|はい|はい|はい|はい|
|インメモリ OLTP ストレージ (GB)|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|データの最大サイズ (GB)|2048|2048|2048|2048|3584|4096|
|最大ログ サイズ (GB)|614|614|614|614|1075|1229|
|TempDB の最大データ サイズ (GB)|224|256|288|320|512|768|
|ストレージの種類|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|
|IO 待機時間 (概算)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|2800|3200|3600|4000|6400|9600|
|プールあたりの最大ログ レート (MBps)|32.8|37.5|37.5|37.5|37.5|37.5|
|プールあたりの最大同時実行ワーカー (要求) 数 *|1470|1680|1890|2100|3360|5040|
|プールあたりの最大同時ログイン (要求) 数*|1470|1680|1890|2100|3360|5040|
|最大同時セッション数|30,000|30,000|30,000|30,000|30,000|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0、0.25、0.5、1...7|0、0.25、0.5、1...8|0、0.25、0.5、1...9|0、0.25、0.5、1...10|0、0.25、0.5、1...10、16|0、0.25、0.5、1...10、16、24|
|レプリカの数|1|1|1|1|1|1|
|マルチ AZ|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|読み取りスケールアウト|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|含まれるバックアップ ストレージ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|

\* 個々のデータベースの最大同時実行ワーカー数については、「[Single database resource limits (単一データベースのリソース制限)](sql-database-vcore-resource-limits-single-databases.md)」を参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

## <a name="general-purpose---provisioned-compute---gen5"></a>General Purpose - プロビジョニング済みコンピューティング - Gen5

### <a name="general-purpose-service-tier-generation-5-compute-platform-part-1"></a>General Purpose サービス レベル:第 5 世代コンピューティング プラットフォーム (パート 1)

|コンピューティング サイズ|GP_Gen5_2|GP_Gen5_4|GP_Gen5_6|GP_Gen5_8|GP_Gen5_10|GP_Gen5_12|GP_Gen5_14|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|コンピューティング世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|
|仮想コア|2|4|6|8|10|12|14|
|メモリ (GB)|10.4|20.8|31.1|41.5|51.9|62.3|72.7|
|プールあたりの最大 DB 数|100|200|500|500|500|500|500|
|列ストアをサポート|はい|はい|はい|はい|はい|はい|はい|
|インメモリ OLTP ストレージ (GB)|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|データの最大サイズ (GB)|512|756|1536|1536|1536|2048|2048|
|最大ログ サイズ (GB)|154|227|461|461|461|614|614|
|TempDB の最大データ サイズ (GB)|64|128|192|256|320|384|448|
|ストレージの種類|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|
|IO 待機時間 (概算)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|800|1600|2400|3200|4000|4800|5600|
|プールあたりの最大ログ レート (MBps)|9.4|18.8|28.1|37.5|37.5|37.5|37.5|
|プールあたりの最大同時実行ワーカー (要求) 数 **|210|420|630|840|1050|1260|1470|
|プールあたりの最大同時ログイン (要求) 数 **|210|420|630|840|1050|1260|1470|
|最大同時セッション数|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0、0.25、0.5、1、2|0、0.25、0.5、1...4|0、0.25、0.5、1...6|0、0.25、0.5、1...8|0、0.25、0.5、1...10|0、0.25、0.5、1...12|0、0.25、0.5、1...14|
|レプリカの数|1|1|1|1|1|1|1|
|マルチ AZ|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|読み取りスケールアウト|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|含まれるバックアップ ストレージ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。その他の 1 仮想コア以下のデータベースあたりの最大仮想コア数設定では、最大同時ワーカー数が同様に再スケールされます。

### <a name="general-purpose-service-tier-generation-5-compute-platform-part-2"></a>General Purpose サービス レベル:第 5 世代コンピューティング プラットフォーム (パート 2)

|コンピューティング サイズ|GP_Gen5_16|GP_Gen5_18|GP_Gen5_20|GP_Gen5_24|GP_Gen5_32|GP_Gen5_40|GP_Gen5_80|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|コンピューティング世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|
|仮想コア|16|18|20|24|32|40|80|
|メモリ (GB)|83|93.4|103.8|124.6|166.1|207.6|415.2|
|プールあたりの最大 DB 数|500|500|500|500|500|500|500|
|列ストアをサポート|はい|はい|はい|はい|はい|はい|はい|
|インメモリ OLTP ストレージ (GB)|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|データの最大サイズ (GB)|2048|3072|3072|3072|4096|4096|4096|
|最大ログ サイズ (GB)|614|922|922|922|1229|1229|1229|
|TempDB の最大データ サイズ (GB)|512|576|640|768|1024|1280|2560|
|ストレージの種類|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|Premium (リモート) ストレージ|
|IO 待機時間 (概算)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS * |6,400|7,200|8,000|9,600|12,800|16,000|32,000|
|プールあたりの最大ログ レート (MBps)|37.5|37.5|37.5|37.5|37.5|37.5|37.5|
|プールあたりの最大同時実行ワーカー (要求) 数 **|1680|1890|2100|2520|3360|4200|8400|
|プールあたりの最大同時ログイン (要求) 数 **|1680|1890|2100|2520|3360|4200|8400|
|最大同時セッション数|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0、0.25、0.5、1...16|0、0.25、0.5、1...18|0、0.25、0.5、1...20|0、0.25、0.5、1...20、24|0、0.25、0.5、1...20、24、32|0、0.25、0.5、1...16、24、32、40|0、0.25、0.5、1...16、24、32、40、80|
|レプリカの数|1|1|1|1|1|1|1|
|マルチ AZ|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|読み取りスケールアウト|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|含まれるバックアップ ストレージ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

## <a name="general-purpose---provisioned-compute---fsv2-series"></a>General Purpose - プロビジョニング済みコンピューティング - Fsv2 シリーズ

### <a name="fsv2-series-compute-generation-preview"></a>Fsv2 シリーズのコンピューティング世代 (プレビュー)

|コンピューティング サイズ|GP_Fsv2_72|
|:--- | --: |
|コンピューティング世代|Fsv2 シリーズ|
|仮想コア|72|
|メモリ (GB)|136.2|
|プールあたりの最大 DB 数|500|
|列ストアをサポート|はい|
|インメモリ OLTP ストレージ (GB)|該当なし|
|データの最大サイズ (GB)|4096|
|最大ログ サイズ (GB)|1024|
|TempDB の最大データ サイズ (GB)|333|
|ストレージの種類|Premium (リモート) ストレージ|
|IO 待機時間 (概算)|5 ～ 7 ミリ秒 (書き込み)<br>5 ～ 10 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|16,000|
|プールあたりの最大ログ レート (MBps)|37.5|
|プールあたりの最大同時実行ワーカー (要求) 数 **|3780|
|プールあたりの最大同時ログイン (要求) 数 **|3780|
|最大同時セッション数|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0 から 72|
|レプリカの数|1|
|マルチ AZ|該当なし|
|読み取りスケールアウト|該当なし|
|含まれるバックアップ ストレージ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

## <a name="business-critical---provisioned-compute---gen4"></a>Business Critical - プロビジョニング済みコンピューティング - Gen4

> [!IMPORTANT]
> 新しい Gen4 データベースは、オーストラリア東部とブラジル南部リージョンでサポートされなくなりました。

### <a name="business-critical-service-tier-generation-4-compute-platform-part-1"></a>Business Critical サービス レベル:第 4 世代コンピューティング プラットフォーム (パート 1)

|コンピューティング サイズ|BC_Gen4_2|BC_Gen4_3|BC_Gen4_4|BC_Gen4_5|BC_Gen4_6|
|:--- | --: |--: |--: |--: |--: |--: |
|コンピューティング世代|Gen4|Gen4|Gen4|Gen4|Gen4|
|仮想コア|2|3|4|5|6|
|メモリ (GB)|14|21|28|35|42|
|プールあたりの最大 DB 数|100|100|100|100|100|
|列ストアをサポート|はい|はい|はい|はい|はい|
|インメモリ OLTP ストレージ (GB)|2|3|4|5|6|
|ストレージの種類|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|
|データの最大サイズ (GB)|1024|1024|1024|1024|1024|
|最大ログ サイズ (GB)|307|307|307|307|307|
|TempDB の最大データ サイズ (GB)|64|96|128|160|192|
|IO 待機時間 (概算)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|9,000|13,500|18,000|22,500|27,000|
|プールあたりの最大ログ レート (MBps)|20|30|40|50|60|
|プールあたりの最大同時実行ワーカー (要求) 数 **|420|630|840|1050|1260|
|プールあたりの最大同時ログイン (要求) 数 **|420|630|840|1050|1260|
|最大同時セッション数|30,000|30,000|30,000|30,000|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0、0.25、0.5、1、2|0、0.25、0.5、1...3|0、0.25、0.5、1...4|0、0.25、0.5、1...5|0、0.25、0.5、1...6|
|レプリカの数|4|4|4|4|4|
|マルチ AZ|はい|はい|はい|はい|はい|
|読み取りスケールアウト|はい|はい|はい|はい|はい|
|含まれるバックアップ ストレージ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

### <a name="business-critical-service-tier-generation-4-compute-platform-part-2"></a>Business Critical サービス レベル:第 4 世代コンピューティング プラットフォーム (パート 2)

|コンピューティング サイズ|BC_Gen4_7|BC_Gen4_8|BC_Gen4_9|BC_Gen4_10|BC_Gen4_16|BC_Gen4_24|
|:--- | --: |--: |--: |--: |--: |--: |
|コンピューティング世代|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|仮想コア|7|8|9|10|16|24|
|メモリ (GB)|49|56|63|70|112|159.5|
|プールあたりの最大 DB 数|100|100|100|100|100|100|
|列ストアをサポート|該当なし|該当なし|該当なし|該当なし|該当なし|該当なし|
|インメモリ OLTP ストレージ (GB)|7|8|9.5|11|20|36|
|ストレージの種類|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|
|データの最大サイズ (GB)|1024|1024|1024|1024|1024|1024|
|最大ログ サイズ (GB)|307|307|307|307|307|307|
|TempDB の最大データ サイズ (GB)|224|256|288|320|512|768|
|IO 待機時間 (概算)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|31,500|36,000|40,500|45,000|72,000|96,000|
|プールあたりの最大ログ レート (MBps)|70|80|80|80|80|80|
|プールあたりの最大同時実行ワーカー (要求) 数 **|1470|1680|1890|2100|3360|5040|
|プールあたりの最大同時ログイン (要求) 数 **|1470|1680|1890|2100|3360|5040|
|最大同時セッション数|30,000|30,000|30,000|30,000|30,000|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0、0.25、0.5、1...7|0、0.25、0.5、1...8|0、0.25、0.5、1...9|0、0.25、0.5、1...10|0、0.25、0.5、1...10、16|0、0.25、0.5、1...10、16、24|
|レプリカの数|4|4|4|4|4|4|
|マルチ AZ|はい|はい|はい|はい|はい|はい|
|読み取りスケールアウト|はい|はい|はい|はい|はい|はい|
|含まれるバックアップ ストレージ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

## <a name="business-critical---provisioned-compute---gen5"></a>Business Critical - プロビジョニング済みコンピューティング - Gen5

### <a name="business-critical-service-tier-generation-5-compute-platform-part-1"></a>Business Critical サービス レベル:第 5 世代コンピューティング プラットフォーム (パート 1)

|コンピューティング サイズ|BC_Gen5_4|BC_Gen5_6|BC_Gen5_8|BC_Gen5_10|BC_Gen5_12|BC_Gen5_14|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|コンピューティング世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|
|仮想コア|4|6|8|10|12|14|
|メモリ (GB)|20.8|31.1|41.5|51.9|62.3|72.7|
|プールあたりの最大 DB 数|100|100|100|100|100|100|
|列ストアをサポート|はい|はい|はい|はい|はい|はい|
|インメモリ OLTP ストレージ (GB)|3.14|4.71|6.28|8.65|11.02|13.39|
|データの最大サイズ (GB)|1024|1536|1536|1536|3072|3072|
|最大ログ サイズ (GB)|307|307|461|461|922|922|
|TempDB の最大データ サイズ (GB)|128|192|256|320|384|448|
|ストレージの種類|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|
|IO 待機時間 (概算)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|18,000|27,000|36,000|45,000|54,000|63,000|
|プールあたりの最大ログ レート (MBps)|60|90|120|120|120|120|
|プールあたりの最大同時実行ワーカー (要求) 数 **|420|630|840|1050|1260|1470|
|プールあたりの最大同時ログイン (要求) 数 **|420|630|840|1050|1260|1470|
|最大同時セッション数|30,000|30,000|30,000|30,000|30,000|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0、0.25、0.5、1...4|0、0.25、0.5、1...6|0、0.25、0.5、1...8|0、0.25、0.5、1...10|0、0.25、0.5、1...12|0、0.25、0.5、1...14|
|レプリカの数|4|4|4|4|4|4|
|マルチ AZ|はい|はい|はい|はい|はい|はい|
|読み取りスケールアウト|はい|はい|はい|はい|はい|はい|
|含まれるバックアップ ストレージ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

### <a name="business-critical-service-tier-generation-5-compute-platform-part-2"></a>Business Critical サービス レベル:第 5 世代コンピューティング プラットフォーム (パート 2)

|コンピューティング サイズ|BC_Gen5_16|BC_Gen5_18|BC_Gen5_20|BC_Gen5_24|BC_Gen5_32|BC_Gen5_40|BC_Gen5_80|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|コンピューティング世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|第 5 世代|
|仮想コア|16|18|20|24|32|40|80|
|メモリ (GB)|83|93.4|103.8|124.6|166.1|207.6|415.2|
|プールあたりの最大 DB 数|100|100|100|100|100|100|100|
|列ストアをサポート|はい|はい|はい|はい|はい|はい|はい|
|インメモリ OLTP ストレージ (GB)|15.77|18.14|20.51|25.25|37.94|52.23|131.68|
|データの最大サイズ (GB)|3072|3072|3072|4096|4096|4096|4096|
|最大ログ サイズ (GB)|922|922|922|1229|1229|1229|1229|
|TempDB の最大データ サイズ (GB)|512|576|640|768|1024|1280|2560|
|ストレージの種類|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|ローカル SSD|
|IO 待機時間 (概算)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|72,000|81,000|90,000|108,000|144,000|180,000|256,000|
|プールあたりの最大ログ レート (MBps)|120|120|120|120|120|120|120|
|プールあたりの最大同時実行ワーカー (要求) 数 **|1680|1890|2100|2520|3360|4200|8400|
|プールあたりの最大同時ログイン (要求) 数 **|1680|1890|2100|2520|3360|4200|8400|
|最大同時セッション数|30,000|30,000|30,000|30,000|30,000|30,000|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0、0.25、0.5、1...16|0、0.25、0.5、1...18|0、0.25、0.5、1...20|0、0.25、0.5、1...20、24|0、0.25、0.5、1...20、24、32|0、0.25、0.5、1...20、24、32、40|0、0.25、0.5、1...20、24、32、40、80|
|レプリカの数|4|4|4|4|4|4|4|
|マルチ AZ|はい|はい|はい|はい|はい|はい|はい|
|読み取りスケールアウト|はい|はい|はい|はい|はい|はい|はい|
|含まれるバックアップ ストレージ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

## <a name="business-critical---provisioned-compute---m-series"></a>Business Critical - プロビジョニング済みコンピューティング - M シリーズ

### <a name="m-series-compute-generation-preview"></a>M シリーズのコンピューティング世代 (プレビュー)

|コンピューティング サイズ|BC_M_128|
|:--- | --: |
|コンピューティング世代|M シリーズ|
|仮想コア|128|
|メモリ (GB)|3767.1|
|プールあたりの最大 DB 数|100|
|列ストアをサポート|はい|
|インメモリ OLTP ストレージ (GB)|1768|
|データの最大サイズ (GB)|4096|
|最大ログ サイズ (GB)|2048|
|TempDB の最大データ サイズ (GB)|4096|
|ストレージの種類|ローカル SSD|
|IO 待機時間 (概算)|1 ～ 2 ミリ秒 (書き込み)<br>1 ～ 2 ミリ秒 (読み取り)|
|プールあたりの最大データ IOPS *|200,000|
|プールあたりの最大ログ レート (MBps)|333|
|プールあたりの最大同時実行ワーカー (要求) 数 *|13,440|
|プールあたりの最大同時ログイン (要求) 数*|13,440|
|最大同時セッション数|30,000|
|エラスティック プール仮想コアのデータベースあたりの最小/最大選択肢|0 から 128|
|レプリカの数|4|
|マルチ AZ|はい|
|読み取りスケールアウト|はい|
|含まれるバックアップ ストレージ|1X DB サイズ|

\* IO サイズの最大値。範囲は 8 KB ～ 64 KB。 実際の IOPS はワークロードに依存します。 詳細については、[データ IO のガバナンス](sql-database-resource-limits-database-server.md#resource-governance)に関するページを参照してください。

\*\* 個々のデータベースの最大同時実行ワーカー数 (要求数) については、[単一データベースのリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください。 たとえば、エラスティック プールが Gen5 を使用し、データベースあたりの最大仮想コア数が 2 に設定されている場合、最大同時ワーカー数の値は 200 です。  データベースあたりの最大仮想コアが 0.5 に設定されている場合、Gen 5 では仮想コアあたりの最大同時ワーカー数が 100 なので、最大同時ワーカー数の値は 50 です。  その他にもデータベースあたりの最大仮想コア数設定が 1 仮想コア以下である場合は、最大同時ワーカー数が同様に再スケールされます。

エラスティック プールのすべての仮想コアがビジーの場合は、プール内の各データベースが、同量のコンピューティング リソースを受け取ってクエリを処理します。 SQL Database サービスは、コンピューティング時間を均等にすることで、データベース間におけるリソース共有の公平性を実現します。 それ以外の場合、エラスティック プールのリソース共有の公平性は、データベースあたりの仮想コア分が 0 以外の値に設定されているときに、リソース量に加えて各データベースに適用されることが保証されます。

## <a name="database-properties-for-pooled-databases"></a>プールされたデータベースのデータベース プロパティ

次の表では、プールされたデータベースのプロパティについて説明します。

> [!NOTE]
> エラスティック プール内の個々のデータベースのリソース制限は、一般的に同じコンピューティング サイズのプール外の単一のデータベースのリソース制限と同じです。 たとえば、GP_Gen4_1 データベースの最大同時実行ワーカー数は 200 ワーカーです。 そのため、GP_Gen4_1 プール内のデータベースの最大の同時実行ワーカー数も 200 ワーカーです。 GP_Gen4_1 プールの同時実行ワーカーの総数は 210 です。

| プロパティ | 説明 |
|:--- |:--- |
| データベースあたりの最大仮想コア数 |プール内の他のデータベースによる使用状況に基づいて使用可能な場合にプール内の任意のデータベースが使用できる仮想コアの最大数。 データベースごとの最大仮想コア数は、データベースに対して保証されたリソースではありません。 これは、プール内のすべてのデータベースに適用されるグローバル設定です。 データベースのピーク使用率を処理するのに十分高いデータベースあたり最大仮想コア数を設定します。 プールでは通常、ホットとコールドのデータベース使用パターンがあり、すべてのデータベースが同時に最大に使用されることはないため、ある程度高めに上限が設定されています。|
| データベースごとの最小の仮想コア数 |プール内の任意のデータベースで保証される仮想コアの最小数。 これは、プール内のすべてのデータベースに適用されるグローバル設定です。 データベースあたりの最小仮想コア数は 0 に設定でき、これが既定値です。 このプロパティは、0 とデータベースあたりの平均仮想コア使用率の間に設定されます。 プール内のデータベースの数とデータベースごとの最小仮想コア数の積がプールごとの仮想コア数の値を超えることはできません。|
| データベースあたりの最大ストレージ容量 |プール内のデータベースに対してユーザーによって設定される最大データベース サイズ。 プールされたデータベースは割り当てられたプール ストレージを共有するので、データベースが到達できるサイズは、残りのプール ストレージとデータベース サイズのうち、どちらか小さい方に制限されます。 最大データベース サイズとはデータ ファイルの最大サイズのことであり、ログ ファイルによって使用される領域は含まれません。 |
|||

## <a name="next-steps"></a>次のステップ

- 単一データベースに対する仮想コア リソースの制限については、[仮想コア購入モデルを使用した単一データベースに対するリソース制限](sql-database-vcore-resource-limits-single-databases.md)に関するページを参照してください
- 単一データベースに対する DTU のリソース制限については、[DTU 購入モデルを使用した単一データベースに対するリソース制限](sql-database-dtu-resource-limits-single-databases.md)に関するページを参照してください
- エラスティック プールに対する DTU リソースの制限については、「[DTU ベースの購入モデルを使用したエラスティック プールのリソース制限](sql-database-dtu-resource-limits-elastic-pools.md)」を参照してください
- マネージド インスタンスに対するリソース制限については、[マネージド インスタンスのリソース制限](sql-database-managed-instance-resource-limits.md)に関するページを参照してください。
- Azure の一般的な制限については、「[Azure サブスクリプションとサービスの制限、クォータ、制約](../azure-resource-manager/management/azure-subscription-service-limits.md)」をご覧ください。
- データベース サーバーでのリソース制限については、サーバーおよびサブスクリプション レベルの制限に関する情報が記載された、[SQL Database サーバー上のリソース制限の概要](sql-database-resource-limits-database-server.md)に関するページを参照してください。
