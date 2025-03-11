---
title: "Jarvis Welcome Automation"
date: 2025-03-11
draft: false
tags: ["python", "ai"]
---

# Jarvis Welcome Automation

### Project Overview

Voice-Activated Workspace Assistant

A Windows voice assistant that launches your coding workspace with a voice command.

Features
- Voice activation with customizable wake phrase
- Launches your coding workspace via shortcut
- Snarky AI responses using Gemini (online) or Ollama (offline)
- Text-to-speech feedback

Are you getting excited yet? You should be!

### Code Highlights

Let's dive into some **awesome code** that makes this project tick:

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
load_dotenv()

# Configuration
GEMINI_API_KEY = os.getenv('GEMINI_API_KEY')
OLLAMA_URL = os.getenv('OLLAMA_URL', 'http://localhost:11434/api/generate')
// ... more code ...
```

### Conclusion

Wow! This project demonstrates incredible skills in **Python** and python, ai. Check out the repository for more details and feel free to contribute! Trust me, you don't want to miss this one!

## Project Details

- GitHub Repository: [Jarvis-welcome-automation](https://github.com/RanL703/Jarvis-welcome-automation)
- Created: 2025-02-24
- Language: Python

