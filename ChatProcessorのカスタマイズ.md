ChatProcessorは、LiveChatオブジェクトから定型的なデータ（[chat_components](https://github.com/taizan-hokuto/pytchat/wiki/chat_component_)：後述）を受け取り、<br>
任意の形式に加工したデータを返すオブジェクトです。

pytchatには組み込みのChatProcessorとして以下のクラスを同梱しています。
+ [DefaultProcessor](https://github.com/taizan-hokuto/pytchat/wiki/DefaultProcessor_) ： チャットデータへのアクセスを容易に行うための標準的なProcessor
+ CompatibleProcessor　： Youtube APIが返すJSONデータと互換性のあるProcessor
+ [JsonfileArchiver](https://github.com/taizan-hokuto/pytchat/wiki/JsonfileArchiver_)　：　チャットデータを１行ずつJSON形式でファイルに保存するProcessor
+ [SpeedCalculator](https://github.com/taizan-hokuto/pytchat/wiki/SpeedCalculator_)　：　チャットの勢いを算出するProcessor
+ [SuperchatCalculator](https://github.com/taizan-hokuto/pytchat/wiki/SuperchatCalculator_)　：　スーパーチャットの金額を集計するProcessor


## 拡張
自作したChatProcessorは、LiveChatオブジェクトのコンストラクタのprocessorパラメータで指定することができます。

```python
from pytchat import LiveChat
import MyProcessor

chat = LiveChat("video_id", processor = MyProcessor())
```
<br>
<br>

ChatProcessorを複数使用する場合は、[タプルで指定します](https://github.com/taizan-hokuto/pytchat/wiki/%E8%A4%87%E6%95%B0%E3%81%AEChat-Processor%E3%82%92%E5%90%8C%E6%99%82%E3%81%AB%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B)。

```python
chat = LiveChat("video_id", processor = (Processor1(), Processor2()) )
data1, data2 = chat.get()
```
## インタフェース

ChatProcessorは、1個のリスト(chat_components)を引数にとる**process**という関数を持たなければなりません。

```python
class MyProcessor:
    def process(self, chat_components:List[dict]):
        #...process chatdata...
```

_chat_components_ は、video_id、timeout、chatdataをキーに持つ辞書([chat_component](https://github.com/taizan-hokuto/pytchat/wiki/chat_component_:))のリストです。
```python
chat_components:List[chat_component:dict]

chat_component = {
    "video_id" : "xxxxxxxxxxx",  #動画ID
    "timeout"  : 7.5231,              #チャットデータのタイムアウト時間
    "chatdata" : {"addChatItemAction":{"item":{"liveChatTextMessageRenderer":[......}}} #Youtubeから取得したチャットデータ
}
```

chatdata は Youtubeから取得したjson形式のチャットデータをpython辞書形式に変換したものです。


