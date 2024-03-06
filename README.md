# Cassie_ILY: LLAMAv2 Question Answering on Multiple PDFs

This notebook implements LLAMAv2 for answering user questions across a collection of PDF documents. It leverages the following technologies:

- **Langchain:** Facilitates prompt design, history retention, and chained queries.
- **Apache Cassandra:** Distributed NoSQL database for storing document embeddings.
- **LLAMA-Index:** Framework for utilizing LLAMAv2 within the Hugging Face ecosystem.
- **Datastax Astra:** Managed Apache Cassandra service for ease of deployment.

## Initialization of Credentials

Make sure to initialize all credentials in the notebook, particularly in the secret section of Google Colab, and access them using `userdata.get("GRADIENT_ACCESS_TOKEN")`.

Also, when creating an account in Server-based vector store Datastax Astra, you will receive a zip file and a JSON to configure client ID and secret. Place it correctly in a Colab session directory.

## Asking Questions to PDF Files

To ask questions to any PDF file, use the following lines:

```python
# Load the PDFs
documents = SimpleDirectoryReader("/content/Documents").load_data()
print(f"Loaded {len(documents)} document(s).")

# Setup and Query Index
index = VectorStoreIndex.from_documents(documents, service_context=service_context)
query_engine = index.as_query_engine()

# Query
response = query_engine.query("What is Yolov7?")
print(response)
```

Keep the pdf files targeted in Documents directory of your Google Colab session.
