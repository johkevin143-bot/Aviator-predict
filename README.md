# Aviator-predict
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel
import numpy as np

app = FastAPI()

# TENA ILAINA: Mamela an'i Lovable hiantso an'ity API ity
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Azonao ovaina ho URL-n'ny Lovable app-nao rehefa mivoaka
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

class HistoryData(BaseModel):
    multipliers: list

@app.get("/")
def read_root():
    return {"message": "Ny API-nao dia mandeha tsara ao amin'ny Render!"}

@app.post("/predict")
def get_prediction(data: HistoryData):
    # Raisina ny data 10 farany avy amin'ny Lovable
    input_data = data.multipliers
    
    # Eto no asiana an'ilay LSTM + XGBoost model-nao rehefa avy eo
    # Ohatra fotsiny ity valiny ity aloha:
    pred_prob = 0.78  
    target = "1.80x"
    
    return {
        "status": "success",
        "prediction": target,
        "probability": f"{pred_prob * 100:.0f}%"
    }
    fastapi
uvicorn
pydantic
numpy
xgboost
tensorflow-cpu
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["uvicorn", "main.py:app", "--host", "0.0.0.0", "--port", "10000"]
