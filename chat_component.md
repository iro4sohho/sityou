# chat_component : dict

Block of chat data.

Buffer accumulates list of chat_components.

When User calls LiveChat.get() function, list of chat_components are processed by Chat Processor.
And processed chat data are thrown to user.

If callback mode is on, chat components are processed by Chat Processor and thrown to specified callback function.

key name|value type|remarks
---|---|---
video_id|str|video ID
timeout|float|interval of fetching next chat data
chatdata|List[dict]|chat data of youtube


