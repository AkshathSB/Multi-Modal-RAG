# Multi-Modal Retrieval System 

## Overview

This project is a **Multi-Modal Retrieval System** that allows users to search and retrieve both text and images based on semantic similarity. It leverages state-of-the-art machine learning models (OpenAI CLIP) and a vector database (Qdrant) to enable cross-modal search—meaning you can search for images using text queries and vice versa. The system is built with a user-friendly web interface using Streamlit.

## Features

- **Semantic Search:** Retrieve relevant Wikipedia articles and images using natural language queries.
- **User Uploads:** Add your own text or images to the database for personalized retrieval.
- **Multi-Modal:** Supports both text and image data, enabling cross-modal search.
- **Efficient Storage:** Uses Qdrant for fast vector similarity search.
- **Interactive UI:** Built with Streamlit for easy interaction.

## Project Structure

```
GenAi-MMRAG-master/
  └── GenAi-MMRAG/
      ├── Main1.py                # Main Streamlit app and backend logic
      ├── requirements.txt        # Python dependencies
      ├── data_wiki/              # Wikipedia articles and images (sample dataset)
      │   ├── *.txt               # Wikipedia article text files
      │   ├── *.jpg               # Associated images
      │   └── images/             # Additional images (possibly user or system generated)
      └── user_data/
          └── images/             # Stores user-uploaded images
```

## How It Works

1. **Data Ingestion:**
   - Loads Wikipedia articles and images from `data_wiki/`.
   - Users can upload their own text or images via the web interface.

2. **Embedding Generation:**
   - Uses OpenAI's CLIP model to generate 512-dimensional embeddings for both text and images.

3. **Vector Storage:**
   - Stores embeddings in Qdrant collections (`text_collection_0` and `image_collection_0`).

4. **Retrieval:**
   - When a user enters a query, the system computes its embedding and retrieves the most similar texts and images from Qdrant.

5. **User Interface:**
   - Streamlit app provides:
     - Text area for uploading articles.
     - Image uploader for custom images.
     - Search bar for querying the database.
     - Display of retrieved articles and images.

## Setup Instructions

### Prerequisites

- Python 3.8+
- [Qdrant](https://qdrant.tech/) instance (local or remote)
- CUDA-enabled GPU (optional, for faster inference)
- [Git](https://git-scm.com/) (for some dependencies)

### Installation

1. **Clone the repository:**
   ```bash
   git clone <repo-url>
   cd GenAi-MMRAG-master/GenAi-MMRAG
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables:**
   - Create a `.env` file in `GenAi-MMRAG/` with:
     ```
     QDRANT_URL=http://localhost:6333
     ```
     (Replace with your Qdrant instance URL if different.)

4. **Start Qdrant (if running locally):**
   ```bash
   docker run -p 6333:6333 -p 6334:6334 qdrant/qdrant
   ```

5. **Run the Streamlit app:**
   ```bash
   streamlit run Main1.py
   ```

6. **Open your browser:**
   - Go to `http://localhost:8501`

## Usage

- **Add Text:** Paste or type your own article and click "Add My Text".
- **Add Image:** Upload a `.jpg` or `.png` image and click "Add My Image".
- **Search:** Enter a query (e.g., "What is the significance of the Kesavananda Bharati case?") and click "Retrieve Results".
- **View Results:** See the most relevant articles and images displayed on the page.

## Data

- **Sample Data:** The `data_wiki/` folder contains Wikipedia articles and images for demonstration.
- **User Data:** Uploaded images are stored in `user_data/images/`.

## Dependencies

Key packages (see `requirements.txt` for full list):

- `torch`, `transformers` (for CLIP model)
- `qdrant-client` (vector database)
- `streamlit` (web UI)
- `Pillow` (image processing)
- `python-dotenv` (environment variables)

## Customization

- **Add More Data:** Place additional `.txt` or `.jpg` files in `data_wiki/` and restart the app.
- **Change Model:** Swap out the CLIP model in `Main1.py` for another supported by HuggingFace Transformers.
- **Tune Retrieval:** Adjust `top_k` in retrieval functions for more or fewer results.

## License

[MIT License] (add your license here)

## Acknowledgements

- [OpenAI CLIP](https://github.com/openai/CLIP)
- [Qdrant Vector Database](https://qdrant.tech/)
- [Streamlit](https://streamlit.io/)
- Wikipedia for sample articles 
