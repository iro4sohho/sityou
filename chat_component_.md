# chat_component

chat_componentは、pytchat内で使用する、チャットデータのブロックです。
<br>

＜[PytchatCore](https://github.com/taizan-hokuto/pytchat/wiki/PytchatCore_)（`pytchat.create()`で取得できるオブジェクト）での動作＞
<br>
  get()関数を呼び出すと、取得されたチャットデータが、Chat Processorに渡され、任意の形式に加工されたデータが返ってきます。
<br>

＜[LiveChat](https://github.com/taizan-hokuto/pytchat/wiki/LiveChat_)／[LiveChatAsync](https://github.com/taizan-hokuto/pytchat/wiki/LiveChatAsync_)での動作＞
<br>
LiveChat、LiveChatAsyncオブジェクトでは、チャットデータが一定間隔で取得されバッファに蓄積されます。
<br><br>
LiveChat.get()関数を呼び出すと、バッファ内のchat_componentのリストがChat Processorに渡され、任意の形式に加工されたデータが返ってきます。
<br><br>
LiveChatオブジェクトのコンストラクタでcallbackに関数を指定している場合、バッファ内のchat_componentのリストがChat Processorに渡され、加工後のデータが指定した関数の引数に渡されます。

### chat_componentの構造

キー名|値の型|備考
---|---|---
video_id|str|動画ID
timeout|float|次のチャットデータを取得するまでの時間（ミリ秒）
chatdata|List[dict]|YouTubeから取得したチャットデータのリスト（actionsの要素）
