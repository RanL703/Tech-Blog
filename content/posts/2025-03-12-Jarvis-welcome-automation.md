---
title: "Jarvis Welcome Automation"
date: 2025-03-12
draft: false
tags: ["python", "ai"]
---

# Jarvis Welcome Automation

Hey there, tech enthusiast! Are you ready to take your productivity to the next level? **Imagine being able to launch your entire coding workspace with just a voice command**! Sounds like something out of a sci-fi movie, right? Well, welcome to the **Jarvis-welcome-automation** project on GitHub, where this fantasy becomes a reality!

### Project Overview
So, what exactly is this project all about? In a nutshell, it's a **Windows voice assistant** that lets you launch your coding workspace with a simple voice command. But that's not all - it also comes with some amazing features like **snarky AI responses** and **text-to-speech feedback**. Can you imagine having a conversation with your computer like you would with a friend? 

### Key Features
Here are some of the standout features of this project:
* **Voice activation** with a customizable wake phrase - because who doesn't want to feel like a boss?
* Launches your coding workspace via a shortcut - no more tedious clicking and typing!
* **Snarky AI responses** using Gemini (online) or Ollama (offline) - because a little humor never hurt anyone!
* **Text-to-speech feedback** - so you can stay focused on your code without having to constantly check your screen

### Technical Highlights
So, what makes this project technically impressive? For starters, it's built using **Python 3.11**, which is the latest and greatest version of the language. It also uses **PyAudio** for audio processing, which is a powerful library that makes it easy to work with audio in Python. And let's not forget about the **AI models** used for the snarky responses - Gemini and Ollama are both cutting-edge models that can understand and respond to natural language input.

### Use Cases
But how would you actually use this project in real life? Here are a few examples:
1. **Launch your coding workspace** with a voice command, so you can start working on your project right away.
2. **Get feedback** on your code with text-to-speech responses, so you can stay focused on your work without having to constantly check your screen.
3. **Have fun** with the snarky AI responses - because coding can be serious business, but it doesn't have to be boring!

### Pro Tips or Implementation Details
So, you want to get started with the project? Here are some pro tips to keep in mind:
* Make sure to **install Python 3.11** and **PyAudio** before running the project.
* **Configure your environment** by setting up your `.env` file with your Gemini API key and workspace shortcut.
* **Choose your AI model** - do you want to use Gemini for online responses or Ollama for offline responses?
* If you're using **PowerToys**, make sure to set up your workspace and create a shortcut to activate it.

Some other things to keep in mind:
* You'll need to **pull the Ollama model** if you want to use it for offline responses.
* You can **customize your wake phrase** to whatever you like - just make sure it's not too similar to other voice commands you use!

### Conclusion
So, what are you waiting for? **Head on over to the Jarvis-welcome-automation repo** and start exploring the code! With this project, you'll be able to launch your coding workspace with just a voice command, and get feedback on your code with text-to-speech responses. It's like having your own personal assistant, right at your fingertips! **Don't be shy - give it a try and see what you can create**!

### Code Highlights

Check out this **awesome code snippet** from the project:

#### voice_assistant.py

```
import speech_recognition as sr
import pyttsx3
import google.generativeai as genai
import requests
import subprocess
from dotenv import load_dotenv
import os
import socket

# Load environment variables
// ... more code ...
```

## Project Details

- GitHub Repository: [Jarvis-welcome-automation](https://github.com/RanL703/Jarvis-welcome-automation)
- Created: 2025-02-24
- Language: Python

