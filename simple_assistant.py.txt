import pyttsx3
import speech_recognition as sr
import datetime
import webbrowser
import os


wb=webbrowser.get('chrome %s')
engine=pyttsx3.init()
v=engine.getProperty('voices')
engine.setProperty('voice',v[1].id)




def speak(audio):
    engine.say(audio)
    engine.runAndWait()




def wishme():
    hour=int(datetime.datetime.now().hour)
    if(hour>=0 and hour<12):
        print("Hello, Good Morning!")
        speak("Hello, Good Morning!")
    elif(hour>=12 and hour<18):
        print("Hello, Good Afternoon!")
        speak("Hello, Good Afternoon!")
    else:
        print("Hello, Good Evening!")
        speak("Hello, Good Evening!")
    print("I am Veronica. Your Personal Assistance.")
    speak("I am Veronica. Your Personal Assistance.")




def takeaudio():
    r=sr.Recognizer()
    with sr.Microphone() as source:
        r.adjust_for_ambient_noise(source, duration=0.5)
        print("Listening...")
        audio1=r.listen(source,phrase_time_limit=10)
       
    try:
        print("Recognizing...")
        query=r.recognize_google(audio1, language='en-in')
        print(f"User said: {query}\n")
    except Exception as e:
        print("Say that again please...")
        return "None"
    return query




if __name__=="__main__":
    wishme()
    print("What is your name, Human?")
    speak("What is your name, Human?")
    name='Human'
    name=takeaudio()
    print("Hello, "+name+'.'+" Please tell me how may I help you?")
    speak("Hello, "+name+'.'+" Please tell me how may I help you?")
    
    while True:
        query=takeaudio().lower()


        if "who are you" in query or "define yourself" in query:
            say="Hello, I am Veronica. Your Personal Assistance."
            print(say)
            speak(say)
        elif "who made you" in query or "created you" in query:
            say="I have been created by the members of Group 3."
            print(say)
            speak(say)
        elif "how are you" in query:
            say="I'm fine. What about you?"
            print(say)
            speak(say)
        elif "fine" in query or "good" in query or "well" in query:
            say="Happy to hear that."
            print(say)
            speak(say)
        elif "wikipedia" in query:
            print("Searching Wikipedia...")
            speak("Searching Wikipedia...")
            indx=query.lower().split().index('wikipedia')
            search_ques=query.split()[indx+1:]
            wb.open("https://en.wikipedia.org/wiki/"+ '+'.join(search_ques))
        elif "youtube" in query:
            print("Opening YouTube...")
            speak("Opening YouTube...")
            indx=query.lower().split().index('youtube')
            search_ques=query.split()[indx+1:]
            wb.open("https://www.youtube.com/search?q="+ '+'.join(search_ques))
        elif "google" in query:
            print("Opening Google...")
            speak("Opening Google...")
            indx=query.lower().split().index('google')
            search_ques=query.split()[indx+1:]
            wb.open("https://www.google.com/search?q="+ '+'.join(search_ques))
        elif "word" in query:
            print("Opening MS-Word...")
            speak("Opening MS-Word...")
            os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Word")
        elif "powerpoint" in query:
            print("Opening MS-Powerpoint...")
            speak("Opening MS-Powerpoint...")
            os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\PowerPoint")
        elif "excel" in query:
            print("Opening MS-Excel...")
            speak("Opening MS-Excel...")
            os.startfile("C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Excel")
        elif "play music" in query:
            print("Playing Music...")
            speak("Playing Music...")
            music_dir="Music"
            songs=os.listdir(music_dir)
            os.startfile(os.path.join(music_dir,songs[6]))
        elif "date and time" in query:
            strDate=datetime.date.today().strftime("%d-%m-%Y")
            strTime=datetime.datetime.now().strftime("%H:%M:%S")
            print(f"Today's date is {strDate}")
            speak(f"Today's date is {strDate}")
            print(f"The time is {strTime}")
            speak(f"The time is {strTime}")
            
        elif "stop" in query:
            print("Bye. Stay safe and healthy.")
            speak("Bye. Stay safe and healthy.")
            break
        else:
            print("Sorry, it is not available..")
