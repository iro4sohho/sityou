LiveChat オブジェクト
+ ThreadpoolExecutorを使用してバックグラウンドでライブチャットデータを監視・自動取得し、bufferにデータを蓄積します。
+ 任意のタイミングでget()関数を使用し、bufferに蓄積したチャットデータを取得できます。
+ callbackパラメータに任意の関数を指定することで、バックグラウンドでライブチャットデータを指定した関数に渡すことができます。
+ アーカイブ済み動画のチャットのリプレイにも対応しています。
## 使用例
```
from pytchat import LiveChat
chat = LiveChat("gb01h_eT0pw")

while chat.is_alive():
    data = chat.get()
    items = data.items()
    for c in items:
        print(c.author.name, c.message)
        data.tick()
```
## #コンストラクタで指定可能なパラメータ一覧

パラメータ名|型|必須|備考|規定値
---|---|---|---|---
video_id|str|*|動画ID (`https://www.youtube.com/watch?v=xxx`　の「xxx」の部分)|-
processor|ChatProcessor||チャットを加工するオブジェクト|DefaultProcessor
buffer|buffer||チャットデータを蓄積するバッファ|Buffer(maxsize=20)
interruptable|bool||Ctrl+Cでチャット取得を停止するか否か|True
callback|func||一定間隔でチャットデータを渡す関数|None
done_callback|func||チャット取得終了時に呼び出す関数|None
direct_mode|bool| |Trueを指定した場合、bufferを使用しません|False
seektime|int| |チャットリプレイの開始時間(秒)。アーカイブチャットのリプレイ時のみ有効。負の数を指定した場合、配信開始前に流れていたチャット（一部）を取得します（アーカイブされているデータのみ）。|0
force_replay|bool| |指定した動画IDがライブ状態であっても、強制的にアーカイブされたチャットを取得します。|False
## get()
説明|戻り値
---|---
チャットデータをbufferから取得します。|ChatProcessorによって加工されたチャットデータ

## is_alive()
説明|戻り値
---|---
監視中のデータがライブ中かどうか|bool

## terminate()
説明|戻り値
---|---
チャットの取得を停止します。|-

