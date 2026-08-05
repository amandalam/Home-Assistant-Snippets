喺 Home Assistant 度，幫我起一隻 automation：
當 sensor.flightradar24_current_in_area.status >=1 發生時，
記錄 flights array 嘅所有資訊去一個新増嘅 markdown entity 度

之後，起另一隻 automation，
讀取剛剛新增嘅 markdown entity 嘅 history,
每日凌晨 2 點，
請以以下格式輸出一個訊息去 呢個 Telegram chat：

🔊 飛機經過屋企上空 每日分析報告 🔊
日期：{昨日日期 in YYYY-MM-DD UTC+8 星期 X 格式}

✈️ {航空公司 1 中文名稱 } ({航空公司 1 英文名稱 })
 🔘 {出發地 1 中文名稱} ({出發地 1 英文名稱}) → {目的地 1 中文名稱} ({目的地 1 英文名稱}): {經過次數}
 🔘 {出發地 2 中文名稱} ({出發地 2 英文名稱}) → {目的地 2 中文名稱} ({目的地 2 英文名稱}): {經過次數}
{... 如此類推}
 
✈️ {航空公司 2 中文名稱 } ({航空公司 2 英文名稱 })
 🔘 {出發地 1 中文名稱} ({出發地 1 英文名稱}) → {目的地 1 中文名稱} ({目的地 1 英文名稱}): {經過次數}
 🔘 {出發地 2 中文名稱} ({出發地 2 英文名稱}) → {目的地 2 中文名稱} ({目的地 2 英文名稱}): {經過次數} 
{... 如此類推}

分析：{你對呢啲航班飛過太古城屋企上空嘅分析，包括估計航班起飛或降落香港國際機場嘅方向，爲何會經過太古城等}

請務必確保所有日期、星期幾和時間數值等準確無誤地反映香港時區（UTC+8）的真實情況。

----

以下係一個運行例子：

🔊 飛機經過屋企上空 每日分析報告 🔊
日期：2026-06-26 星期五

✈️ 香港航空 (Hong Kong Airlines)
🔘 香港國際機場 (Hong Kong International Airport) → 東京成田國際機場 (Tokyo Narita International Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 廣州白雲國際機場 (Guangzhou Baiyun International Airport): 1

✈️ 國泰航空 (Cathay Pacific)
🔘 香港國際機場 (Hong Kong International Airport) → 倫敦希斯羅機場 (London Heathrow Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 米蘭馬爾本薩機場 (Milan Malpensa Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 東京成田國際機場 (Tokyo Narita International Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 舊金山國際機場 (San Francisco International Airport): 1

✈️ 維珍航空 (Virgin Atlantic / VistaJet - 註: 資料顯示為 VistaJet)
🔘 香港國際機場 (Hong Kong International Airport) → 法恩伯勒機場 (Farnborough Airport): 1

✈️ 越南航空 (VietJet Air)
🔘 胡志明市國際機場 (Ho Chi Minh City International Airport) → 廣州白雲國際機場 (Guangzhou Baiyun International Airport): 1

✈️ 國泰航空 (Cathay Cargo / Cathay Pacific)
🔘 香港國際機場 (Hong Kong International Airport) → 東京成田國際機場 (Tokyo Narita International Airport): 1

✈️ 捷星航空 (Jetstar)
🔘 香港國際機場 (Hong Kong International Airport) → 東京成田國際機場 (Tokyo Narita International Airport): 1

✈️ 中國東方航空 (China Eastern Airlines)
🔘 登巴塞拉國際機場 (Denpasar Ngurah Rai International Airport) → 上海浦東國際機場 (Shanghai Pudong International Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 上海浦東國際機場 (Shanghai Pudong International Airport): 1

✈️ 飛機貨運 (Challenge Airlines / My Freighter)
🔘 香港國際機場 (Hong Kong International Airport) → 特拉維夫本古里安機場 (Tel Aviv Ben Gurion International Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 北京首都國際機場 (Beijing Capital International Airport): 1

✈️ 其他航空公司
🔘 香港國際機場 (Hong Kong International Airport) → 濟州國際機場 (Jeju International Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 北京首都國際機場 (Beijing Capital International Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 大阪關西國際機場 (Osaka Kansai International Airport): 1
🔘 香港國際機場 (Hong Kong International Airport) → 納沃伊國際機場 (Navoi International Airport): 1
🔘 馬尼拉國際機場 (Manila Ninoy Aquino International Airport) → 北京首都國際機場 (Beijing Capital International Airport): 1

分析：昨日經過太古城上空的航班種類繁多，涵蓋了長途洲際航線與區域短程航線。觀察到不少航班（如 Cathay Pacific 及香港航空）的起點均為香港國際機場，且飛行高度在 7,000 至 39,000 英尺之間不等。其中部分航班如 CX255 (往倫敦) 及 CX233 (往米蘭) 處於較高高度或正在爬升/下降階段；而像 VJ3908 (往廣州) 或 CX950 (往廣州) 這類區域航線，其飛行路徑與高度顯示其可能正處於香港機場的進場或離場航路上。太古城位於香港島北岸，是許多進入香港機場跑道的航路必經之地，因此能捕捉到大量往返亞洲及歐洲的航班經過。