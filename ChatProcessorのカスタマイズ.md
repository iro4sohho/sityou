pytchatはバックグラウンドでYoutubeから一定間隔でライブチャットデータを取得し、Bufferに一時的に貯めます。<br>
動作モードによりタイミングや経路は異なりますが、いずれもChatProcessorはLiveChatオブジェクトから<br>
定型的なデータ（chat_components：後述）を受け取り、任意の形に加工したデータを返す、という点を押さえておけばokです。

### on-demandモード時：
ユーザーからのget()要求があったとき、Bufferに残っている全てのチャットデータ（chat_components）を取り出してChatProcessorに一旦渡します。
その後ChatProcessorから加工後のデータを受け取ってユーザーに返します。


### callbackモード時：
一定間隔でcallback呼び出しが行われる際、Bufferに残っている全てのchat_componentsを取り出してChatProcessorに一旦渡します。
その後ChatProcessorから加工後のデータを受け取ってcallback関数の引数に設定し呼び出します。


### directモード時：
Bufferを経由せず、チャットデータを取得した後すぐに、ChatProcessorにchat_componentsを渡します。
その後ChatProcessorから加工後のデータを受け取ってcallback関数の引数に設定し呼び出します。

ChatProcessorは、自作してコンストラクタのprocessorパラメータで指定することができます。

ChatProcessorは、下記のように、chat_componentsを引数にとるprocessというインターフェースを持ちます。

```python
class ChatProcessor:
    def process(self, chat_components):
        pass
```

chat_componentsは、以下のように、video_id、timeout、chatdataをキーに持つ辞書(component)のリストです。
```python
chat_components:[LIST:component]

component = {
    "video_id" : "xxxxxxxxxxx",  #動画ID
    "timeout"  : 7.5231,              #チャットデータのタイムアウト時間
    "chatdata" : {"addChatItemAction":{"item":{"liveChatTextMessageRenderer":[......}}} #Youtubeから取得したチャットデータ
}
```



