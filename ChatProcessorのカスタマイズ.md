ChatProcessorは、LiveChatオブジェクトから定型的なデータ（[chat_components](https://github.com/taizan-hokuto/pytchat/wiki/chat_component)：後述）を受け取り、<br>
任意の形式に加工したデータを返すオブジェクトです。

pytchatには組み込みのChatProcessorとして以下のクラスを同梱しています。
+ [DefaultProcessor](https://github.com/taizan-hokuto/pytchat/wiki/DefaultProcessor) ： チャットデータへのアクセスを容易に行うための標準的なProcessor
+ CompatibleProcessor　： Youtube APIが返すjsonデータと互換性のあるProcessor
+ JsonfileArchiveProcessor　：　チャットデータを辞書形式でファイルに保存するProcessor
+ [SpeedCalculator](https://github.com/taizan-hokuto/pytchat/wiki/SpeedCalculator)　：　チャットの勢いを算出するProcessor



## 拡張
自作したChatProcessorは、LiveChatオブジェクトのコンストラクタのprocessorパラメータで指定することができます。

```python
from pytchat import LiveChat
import MyProcessor

chat = LiveChat("video_id", processor = MyProcessor())
```
<br>
<br>

ChatProcessorを複数使用する場合は、タプルで指定します。（[詳細](Multiple-chat-processors)）

```python
chat = LiveChat("video_id", processor = Processor1(), Processor2())
```
## インタフェース

ChatProcessorは、1個のリスト(chat_components)を引数にとる**process**という関数を持たなければなりません。

```python
class MyProcessor:
    def process(self, chat_components:List[dict]):
        #...process chatdata...
```

_chat_components_ は、video_id、timeout、chatdataをキーに持つ辞書([chat_component](https://github.com/taizan-hokuto/pytchat/wiki/chat_component))のリストです。
```python
chat_components:List[chat_component:dict]

chat_component = {
    "video_id" : "xxxxxxxxxxx",  #動画ID
    "timeout"  : 7.5231,              #チャットデータのタイムアウト時間
    "chatdata" : {"addChatItemAction":{"item":{"liveChatTextMessageRenderer":[......}}} #Youtubeから取得したチャットデータ
}
```

chatdata は Youtubeから取得したjson形式のチャットデータをpython辞書形式に変換したものです。


