# AI SMTP Security Gateway — инструкция для backend

## Что у вас есть от аналитика

### 1. Датасет
- `test-data/manifest.csv` — разметка 70 писем
- `test-data/{CATEGORY}/*.eml` — сами письма

### 2. Промпты
- `backend/app/classifier/prompts/system_v1.txt` — базовая инструкция
- `backend/app/classifier/prompts/system_v2.txt` — улучшенная инструкция
- `backend/app/classifier/prompts/few_shot_v1.json` — 7 примеров
- `backend/app/classifier/prompts/few_shot_v2.json` — 12 примеров

### 3. Тесты
- `backend/tests/test_classifier.py` — юнит-тесты

### 4. Контракт
- `docs/classifier-contract-v1.md` — Email ↔ DeepSeek

## Что нужно сделать

### Шаг 1. Парсер .eml → JSON
Реализовать функцию:
```python
def email_to_deepseek_json(raw_email: bytes) -> dict:
    """
    Парсит .eml и возвращает нормализованный JSON:
    {
      "subject": "...",
      "