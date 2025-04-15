---
title: "My very own Local AI server!"
date: 2025-02-07
draft: false
tags:
- AI
- blogging 
---
Okay, so AI is EVERYWHERE, right? It's changing how we work, learn, create – you name it! I'm not gonna lie, I wanted my family to get in on this AI revolution too. Imagine my parents crushing it at work with super-powered research, and my little cousin sis becoming a creative genius with AI tools! 

But here's the thing that kept me up at night: _privacy_. Seriously, handing over all our family's data to massive AI companies, especially ones based in places where governments can just demand access? 

No, thanks! 

That's why I went full DIY and built a personal AI server right here at home. Boom! Total control over our data, zero worries about prying eyes. Plus, I get to be the cool tech guy who sets up a safe, kid-friendly AI zone for my cousin, and an unrestricted, power-user AI for my parents. Ready to ditch the privacy headaches and build your own awesome family AI server? Let's dive into the WSL setup!

Here are the steps, I followed, to bring this personal AI server to life:

## **Prerequisites for WSL Installation:**

- **Enable WSL:** If you haven't already, you need to enable WSL on your Windows machine. Open PowerShell as Administrator and run:
    ```powershell
    wsl --install
    ```
    This command will install the default Ubuntu distribution. You may need to restart your computer after this step.
    
- **Update WSL:** After installation, ensure your WSL environment is up-to-date by opening your Ubuntu terminal (you can search for "Ubuntu" in the Start Menu) and running:
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

## **Step 1: Laying the Foundation with Ollama

- **What is Ollama?** Think of Ollama as the engine that powers your AI models. Installing Ollama within WSL on Windows provides a performance advantage.
    
- **Installation in WSL:** Open your Ubuntu terminal in WSL and use the following command to install Ollama:
    ```bash
    curl -fsSL https://ollama.com/install.sh | sh
    ```
    This command downloads and executes the official Ollama installation script directly in your WSL environment.
    
- **Verify Installation:** After the script completes, you can verify Ollama is installed by running:
    ```bash
    ollama --version
    ```
    This should display the installed Ollama version.
    
- **Pull the DeepSeek 1.5B Model:** Immediately after verifying Ollama, pull the `deepseek-1.5b` model. This model is a capable and efficient language model you can start experimenting with. Run this command in your Ubuntu terminal:
    ```bash
    ollama pull deepseek-r1:1.5b
    ```
    Ollama will download the `deepseek-r1:1.5b` model. The download time will depend on your internet connection.

## **Step 2: Creating a Web Interface with Open Web UI!
- **Why Open Web UI?** This provides a clean and intuitive web interface to interact with your AI models. It runs inside a Docker container.
    
- **Docker Desktop Installation (Windows):** You'll need to install Docker Desktop on your Windows host machine (not inside WSL directly). Download and install [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/). Ensure that WSL 2 based engine is enabled in Docker Desktop settings (Settings -> General -> Use the WSL 2 based engine).
    
- **Deploying Open Web UI in WSL:** Open your Ubuntu terminal in WSL and use the following Docker command to deploy Open Web UI:
    ```bash
    docker run -d -p 8080:8080 --name open-webui --volume open-webui:/app/data --network=host ghcr.io/open-webui/open-webui:main
    ```
    
    Let's break down this command:
    
    - `docker run -d`: Runs the Docker container in detached mode (in the background).
    - `-p 8080:8080`: Maps port 8080 on your host machine to port 8080 in the container, allowing you to access Open Web UI via `http://localhost:8080` in your Windows browser.
    - `--name open-webui`: Assigns the name "open-webui" to the container for easier management.
    - `--volume open-webui:/app/data`: Creates a Docker volume named "open-webui" and mounts it to `/app/data` inside the container. This persists your Open Web UI data even if the container is removed.
    - `--network=host`: This is important for WSL. Using `host` network mode allows the Docker container to directly use the host's network, which simplifies networking with Ollama running in WSL.
    - `ghcr.io/open-webui/open-webui:main`: Specifies the Docker image to use for Open Web UI.
- **Accessing the Web UI:** After Docker pulls the image and starts the container, navigate to `http://localhost:8080` in your web browser (on Windows). You'll be greeted with the Open Web UI interface.
    

## **Step 3: Integrating Image Generation with Stable Diffusion**

- **Stable Diffusion and Automatic 1111:** For AI image generation.
    
- **Prerequisites in WSL:** Open your Ubuntu terminal in WSL. We'll use `conda` for Python environment management within WSL.
    ```bash
    sudo apt install curl git wget
    sudo apt install python3 python3-venv
    ```

- **Install Automatic 1111 in WSL:**
    ```bash
    git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
    cd stable-diffusion-webui
    ./webui.sh
    ```
    - `git clone ...`: Clones the Automatic 1111 repository.
    - `cd stable-diffusion-webui`: Changes directory into the cloned repository.
    - `./webui.sh`: Executes the installation script. This will take a while as it downloads necessary components, including PyTorch and Stable Diffusion models, within your WSL environment.

- **Accessing Stable Diffusion:** Once the `webui.sh` script completes and starts, Stable Diffusion will be accessible through a web interface, on port 7860 (`http://localhost:7860`) in your Windows browser.
- **Connecting Stable Diffusion to Open Web UI:** In Open Web UI's settings (accessed via `http://localhost:8080`), find the "images" section. Add the base URL of your Automatic 1111 installation. If you are running both Open Web UI and Automatic 1111 on the same machine (even with WSL), this will likely be `http://localhost:7860`.

Alright! Follow these WSL steps, grab that `deepseek-1.5b` model, and just like that, you've got your own super-private AI server set up on your Windows machine, ready for the whole family to use! Just a heads-up – if things feel a little sluggish, you might need to adjust the settings in Docker Desktop and WSL to give everything enough resources, especially if you're running both Ollama and Stable Diffusion at the same time.
Have fun exploring and see what amazing things you and your family can create together!