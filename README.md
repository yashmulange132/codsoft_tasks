# codsoft_tasks
I completed 3 task here
TASK 1
def chatbot():
    print("Chatbot: Hello! I am a rule-based chatbot.")
    print("Chatbot: Type 'bye' to exit.")

    while True:
        user_input = input("You: ").lower().strip()

        if user_input in ["hello", "hi", "hey"]:
            print("Chatbot: Hello! How can I help you?")

        elif "how are you" in user_input:
            print("Chatbot: I am doing well. Thank you for asking!")

        elif "your name" in user_input or "who are you" in user_input:
            print("Chatbot: I am a simple rule-based chatbot.")

        elif "what can you do" in user_input:
            print("Chatbot: I can respond to basic questions using predefined rules.")

        elif "help" in user_input:
            print("Chatbot: Sure! Tell me what you need help with.")

        elif "thank" in user_input:
            print("Chatbot: You're welcome!")

        elif user_input in ["bye", "goodbye", "exit", "quit"]:
            print("Chatbot: Goodbye! Have a nice day!")
            break

        else:
            print("Chatbot: Sorry, I don't understand that. Please try another question.")


if __name__ == "__main__":
    chatbot()
    TASK 2
    from transformers import BlipProcessor, BlipForConditionalGeneration
from PIL import Image
import torch

def generate_caption(image_path):
    processor = BlipProcessor.from_pretrained("Salesforce/blip-image-captioning-base")
    model = BlipForConditionalGeneration.from_pretrained("Salesforce/blip-image-captioning-base")

    image = Image.open(image_path).convert("RGB")

    inputs = processor(images=image, return_tensors="pt")

    with torch.no_grad():
        output = model.generate(**inputs, max_new_tokens=50)

    caption = processor.decode(output[0], skip_special_tokens=True)

    return caption

if __name__ == "__main__":
    image_path = input("Enter image path: ")

    try:
        caption = generate_caption(image_path)
        print("Generated Caption:", caption)
    except FileNotFoundError:
        print("Image file not found.")
    except Exception as e:
        print("Error:", e)

        TASK 3

        import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

data = {
    "title": [
        "Avengers: Endgame",
        "Iron Man",
        "Spider-Man",
        "Interstellar",
        "The Martian",
        "Inception",
        "The Dark Knight",
        "Titanic",
        "The Notebook",
        "Jurassic Park"
    ],
    "genre": [
        "action superhero science fiction",
        "action superhero science fiction",
        "action superhero adventure",
        "science fiction adventure drama",
        "science fiction adventure drama",
        "science fiction action thriller",
        "action crime thriller",
        "romance drama",
        "romance drama",
        "science fiction adventure"
    ]
}

df = pd.DataFrame(data)

vectorizer = TfidfVectorizer()
genre_matrix = vectorizer.fit_transform(df["genre"])

similarity_matrix = cosine_similarity(genre_matrix)

def recommend_movies(movie_title, number_of_recommendations=5):
    if movie_title not in df["title"].values:
        print("Movie not found.")
        return

    movie_index = df[df["title"] == movie_title].index[0]

    similarity_scores = list(enumerate(similarity_matrix[movie_index]))
    similarity_scores = sorted(
        similarity_scores,
        key=lambda x: x[1],
        reverse=True
    )

    recommendations = []

    for index, score in similarity_scores[1:number_of_recommendations + 1]:
        recommendations.append(df.iloc[index]["title"])

    print("\nRecommended Movies:")
    for movie in recommendations:
        print(movie)

print("Movie Recommendation System")
print("\nAvailable Movies:")

for movie in df["title"]:
    print(movie)

movie = input("\nEnter a movie you like: ")

recommend_movies(movie)
