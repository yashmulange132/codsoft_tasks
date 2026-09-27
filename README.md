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
   import math

board = [" " for _ in range(9)]

def print_board():
    print()
    for i in range(0, 9, 3):
        print(f" {board[i]} | {board[i+1]} | {board[i+2]} ")
        if i < 6:
            print("---+---+---")
    print()

def check_winner():
    combinations = [
        (0, 1, 2), (3, 4, 5), (6, 7, 8),
        (0, 3, 6), (1, 4, 7), (2, 5, 8),
        (0, 4, 8), (2, 4, 6)
    ]

    for a, b, c in combinations:
        if board[a] == board[b] == board[c] and board[a] != " ":
            return board[a]

    if " " not in board:
        return "Draw"

    return None

def minimax(is_maximizing):
    result = check_winner()

    if result == "O":
        return 1
    if result == "X":
        return -1
    if result == "Draw":
        return 0

    if is_maximizing:
        best_score = -math.inf

        for i in range(9):
            if board[i] == " ":
                board[i] = "O"
                score = minimax(False)
                board[i] = " "
                best_score = max(best_score, score)

        return best_score

    else:
        best_score = math.inf

        for i in range(9):
            if board[i] == " ":
                board[i] = "X"
                score = minimax(True)
                board[i] = " "
                best_score = min(best_score, score)

        return best_score

def ai_move():
    best_score = -math.inf
    best_move = None

    for i in range(9):
        if board[i] == " ":
            board[i] = "O"
            score = minimax(False)
            board[i] = " "

            if score > best_score:
                best_score = score
                best_move = i

    board[best_move] = "O"

def human_move():
    while True:
        try:
            position = int(input("Enter your position (1-9): ")) - 1

            if position < 0 or position > 8:
                print("Enter a number between 1 and 9.")
            elif board[position] != " ":
                print("That position is already occupied.")
            else:
                board[position] = "X"
                break
        except ValueError:
            print("Enter a valid number.")

def main():
    print("Tic-Tac-Toe")
    print("You are X. AI is O.")
    print("Positions:")
    print(" 1 | 2 | 3 ")
    print("---+---+---")
    print(" 4 | 5 | 6 ")
    print("---+---+---")
    print(" 7 | 8 | 9 ")

    while True:
        print_board()

        human_move()

        result = check_winner()

        if result:
            print_board()
            if result == "X":
                print("You win!")
            else:
                print("Draw!")
            break

        ai_move()

        result = check_winner()

        if result:
            print_board()
            if result == "O":
                print("AI wins!")
            else:
                print("Draw!")
            break

if __name__ == "__main__":
    main()

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
