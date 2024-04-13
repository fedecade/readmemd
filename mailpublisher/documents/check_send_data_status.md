# 送信データ状態確認
[メールデータ送信](documents/send_datas.md)で送信したデータの送信状態を確認します

## 提供メソッド
- [送信データ状態確認](#送信データ状態確認)

## 送信データ状態確認

### メソッドシグネチャ
CheckSendDataStatus(RequestId) (SendDataStatus, error)

#### RequestId
- [メールデータ送信](./send_datas.md)で取得した、MailPublisherのAPIである`archive_upload.php`のレスポンスに`REQUST_ID`として格納される値

#### SendDataStatus
- 処理の状態を返す
- エラー発生時はUndefineを返し、それ以外の場合はUndefine以外のいずれかの値を状態によって返す
```go
type SendDataStatus int
var SendDataStatuses = struct{
    // まだ送信データが受け付けられていない状態 (リトライ対象)
    Busy      SendDataStatus
    // 送信データが受け付けられた 
    Done      SendDataStatus
    // 不定値
    Undefine  SendDataStatus
} {
    Busy:     SendDataStatus{1}
    Done:     SendDataStatus{0}
    Undefine: SendDataStatus{-1}
}
```

#### error
- 正常終了した場合はnil
- 異常終了した場合は以下のいずれかのエラーを返却する
    + [MtaError](./mta_error.md)
    + [UnhandledError](./system_error.md)
