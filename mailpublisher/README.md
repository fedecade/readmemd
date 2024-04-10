# MailPublisher Driver
このパッケージは[エンバーポイントホールディングス株式会社](https://emberpoint.com/)が提供するメール配信サービスである [MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)をMC2コンソールバックエンドがメール配信で使用するための機能を提供します
## メール配信サービスの利用者
このドライバーは下記の事業者様のみをメール配信の利用者として想定しています。
- [ブックオフグループホールディングス株式会社](https://www.bookoffgroup.co.jp/)
## 提供するAPI
このドライバーは以下のAPIを提供します。
### [連携ファイル送信](documents/send_datas.md)
メール配信で使用される配信先リストと差し込みデータをMTAに送信します
### [連携ファイル状態確認](documents/check_send_data_status.md)
[連携ファイル送信](documents/send_datas.md)で送信したデータの受信状態を確認します
### [メール予約](documents/schedule_email_delivery.md)
メール配信を予約します
