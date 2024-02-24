from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from typing import List

app = FastAPI()

# Temporary database in memory
db = []

class Todo(BaseModel):
    id: int
    task: str

@app.post("/todos/")
def create_todo(todo: Todo):
    db.append(todo)
    return todo

@app.get("/todos/", response_model=List[Todo])
def read_todos():
    return db

@app.get("/todos/{todo_id}", response_model=Todo)
def read_todo(todo_id: int):
    for todo in db:
        if todo.id == todo_id:
            return todo
    raise HTTPException(status_code=404, detail="Todo not found")

@app.put("/todos/{todo_id}")
def update_todo(todo_id: int, updated_todo: Todo):
    for i, todo in enumerate(db):
        if todo.id == todo_id:
            db[i] = updated_todo
            return {"message": "Todo updated successfully"}
    raise HTTPException(status_code=404, detail="Todo not found")

@app.delete("/todos/{todo_id}")
def delete_todo(todo_id: int):
    for i, todo in enumerate(db):
        if todo.id == todo_id:
            del db[i]
            return {"message": "Todo deleted successfully"}
    raise HTTPException(status_code=404, detail="Todo not found")
