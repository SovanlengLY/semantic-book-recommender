# Semantic Book Recommender 📚🧠

As a book lover, I found this project really interesting and enjoyable to work on. This small project allowed me to learn how to apply natural language processing and semantic search techniques to build an intelligent book recommendation system. It also serves as my personal assistant when I need to find a new book to read. Of course, it would be better if the dataset were larger and included more books—but it's just a start and a foundation to build upon. [Demo](https://huggingface.co/spaces/sovanleng/semantic-book-recommender-demo)

## 🔧 Features

- Semantic search using Sentence Transformers
- Embedding generation and similarity scoring
- Gradio interface for easy interaction
  
## 🚀 My Modifications

While this project builds on the original implementation, I made the following changes to better suit my learning goals and preferences:

- 🔁 Refactored parts of the code for better readability and modularity  
- 🧠 Used a lightweight, open-source embedding model  
- 🔍 Added explanations to improve code understanding

  
# Project Walkthrough

This project utilizes the [**7k Books Dataset**](https://www.kaggle.com/datasets/dylanjcastillo/7k-books-with-metadata) from Kaggle. It’s the collection of nearly 7,000 books containing metadata—identifiers, titles, subtitles, authors, categories, cover thumbnails, descriptions, publication years, average ratings, and the number of ratings. 

Let’s dive deeper into the five core components of the project (as outlined in the [original GitHub repo](https://github.com/t-redactyl/llm-semantic-book-recommender)):

---

## 🧹 Text Data Cleaning

Before feeding anything to our model, **data cleaning** is a must. Why? Because *garbage in, garbage out*—low-quality data leads to poor recommendations and subpar AI performance.

1. **Missing Values:**  
   First, we check for missing values and drop those rows. In this dataset, the missing subset is small, so removing them is more practical than filling in the gaps.

2. **Description Length:**  
   Since recommendations are based on book descriptions, we filter out books with descriptions under 25 words. Short blurbs rarely capture a book’s essence, so keeping only substantial descriptions ensures better semantic understanding.


---

## 🔎 Semantic (Vector) Search

Traditional keyword searches are limited—they match exact words or phrases. But with **semantic search**, we match by *meaning*. Here’s how:

- **Embedding:** Both book descriptions and user queries are passed through a pre-trained embedding model.  
- For this project, I use [`paraphrase-MiniLM-L3-v2`](https://huggingface.co/sentence-transformers/paraphrase-MiniLM-L3-v2) from Hugging Face—a lightweight, fast, and open-source model. You can swap in others, like OpenAI embeddings, depending on your resources.

- **Similarity Calculation:**  
  Once each description and user query is transformed into a vector, we compare them using *cosine similarity*. Books with vectors closer to the query are more relevant!

*Example:*  
A user asks for "a book to teach children about nature."  
We convert this into a vector and find books with similar vectors—voilà, smart recommendations!

---

## 🏷️ Text Classification (Zero-Shot Learning)

What if you want to filter books as "Fiction" or "Non-Fiction"—but don’t have explicit labels?  
Enter **zero-shot classification**: with large language models, you can categorize text into *any* labels you specify, even if the model never saw them during training!

- We use the `"facebook/bart-large-mnli"` model from Hugging Face’s Transformers library.
- By simply prompting the model with labels ("fiction", "non-fiction"), it predicts the best fit based on each book’s description.
- This lets users easily filter or browse by type—no manual labeling required!

---

## 😊 Sentiment Analysis & Emotion Extraction

How do you know if a book is suspenseful, joyful, or tear-jerking?  
We bring in *emotion detection* to enrich recommendations!

- For this, we use [`"j-hartmann/emotion-english-distilroberta-base"`](https://huggingface.co/j-hartmann/emotion-english-distilroberta-base)—a model trained on Ekman’s 6 basic emotions, plus "neutral".
- Each book’s description may span multiple sentences and express different emotions.
- We:
  1. Split the description into sentences.
  2. Run emotion analysis on each sentence.
  3. Assign the book’s emotion based on the highest scoring emotion found.

This allows users to search for "joyful adventures" or "heart-wrenching stories" and actually get emotionally tuned recommendations! 🎭

---

## 🌐 Creating a Web Application with Gradio

Let’s make this tool user-friendly!  
[Gradio](https://gradio.app/) is perfect for rapid prototyping—turn your Python function into a shareable web app in just a few lines.

- **Instant Demo:** Users interact via a clean interface—just enter your preferences and get recommendations (with book covers, blurbs, and even emotion tags).
- **Easy Sharing:** Share your demo as a public link or deploy to [Hugging Face Spaces](https://huggingface.co/spaces).
- **Flexible Input:** Support for text, images, and more—no code tweaks needed.


---

## 📌 Credits
Original project by: [@t-redactyl](https://github.com/t-redactyl)
YouTube tutorial: ["Build an LLM-powered Book Recommendation System"](https://www.youtube.com/watch?v=Q7mS1VHm3Yw) 
