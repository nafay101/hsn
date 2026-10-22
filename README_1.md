# 🧮 AI Math Solver

Upload a photo of any math question. The app reads it with **Google Gemini Flash**, solves it
step by step, and explains each step in simple words. Built with Python + Streamlit.

## Features
- Upload a photo/screenshot (PNG, JPG, WEBP) or take one with the camera
- Step-by-step solution, final answer and a simple explanation
- Choose the explanation style: Simple / Normal / Detailed
- Optional note, e.g. "solve only part b"
- Download the solution as a `.md` file

## Files
| File | Purpose |
|---|---|
| `app.py` | The whole app |
| `requirements.txt` | Python packages |
| `README.md` | This guide |

## 1. Get a free Gemini API key
1. Go to https://aistudio.google.com/apikey and sign in with Google.
2. Click **Create API key** and copy it. Never share it or put it in your code.

## 2. Run it on your computer
Install Python 3.10+ first, then in a terminal inside the project folder:

```bash
pip install -r requirements.txt
streamlit run app.py
```

The app opens at http://localhost:8501. Paste your API key in the sidebar.

Optional: so you don't paste it every time, create `.streamlit/secrets.toml`:

```toml
GEMINI_API_KEY = "paste-your-key-here"
```

## 3. Push to GitHub
Create a free account at https://github.com, then create a **new empty repository**
(for example `math-solver`; do not tick "Add README").

In the project folder (which must contain `app.py`, `requirements.txt`, `README.md`):

```bash
# keep your key out of GitHub
mkdir -p .streamlit
printf ".streamlit/secrets.toml\n__pycache__/\n.env\n" > .gitignore

git init
git add .
git commit -m "AI Math Solver"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/math-solver.git
git push -u origin main
```

On Windows PowerShell, create the `.gitignore` file with Notepad instead of `printf`, and put
these three lines in it: `.streamlit/secrets.toml`, `__pycache__/`, `.env`.

If Git asks for a password, use a **Personal Access Token** (GitHub > Settings > Developer
settings > Personal access tokens) instead of your account password.

## 4. Deploy on Streamlit Community Cloud (free)
1. Go to https://share.streamlit.io and sign in with GitHub.
2. Click **Create app** > **Deploy a public app from GitHub**.
3. Choose your repository, branch `main`, and main file path `app.py`.
4. Open **Advanced settings > Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "paste-your-key-here"
   ```
5. Click **Deploy**. After a minute or two you get a public link like
   `https://your-app-name.streamlit.app`.

To update the app later, change the code and run `git add . && git commit -m "update" && git push`.
Streamlit redeploys automatically.

## Changing the AI model
The model name is at the top of `app.py` (`DEFAULT_MODEL = "gemini-2.5-flash"`). You can also set a
`GEMINI_MODEL` secret to override it without editing code. If you see "model not found", Google
may have renamed it: check the model list at https://ai.google.dev/gemini-api/docs/models.

## Troubleshooting
| Problem | Fix |
|---|---|
| "API key looks invalid" | Create a new key and paste it again, with no spaces |
| "Too many requests" | The free limit is used up; wait a minute or try later |
| "Model not found" | Update the model name (see above) |
| Wrong answer or misread question | Upload a clearer, well-lit, straight photo; use the note box |

AI can make mistakes. Always double-check important answers.
