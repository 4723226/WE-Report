# 第7回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723226
## PUTリクエスト検証用のモデルとAPI部分のコード
@app.put("/todos/{todo_id}", response_model=TodoItem)
def update_todo(todo_id: int, req: TodoItemCreateSchema):
    for i, todo in enumerate(todos):
        if todo.id == todo_id:
            updated_todo = TodoItem(id=todo_id, title=req.title, description=req.description, completed=todo.completed)
            todos[i] = updated_todo
            return updated_todo
    raise HTTPException(status_code=404, detail=f"ID {todo_id} のTODOが見つかりません")
## 動作確認結果
- Swagger UIでのPUTエンドポイントテスト結果
{
  "id": 0,
  "title": "string",
  "description": "string",
  "completed": false
}

{
  "detail": [
    {
      "loc": [
        "string",
        0
      ],
      "msg": "string",
      "type": "string"
    }
  ]
}
- 正常系：存在するタスクの更新
Response body
{
  "id": 1,
  "title": "string",
  "description": "string",
  "completed": false
}

Response headers
content-length: 66 
 content-type: application/json 
 date: Mon,10 Nov 2025 04:52:54 GMT 
 server: uvicorn 
- 異常系：存在しないタスクIDでのエラー確認
Response body
{
  "detail": "ID 8 のTODOが見つかりません"
}

Response headers
content-length: 49 
 content-type: application/json 
 date: Mon,10 Nov 2025 04:52:05 GMT 
 server: uvicorn 