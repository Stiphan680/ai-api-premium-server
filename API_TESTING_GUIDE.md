# API Testing Guide - Advanced AI Server

## Quick Start

### 1. Get Your API Key
```bash
# Local development (no auth needed for testing)
curl http://localhost:8000/health

# Production (add X-API-Key header)
curl -H "X-API-Key: sk-your-api-key" \
     https://ai-api-premium-server.onrender.com/health
```

### 2. Set Environment Variables
```bash
export API_KEY="sk-your-api-key"
export API_URL="https://ai-api-premium-server.onrender.com"
```

---

## Advanced Chat with Extended Thinking

### Basic Chat Request
```bash
curl -X POST $API_URL/api/chat \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "message": "What is machine learning?",
    "model": "claude-3.5-sonnet",
    "max_tokens": 1000,
    "temperature": 0.7
  }'
```

### Complex Query with Extended Thinking
```bash
curl -X POST $API_URL/api/chat \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "message": "Compare quantum computing with classical computing. Discuss the implications for cryptography.",
    "model": "claude-3.5-sonnet",
    "max_tokens": 2000,
    "enable_reasoning": true,
    "thinking_budget": 8000,
    "temperature": 0.7,
    "top_p": 0.9,
    "response_mode": "detailed",
    "filter_level": "minimal",
    "context_window": 16000
  }'
```

### Response Example
```json
{
  "status": "success",
  "response": "Quantum computing represents a paradigm shift in computational models...",
  "model_used": "claude-3.5-sonnet",
  "tokens_used": {
    "input_tokens": 32,
    "reasoning_tokens": 2847,
    "output_tokens": 543,
    "total_tokens": 3422
  },
  "reasoning": "[Step 1] Analyzing the question structure...\n[Step 2] Identifying key concepts...",
  "confidence_score": 0.96,
  "sources": ["knowledge_base", "reasoning_engine"],
  "follow_up_questions": [
    "What are the current limitations of quantum computers?",
    "When will quantum computers be commercially viable?"
  ],
  "metadata": {
    "temperature": 0.7,
    "response_mode": "detailed",
    "response_time_ms": "142.35"
  },
  "timestamp": "2026-01-19T12:30:45.123456"
}
```

### Multi-turn Conversation
```bash
curl -X POST $API_URL/api/chat \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "message": "Explain the second point in more detail.",
    "model": "claude-3.5-sonnet",
    "conversation_history": [
      {
        "role": "user",
        "content": "List the key differences between Python and JavaScript"
      },
      {
        "role": "assistant",
        "content": "Here are the key differences..."
      },
      {
        "role": "user",
        "content": "Which one is better for web development?"
      },
      {
        "role": "assistant",
        "content": "For web development, both have their strengths..."
      }
    ],
    "enable_reasoning": true,
    "response_mode": "detailed"
  }'
```

---

## Vision Analysis

### Analyze Image from URL
```bash
curl -X POST $API_URL/api/vision-analysis \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "image_url": "https://example.com/product.jpg",
    "analysis_type": "comprehensive",
    "include_ocr": true,
    "include_objects": true,
    "include_sentiment": true
  }'
```

### Response Example
```json
{
  "status": "success",
  "image_url": "https://example.com/product.jpg",
  "analysis_type": "comprehensive",
  "findings": {
    "primary_objects": ["laptop", "desk", "monitor"],
    "scene_description": "A professional workspace with modern equipment",
    "detected_text": "Text extracted from the image",
    "sentiment_analysis": {
      "overall_sentiment": "positive",
      "confidence": 0.92,
      "emotions_detected": ["professional", "organized"]
    },
    "colors_dominant": ["#1F2937", "#E5E7EB"],
    "composition_analysis": "Professional setup, well-lit, balanced"
  },
  "confidence_level": 0.94,
  "processing_time_ms": 234,
  "timestamp": "2026-01-19T12:31:00.000000"
}
```

---

## Code Generation

### Generate Production Code
```bash
curl -X POST $API_URL/api/code \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "description": "Create a FastAPI endpoint that accepts user data, validates it with Pydantic, and saves to PostgreSQL database",
    "language": "python",
    "quality": "production",
    "include_tests": true,
    "include_docs": true,
    "optimization_level": "balanced",
    "complexity_level": "intermediate"
  }'
```

### Generate JavaScript Code
```bash
curl -X POST $API_URL/api/code \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "description": "Implement a React component for real-time data visualization using D3.js",
    "language": "javascript",
    "quality": "enterprise",
    "include_tests": true,
    "include_docs": true,
    "optimization_level": "performance"
  }'
```

### Response Example
```json
{
  "status": "success",
  "code": "# Generated code here...",
  "language": "python",
  "quality": "production",
  "includes": {
    "tests": true,
    "documentation": true,
    "type_hints": true,
    "error_handling": true,
    "logging": true
  },
  "metrics": {
    "lines_of_code": 234,
    "cyclomatic_complexity": 3,
    "test_coverage": "100%",
    "documentation_coverage": "95%"
  },
  "timestamp": "2026-01-19T12:32:00.000000"
}
```

---

## Data Analysis

### Analyze Sales Data
```bash
curl -X POST $API_URL/api/analyze \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "data": "{\"months\": [\"Jan\", \"Feb\", \"Mar\"], \"sales\": [10000, 12000, 15000]}",
    "analysis_type": "comprehensive",
    "data_format": "json",
    "include_ml_insights": true,
    "include_predictions": true,
    "confidence_threshold": 0.85
  }'
```

### Response Example
```json
{
  "status": "success",
  "insights": [
    "Strong positive correlation identified (r=0.98)",
    "Average growth rate: 22.5% per month",
    "No significant anomalies detected",
    "Trend: Consistent upward trajectory",
    "Forecast: Expected 18200 for April (±5%)"
  ],
  "ml_predictions": {
    "predicted_trend": "Strong upward trend",
    "prediction_confidence": 0.96,
    "forecasted_values": [18200, 21000, 24500],
    "anomaly_score": 0.01,
    "seasonal_pattern": "Minimal seasonality"
  },
  "confidence_level": 0.96,
  "recommendations": [
    "Increase marketing investment to capitalize on growth",
    "Prepare inventory for increased demand",
    "Consider pricing optimization"
  ],
  "detailed_report": {
    "summary_statistics": {
      "mean": 12333.33,
      "median": 12000,
      "std_dev": 2081.67,
      "min": 10000,
      "max": 15000
    }
  },
  "timestamp": "2026-01-19T12:33:00.000000"
}
```

---

## Translation

### Translate to Multiple Languages
```bash
# Translate to Hindi
curl -X POST $API_URL/api/translate \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "text": "Hello, how are you today?",
    "target_language": "hindi",
    "preserve_formatting": true,
    "include_transliteration": true
  }'

# Translate to Spanish
curl -X POST $API_URL/api/translate \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "text": "The machine learning model achieved 95% accuracy",
    "target_language": "spanish"
  }'
```

### Response Example
```json
{
  "status": "success",
  "original_text": "Hello, how are you today?",
  "source_language": "english",
  "target_language": "hindi",
  "translated_text": "नमस्ते, आप आज कैसे हैं?",
  "transliteration": "Namaste, aap aaj kaise hain?",
  "metrics": {
    "accuracy": 0.998,
    "confidence": 0.997,
    "processing_time_ms": 125
  },
  "alternatives": [
    "नमस्कार, आप आज कैसे हो?",
    "हेलो, आप आज कैसे हैं?"
  ],
  "timestamp": "2026-01-19T12:34:00.000000"
}
```

---

## Configuration

### Update Server Configuration
```bash
curl -X POST $API_URL/api/config \
  -H "Content-Type: application/json" \
  -H "X-API-Key: $API_KEY" \
  -d '{
    "filter_level": "minimal",
    "response_mode": "detailed",
    "enable_caching": true,
    "enable_logging": true,
    "auto_optimization": true
  }'
```

---

## Statistics & Monitoring

### Get API Statistics
```bash
curl -H "X-API-Key: $API_KEY" \
     $API_URL/api/stats
```

### Response Example
```json
{
  "status": "operational",
  "timestamp": "2026-01-19T12:35:00.000000",
  "metrics": {
    "uptime_percentage": 99.99,
    "average_response_time_ms": 45,
    "requests_processed": 1500000,
    "active_connections": 342,
    "cache_hit_rate": 0.87,
    "average_tokens_per_request": 650
  },
  "models_available": {
    "claude-3.5-sonnet": {
      "status": "active",
      "avg_latency_ms": 45
    },
    "claude-3-opus": {
      "status": "active",
      "avg_latency_ms": 50
    },
    "gpt-4-turbo": {
      "status": "active",
      "avg_latency_ms": 60
    }
  }
}
```

---

## Error Handling

### 401 - Unauthorized
```json
{
  "status": "error",
  "error_code": 401,
  "message": "Missing API key",
  "timestamp": "2026-01-19T12:36:00.000000"
}
```

### 429 - Rate Limited
```json
{
  "status": "error",
  "error_code": 429,
  "message": "Rate limit exceeded",
  "timestamp": "2026-01-19T12:37:00.000000"
}
```

### 500 - Server Error
```json
{
  "status": "error",
  "error_code": 500,
  "message": "Internal server error",
  "timestamp": "2026-01-19T12:38:00.000000"
}
```

---

## Performance Tips

1. **Use Streaming**: Large responses benefit from streaming
2. **Batch Requests**: Group multiple requests when possible
3. **Cache Results**: Store frequently used responses
4. **Optimize Tokens**: Use concise prompts
5. **Monitor Rate Limits**: Check X-RateLimit-* headers

---

## Testing Tools

### Postman Collection
Import the included `postman_collection.json` file

### Insomnia Template
Use the `insomnia_export.json` file for Insomnia

### Python Testing
```bash
pip install requests pytest
python -m pytest tests/test_api.py -v
```

### JavaScript Testing
```bash
npm install --save-dev jest axios
npm test
```

---

## Rate Limiting

- **Default Limit**: 1000 requests per hour
- **Headers**:
  - `X-RateLimit-Limit`: Maximum requests
  - `X-RateLimit-Remaining`: Requests left
  - `X-RateLimit-Reset`: Unix timestamp when limit resets

---

## Best Practices

✅ Always use `X-API-Key` in production  
✅ Implement exponential backoff for retries  
✅ Monitor rate limit headers  
✅ Cache responses when appropriate  
✅ Use reasonable timeout values  
✅ Log all errors and responses  
✅ Test with different `temperature` values  
✅ Use appropriate `response_mode` for your use case  

---

**Happy testing! 🚀**
