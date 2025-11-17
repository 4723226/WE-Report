# 第8回 Webエンジニアリング演習 レポート
## 学籍番号（名前は書かなくてよい）
4723226
## 実装した内容
@app.put("/todos/{todo_id}", response_model=TodoItem_Pydantic)
async def update_todo(todo_id: int, req: TodoItemUpdate_Pydantic):
    todo = await TodoItem.get(id=todo_id)
    if not todo:
        raise HTTPException(status_code=404, detail=f"ID {todo_id} のTODOが見つかりません")

    todo.title = req.title if req.title is not None else todo.title
    todo.description = req.description if req.description is not None else todo.description
    todo.completed = req.completed if req.completed is not None else todo.completed
    await todo.save()
    return todo
## 動作確認結果
存在するID

Response body
Download
{
  "id": 1,
  "title": "string",
  "description": "string",
  "completed": false
}
Response headers
 content-length: 66 
 content-type: application/json 
 date: Mon,17 Nov 2025 05:26:47 GMT 
 server: uvicorn 

存在しないID

Response body
Download
{
  "detail": "Object \"TodoItem\" does not exist"
}
Response headers
 content-length: 47 
 content-type: application/json 
 date: Mon,17 Nov 2025 05:08:33 GMT 
 server: uvicorn
