
<img src="https://taizan-hokuto.github.io/statics/LOGO.png" width="400" align="center">


#### pytchatは、YouTube APIを使わずにチャットを取得するための軽量pythonライブラリです。

＜主な特徴＞
+ ブラウザがチャットを取得するのと同じ仕組みで軽量にチャット取得。
+ Selenium等によるスクレイピングに頼らず、使用帯域を節約。
+ 取得したチャットデータを自由に加工するためのクラスを分離。
+ ライブ中のチャット、アーカイブ済み動画のチャットリプレイ両方に対応。

<br>

## インストール

```
pip install pytchat
```
アップグレード
```
pip install --upgrade pytchat
```

## 動作DEMO
![demo](https://taizan-hokuto.github.io/statics/demo.gif "demo")

## API
 * [LiveChat](https://github.com/taizan-hokuto/pytchat/wiki/LiveChat:)
 * [LiveChatAsync](https://github.com/taizan-hokuto/pytchat/wiki/LiveChatAsync:)
 * [ReplayChat](https://github.com/taizan-hokuto/pytchat/wiki/ReplayChat)　*廃止予定（LiveChatに統合）
 * [ReplayChatAsync](https://github.com/taizan-hokuto/pytchat/wiki/ReplayChatAsync) *廃止予定（LiveChatAsyncに統合）
## Chat Processor（チャットデータを加工するための組み込みのクラス）
 * [DefaultProcessor](https://github.com/taizan-hokuto/pytchat/wiki/DefaultProcessor:)
 * CompatibleProcessor
 * JsonfileArchiveProcessor
 * [SpeedCalculator](https://github.com/taizan-hokuto/pytchat/wiki/SpeedCalculator:)

[pytchatについて](https://github.com/taizan-hokuto/pytchat/wiki/feature)<br>
[pytchatの動作モードについて](https://github.com/taizan-hokuto/pytchat/wiki/pytchat%E3%81%AE%E5%8B%95%E4%BD%9C%E3%83%A2%E3%83%BC%E3%83%89)
<br>
[ChatProcessorのカスタマイズ](https://github.com/taizan-hokuto/pytchat/wiki/ChatProcessor%E3%81%AE%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA)

