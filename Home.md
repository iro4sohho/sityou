# pytchatの動作モードについて

pytchatは、バックグラウンドでチャットデータを取得しBuffer（FIFOキュー）に貯めることで、チャットデータの取得タイミングを気にすることなく、データを利用できるようにしています。

pytchatの動作モードは以下の3つがあります。

## on-demandモード
get()により、任意のタイミングでBufferにあるチャットデータを取り出すことができます。
```python
from pytchat import LiveChat

chat = LiveChat("G1w62uEMZ74")
while chat.is_alive():
    data = chat.get()
    for c in data.items:
        print(f"{c.datetime} [{c.author.name}]-{c.message} {c.amountString}")
        data.tick()
```
## callbackモード
calbackモードでは、自動的にcallbackパラメータに指定された関数を呼び出します。<br>
コンストラクタでcallbackパラメータに呼び出し先の関数名を指定することで、callbackモードが有効になります。<br>
callbackモードが有効になっている状態でget()関数を呼び出すと、IllegalFunctinCall例外が発生します。<br>

```python
from pytchat import LiveChat
import time

#callbackパラメータに呼び出し先の関数名を指定します。
chat = LiveChat("G1w62uEMZ74", callback = func)
while chat.is_alive():
    #他のバックグラウンドで行う任意の処理をここに書きます
    time.sleep(3)

#自動的に呼び出される関数
def func(chatdata):
    for c in chatdata.items:
        print(f"{c.datetime} [{c.author.name}]-{c.message} {c.amountString}")
        chat.tick()
```
## directモード
directモードでは、Bufferを使用せずにcallbackパラメータに指定された関数を呼び出します。<br>
directモードを有効にするには以下の2つの条件を満たす必要があります。
+ コンストラクタでdirect_modeを指定
+ コンストラクタでcallbackパラメータに呼び出し先の関数名を指定
directモードが有効になっている状態でget()関数を呼び出すと、IllegalFunctinCall例外が発生します。<br>

directモードはbufferを使用しない分、理論的には使用メモリが抑えられ動作も軽いはずですが、チャットデータ取得

