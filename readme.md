# 🏎️ Code Club: AI License Plate Recognition Project

Welcome to the lab! Today, you are going to set up a professional-grade development environment. We are using **Windows** to write code, **Linux (WSL)** to run it, **Docker** to package the AI, and a **Host File Hack** to give our project a custom URL.

---

## 🏗️ Phase 1: The Toolbox (Pre-requisites)
Before we start, download and install these tools. If a tool asks you to restart your computer, **do it!**

| Tool | Link | Role |
| :--- | :--- | :--- |
| **WSL 2** | [Install Guide](https://learn.microsoft.com/en-us/windows/wsl/install) | The Linux "Brain" inside Windows. |
| **Docker Desktop** | [Download](https://www.docker.com/products/docker-desktop/) | The "Ship" that carries our AI engine. |
| **VS Code** | [Download](https://code.visualstudio.com/) | Our code editor. (Install the "WSL" extension!). |
| **Postman** | [Download](https://www.postman.com/downloads/) | The "Remote Control" to test our AI. |
| **Git** | [Download](https://git-scm.com/) | The tool used to "clone" code from GitHub. |

---

## 📂 Phase 2: Get the Code (GitHub & WSL)
We aren't just downloading a ZIP file; we are "cloning" it into our Linux environment so we can track changes like professional developers.

1. Open your **Ubuntu/WSL** terminal (Search for "Ubuntu" in your Start menu).
2. Run these commands:

```bash
# Create a workspace folder
mkdir -p ~/projects && cd ~/projects

# Clone the AI project from GitHub
git clone https://github.com/punkplod23/fast-alpr-api.git

# Enter the folder and open it in VS Code
cd fast-alpr-api
code .
```

### 🛠️ Phase 3: The "Host File Hack"
Let's make your computer feel like a real web server. Instead of typing localhost, we’ll create a custom domain: my-alpr.local.

1. Search for Notepad in your Start menu.
2. Right-click it and select Run as Administrator (this is important!).
3. Go to File > Open and paste this path: C:\Windows\System32\drivers\etc.
4. Change the file filter (bottom right) to All Files (.) and open the file named hosts.
5. Add this line at the very bottom: 127.0.0.1 my-alpr.local
6. Save and Close.

🐋 Phase 4: Docker & Host File Mapping
Now we tell Docker to run our AI. We will use a Volume to link your Windows folder (the "Host") to the Docker container.

In your WSL terminal, run these two commands:
```bash
# 1. Build the AI 'Image' (This downloads the AI models)
docker build -t alpr-engine .

# 2. Run the 'Container' with Host Mapping
docker run -d -p 8000:8000 -v $(pwd):/app alpr-engine
```
### 📮 Phase 5: Testing with Postman
1. Time to see if the AI can actually read!
2. Open Postman and click New > HTTP Request.
3. Set the method to POST.

below needs UPDATING
5. Use your "Hacker URL": http://my-alpr.local:8000/predict.
6. Go to the Body tab and select form-data.
7. Under Key, type file and change the dropdown to File.
8. Under Value, click "Select Files" and upload a picture of a car license plate.

Click Send!
### 🧠 Summary: How it all fits together
1. Host Files (Windows): You use VS Code to edit the files on your desktop.
2. WSL 2: Acts as the bridge, allowing Windows to talk to Linux.
3. Docker: Runs the "Engine" (Python + AI libraries) so you don't have to install them yourself.
4. Host File Hack: Tricks Windows into using a cool name (my-alpr.local) instead of an IP address.
