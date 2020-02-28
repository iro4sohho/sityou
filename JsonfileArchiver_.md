チャットのJSONデータを１行ごとにファイルに保存します。

### パラメータ

#### save_path : str
保存するファイルパス（ファイル名含む）。<br>
同名のファイルが存在する場合は、ファイル名末尾（拡張子の前）に括弧つきの連番を付与します。

### 戻り値
次の形式の辞書を返します。<br>
```
{
 "save_path" : （ファイルの保存パス）,
 "total_lines" :（ファイルに書き込み済みデータの行数）
}
```
<br>

### 使用例
```python
import asyncio
from pytchat import LiveChatAsync

video_id = "8PIe_F9MI80"

async def main():
  chat = LiveChatAsync(　  
    video_id, 
    callback = func,
    processor = JsonfileArchiver("c:/temp/test.data")
  )
  while chat.is_alive():
    await asyncio.sleep(5)        
 
async def func(param):
  pass

loop = asyncio.get_event_loop()
try:
  loop.run_until_complete(async_def_callback())
except asyncio.CancelledError:
  print('Cancelled')
```
### データフォーマット
1行ずつJSONデータとして保存されます。<br>
例：
```
{"addChatItemAction": {"item": {"liveChatTextMessageRenderer": {"message": {"runs": [{"text": ...}\n
{"addChatItemAction": {"item": {"liveChatPaidMessageRenderer": {"id": "xxx", "timestampUsec": ...}\n
{"addChatItemAction": {"item": {"liveChatTextMessageRenderer": {"message": {"runs": [{"text": ...}\n
```
ファイルを一括してJSONデータとして取り込むことはできません。<br>
ファイルから１行ごとに読み込む必要があります。<br>

