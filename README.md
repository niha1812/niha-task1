import speech_recognition as sr
import pyttsx3
import datetime
import webbrowser
import wikipedia

# Initialize voice engine
engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

# Greeting
def wish_user():
    hour = datetime.datetime.now().hour

    if hour < 12:
        speak("Good Morning")
    elif hour < 18:
        speak("Good Afternoon")
    else:
        speak("Good Evening")

    speak("I am your Python Voice Assistant. How can I help you?")

# Take voice command
def take_command():
    recognizer = sr.Recognizer()

    with sr.Microphone() as source:
        print("Listening...")
        recognizer.pause_threshold = 1
        audio = recognizer.listen(source)

    try:
        print("Recognizing...")
        command = recognizer.recognize_google(audio, language='en-in')
        print("You said:", command)
        return command.lower()

    except Exception:
        print("Sorry, please say that again.")
        return "none"

# Main program
wish_user()

while True:
    query = take_command()

    # Wikipedia Search
    if 'wikipedia' in query:
        speak("Searching Wikipedia")
        query = query.replace("wikipedia", "")
        result = wikipedia.summary(query, sentences=2)
        print(result)
        speak(result)

    # Open YouTube
    elif 'open youtube' in query:
        webbrowser.open("https://www.youtube.com")
        speak("Opening YouTube")

    # Open Google
    elif 'open google' in query:
        webbrowser.open("https://www.google.com")
        speak("Opening Google")

    # Tell Time
    elif 'time' in query:
        time = datetime.datetime.now().strftime("%H:%M:%S")
        speak(f"The time is {time}")
        print(time)

    # Tell Date
    elif 'date' in query:
        date = datetime.datetime.now().strftime("%d %B %Y")
        speak(f"Today's date is {date}")
        print(date)

    # Exit Program
    elif 'exit' in query or 'stop' in query:
        speak("Goodbye")
        break

        🎙️ AI Voice Assistant
An intelligent Voice Assistant built using modern AI and speech technologies that can listen to user commands, process them, and respond naturally in real time.
This project combines Speech Recognition, Natural Language Processing, and Text-to-Speech to create a smart virtual assistant experience.
🚀 Features
🎤 Voice command recognition
🗣️ Text-to-Speech responses
🤖 AI-powered conversation handling
🌐 Web search & information retrieval
📂 Open applications/files using voice commands
⏰ Time, date, weather, and reminders support
🔍 Smart command processing
⚡ Fast and interactive user experience
🛠️ Technologies Used
Python
SpeechRecognition
pyttsx3 / gTTS
OpenAI API / Gemini API (if used)
Flask / FastAPI (if used)
PyAudio
NLP Libraries
📦 Installation
Clone the repository:
Bash
git clone https://github.com/your-username/voice-assistant.git

