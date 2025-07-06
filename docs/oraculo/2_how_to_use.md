---
sidebar_position: 2
title: How to Use
---

# How to use

## Prerequisites
Before getting started, make sure you have the following installed:

- [Docker](https://www.docker.com/) 

   Used to run services such as the PostgreSQL 15 database and the OpenWebUI interface.

- [Python 3.10.17](https://www.python.org/) 

   Required for using the Airbyte library to fetch data from GitHub.

---

## Installation

Follow these steps to set up the project locally:

1. **Create a GitHub personal access token**  
   Add it to the `example.env` file under the variable:

   ```
   GITHUB_TOKEN=your_token_here
   ```

   ➜ [Generate token here](https://github.com/settings/tokens)

2. **Create a Gemini API key**  
   Add it to the same file under:

   ```
   GEMINI_API_KEY=your_key_here
   ```

   ➜ [Get your key here](https://aistudio.google.com/app/apikey)

3. **Rename the environment file**  
   Rename `example.env` to `.env`

4. **Update repository list**  
   In `main.py`, update the `repos` variable with your GitHub repositories.

5. **Start the containers**  
   Run the following command to start services:

   ```
   docker compose up -d
   ```

   > 🕒 It may take a few minutes even after containers are created.

6. **Configure OpenWebUI**  
   - Access [http://localhost:3000](http://localhost:3000)
   - Create a local account (no email verification required)
   - Go to: [http://localhost:3000/admin/functions](http://localhost:3000/admin/functions)
   - Click **“Import functions”** and upload the file:  
     `src/assets/open_web_ui/pipeline_api.json`
   - Enable the imported function.
   - Return to the homepage: [http://localhost:3000](http://localhost:3000)

7. **Stop the containers (optional)**

   To shut everything down, run:

   ```
   docker compose down
   ```

---

## 💬 How to Ask Questions

Once running, you can ask questions in two ways:

### 1. **Using the OpenWebUI Interface**

Visit:

> [http://localhost:3000](http://localhost:3000)

Type your question in natural language. The imported pipeline will send the request to the backend, which returns the answer.



### 2. **Using the FastAPI Endpoint**

Visit:

> [http://localhost:8000](http://localhost:8000)

You can send a `POST` request to the `/ask` endpoint with a JSON body like:

```json
{
  "question": "List all products and their stock quantities"
}
```

The backend will respond with data retrieved from the database using an AI-generated SQL query.

---