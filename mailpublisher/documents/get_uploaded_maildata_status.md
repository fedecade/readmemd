# メールデータアップロード状態取得
[メールデータアップロード](documents/upload_maildata.md)でアップロードしたデータの状態を取得します

## 提供メソッド
- [メールデータアップロード状態取得](#メールデータアップロード状態取得)

## メールデータアップロード状態取得

### メソッドシグネチャ
```go
GetUploadedMaildataStatus(RequestId) (UploadStatus, error)
```

#### RequestId
- [メールデータアップロード](./upload_maildata.md)で取得した、MailPublisherのAPIである`archive_upload.php`のレスポンスに`REQUST_ID`として格納される値

#### UploadStatus
- 処理の状態を返す
- エラー発生時はUndefineを返し、それ以外の場合はUndefine以外のいずれかの値を状態によって返す
```go
type UploadStatus int
var UploadStatuses = struct{
    // まだアップロードしたデータが受け付けられていない (リトライ対象)
    Busy      UploadStatus
    // アップロードしたデータが受け付けられた 
    Done      UploadStatus
    // 不定値
    Undefine  UploadStatus
} {
    Busy:     UploadStatus{1}
    Done:     UploadStatus{0}
    Undefine: UploadStatus{-1}
}
```

#### error
- 正常終了した場合はnil
- 異常終了した場合は以下のいずれかのエラーを返却する
    + [MtaError](./mta_error.md)
    + [UnhandledError](./system_error.md)
