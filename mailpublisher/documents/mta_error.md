# MtaError
[MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)から返却されたエラーを表します。

### パッケージ
apps/console/backend/pkg/infrastructure/mta/mailpublisher

### 構造体名
MtaError

### 生成関数
```go
NewMtaError(Code, Message) MtaError
```
### レシーバーメソッド
```go
// "HTTPステータス: ${Code} エラーメッセージ: ${Message}"フォーマットの文字列を取得します (errors.Errorの実装)
Error() string
// MailPublisher Smart Editionから返却されたHTTPステータスコードを取得します
Code() Code
// MailPublisher Smart Edition]から返却されたメッセージを取得します
Message() Message
```
#### Code [MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)から返却されたHTTPステータスコード
##### 生成関数
```go
ToCode(int) Code
```
##### レシーバーメソッド
```go
// HTTPステータスコードの値を取得します
Int() int
```
#### Message [MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)から返却されたメッセージ
##### 生成関数
```go
ToMessage(string) Message
```
##### レシーバーメソッド
```go
// メッセージ文字列を取得します
String() string
```
