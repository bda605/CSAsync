#  .NET/C# 開發實戰 C# 非同步練習範例

## 1.作業系統知識回顧

|專案名稱|專案說明|備註|
|-|-|-|
|001 只有一個主要執行緒|使用一個執行緒來執行所設計的 C# 程式碼|這裡的範例程式碼，將會體驗如何這個專案將會使用一個執行緒來執行所設計的 C# 程式碼，也就是，依照 C# 程式碼設計邏輯，依序來執行，因此主執行緒 執行的時候，會輸出 M 字元。|
|002 多執行緒|使用多個執行緒來執行所設計的 C# 程式碼|如何使用 Thread 類別，建立兩個新的執行緒，加上原先的主執行緒，因此，這個處理程序內，共有三個執行緒同時在執行|
|003 執行緒競爭|在多執行緒程式內，共用資源可以同時被多個執行緒存取，應注意競爭產生問題|當程式設計師沒有妥善的控制執行緒存取共用變數的執行順序，，這將導致不可預知結果，也就是共用變數的值會計算不正確|
|004 執行緒競爭解決方法|在多執行緒程式內，要如何解決共用資源可以同時被多個執行緒存取所產生問題||
|005 執行緒產生死結|||
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
|001 建立Thread使用ThreadStart|||
|002 建立Thread使用Lambda|||
|003 背景執行緒|||
|004 前景執行緒|||
|005 強制終止Abort|||
|006 終止使用變數|||
|007 終止CancellationToken|||
|008 使用BackgroundWorker|||
|009 WPF使用BackgroundWorker|||
|010 大量執行緒產生與執行|||
|011 不同優先權的執行緒|||
|012 執行緒區域儲存區|||
|013 執行緒的集區|||
|014 執行緒資料位置|||
|015 執行緒GetDataSetData|||
|015 執行緒資料位置ThreadStatic屬性|||
|016 執行緒問題1競爭|||
|017 執行緒問題1競爭解決方法|||
|018 執行緒問題2產生死結|||
|019 執行緒同步處理內容|||
|020 執行緒發生例外異常|||
|021 定時循環事件的使用方式|||
|022 封鎖並執行緒終止|||
|023 使用WaitHandle等候執行緒結束|||
|024 執行緒完成後使用回報事件|||
|025 執行緒完成後使用委派方法通知|||
|001 啟動處理序|||
|002 等候處理程序結束|||
|003 使用ProcessStartInfo啟動程序|||
|004 停止處理程序|||
|005 取得本機所有處理程序|||
||||


## 3.非同步程式設計模式 Asynchronous Programming Patterns

|專案名稱|專案說明|備註|
|-|-|-|
|001 封鎖應用程式執行AsyncWaitHandle|||
|002 封鎖應用程式執行結束非同步作業方式|||
|003 輪詢非同步作業的狀態|||
|004 AsyncCallback委派結束非同步作業|||
|001 APM非同步程式設計模型|||
|002 EAP事件架構非同步模式|||
|003 TAP以工作為基礎的非同步模式|||
||||


## 4.工作平行程式

|專案名稱|專案說明|備註|
|-|-|-|
|001 建立和起始非同步工作|||
|002 建立和起始有參數非同步工作|||
|003 Await接續封送處理測試|||
|004 WPF_Await接續封送處理測試|||
|005 同時啟動多個工作|||
|006 工作有繼續|||
|007 工作有繼續的不同狀態|||
|008 等候所有工作完成執行|||
|009 等候任一工作完成執行|||
|010 當任一工作完成執行|||
|011 WPF當任一工作完成執行|||
|012 等候Task的awaiter|||
|013 工作死結|||
|014 客製非同步作業IO繫結|||
|015 客製非同步作業CPU繫結|||
|016 WPF工作進度與取消|||
|017 Sleep與Delay差異|||
|018 WhenAll工作中發生例外狀況|||
|019 等候單一工作中發生例外狀況|||
|AsyncAwait反組譯範例|||
||||
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


