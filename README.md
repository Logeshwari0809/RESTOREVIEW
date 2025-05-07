# RESTOREVIEW

# RestoReview: Context-Aware Restaurant Review Retrieval and Analysis 🍽️

**RestoReview** is an end-to-end restaurant recommendation and review analysis platform built using Retrieval-Augmented Generation (RAG). It leverages Elasticsearch for semantic search and integrates with Google's Gemini LLM via LlamaIndex to provide insightful, personalized suggestions based on real user reviews.

---

## 🚀 Features
- **Context-aware Restaurant Recommendations**
- **Semantic Search on Reviews (KNN + Dense Vectors)**
- **AI-generated Responses using Gemini LLM**
- **Interactive Frontend via Streamlit**
- **FastAPI Backend for RESTful APIs**
- **Optimized with Caching and Persistent Storage**
- **Dockerized with GitHub Actions for CI/CD**

---

## 🧠 RAG Architecture Overview

### 1. Store Data in Elasticsearch
- Reviews are stored in an Elasticsearch index.
- Vector embeddings of reviews are stored for similarity search.
- Deployed via Docker for easy setup.

📓 Notebook: [`notebooks/indexData.ipynb`](Notebook/indexData.ipynb)

```python
indexMapping = {
  "properties": {
    "restaurant_name": {"type": "text"},
    "review": {"type": "text"},
    "rating": {"type": "integer"},
    "rating_category": {"type": "text"},
    "review_vector": {
      "type": "dense_vector", "dims": 768,
      "index": True, "similarity": "cosine"
    }
  }
}
es.indices.create(index="review_index", mappings=indexMapping)
```

---

### 2. Semantic Search in Elasticsearch
- Converts user query into vector embeddings using Gemini.
- Performs KNN search to find semantically relevant reviews.

```python
result = genai.embed_content(model="models/text-embedding-004", content=text)
```

---

### 3. Connecting to LLM via LlamaIndex
- Integrates Gemini LLM using LlamaIndex.
- Retrieves relevant reviews and formulates a natural language response.

📓 Notebook: [`notebooks/llamaIndex.ipynb`](Notebook/llamaIndex.ipynb)

```python
query_engine = index.as_query_engine(llm, similarity_top_k=10)
response = query_engine.query(QueryBundle(query_str=query))
print(response.response)
```

---

### 4. Gemini LLM for Insightful Responses
- Summarizes reviews
- Highlights must-try dishes
- Formats output clearly with recommendations and conclusions

📓 Notebook: [`notebooks/app_workflow.ipynb`](Notebook/app_workflow.ipynb)

```python
prompt = f"You are a restaurant suggestor..."
response = model.generate_content(prompt)
```

---

### 5. Frontend with Streamlit
- Clean, intuitive UI
- Instant review insights and restaurant chat

📄 Script: [`src/app2.py`](SRC/app2.py)

---

### 6. Backend with FastAPI
- Manages API requests and LLM communications

📄 Script: [`api/main.py`](API/main.py)

---

### 7. Docker + GitHub Actions
- Dockerized microservices
- CI/CD pipeline using GitHub Actions

📄 Workflow: [`.github/workflows/main.yaml`](Workflows/main.yaml)

---

### 8. Performance Optimization
- Streamlit caching via `@cache_data`
- Persistent vector index using `StorageContext`

```python
storage_context = StorageContext.from_defaults(persist_dir="./storage")
index = load_index_from_storage(storage_context=storage_context, index_id="vector_index")
```

---

## 🎥 Video Demonstration
Stay tuned! Coming soon in the repository.

---

## 📚 Conclusion
This project has been an insightful journey into RAG-based applications. With tools like Gemini, Elasticsearch, LlamaIndex, and Docker, building intelligent systems becomes both fun and impactful. The takeaway? Start small, learn by doing, and iterate fast.

---

## 🧾 Source Code
The complete source code, notebooks, and configurations are available in this repository.

---

## 🛠️ Tech Stack
- **Elasticsearch**
- **Streamlit**
- **FastAPI**
- **Gemini LLM**
- **LlamaIndex**
- **Docker**
- **GitHub Actions**
- **Python 3.11**

---

## ✨ Author
Logeshwari — MSc Applied Data Science | AI Enthusiast | Open to Collaboration

---

## 🌍 SDG Goal
**Industry, Innovation and Infrastructure** (SDG Goal 9): Leveraging AI and technology to enhance decision-making in food and hospitality.

---
