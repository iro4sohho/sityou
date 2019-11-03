Welcome to the pytchat wiki!

pytchatは、Youtubeのライブチャットを取得するためのpythonライブラリです。

特徴
+ ブラウザがYoutube配信ページでライブチャットを取得する仕組みをエミュレーションしているため、比較的軽量にチャットデータを取得できます。

+ ブラウザと同じ仕組みでチャットを取得しているので、当然Youtube apiは不要です。また、Selenium(ヘッドレスブラウザ)やBeautiful Soupによるスクレイピングを一切行っていません。

+ SeleniumやYoutube APIで取得したチャットデータで必要だった「重複チャットデータの比較と排除」が不要のため、cpuパワーや帯域が抑えられています。

+ これまでは一番最初のcontinuationパラメータを取得するために数百キロバイトある配信ページをスクレイピングする必要がありましたが、このライブラリではそのパラメータそのものを計算して生成しているため、素早く最初のチャットデータを取得することができます。

+ チャットデータをバッファリングするため、チャットデータの取得タイミングを気にせずにデータを利用できます。（バッファを使用しない動作モードも用意しています）

+ バッファリングは、マルチスレッドを利用するクラスに加え、pythonの強力な非同期I/O(asyncio）を利用するためのクラスも用意しています。

+ Youtube APIが出力するJSONデータと互換性のあるChatProcessorを同梱しているので、既存アプリの置き換えも用意です。
チャットを加工するクラスはカスタマイズ可能です。

[pytchatの動作モードについて](https://github.com/taizan-hokuto/pytchat/wiki/pytchat%E3%81%AE%E5%8B%95%E4%BD%9C%E3%83%A2%E3%83%BC%E3%83%89)
<br>
[ChatProcessorのカスタマイズ](https://github.com/taizan-hokuto/pytchat/wiki/ChatProcessor%E3%81%AE%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA)

※開発中のためwiki記載の内容は変更になる可能性があります。あらかじめご了承ください。