---
title: クイック スタート:音声テキスト変換を翻訳する、C# (UWP) - Speech サービス
titleSuffix: Azure Cognitive Services
description: TBD
services: cognitive-services
author: lisaweixu
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.date: 12/09/2019
ms.author: erhopf
ms.topic: include
ms.openlocfilehash: 70db4e23aebe2a986c9aa4c85c28ac6529ac3202
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "76156008"
---
## <a name="prerequisites"></a>前提条件

開始する前に、必ず次のことを行ってください。

> [!div class="checklist"]
> * [Azure Speech リソースを作成する](../../../../get-started.md)
> * [使用する開発環境を設定する](../../../../quickstarts/setup-platform.md?tabs=uwp)
> * [空のサンプル プロジェクトを作成する](../../../../quickstarts/create-project.md?tabs=uwp)

## <a name="add-sample-code"></a>サンプル コードを追加する

今度は、アプリケーションのユーザー インターフェイスを定義する XAML コードを追加し、C# のコードビハインド実装を追加します。

1. **ソリューション エクスプローラー**で、`MainPage.xaml` を開きます。

1. デザイナーの XAML ビューで、次の XAML スニペットを **Grid** タグに挿入します (`<Grid>` と `</Grid>` の間)。

   [!code-xml[UI elements](~/samples-cognitive-services-speech-sdk/quickstart/csharp/uwp/translate-speech-to-text/helloworld/MainPage.xaml#StackPanel)]

1. **ソリューション エクスプローラー**で、コードビハインドのソース ファイル `MainPage.xaml.cs` を開きます (`MainPage.xaml` にグループ化されています)。

1. その中のすべてのコードを次のスニペットに置き換えます。

   [!code-csharp[Quickstart Code](~/samples-cognitive-services-speech-sdk/quickstart/csharp/uwp/translate-speech-to-text/helloworld/MainPage.xaml.cs#code)]

1. このファイルの `SpeechTranslationFromMicrophone_ButtonClicked` ハンドラーから `YourSubscriptionKey` という文字列を見つけて、ご利用のサブスクリプション キーに置き換えます。

1. `SpeechTranslationFromMicrophone_ButtonClicked` ハンドラーから `YourServiceRegion` という文字列を見つけて、ご利用のサブスクリプションに関連付けられている[リージョン](~/articles/cognitive-services/Speech-Service/regions.md)に置き換えます。 たとえば、無料試用版サブスクリプションの場合は `westus` を使用します。

1. メニュー バーから **[ファイル]**  >  **[すべて保存]** を選択して変更内容を保存します。

## <a name="build-and-run-the-application"></a>アプリケーションの構築と実行

アプリケーションをビルドしてテストする準備が整いました。

1. メニュー バーから **[ビルド]**  >  **[ソリューションのビルド]** を選択してアプリケーションをビルドします。 これで、コードは、エラーなしでコンパイルされます。

1. **[デバッグ]**  >  **[デバッグの開始]** の順に選択するか、**F5** キーを押して、アプリケーションを起動します。 **[helloworld]** ウィンドウが表示されます。

   ![サンプル UWP 翻訳アプリケーション (C#) - クイックスタート](~/articles/cognitive-services/Speech-Service/media/sdk/qs-translate-speech-uwp-helloworld-window.png)

1. **[Enable Microphone]** を選択し、アクセス許可要求がポップアップ表示されたら、 **[はい]** を選択します。

   ![マイクへのアクセス許可要求](~/articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-10-access-prompt.png)

1. **[Translate speech from the microphone input]** を選択し、デバイスのマイクに向かって英語のフレーズや文章を話します。 その音声が Speech Services に転送されて別の言語 (このケースではドイツ語) のテキストに翻訳されます。 翻訳済みのテキストが Speech Services からアプリケーションに返されてウィンドウに表示されます。

   ![音声翻訳ユーザー インターフェイス](~/articles/cognitive-services/Speech-Service/media/sdk/qs-translate-csharp-uwp-ui-result.png)

## <a name="next-steps"></a>次のステップ

[!INCLUDE [footer](./footer.md)]
