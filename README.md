# main.py
from fastapi import FastAPI
from loguru import logger
import uvicorn

app = FastAPI(title="Atlantica Bot API", version="1.0")

# 🔹 Inisialisasi logger
logger.add("bot.log", rotation="1 MB", retention="7 days", level="INFO")

# 🔹 Endpoint tes (health check)
@app.get("/")
async def root():
    logger.info("Endpoint root diakses")
    return {"status": "Bot server ready!"}

# 🔹 Contoh endpoint untuk trigger bot
@app.post("/start-bot")
async def start_bot():
    logger.info("Bot mulai dijalankan")
    # TODO: tambahkan fungsi auto-battle di sini
    return {"message": "Bot started"}

# 🔹 Endpoint untuk stop bot (placeholder)
@app.post("/stop-bot")
async def stop_bot():
    logger.info("Bot dihentikan")
    # TODO: tambahkan fungsi stop
    return {"message": "Bot stopped"}

if __name__ == "__main__":
    uvicorn.run("main:app", host="0.0.0.0", port=10000)
