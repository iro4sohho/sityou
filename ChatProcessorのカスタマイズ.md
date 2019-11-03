pytchatはバックグラウンドでYoutubeから一定間隔でライブチャットデータを取得し、Bufferに一時的に貯めます。<br>
動作モードによりタイミングや経路は異なりますが、いずれもChatProcessorはLiveChatオブジェクトから<br>
定型的なデータ（chat_components：後述）を受け取り、任意の形に加工したデータを返す、という点を押さえておけばokです。

参考:[pytchatの動作モード](https://github.com/taizan-hokuto/pytchat/wiki/pytchat%E3%81%AE%E5%8B%95%E4%BD%9C%E3%83%A2%E3%83%BC%E3%83%89)


ChatProcessorは任意に拡張し、コンストラクタのprocessorパラメータで指定することができます。

自作のChatProcessorは、chat_componentsを引数にとるprocessというインターフェースを持たなければなりません。

```python
from .processors.chat_processor import ChatProcessor
class MyProcessor(ChatProcessor):
    def process(self, chat_components):
        #...process chatdata...
```

_chat_components_ は、video_id、timeout、chatdataをキーに持つ辞書(component)のリストです。
```python
chat_components:[LIST:component]

component = {
    "video_id" : "xxxxxxxxxxx",  #動画ID
    "timeout"  : 7.5231,              #チャットデータのタイムアウト時間
    "chatdata" : {"addChatItemAction":{"item":{"liveChatTextMessageRenderer":[......}}} #Youtubeから取得したチャットデータ
}
```



