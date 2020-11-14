**PytchatCore** はチャットを取得するためのオブジェクトです。<br>

＜指定した動画がライブの場合＞<br>

`get()`を呼ぶと、最新のチャットデータを取得します。<br>

一度`get()`を呼んだあと、続けて`get()`を呼んだ場合、次のチャットデータを自動的に読み込みます。<br>

ライブ配信に対して`get()`を呼び出す間隔の推奨値は3～5秒です。

それより短ければよりリアルタイム性は高まりますが、あまりに短いとデータが空であるパターンが多くなるため効率は低くなります。

一方取得間隔が長すぎるとデータの取りこぼしを生じる場合があります。<br>
<br><br>
＜指定した動画がアーカイブ済みの場合＞

最初に`get()`を呼ぶとアーカイブされたチャットデータの最初のチャットデータを読み込みます。<br>
次に`get()`を呼ぶことで順次チャットデータを読み込みます。

`seektime`引数に時刻（秒）を指定することで、指定した時刻以降のチャットデータを順次読み込みます


## 使用例
PytchatCore オブジェクトは、pytchatをインポートして、create()関数を呼ぶことで取得できます。<br>
```python
import pytchat
import time
# PytchatCoreオブジェクトの取得
livechat = pytchat.create(video_id = "Zvp1pJpie4I")

while livechat.is_alive():
    # チャットデータの取得
    chatdata = livechat.get()
    for c in chatdata.items:
        print(f"{c.datetime} {c.author.name} {c.message} {c.amountString}")
        '''
        JSON文字列で取得:
        print(c.json())
        '''
    time.sleep(5)
```
※ items は [DefaultProcessor](https://github.com/taizan-hokuto/pytchat/wiki/DefaultProcessor_)固有の機能です。


## コンストラクタで指定可能なパラメータ一覧

パラメータ名|型|必須|備考|規定値
---|---|---|---|---
video_id|str|*|動画ID または動画IDを含むURL|-
processor|[ChatProcessor](https://github.com/taizan-hokuto/pytchat/wiki/ChatProcessor)||チャットデータを加工するオブジェクト|[DefaultProcessor](https://github.com/taizan-hokuto/pytchat/wiki/DefaultProcessor_)
interruptable|bool||Ctrl+Cでチャット取得を停止するか否か。pytchatを組み込んだアプリで不具合が生じる場合は、このパラメータをFalseに指定してください。|True
seektime|int| |チャットリプレイの開始時間(秒)。アーカイブチャットのリプレイ時のみ有効。負の数を指定した場合、配信開始前に流れていたチャット（一部）を取得します。|0
force_replay|bool| |指定した動画IDがライブ状態であっても、強制的にアーカイブされたチャットを取得します。|False
hold_exception|bool||内部で発生した例外を保持するかどうかを設定します。規定値はTrueです。Trueの場合、発生した例外を保持し、is_alive()関数がFalseになった後raise_for_status()関数を呼ぶことで、保持した例外を発生させることができます。Falseにした場合、例外を捕捉するため、get()の処理部分をtry...except節で囲む必要があります。|True
topchat_only|bool| |Trueの場合、上位チャットのみを取得します。（設定しない場合、またはFalseの場合「すべてのチャット」を取得）|False
[logger](https://github.com/taizan-hokuto/pytchat/wiki/Logging-pytchat:)|logging.Logger||ログ出力を取得する場合、任意のLoggerオブジェクトを設定します。|logging.NullHandler
## get()
説明|戻り値
---|---
チャットデータを取得します。（冒頭の説明文参照）|ChatProcessorによって加工されたチャットデータ


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
リプレイモードで動作している場合True（※この関数は、get()の呼び出し以降でなければ正しい値を返しません）|bool



## terminate()
説明|
---|
pytchatを終了します。|


## raise_for_status()
内部に保持した例外を発生させます。
`hold_exceptions`引数が`True`の時のみ有効です。