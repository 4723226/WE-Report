# 第5回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723226
## 各エンドポイントのSwagger UIでのテスト結果
### GET /
'''
Response body
Download
{
  "Hello": "World"
}
Response headers
 content-length: 17 
 content-type: application/json 
 date: Mon,27 Oct 2025 05:29:40 GMT 
 server: uvicorn

Response body
Download
{
  "status": "healthy"
}
'''

### GET/helthy
Response body
Download
{
  "status": "healthy"
}
Response headers
 content-length: 20 
 content-type: application/json 
 date: Mon,27 Oct 2025 05:28:46 GMT 
 server: uvicorn

Response body
{
  "item_id": 1,
  "q": "hello"
}

### GET /items/{item_id}
Response body
{
  "item_id": 1,
  "q": "hello"
}
Response headers
 content-length: 25 
 content-type: application/json 
 date: Mon,27 Oct 2025 05:30:43 GMT 


{
 server: uvicorn
  "item_id": 1,
  "q": "hello"
}
### GET /items/{item_id} エラーハンドリング
Response body
{
  "detail": "Item ID must be positive"
}
Response headers
 content-length: 37 
 content-type: application/json 
 date: Mon,27 Oct 2025 05:36:53 GMT 
 server: uvicorn 
