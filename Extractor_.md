Extractorオブジェクトは、チャットを抽出します。

## パラメータ
### video_id
動画ID

### div
並行ダウンロードのための分割数。<br>
（1～10の整数。10を超える数を指定した場合であっても10で処理されます。）

### callback
ダウンロード中の途中経過データを渡す関数。<br>
読み込んだチャットデータの秒数（ミリ秒）と、読み込んだチャットデータが渡されます。<br>
ただし、callbackに渡される秒数およびチャットデータは一部重複する可能性があります。

### processor
抽出後の後処理を行う[ChatProcessor](https://github.com/taizan-hokuto/pytchat/wiki/ChatProcessor)
