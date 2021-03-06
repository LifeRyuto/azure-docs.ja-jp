---
title: SQL データベースをインポートまたはエクスポートする
description: Azure サービスのサーバーへのアクセスを許可することなく Azure SQL データベースをインポートまたはエクスポートします。
services: sql-database
ms.service: sql-database
ms.subservice: migration
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.reviewer: ''
ms.date: 01/08/2020
ms.openlocfilehash: 9f694f3f0ec740d0a4e8dc4e6bf8845c408802c8
ms.sourcegitcommit: 8e9a6972196c5a752e9a0d021b715ca3b20a928f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2020
ms.locfileid: "75899031"
---
# <a name="import-or-export-an-azure-sql-database-without-allowing-azure-services-to-access-the-server"></a>Azure サービスのサーバーへのアクセスを許可することなく Azure SQL データベースをインポートまたはエクスポートする

この記事では、Azure SQL サーバー上で *[Azure サービスを許可する]* が *[オフ]* に設定されている場合に Azure SQL データベースをインポートまたはエクスポートする方法について説明します。 このワークフローでは、インポートまたはエクスポート操作を行う SqlPackage を実行するために Azure 仮想マシンを使用します。

## <a name="sign-in-to-the-azure-portal"></a>Azure portal にサインインする

[Azure portal](https://portal.azure.com/) にサインインする

## <a name="create-the-azure-virtual-machine"></a>Azure 仮想マシンを作成する

**[Azure へのデプロイ]** ボタンを選択して Azure 仮想マシンを作成します。

このテンプレートでは、修正プログラムが適用された最新バージョンを使用して、Windows バージョンのいくつかの異なるオプションを使用して単純な Windows 仮想マシンをデプロイできます。 これにより、A2 サイズの VM がリソース グループの場所にデプロイされ、その VM の完全修飾ドメイン名が返されます。
<br><br>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-simple-windows%2Fazuredeploy.json" target="_blank">
    <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.png"/>
</a>

詳細については、[Windows VM の非常に単純なデプロイ](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)に関するページを参照してください。


## <a name="connect-to-the-virtual-machine"></a>仮想マシンへの接続

次の手順は、リモート デスクトップ接続を使用して仮想マシンに接続する方法を示しています。

1. デプロイが完了したら、仮想マシン リソースに移動します。

    ![VM](./media/import-export-from-vm/vm.png)  

2. **[接続]** を選択します。

   リモート デスクトップ プロトコル ファイル (.rdp ファイル) のフォームが表示され、仮想マシンのパブリック IP アドレスとポート番号が示されます。

   ![RDP フォーム](./media/import-export-from-vm/rdp.png)  

3. **[RDP ファイルのダウンロード]** を選択します。

   > [!NOTE]
   > SSH を使用して VM に接続することもできます。

4. **[仮想マシンに接続する]** フォームを閉じます。
5. VM に接続するには、ダウンロードした RDP ファイルを開きます。
6. メッセージが表示されたら、 **[Connect]** を選択します。 Mac では、この[リモート デスクトップ クライアント](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12)のような RDP クライアントを Mac App Store から入手する必要があります。

7. 仮想マシンの作成時に指定したユーザー名とパスワードを入力し、 **[OK]** を選択します。

8. サインイン処理中に証明書の警告が表示される場合があります。 **[はい]** または **[続行]** を選択して接続処理を続行します。



## <a name="install-sqlpackage"></a>SqlPackage をインストールする

[最新バージョンの SqlPackage をダウンロードしてインストール](https://docs.microsoft.com/sql/tools/sqlpackage-download)します。




詳細については、「[SqlPackage.exe](https://docs.microsoft.com/sql/tools/sqlpackage)」を参照してください。

## <a name="create-a-firewall-rule-to-allow-the-vm-access-to-the-database"></a>データベースへの VM アクセスを許可するためのファイアウォール規則を作成する

SQL Database サーバーのファイアウォールに仮想マシンのパブリック IP アドレスを追加します。

次の手順では、仮想マシンのパブリック IP アドレスのためのサーバー レベルの IP ファイアウォール規則を作成し、仮想マシンからの接続を有効にします。

1. 左側のメニューから **[SQL データベース]** を選択し、 **[SQL データベース]** ページでデータベースを選択します。 データベースの概要ページが開き、完全修飾サーバー名 (**servername.database.windows.net** など) と、さらに構成するためのオプションが表示されます。

2. サーバーやそのデータベースに接続するときに使用するために、この完全修飾サーバー名をコピーします。

   ![サーバー名](./media/sql-database-get-started-portal/server-name.png)

3. ツール バーで **[サーバー ファイアウォールの設定]** を選択します。 データベース サーバーの **[ファイアウォール設定]** ページが開きます。

   ![サーバーレベルの IP ファイアウォール規則](./media/sql-database-get-started-portal/server-firewall-rule.png)

4. ツールバーの **[クライアント IP の追加]** を選択して、サーバー レベルの新しい IP ファイアウォール規則に仮想マシンのパブリック IP アドレスを追加します。 サーバーレベルの IP ファイアウォール規則は、単一の IP アドレスまたは IP アドレスの範囲に対して、ポート 1433 を開くことができます。

5. **[保存]** を選択します。 サーバー レベルの IP ファイアウォール規則が、SQL Database サーバー上のポート 1433 を開いている仮想マシンのパブリック IP アドレスに対して作成されます。

6. **[ファイアウォール設定]** ページを閉じます。



## <a name="export-a-database-using-sqlpackage"></a>SqlPackage を使用してデータベースをエクスポートする

[SqlPackage](https://docs.microsoft.com/sql/tools/sqlpackage) コマンドライン ユーティリティを使用して SQL データベースをエクスポートするには、「[エクスポートのパラメーターおよびプロパティ](https://docs.microsoft.com/sql/tools/sqlpackage#export-parameters-and-properties)」を参照してください。 SqlPackage ユーティリティには、最新バージョンの [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) と [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) が付属しています。または、最新バージョンの [SqlPackage](https://docs.microsoft.com/sql/tools/sqlpackage-download) をダウンロードすることもできます。

ほとんどの運用環境でのスケールとパフォーマンスのために、SqlPackage ユーティリティを使用することをお勧めします。 BACPAC ファイルを使用した移行に関する SQL Server Customer Advisory Team のブログについては、「[Migrating from SQL Server to Azure SQL Database using BACPAC Files (BACPAC ファイルを使用した SQL Server から Azure SQL Database への移行)](https://blogs.msdn.microsoft.com/sqlcat/20../../migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)」を参照してください。

この例は、SqlPackage.exe と Active Directory ユニバーサル認証を使用してデータベースをエクスポートする方法を示しています。 環境に固有の値に置き換えてください。

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=<servername>.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```




## <a name="import-a-database-using-sqlpackage"></a>SqlPackage を使用してデータベースをインポートする

[SqlPackage](https://docs.microsoft.com/sql/tools/sqlpackage) コマンドライン ユーティリティを使用して SQL Server データベースをインポートするには、「[インポート パラメーターとプロパティ](https://docs.microsoft.com/sql/tools/sqlpackage#import-parameters-and-properties)」をご覧ください。 SqlPackage には、最新の [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) と [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) が含まれています。 また、最新バージョンの [SqlPackage](https://docs.microsoft.com/sql/tools/sqlpackage-download) をダウンロードすることもできます。

スケールとパフォーマンスのために、ほとんどの運用環境では、Azure portal の使用ではなく SqlPackage の使用をお勧めします。 `BACPAC` ファイルを使用した移行に関する SQL Server Customer Advisory Team のブログについては、「[Migrating from SQL Server to Azure SQL Database using BACPAC Files (BACPAC ファイルを使用した SQL Server から Azure SQL Database への移行)](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)」をご覧ください。

次の SqlPackage コマンドは、**AdventureWorks2017** データベースをローカル ストレージから Azure SQL Database サーバーにインポートします。 **Premium** サービス層と **P6** サービス オブジェクトがある **myMigratedDatabase** という新しいデータベースが作成されます。 これらの値は、お使いの環境に合わせて変更してください。

```cmd
sqlpackage.exe /a:import /tcs:"Data Source=<serverName>.database.windows.net;Initial Catalog=myMigratedDatabase>;User Id=<userId>;Password=<password>" /sf:AdventureWorks2017.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

> [!IMPORTANT]
> 企業のファイアウォールの外側から単一のデータベースを管理している SQL Database サーバーに接続するには、そのファイアウォールでポート 1433 が開かれている必要があります。 マネージド インスタンスに接続するには、[ポイント対サイト接続](sql-database-managed-instance-configure-p2s.md)または Express Route 接続が使用できる必要があります。

この例では、SqlPackage と Active Directory ユニバーサル認証を使用してデータベースをインポートする方法を示します。

```cmd
sqlpackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項

エクスポートの速度は多くの要因 (データ シェープなど) によって異なるため、どのような速度が期待されるかを予測することはできません。 特に大規模なデータベースの場合は、SqlPackage にかなりの時間がかかることがあります。

最高のパフォーマンスを得るために、次の方法を試してみることができます。

1. データベース上で確実に他のどのワークロードも実行されないようにします。 他のどのワークロードも実行されないようにするには、エクスポートの前のコピーの作成が最適なソリューションである可能性があります。
2. エクスポート ワークロード (主に読み取り I/O) をより適切に処理するには、データベースのサービス レベル目標 (SLO) を上げます。 現在、データベースが GP_Gen5_4 である場合は、Business Critical レベルが読み取りワークロードに役立つことがあります。
3. 特に大規模なテーブルに対して、確実にクラスター化インデックスが存在するようにします。 
4. ネットワークの制約を回避できるように、仮想マシン (VM) はデータベースと同じリージョンにある必要があります。
5. VM には、BLOB ストレージにアップロードする前の一時的な成果物を生成するための十分なサイズを持つ SSD が存在する必要があります。
6. VM は、特定のデータベースのための十分なコアおよびメモリ構成を備えている必要があります。

## <a name="store-the-imported-or-exported-bacpac-file"></a>インポートまたはエクスポートされた .BACPAC ファイルを格納する

.BACPAC ファイルは、[Azure BLOB](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-overview) または [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) に格納できます。 

最高のパフォーマンスを実現するには、Azure Files を使用します。 SqlPackage はファイル システムで動作するため、Azure Files に直接アクセスできます。

コストを削減するには、Premium Azure ファイル共有よりコストの低い Azure BLOB を使用します。 ただし、それには、インポートまたはエクスポート操作の前に BLOB とローカル ファイル システムの間で [.BACPAC ファイル](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications#bacpac)をコピーする必要があります。 その結果、このプロセスにかかる時間は長くなります。

.BACPAC ファイルをアップロードまたはダウンロードするには、「[AzCopy と Blob Storage でデータを転送する](../storage/common/storage-use-azcopy-blobs.md)」および「[AzCopy とファイル ストレージでデータを転送する](../storage/common/storage-use-azcopy-files.md)」 を参照してください。

環境によっては、[Azure Storage ファイアウォールおよび仮想ネットワークを構成する](../storage/common/storage-network-security.md)ことが必要になる場合があります

## <a name="next-steps"></a>次のステップ

- インポートした SQL Database に接続してそれを照会する方法については、「[クイック スタート:Azure SQL Database:SQL Server Management Studio を使ってデータに接続してクエリを行う方法](sql-database-connect-query-ssms.md)に関する記事をご覧ください。
- BACPAC ファイルを使用した移行に関する SQL Server Customer Advisory Team のブログについては、「[Migrating from SQL Server to Azure SQL Database using BACPAC Files (BACPAC ファイルを使用した SQL Server から Azure SQL Database への移行)](https://techcommunity.microsoft.com/t5/DataCAT/Migrating-from-SQL-Server-to-Azure-SQL-Database-using-Bacpac/ba-p/305407)」を参照してください。
- パフォーマンスの推奨事項も含む、SQL Server データベースの移行プロセス全体の詳細については、[Azure SQL Database への SQL Server データベースの移行](sql-database-single-database-migrate.md)に関するページを参照してください。
- ストレージ キーと共有アクセス署名を管理および共有する方法については、「[Azure Storage セキュリティ ガイド](https://docs.microsoft.com/azure/storage/common/storage-security-guide)」をご覧ください。
