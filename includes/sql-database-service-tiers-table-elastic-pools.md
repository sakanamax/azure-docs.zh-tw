<!--
Used in:
sql-database-elastic-pool.md 
-->

 
### <a name="basic-elastic-pool-limits"></a>基本彈性集區限制

| 每集區 eDTU | **50** | **100** | **200** | **300** | **400** | **800** | **1200** | **1600** |
|:---|---:|---:|---:| ---: | ---: | ---: | ---: | ---: |
| 每個集區內含的儲存體 (GB) | 5 | 10 | 20 | 29 | 39 | 78 | 117 | 156 |
| 每個集區的最大儲存體選擇 (GB) | 5 | 10 | 20 | 29 | 39 | 78 | 117 | 156 |
| 每個集區的記憶體內部 OLTP 儲存體上限 (GB) | N/A | N/A | N/A | N/A | N/A | N/A | N/A | N/A |
| 每個集區的最大 DB 數 | 100 | 200 | 500 | 500 | 500 | 500 | 500 | 500 |
| 每個集區的並行背景工作 (要求) 數上限 | 100 | 200 | 400 | 600 | 800 | 1600 | 2400 | 3200 |
| 每集區的並行登入數上限 | 100 | 200 | 400 | 600 | 800 | 1600 | 2400 | 3200 |
| 每集區並行工作階段數上限 | 30000 | 30000 | 30000 | 30000 |30000 | 30000 | 30000 | 30000 |
| 每個資料庫的最小 eDTU 選擇 | 0, 5 | 0, 5 | 0, 5 | 0, 5 | 0, 5 | 0, 5 | 0, 5 | 0, 5 |
| 每個資料庫的最大 eDTU 選擇 | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 |
| 每個資料庫的儲存體上限 (GB) | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 
||||||||

### <a name="standard-elastic-pool-limits"></a>標準彈性集區限制

| 每集區 eDTU | **50** | **100** | **200** | **300** | **400** | **800**| 
|:---|---:|---:|---:| ---: | ---: | ---: | 
| 每個集區內含的儲存體 (GB) | 50 | 100 | 200 | 300 | 400 | 800 | 
| 每個集區的最大儲存體選擇 (GB)* | 50, 250, 500 | 100, 250, 500, 750 | 200, 250, 500, 750, 1024 | 300, 500, 750, 1024, 1280 | 400, 500, 750, 1024, 1280, 1536 | 800, 1024, 1280, 1536, 1792, 2048 | 
| 每個集區的記憶體內部 OLTP 儲存體上限 (GB) | N/A | N/A | N/A | N/A | N/A | N/A | 
| 每個集區的最大 DB 數 | 100 | 200 | 500 | 500 | 500 | 500 | 
| 每個集區的並行背景工作 (要求) 數上限 | 100 | 200 | 400 | 600 | 800 | 1600 |
| 每集區的並行登入數上限 | 100 | 200 | 400 | 600 | 800 | 1600 |
| 每集區並行工作階段數上限 | 30000 | 30000 | 30000 | 30000 | 30000 | 30000 |
| 每個資料庫的最小 eDTU 選擇** | 0, 10, 20, 50 | 0、10、20、50、100 | 0, 10, 20, 50, 100, 200 | 0, 10, 20, 50, 100, 200, 300 | 0, 10, 20, 50, 100, 200, 300, 400 | 0, 10, 20, 50, 100, 200, 300, 400, 800 |
| 每個資料庫的最大 eDTU 選擇** | 10, 20, 50 | 10、20、50、100 | 10, 20, 50, 100, 200 | 10, 20, 50, 100, 200, 300 | 10, 20, 50, 100, 200, 300, 400 | 10, 20, 50, 100, 200, 300, 400, 800 | 
| 每個資料庫的儲存體上限 (GB)* | 500 | 750 | 1024 | 1024 | 1024 | 1024 |
||||||||

### <a name="standard-elastic-pool-limits-continued"></a>標準彈性集區限制 (續) 

| 每集區 eDTU | **1200** | **1600** | **2000** | **2500** | **3000** |
|:---|---:|---:|---:| ---: | ---: |
| 每個集區內含的儲存體 (GB) | 1200 | 1600 | 2000 | 2500 | 3000 | 
| 每個集區的最大儲存體選擇 (GB)* | 1200, 1280, 1536, 1792, 2048, 2304, 2560 | 1600, 1792, 2048, 2304, 2560, 2816, 3072 | 2000, 2048, 2304, 2560, 2816, 3072, 3328, 3584 | 2500, 2560, 2816, 3072, 3328, 3584, 3840, 4096 | 3000, 3072, 3328, 3584, 3840, 4096 |
| 每個集區的記憶體內部 OLTP 儲存體上限 (GB) | N/A | N/A | N/A | N/A | N/A | 
| 每個集區的最大 DB 數 | 500 | 500 | 500 | 500 | 500 | 
| 每個集區的並行背景工作 (要求) 數上限 | 2400 | 3200 | 4000 | 5000 | 6000 |
| 每集區的並行登入數上限 | 2400 | 3200 | 4000 | 5000 | 6000 |
| 每集區並行工作階段數上限 | 30000 | 30000 | 30000 | 30000 | 30000 | 
| 每個資料庫的最小 eDTU 選擇** | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200 | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600 | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000 | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000, 2500 | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000, 2500, 3000 |
| 每個資料庫的最大 eDTU 選擇** | 10, 20, 50, 100, 200, 300, 400, 800, 1200 | 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600 | 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000 | 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000, 2500 | 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000, 2500, 3000 | 
| 每個資料庫的最大儲存體選擇 (GB)* | 1024 | 1024 | 1024 | 1024 | 1024 | 
||||||||

### <a name="premium-elastic-pool-limits"></a>高階彈性集區限制

| 每集區 eDTU | **125** | **250** | **500** | **1000** | **1500**| 
|:---|---:|---:|---:| ---: | ---: | 
| 每個集區內含的儲存體 (GB) | 250 | 500 | 750 | 1024 | 1536 | 
| 每個集區的最大儲存體選擇 (GB)* | 250, 500, 750, 1024 | 500, 750, 1024 | 750, 1024 | 1024 | 1536 |
| 每個集區的記憶體內部 OLTP 儲存體上限 (GB) | 1 | 2 | 4 | 10 | 12 | 
| 每個集區的最大 DB 數 | 50 | 100 | 100 | 100 | 100 | 
| 每個集區的並行背景工作 (要求) 數上限 | 200 | 400 | 800 | 1600 | 2400 | 
| 每集區的並行登入數上限 | 200 | 400 | 800 | 1600 | 2400 |
| 每集區並行工作階段數上限 | 30000 | 30000 | 30000 | 30000 | 30000 | 
| 每資料庫的 eDTU 下限 | 0, 25, 50, 75, 125 | 0, 25, 50, 75, 125, 250 | 0, 25, 50, 75, 125, 250, 500 | 0, 25, 50, 75, 125, 250, 500, 1000 | 0, 25, 50, 75, 125, 250, 500, 1000, 1500 | 
| 每資料庫的 eDTU 上限 | 25, 50, 75, 125 | 25, 50, 75, 125, 250 | 25, 50, 75, 125, 250, 500 | 25, 50, 75, 125, 250, 500, 1000 | 25, 50, 75, 125, 250, 500, 1000, 1500 |
| 每個資料庫的儲存體上限 (GB)* | 1024 | 1024 | 1024 | 1024 | 1024 | 
||||||||

### <a name="premium-elastic-pool-limits-continued"></a>高階彈性集區限制 (續) 

| 每集區 eDTU | **2000** | **2500** | **3000** | **3500** | **4000**|
|:---|---:|---:|---:| ---: | ---: | 
| 每個集區內含的儲存體 (GB) | 2048 | 2560 | 3072 | 3548 | 4096 |
| 每個集區的最大儲存體選擇 (GB)* | 2048 | 2560 | 3072 | 3548 | 4096|
| 每個集區的記憶體內部 OLTP 儲存體上限 (GB) | 16 | 20 | 24 | 28 | 32 |
| 每個集區的最大 DB 數 | 100 | 100 | 100 | 100 | 100 | 
| 每個集區的並行背景工作 (要求) 數上限 | 3200 | 4000 | 4800 | 5600 | 6400 |
| 每集區的並行登入數上限 | 3200 | 4000 | 4800 | 5600 | 6400 |
| 每集區並行工作階段數上限 | 30000 | 30000 | 30000 | 30000 | 30000 | 
| 每個資料庫的最小 eDTU 選擇 | 0, 25, 50, 75, 125, 250, 500, 1000, 1750 | 0, 25, 50, 75, 125, 250, 500, 1000, 1750 | 0, 25, 50, 75, 125, 250, 500, 1000, 1750 | 0, 25, 50, 75, 125, 250, 500, 1000, 1750 | 0, 25, 50, 75, 125, 250, 500, 1000, 1750, 4000 | 
| 每個資料庫的最大 eDTU 選擇 | 25, 50, 75, 125, 250, 500, 1000, 1750 | 25, 50, 75, 125, 250, 500, 1000, 1750 | 25, 50, 75, 125, 250, 500, 1000, 1750 | 25, 50, 75, 125, 250, 500, 1000, 1750 | 25, 50, 75, 125, 250, 500, 1000, 1750, 4000 | 
| 每個資料庫的儲存體上限 (GB)* | 1024 | 1024 | 1024 | 1024 | 1024 | 
||||||||

### <a name="premium-rs-elastic-pool-limits"></a>進階 RS 彈性集區限制

| 每集區 eDTU | **125** | **250** | **500** | **1000** |
|:---|---:|---:|---:| ---: | ---: | 
| 每個集區內含的儲存體 (GB) | 250 | 500 | 750 | 750 |
| 每個集區的最大儲存體選擇 (GB)* | 250, 500, 750, 1024 | 500, 750, 1024 | 750, 1024 | 1024 | 
| 每個集區的記憶體內部 OLTP 儲存體上限 (GB) | 1 | 2 | 4 | 10 |
| 每個集區的最大 DB 數 | 50 | 100 | 100 | 100 |
| 每個集區的並行背景工作 (要求) 數上限 | 200 | 400 | 800 | 1600 |
| 每集區的並行登入數上限 | 200 | 400 | 800 | 1600 |
| 每集區並行工作階段數上限 | 30000 | 30000 | 30000 | 30000 |
| 每個資料庫的最小 eDTU 選擇 | 0, 25, 50, 75, 125 | 0, 25, 50, 75, 125, 250 | 0, 25, 50, 75, 125, 250, 500 | 0, 25, 50, 75, 125, 250, 500, 1000 |
| 每個資料庫的最大 eDTU 選擇 | 25, 50, 75, 125 | 25, 50, 75, 125, 250 | 25, 50, 75, 125, 250, 500 | 25, 50, 75, 125, 250, 500, 1000 | 
| 每個資料庫的儲存體上限 (GB)* | 1024 | 1024 | 1024 | 1024 | 
||||||||

> [!IMPORTANT]
> \* 大於內含儲存體數量的儲存體大小尚在預覽中，而且會產生額外成本。 如需詳細資訊，請參閱 [SQL Database 價格頁面](https://azure.microsoft.com/pricing/details/sql-database/)。 大於內含儲存體數量的儲存體大小為預覽版，而且會產生額外成本。 如需詳細資訊，請參閱 [SQL Database 價格頁面](https://azure.microsoft.com/pricing/details/sql-database/)。
>
> \* 在進階層中，超過 1 TB 的儲存體目前在下列區域為可用狀態：澳大利亞東部、澳大利亞東南部、加拿大中部、加拿大東部、法國中部、德國中部、日本東部、韓國中部、美國中南部、東南亞、美國東部 2、美國西部、美國維吉尼亞州政府及西歐。 
>
>\*\* [標準] 集區中起始數量為 200 eDTU 以上的每個資料庫 eDTU 下限/上限目前為預覽版。
>
