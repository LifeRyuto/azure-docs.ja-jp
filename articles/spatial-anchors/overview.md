---
title: Azure Spatial Anchors の概要
description: Azure Spatial Anchors がクロスプラットフォーム対応の複合現実エクスペリエンスの開発にどのように役立つかについて説明します。
author: craigktreasure
manager: aliemami
services: azure-spatial-anchors
ms.author: crtreasu
ms.date: 02/24/2019
ms.topic: overview
ms.service: azure-spatial-anchors
ms.openlocfilehash: 503004cba0d4109adcfee62f7acd108cbcb73eb6
ms.sourcegitcommit: 653e9f61b24940561061bd65b2486e232e41ead4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74277156"
---
# <a name="azure-spatial-anchors-overview"></a>Azure Spatial Anchors の概要

Azure Spatial Anchors へようこそ。 Azure Spatial Anchors は、空間を認識する複合現実アプリケーションのビルドに不可欠な機能を開発者に提供します。 これらのアプリケーションでは、Microsoft HoloLens、ARKit をサポートする iOS ベースのデバイス、および ARCore をサポートする Android ベースのデバイスをサポートできます。 Azure Spatial Anchors によって、開発者は、複合現実プラットフォームで作業を行って、空間の認識、正確な関心ポイントの指定、およびサポートされているデバイスからのこれらの関心ポイントの再呼び出しを実行できます。
これらの正確な関心ポイントは、空間アンカーと呼ばれます。

![クロス プラットフォーム](./media/cross-platform.png)

## <a name="examples"></a>例

空間アンカーによって可能になるユース ケースの例には、以下が含まれます。

- [マルチユーザー エクスペリエンス](tutorials/tutorial-share-anchors-across-devices.md)。 空間アンカーによって、同じ場所にいるユーザーがマルチユーザー対応混合現実アプリケーションに簡単にアクセスできます。 たとえば、仮想チェス ボードをテーブルに置くことで、2 人のユーザーが複合現実チェス ゲームを開始できます。 その後、テーブルで各自のデバイスをポイントすることで、仮想チェス ボードを一緒に見ながら対戦できます。

- [道案内](concepts/anchor-relationships-way-finding.md)。 開発者は、空間アンカーをつなげて、それらの間にリレーションシップを作成することもできます。 たとえば、あるタスクを完了するためにユーザーが対話する必要がある 2 つまたは 3 つの関心ポイントがあるエクスペリエンスをアプリに含めることができます。 これらの関心ポイントをつなげるように作成できます。 その後、アプリでは、ユーザーがマルチステップ タスクを完了すると、現在のアンカーの近くにあるアンカーが要求され、タスクの次の手順にユーザーを案内することができます。

- [仮想コンテンツの現実世界での永続化](how-tos/create-locate-anchors-unity.md#create-a-cloud-spatial-anchor)。 あるユーザーが仮想カレンダーを会議室の壁に配置し、他のユーザーがフォン アプリまたは HoloLens デバイスを使用してそれを見ることができるようにするアプリが可能です。 労働環境では、ユーザーは、サポートされているデバイス カメラを機械に向けることで、コンテキスト情報を受け取ることができます。

Azure Spatial Anchors は、サポート対象のデバイス プラットフォーム用のマネージド サービスとクライアント SDK で構成されています。 以下のセクションで、Azure Spatial Anchors を使用するアプリのビルドの開始に関する情報を提供します。

## <a name="next-steps"></a>次の手順

Spatial Anchors を使用して初めてのアプリを作成します。

> [!div class="nextstepaction"]
> [Unity](unity-overview.yml)

> [!div class="nextstepaction"]
> [iOS](quickstarts/get-started-ios.md)

> [!div class="nextstepaction"]
> [Android](quickstarts/get-started-android.md)

> [!div class="nextstepaction"]
> [HoloLens](quickstarts/get-started-hololens.md)
