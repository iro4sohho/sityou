DefaultProcessor is a default chat processor of pytchat.
### Usage
```python
chat = LiveChat("xxxxxxxxxxx") #video_id

while chat.is_alive():
    data = chat.get() #get processed data.
    items = data.items
    for c in items:
        print(c.author.name, c.message)
        data.tick()
```
## items
description|return value
---|---
Get list of [chat items](#members-of-chat-item).|List of chat items

## tick()
description|return value
---|---
wait for next chat.|-

## [await] tick_async()
description|return value
---|---
wait for next chat on asyncio context.|-


## Attributes of Chat Item

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
    <td></td>
  </tr>
  <tr>
    <td>message</td>
    <td>str</td>
    <td>Emojis are represented by ":(shortcut text):"</td>
  </tr>
  <tr>
    <td>messageEx</td>
    <td>str</td>
    <td>List of messages and emojis: emojis are represented by URL for image.</td>
  </tr>
  <tr>
    <td>timestamp</td>
    <td>int</td>
    <td>unixtime milliseconds</td>
  </tr>
  <tr>
    <td>datetime</td>
    <td>str</td>
    <td>e.g. "2019-10-10 12:34:56"</td>
  </tr>
    <td>elapsedTime</td>
    <td>str</td>
    <td>elapsed time. (e.g. "1:02:27") *Replay Only.</td>
  </tr>
  <tr>
    <td>amountValue</td>
    <td>float</td>
    <td>e.g. 1,234.0</td>
  </tr>
  <tr>
    <td>amountString</td>
    <td>str</td>
    <td>e.g. "$ 1,234"</td>
  </tr>
  <tr>
    <td>currency</td>
    <td>str</td>
    <td><a href="https://en.wikipedia.org/wiki/ISO_4217">ISO 4217 currency codes</a> (e.g. "USD")</td>
  </tr>
  <tr>
    <td>bgColor</td>
    <td>int (ARGB)</td>
    <td></td>
  </tr>
  <tr>
    <td>author</td>
    <td>object</td>
    <td>see <a href="#author">author</a></td>
  </tr>  <tr>
    <td>colors</td>
    <td>object</td>
    <td>see <a href="#colors">colors</a></td>
  </tr>
</table>

### author
Attributes of author object.
<table>
  <tr>
    <th>name</th>
    <th>type</th>
    <th>remarks</th>
  </tr>
  <tr>
    <td>name</td>
    <td>str</td>
    <td></td>
  </tr>
  <tr>
    <td>channelId</td>
    <td>str</td>
    <td>chatter's channel ID.</td>
  </tr>
  <tr>
    <td>channelUrl</td>
    <td>str</td>
    <td></td>
  </tr>
  <tr>
    <td>imageUrl</td>
    <td>str</td>
    <td>chatter's icon</td>
  </tr>
  <tr>
    <td>badgeUrl</td>
    <td>str</td>
    <td>member badge</td>
  </tr>
  <tr>
    <td>isVerified</td>
    <td>bool</td>
    <td></td>
  </tr>
  <tr>
    <td>isChatOwner</td>
    <td>bool</td>
    <td></td>
  </tr>
  <tr>
    <td>isChatSponsor</td>
    <td>bool</td>
    <td>when the chat is superchat/supersticker, always False</td>
  </tr>
  <tr>
    <td>isChatModerator</td>
    <td>bool</td>
    <td></td>
  </tr>
</table>

### colors
Attributes of colors object.
<table>
  <tr>
    <th>name</th>
    <th>type</th>
    <th>remarks</th>
  </tr>
  <tr>
    <td>headerBackgroundColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superChat`</td>
  </tr>
  <tr>
    <td>headerTextColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superChat`.</td>
  </tr>
  <tr>
    <td>bodyBackgroundColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superChat`. Same as `bgColor`.</td>
  </tr>
  <tr>
    <td>bodyTextColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superChat`</td>
  </tr>
  <tr>
    <td>timestampColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superChat`</td>
  </tr>
  <tr>
    <td>authorNameTextColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superChat` and `superSticker`</td>
  </tr>
  <tr>
    <td>backgroundColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superSticker` Same as `bgColor`.</td>
  </tr>
  <tr>
    <td>moneyChipBackgroundColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superSticker`</td>
  </tr>
  <tr>
    <td>moneyChipTextColor</td>
    <td>int (ARGB)</td>
    <td>available only type:`superSticker`</td>
  </tr>
</table>
