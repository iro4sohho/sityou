LiveChatAsync オブジェクト
+ asyncioを使用してバックグラウンドでライブチャットデータを監視・自動取得し、bufferにデータを蓄積します。
+ 任意のタイミングでbufferに蓄積したチャットデータを取得できます。（[get()](#await--get) 関数)
+ callbackパラメータに任意の関数を指定することで、バックグラウンドで自動的・定期的にライブチャットデータを指定した関数に渡すことができます。
+ アーカイブ済み動画のチャットのリプレイにも対応しています。
（指定した動画がアーカイブ済みの場合、自動的にリプレイモードになります）
## 使用例
```python
from pytchat import LiveChatAsync
from concurrent.futures import CancelledError
import asyncio

async def main():
  livechat = LiveChatAsync("Zvp1pJpie4I", callback = func)
  while livechat.is_alive():
    await asyncio.sleep(3)
    #チャットの取得と並行で行いたい処理をここに書きます。

#callbackに指定した関数は、バックグラウンドで自動的かつ定期的に呼び出されます。
#引数に、ChatProcessorによって加工されたチャットデータが渡されます。
async def func(chatdata):
  for c in chatdata.items:
    print(f"{c.datetime} [{c.author.name}]-{c.message} {c.amountString}")
    await chatdata.tick_async()

if __name__=='__main__':
  try:
    loop = asyncio.get_event_loop()
    loop.run_until_complete(main())
  except CancelledError:
    pass
```
## コンストラクタで指定可能なパラメータ一覧

パラメータ名|型|必須|備考|規定値
---|---|---|---|---
video_id|str|*|動画ID (`https://www.youtube.com/watch?v=xxx`　の「xxx」の部分)|-
processor|ChatProcessor||チャットを加工するオブジェクト|DefaultProcessor
buffer|buffer||チャットデータを蓄積するバッファ|Buffer(maxsize=20)
interruptable|bool||Ctrl+Cでチャット取得を停止するか否か|True
callback|func||一定間隔でチャットデータを渡す関数|None
done_callback|func||チャット取得終了時に呼び出す関数|None
direct_mode|bool| |Trueの場合、bufferを使用しません。このパラメータをTrueにする場合、callbackにも任意の関数を指定する必要があります。|False
seektime|int| |チャットリプレイの開始時間(秒)。アーカイブチャットのリプレイ時のみ有効。負の数を指定した場合、配信開始前に流れていたチャット（一部）を取得します（アーカイブされているデータのみ）。|0
force_replay|bool| |指定した動画IDがライブ状態であっても、強制的にアーカイブされたチャットを取得します。|False
# 関数

## _await_  get()
説明|戻り値
---|---
チャットデータをbufferから取得します。|ChatProcessorによって加工されたチャットデータ

※callbackモードに関数を指定している場合、get()は使用できません（IllegalFunctionCall例外が発生します）

## is_alive()
<table>
	<tbody>
		<tr>
			<td>説明</td>
			<td>戻り値の型</td>
		</tr>
		<tr>
			<td>ライブ動画⇒配信が終わるまでTrue。<br>注：チャット取得開始時にすでに配信が終わっている場合はリプレイモードに切り替わります。</td>
			<td rowspan="2">bool</td>
		</tr>
		<tr>
			<td>アーカイブ動画⇒チャットデータが取得できなくなるまでTrue</td>
		</tr>
	</tbody>
</table>

## is_replay()
説明|戻り値の型
---|---
リプレイモードで動作している場合True（※この関数は、get()の呼び出し以降、またはcallbackの呼び出し以降でなければ正しい結果を返しません）|bool



## pause()
説明|
---|
バックグラウンドのチャット取得を一時停止します（※callbackを指定しているときのみ有効）|

## resume()
説明|
---|
バックグラウンドのチャット取得を再開します（※callbackを指定しているときのみ有効）|


## terminate()
説明|
---|
pytchatを終了します。|

