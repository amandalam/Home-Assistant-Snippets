幫我執行呢個指令，獲取大門門鐘影到最新嘅影像分析：

mcporter call 'home-assistant.get_history("sensor.markdown_main_door_summary","{from_time}","{to_time}")'

當中，

{from_time} 係 ISO 8601 格式嘅日期同時間，數值係香港時間（UTC+8）昨日嘅 00:00:00
{to_time} 係 ISO 8601 格式嘅日期同時間，數值係香港時間（UTC+8）昨日嘅 23:59:59
記得唔好喺記憶或 cache 度拎，我要最新嘅資訊

你將會獲得一串 JSON 結果顯示昨日所有影像轉變事件嘅分析，每一段都有 state 同 last_changed 值

請綜合你拎到嘅結果，將資訊以以下格式顯示：

🔊 大門門鐘影像 每日分析報告 🔊

日期：(昨日 UTC+8 的 yyyy-mm-dd 星期 X 格式)
時間：(列出指令結果所有 last_changed 值，轉換成 UTC+8 的 HH:mm 格式，以發生時間順序，並以逗號分隔)
分析：(分析指令結果每段嘅 state 值，綜合你嘅觀察，包括傳回結果出現嘅人物及動作，分析有冇保安疑慮需要留意；如果有，請指出具體嘅發生時間同內容)
