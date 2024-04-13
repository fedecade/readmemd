# 送信データ状態確認
[メールデータ送信](documents/send_datas.md)で送信したデータの送信状態を確認します

## 提供メソッド
- [送信データ状態確認](#送信データ状態確認)

## 送信データ状態確認

### メソッドシグネチャ
CheckSendDataStatus(RequestId) error

#### RequestId
- [メールデータ送信](./send_datas.md)で取得した、MailPublisherのAPIである`archive_upload.php`のレスポンスに`REQUST_ID`として格納される値

#### error
- メールデータの送信が完了した場合はnilを返却する
- 上記以外の場合以下のエラーを返却する可能性がある
    + [NotYetCompleteError](./not_yet_complete_error.md)
    + [MtaError](./mta_error.md)
    + [UnhandledError](./system_error.md)
