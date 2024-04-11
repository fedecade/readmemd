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
// Error エラーを表す文字列を取得します (errors.Errorの実装)
Error() string
```
#### Code [MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)から返却されたHTTPステータスコード
##### 生成関数
```go
ToCode(int) Code
```
##### レシーバーメソッド
```go
// Int HTTPステータスコードの値を取得します
Int() int
```
#### Message [MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)から返却されたメッセージ文字列
##### 生成関数
```go
ToMessage(string) Message
```
##### レシーバーメソッド
```go
// String メッセージ文字列を取得します
String() string
```
