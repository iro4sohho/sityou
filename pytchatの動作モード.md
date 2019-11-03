pytchatは、バックグラウンドでチャットデータを取得しBuffer（FIFOキュー）に貯めることで、チャットデータの取得タイミングと独立に、データを利用できるようにしています。

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
    #任意の処理をここに書きます
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
+ コンストラクタでdirect_mode = Trueを指定

　　　かつ

+ コンストラクタでcallbackパラメータに呼び出し先の関数名を指定<br>

⇒direct_modeが有効になります。<br><br>

逆に

+ directモードが有効になっている状態でget()関数を呼び出した場合

　　　または

+ direct_mode = Trueにもかかわらずcallbackパラメータに何も指定しなかった場合<br>

⇒IllegalFunctinCall例外が発生します。<br><br>

directモードはbufferを使用しない分、理論的に使用メモリが抑えられ動作も軽いはずですが、呼び出し先のcallback内での処理に長時間（10秒以上）かかる場合、チャットデータの取得遅延が生じます。

```python
from pytchat import LiveChat
import time

#callbackパラメータに呼び出し先の関数名を指定します。
#direct_mode = Trueを指定します。
chat = LiveChat("G1w62uEMZ74", callback = func,
                               direct_mode = True)
while chat.is_alive():
    #任意の処理をここに書きます
    time.sleep(3)

#自動的に呼び出される関数
#returnまで10秒以上かかる場合、チャットデータの取得遅延が生じます。
def func(chatdata):
    for c in chatdata.items:
        print(f"{c.datetime} [{c.author.name}]-{c.message} {c.amountString}")
        chat.tick()
```
モード図解
<img src ="https://taizan-hokuto.github.io/statics/pytchat_mode%20diagram.svg" alt="pytchat_3modes_diagram" width="100%" height="100%">

