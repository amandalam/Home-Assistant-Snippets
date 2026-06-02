運行以下指令，看看過去一天的步行、爬升及下降記錄：
	步行步數：
	mcporter call home-assistant.get_history "entity_id":"sensor.apple_iphone_17_pro_max_steps" "start_time":"{from_time}" "end_time":"{to_time}"

	爬升記錄：
	mcporter call home-assistant.get_history "entity_id":"sensor.apple_iphone_17_pro_max_floors_ascended" "start_time":"{from_time}" "end_time":"{to_time}"

	下降記錄：
	mcporter call home-assistant.get_history "entity_id":"sensor.apple_iphone_17_pro_max_floors_descended" "start_time":"{from_time}" "end_time":"{to_time}"

	距離記錄：
	mcporter call home-assistant.get_history "entity_id":"sensor.apple_iphone_17_pro_max_distance" "start_time":"{from_time}" "end_time":"{to_time}"

當中，
- {from_time} 係 ISO 8601 格式嘅日期同時間，數值係香港時間（UTC+8）昨日嘅 23:59:59
- {to_time} 係 ISO 8601 格式嘅日期同時間，數值係香港時間（UTC+8）昨日嘅 23:59:59
這裡 {from_time} 和 {to_time} 數值相同的原因，是因爲這個實體記錄數據的方式是疊加的，而我只需要知道昨天一整天最後一分鐘的相關數值，因它代表着一整天疊加後的結果。

記得唔好喺記憶或 cache 度拎，我要最新嘅資訊

收集好以上數據後，請加以覆核其合理性，然後以以下格式輸出：

	👟 用家步行運動量報告 👟
	更新日期及時間：{UTC+8 時區的運行日期及時間，以 YYYY 年 MM 月 DD 日 HH:mm 顯示} {UTC+8 時區的運行日期及時間，以星期 W 格式顯示}
	
	運動日期：{UTC+8 時區昨日的 23:59:59，以 YYYY 年 MM 月 DD 日顯示} {UTC+8 時區昨日的 23:59:59，以 星期 W 格式顯示}
	步行步數: {步數的絕對值，以 #,##0 格式顯示}
	步行爬升：{爬升的絕對值} 層
	步行下降：{下降的絕對值} 層
	步行距離：{距離的絕對值，由米轉換成公里並四捨五入至小數點後一位數} 公里
	
	⚖️ 因步行、爬升及下降而消耗的卡路里估算 ⚖
	消耗總卡路里：{總卡路里估算的絕對值，換算成 kcal 單位的 #,##0 格式} kcal

請將上述結果，以 CSV 的方式：
	標題列：
		運動日期,步行步數,步行爬升（層）,步行下降（層）,步行距離（公里）,消耗的卡路里（kcal） 
	
	數值列：
		{UTC+8 時區的昨日 23:59:59，以 YYYY-MM-DD 格式顯示},{步數的絕對值},{爬升的絕對值},{下降的絕對值},{距離的絕對值，由米轉換成公里並四捨五入至小數點後一位數},{總卡路里估算的絕對值，換算成 kcal}
		
疊加寫入到 ~/clawd/logs/user_health.log
不要覆蓋整個檔案內容；如標題列不存在，建立標題列及數值列；如標題列已存在，僅將數值列開新列寫入到檔案末端

之後分析 ~/clawd/logs/user_health.log 的內容。如果檔案內含有 1 週或以上的內容，輸出以下結果：

	📆 過去一週... 📅
	每日平均步數：{過去一週每日平均步數的絕對值，四捨五入至小數點後 1 位數} 步
	每日平均爬升+下降次數：{過去一週每日平均步數的絕對值，四捨五入至小數點後 1 位數} 次
	每日平均步行距離：{過去一週每日平均步行距離的絕對值，由米轉換成公里，四捨五入至小數點後 1 位數的 km} 公里 

	⚖️ 因步行、爬升及下降而消耗的卡路里估算 ⚖
	上週消耗總卡路里：{總卡路里估算的絕對值，換算成 kcal 單位的 #,##0 格式} kcal
	上週每日平均消耗卡路里：{每日平均卡路里估算的絕對值，換算成 kcal 單位的 #,##0 格式} kcal

	分析：{ 針對上述結果，對 用家步行運動量評估的分析 }
	
請務必確保所有日期、星期幾和時間數值等準確無誤地反映香港時區（UTC+8）的真實情況。	