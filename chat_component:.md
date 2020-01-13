# chat_component

chat_componentは、pytchat内で使用する、チャットデータのブロックです。

Youtubeから1回に取得できるチャットデータのリスト(約5秒～10秒分）に相当し、一定間隔でバッファに蓄積されます。
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
