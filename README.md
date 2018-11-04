#  .NET/C# 開發實戰 C# 非同步練習範例

## 1.作業系統知識回顧

|專案名稱|專案說明|備註|
|-|-|-|
|001 只有一個主要執行緒|使用一個執行緒來執行所設計的 C# 程式碼|這裡的範例程式碼，將會體驗如何這個專案將會使用一個執行緒來執行所設計的 C# 程式碼，也就是，依照 C# 程式碼設計邏輯，依序來執行，因此主執行緒 執行的時候，會輸出 M 字元。|
|002 多執行緒|使用多個執行緒來執行所設計的 C# 程式碼|如何使用 Thread 類別，建立兩個新的執行緒，加上原先的主執行緒，因此，這個處理程序內，共有三個執行緒同時在執行|
|003 執行緒競爭|在多執行緒程式內，共用資源可以同時被多個執行緒存取，應注意競爭產生問題|當程式設計師沒有妥善的控制執行緒存取共用變數的執行順序，，這將導致不可預知結果，也就是共用變數的值會計算不正確|
|004 執行緒競爭解決方法|在多執行緒程式內，要如何解決共用資源可以同時被多個執行緒存取所產生問題|這個範例，將由兩個執行緒執行同樣的方法，計算迴圈共執行了幾次，其中，counter共用變數，則是負責計算累計迴圈執行的次數，當要存取 counter共用變數時候，需要透過lock方式來解決|
|005 執行緒產生死結|為了要存取共用資源，需要透過封鎖機制確保可以正常存取共用資源，但設計不當，將會造成程式當掉的問題|這個範例展示了執行緒互相打死結的範例；執行緒1 & 執行緒2 互相鎖定，導致無法解開|
|006 多工之計算非同步|這是一個簡單的非同步運算的範例|這裡使用了 15 個執行緒，非同步的進行計算迴圈數量，最後進行加總累計，要注意如何在不同執行緒中，存取共同的資源進而產生的問題|
|007 同步造成UI凍結|在這裡將會體驗若程式設計不當，將會造成不佳使用者體驗應用程式，此時，可以透過多執行緒設計出多工程式碼來解決問題|當有大量同步程式在 UI Thread 上執行的時候，會造成 WPF 的整個視窗被凍結了，而無法操作|
|009 執行緒的同步處理內容WPF|在 WPF 使用 執行緒的同步內 SynchronizationContext 進行非同步工作處理問題|在您的 WPF 專案中有使用到 多執行緒 Multiple Thread 或者 非同步 Asynchronous 處理需求，若沒有特別注意，將會發生不可預期的例外異常問題。|
|010 執行緒的同步處理內容ASPNET|在 ASP.NET 使用 執行緒的同步內 SynchronizationContext 進行非同步工作處理問題|在您的 ASP.NET 專案中有使用到 多執行緒 Multiple Thread 或者 非同步 Asynchronous 處理需求，若沒有特別注意，將會發生不可預期的例外異常問題。|
|011 客製化同步內容運作機制|了解同步內容的內部設計方法|我們將會建立一個 Console 類型的專案，並且自訂一個 SynchronizationContext 類別，提供類似 WPF 的同步內容運作機制。|
|012 HttpContext的各種非同步工作使用情境|HttpContext的各種非同步工作使用情境與測試|請試著修改各項參數，查看執行結果有何差異與為什麼會有這樣的問題|
||||

## 2.執行緒

|專案名稱|專案說明|備註|
|-|-|-|
|001 建立Thread使用ThreadStart|一個非常典型的使用 Thread 來做到非同步作業的範例|如何使用 ThreadStart 與 ParameterizedThreadStart 來指定一個委派的方法，並且啟動一個執行緒|
|002 建立Thread使用Lambda|一個非常典型的使用 Thread 來做到非同步作業的範例|使用 Lambda 表示式 來指定一個委派的方法，並且啟動一個執行緒|
|003 背景執行緒|建立 Thread 類別物件與啟動 Thread，並且指定皆為 背景執行緒|在 Main 方法中，只是啟動該執行緒，之後 主執行緒 就會結束了，因此，不等到 背景執行緒 結束，App會自動終止所有的 背景執行緒|
|004 前景執行緒|建立 Thread 類別物件與啟動 Thread，預設為前景執行緒|在 Main 方法中，會啟動一個前景執行緒，之後 主執行緒 就會結束了，因此，此為前景執行緒，因此也需要等候該執行緒結束執行，該處理程序才會結束|
|005 強制終止Abort|體驗要停止一個執行緒的執行|因為 Abort 方法是在另外一個執行緒上執行(我們是從主執行緒呼叫該方法)，並於所在執行緒中引發 ThreadAbortException，開始處理執行緒的結束作業|
|006 終止使用變數|使用變數與輪詢方式，確認執行緒是否要結束執行|要停止一個執行緒的執行，可以使用一個變數旗標來控制，該執行緒是否需要繼續執行| 
|007 終止CancellationToken|學習使用CancellationTokenSource來進行取消 Thread的執行|可以使用 取消許可證來源 CancellationTokenSource 物件，向 CancellationToken 發出訊號，表示應該將它取消，並且在執行緒內應該要結束該執行緒的執行|
|008 使用BackgroundWorker|BackgroundWork 這個類別來建立背景執行緒|BackgroundWork類別簡化了要進行多工非同步的程式設計複雜度，並且提供了多樣性的事件，可讓我們方便處理各項事務，這樣，讓我們可以不用再面對 Thread，也可以做到多工處理|
|009 WPF使用BackgroundWorker|||
|010 大量執行緒產生與執行|大量執行緒的程式設計考量|我們將會產生2000個執行緒，接著我們會觀察整體系統的 CPU使用率、Process數量、執行緒數量、可用記憶體數量、環境交換次數，嘗試了解，當執行緒過多的時候，對於系統有何影響?|
|011 不同優先權的執行緒|練習對於不同優先權的執行緒，對於工作排成 Scheduler 所占用時間之觀察|這個範例將會產生五個執行緒，並且賦予每個執行緒擁有不同執行優先權|
|012 執行緒區域儲存區|使用 ThreadStatic 屬性 來建立執行緒區域儲存區|使用[ThreadStatic] 屬性與LocalDataStoreSlot 結構來設計執行緒及App定義是唯一的資料此一需求|
|013 執行緒的集區|練習使用執行緒集區建立背景執行緒|這個範例展示了如何透過 ThreadPool 來做到多執行緒的多工處理|
|014 執行緒資料位置|使用 ThreadLocal<T> 來建立執行緒區域儲存區|使用 System.Threading.ThreadLocal<T> 類別來建立第一次取用物件時進行延遲初始化的執行緒區域物件|
|015 執行緒具名資料插槽|如何使用具名的資料插槽 (data slots)來儲存執行緒特定資訊|在這個範例示範如何使用資料位置來儲存執行緒特定資訊，使用 Thread.AllocateDataSlot  Thread.SetData 和 Thread.GetData 方法來設定和擷取插槽中的資訊|
|019 WPF執行緒同步處理內容|展示 WPF 應用程式之使用執行緒的同步內容與取消事件注意事項|這個共有兩個功能展示區塊，左半部的開始、取消與右半部的開始與取消，左半部有使用[執行緒的同步處理內容]功能，右半部則沒有使用[執行緒的同步處理內容]功能|
|020 執行緒發生例外異常|當在執行緒執行中，遇到例外異常該如何處理|在這個範例中，共啟動了4個執行緒 (一個主執行緒，3個自訂執行緒)，當執行緒內的執行方法發生了例外異常，是會造成整個處理程序意外終止|
|021 定時循環事件的使用方式|||
|022 封鎖並執行緒終止|如何等候其他執行緒完成執行的作法|學習如何在使用 有 Thread 物件的前景執行緒 & 執行集區背景執行緒 的程式碼已經正常結束了，要在主執行緒等候這些執行緒結束做法|
|023 使用WaitHandle等候執行緒結束|練習使用這個類別來做到不同執行緒間取得或者釋出共用資源的存取權，做到執行緒同步需求|在這個範例中，在主執行緒使用 WaitHandle 類別的靜態 WaitAny 和 WaitAll 方法等候工作完成時，兩個執行緒要執行背景工作的方式。|
|024 執行緒完成後使用回報事件|設計執行緒的完成事件，得知該執行緒最後執行結果(無須封鎖 Block 等候)|在這個範例內，我們將會透過自訂類別，傳遞多個參數到執行緒內，並且當執行緒執行完成後，會自動執行我們事前設定事件方法，在完成的事件方法內，我們可以取得該執行緒的最後執行完成結果|
|025 執行緒完成後使用委派方法通知|設計執行緒的委派方法，得知該執行緒最後執行結果(無須封鎖 Block 等候)|在這個範例中，我們展示了當執行緒執行完成之後，會呼叫一個我們指定的委派方法，通知這個執行緒已經完成了|
|026 執行緒匿名資料插槽|如何使用匿名的資料插槽 (data slots)來儲存執行緒特定資訊|在這個範例示範如何使用資料位置來儲存執行緒特定資訊，使用 Thread.GetNamedDataSlot  Thread.SetData 和 Thread.GetData 方法來設定和擷取插槽中的資訊|
|027 執行緒資料位置ThreadStatic屬性|對於靜態欄位或者屬性，能夠區分在每個執行緒內都具備靜態唯一性，而不會受到不同執行緒執行的影響|將有標示 ThreadStatic 的靜態欄位儲存該執行緒的 Managed執行緒代號，其在每個執行緒內，都具有唯一性|
|016 獨佔鎖定Monitor|||
|017 lock陳述式的深層鎖定問題|||
|018 獨佔鎖定Mutex|||
|028 獨佔鎖定SpinLock|||
|029 巢狀lock|||
|030 用Mutex限制只有一個處理程序可以執行|||
|031 用Mutex進行跨處理程序的執行緒同步|||
||||
||||
||||

### 執行緒同步範例

|專案名稱|專案說明|備註|
|-|-|-|
|lock敘述的封鎖物件誤用範例|不建議使用 lock(this) 這個方法，而要採用私有 object 物件|在這個範例中，MyClass 的 AddNumber 方法，當要進行多執行緒下的數值相加作業時候，需要使用 lock 來做到執行緒同步處理，由於採用 lock(this) 敘述，將會造成程式除錯上的盲點，因為，只要有參考到這個執行個體的變數，都可以拿來做同步封鎖物件，進而影響到該類別內的原有封鎖作業，間接會有死結的問題|
|指定處理程序或執行緒在特定CPU上執行|了解當設定處理序中執行緒可用處理器數量時候的各種執行結果|這個範例程式將會使用 Process.GetCurrentProcess().ProcessorAffinity 來限制處理程序中所有執行緒可用的 CPU 核心數量，我們將透過工作管理員的 CPU 使用率來觀察，限制使用不同數量的 CPU 核心，其多執行緒執行效能|
||||
||||
||||
||||


## 3.非同步程式設計模式 Asynchronous Programming Patterns

|專案名稱|專案說明|備註|
|-|-|-|
|001 封鎖應用程式執行AsyncWaitHandle|使用 APM 非同步方法，但為同步設計 1|使用同步設計方式，請求非同步呼叫，查詢DNS資訊|
|002 封鎖應用程式執行結束非同步作業方式|使用 APM 非同步方法，但為同步設計 2|以結束非同步作業的方式封鎖應用程式執行，無法在等候非同步作業的結果時繼續執行其他工作的應用程式必須封鎖，直到作業完成為止|
|003 輪詢非同步作業的狀態|使用 APM 非同步方法，但為同步設計 3|輪詢非同步作業的狀態，以便得知該非同步作業是否已經完成了|
|004 AsyncCallback委派結束非同步作業|使用 APM 非同步方法，但為同步設計 4|使用 AsyncCallback 委派結束非同步作業|
|005 APM非同步程式設計模型|了解APM非同步程式設計模型的使用方式|使用了 HttpRequest 來進行讀取遠端網頁內容，透過 HttpWebRequest 非同步 APM 方法 BeginGetResponse 方法啟動非同步的呼叫，完成後，使用 EndGetResponse 結束非同步呼叫並且取得結果內容|
|006 EAP事件架構非同步模式|了解EAP非同步程式設計模型的使用方式|使用 WebClient 類別來做為 EAP 設計方法的練習說明|
|007 TAP以工作為基礎的非同步模式|了解TAP非同步程式設計模型的使用方式|使用 TAP Task-based Asynchronous Pattern 來呼叫非同步的工作|
||||


## 4.工作平行程式

|專案名稱|專案說明|備註|
|-|-|-|
|001 建立和起始非同步工作|各種非同步工作的建立與啟動方法|使用 ThreadPool.QueueUserWorkItem / new Task / Task.Factory.StartNew / Task.Run|
|002 建立和起始有參數非同步工作|各種有參數非同步工作的建立與啟動方法|ThreadPool.QueueUserWorkItem / new Task / Task.Factory.StartNew / Task.Run|
|003 Await接續封送處理測試|在沒有UI執行緒類型專案下，了解ConfigureAwait(true/false)的差異|在這裡，我們呼叫 HttpClient 非同步讀取網頁資料資料，分別使用 ConfigureAwait(true) 與 ConfigureAwait(false)，觀察執行前後的執行緒變化|
|004 WPF_Await接續封送處理測試|等候非同步工作完成後，是否要回到原執行緒繼續執行的不同作法練習|我們可以在呼叫非同步方法後，也就是在 await 之後，嘗試將接續封送處理回原始擷取的內容|
|005 同時啟動多個工作|使用了 Task.Factory.StartNew 同時啟動了 8 個非同步工作，用來計算總合|在這裡我們雖然執行了八個非同步工作，可以在取得每個子工作結果的時候，卻是使用同步方式來取得 results[i] = taskArray[i].Result;|
|006 工作等候結束|練習如何透過非同步工作，讀取一個處理完成的回傳內容|建立一個工作，該工作會回傳 42，分別使用 ContinueWith、Wait 與 await|
|007 工作有繼續的不同狀態|當工作完成之後，我們想要接續工作內容，繼續來處理|正常完成的時候，要執行那些工作、若有發出取消指令的時候，要執行那些工作、當工作有異常發生的時候，該做哪些事情|
|008 等候所有工作完成執行|Task.WaitAll 我們先啟動了3個非同步工作，分別需要花費 1, 2, 3 秒鐘的時間|接下來會等候，直到所有的工作都執行完成，並且將工作的執行結果輸出到Console上|
|009 等候任一工作完成執行|Task.WaitAny 我們先啟動了3個非同步工作，分別需要花費 1, 2, 3 秒鐘的時間|接下來會等候，直到任一工作執行完成，並且將工作的執行結果輸出到Console上|
|010 當任一工作完成執行|Task.WhenAny 每個網頁都提供相同的服務，我們希望最新回應的服務，就立即顯示出來|我們要抓取網頁的內容與知道全部字串的長度，不過，我們需要抓取六個網頁，只要其中一個網頁內容有成功抓取到，我們就將該網頁的文字長度列印出來|
|011 |||
|013 工作死結|各種工作呼叫方式與執行緒的同步處理內容(SynchronizationContext)的應用|了解到如何使用不同的呼叫會產生不同的結果，甚至可能會產生 App 凍結或者死結|
|014 客製非同步作業IO繫結|使用 TaskCompletionSource 定義出非同步工作方法，但是，不需要依賴 Thread Pool |在這個範例中，我們建立一個 I/O繫結 非同步的方法，但是，不需要依賴一直持續耗用一個以上 Thread 來執行這個非同步方法|
|015 客製非同步作業CPU繫結|使用 Task.Run 直接定義出非同步工作方法，並且使用額外執行緒來處理|我們建立一個 CPU繫結 非同步的方法，但是，需要依賴 Thread Pool與資料平行化的方式來進行處理，執行這個非同步方法|
|016 WPF工作進度與取消|使用 WebClient 從網路下載一個大檔案|下載的時候，進度狀態棒會根據下載數量更新完成百分比，當然，您也可以按下取消按鈕，已取消這個非同步工作|
|017 Sleep與Delay差異|透過 GUI 應用程式，如 WPF，實際體驗 Sleep 與 Delay 的差異|Thread.Sleep 會造成當時執行緒被封鎖(例如，UI執行緒無法執行任何指令)；Task.Delay 因為使用非同步等候方式，所以，當時的執行緒是不會被封鎖的|
|018 WhenAll工作中發生例外狀況|當所有等候工作都執行結束後，可以檢查是否有執行失敗的工作|建立起9個非同步工作，之後使用 Task.WhenAll，等候所有工作完成|
|019 等候單一工作中發生例外狀況|若非同步工作內有異常發生的時候，使用 TPL方式 Wait 與 await 關鍵字，其針對例外異常處理的方式|了解這兩者對於例外處理的不同|
|AsyncAwait反組譯範例|||
|020 WPF當任一工作完成執行|WPF 演練實際專案開發情境|我們需要一個查詢命令，產生許多Task工作，這些工作將會讀取各個網頁的非同步工作之後，我們將會等候任何一個工作完成即可|
||||
||||
||||
||||
||||
||||
||||
||||
||||
|-|-|-|
||||


