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
  
