<br>
pytchatでは、processorパラメータに何も指定しない場合、このDefaultProcessorによって加工されたチャットデータが返されます。<br>

### 使用例
```python
chat = LiveChat("xxxxxxxxxxx") #video_id
#chat = LiveChat("xxxxxxxxxxx", processor = DefaultProcessor()) と同義。
while chat.is_alive():
    data = chat.get() #get processed data.
    items = data.items
    for c in items:
        print(f"{c.datetime} [{c.author.name}]-{c.message} -{c.amountString}")
        data.tick()
```
## items
description|return value
---|---
[チャットデータ](#チャットデータ)のリストを取得します。|チャットデータのリスト

## tick()
description|
---|
次のチャットが表示されるまで待ちます.|

## _await_ 　tick_async()
description|
---|
（LiveChatAsync使用時のみ有効）次のチャットが表示されるまで待ちます。この関数はawaitをつけて呼び出さなければなりません。|


## #チャットデータ

<table>
  <tr>
    <th>name</th>
    <th>type</th>
    <th>remarks</th>
  </tr>
  <tr>
    <td>type</td>
    <td>str</td>
    <td>"superChat","textMessage","superSticker","newSponsor"</td>
  </tr>
  <tr>
    <td>id</td>
    <td>str</td>
    <td>チャットの個別ID</td>
  </tr>
  <tr>
    <td>message</td>
    <td>str</td>
    <td>カスタム絵文字は ":(テキスト):"のように表示されます。</td>
  </tr>
  <tr>
    <td>messageEx</td>
    <td>str</td>
    <td>メッセージおよびカスタム絵文字のリスト。カスタム絵文字は画像URLとして表示されます。</td>
  </tr>
  <tr>
    <td>timestamp</td>
    <td>int</td>
    <td>チャット投稿時刻（unixタイムスタンプ、ミリ秒）</td>
  </tr>
  <tr>
    <td>datetime</td>
    <td>str</td>
    <td>例： "2019-10-10 12:34:56"</td>
  </tr>
    <td>elapsedTime</td>
    <td>str</td>
    <td>経過時間 (例 "1:02:27") *リプレイモードのみ対応</td>
  </tr>
  <tr>
    <td>amountValue</td>
    <td>float</td>
    <td>スパチャの金額部分（例： 1,234.0）</td>
  </tr>
  <tr>
    <td>amountString</td>
    <td>str</td>
    <td>スパチャの通貨＋金額表示（例 "$ 1,234"）</td>
  </tr>
  <tr>
    <td>currency</td>
    <td>str</td>
    <td><a href="https://en.wikipedia.org/wiki/ISO_4217">ISO 4217 通貨記号</a> (例： "USD")</td>
  </tr>
  <tr>
    <td>bgColor</td>
    <td>int</td>
    <td>メッセージの背景色（RGB）</td>
  </tr>
  <tr>
    <td>author</td>
    <td>object</td>
    <td>チャット投稿者データ。<a href="#author">下記参照</a>。</td>
  </tr>
  <tr>
    <td>colors</td>
    <td>object</td>
    <td>スーパーチャット・スパーステッカーの色データ。<a href="#colors">下記参照</a></td>
  </tr>
</table>

### author
チャット投稿者データ
<table>
  <tr>
    <th>name</th>
    <th>type</th>
    <th>remarks</th>
  </tr>
  <tr>
    <td>name</td>
    <td>str</td>
    <td>投稿者名</td>
  </tr>
  <tr>
    <td>channelId</td>
    <td>str</td>
    <td>投稿者のユーザーチャンネルID.</td>
  </tr>
  <tr>
    <td>channelUrl</td>
    <td>str</td>
    <td>投稿者のユーザーチャンネルURL</td>
  </tr>
  <tr>
    <td>imageUrl</td>
    <td>str</td>
    <td>投稿者のプロフィール画像URL</td>
  </tr>
  <tr>
    <td>badgeUrl</td>
    <td>str</td>
    <td>メンバーのバッジ画像URL</td>
  </tr>
  <tr>
    <td>isVerified</td>
    <td>bool</td>
    <td>確認済み</td>
  </tr>
  <tr>
    <td>isChatOwner</td>
    <td>bool</td>
    <td>配信者本人</td>
  </tr>
  <tr>
    <td>isChatSponsor</td>
    <td>bool</td>
    <td>メンバーシップ加入者(※スパチャデータの場合、メンバーか否かにかかわらず常にFalse)</td>
  </tr>
  <tr>
    <td>isChatModerator</td>
    <td>bool</td>
    <td>モデレータ</td>
  </tr>
</table>

### colors
色データ
<table>
  <tr>
    <th>name</th>
    <th>type</th>
    <th>remarks</th>
  </tr>
  <tr>
    <td>headerBackgroundColor</td>
    <td>int (ARGB)</td>
    <td>type:`superChat`でのみ利用可能</td>
  </tr>
  <tr>
    <td>headerTextColor</td>
    <td>int (ARGB)</td>
    <td>type:`superChat`でのみ利用可能</td>
  </tr>
  <tr>
    <td>bodyBackgroundColor</td>
    <td>int (ARGB)</td>
    <td>type:`superChat`でのみ利用可能。`bgColor`と同じ値を返します。</td>
  </tr>
  <tr>
    <td>bodyTextColor</td>
    <td>int (ARGB)</td>
    <td>type:`superChat`でのみ利用可能</td>
  </tr>
  <tr>
    <td>timestampColor</td>
    <td>int (ARGB)</td>
    <td>type:`superChat`でのみ利用可能</td>
  </tr>
  <tr>
    <td>authorNameTextColor</td>
    <td>int (ARGB)</td>
    <td>type:`superChat` と `superSticker`でのみ利用可能</td>
  </tr>
  <tr>
    <td>backgroundColor</td>
    <td>int (ARGB)</td>
    <td>type:`superSticker`でのみ利用可能。`bgColor`と同じ値を返します。</td>
  </tr>
  <tr>
    <td>moneyChipBackgroundColor</td>
    <td>int (ARGB)</td>
    <td>type:`superSticker`でのみ利用可能。</td>
  </tr>
  <tr>
    <td>moneyChipTextColor</td>
    <td>int (ARGB)</td>
    <td>type:`superSticker`でのみ利用可能</td>
  </tr>
</table>