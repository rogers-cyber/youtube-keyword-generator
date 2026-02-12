# YouTube Keyword Generator – Free SEO Tool

Generate high-impact YouTube keywords, tags, and video titles instantly. Designed for creators, this tool uses A–Z expansion, keyword scoring, and title suggestions to help you grow your channel faster.

---

## 🚀 Features

- **A–Z Keyword Expansion** – Automatically discover long-tail YouTube keywords.  
- **Keyword Scoring** – Instant difficulty & opportunity scoring (fake metric for UX).  
- **Title Generator** – Generate clickable YouTube titles in seconds.  
- **CSV Export** – Download your generated keywords for SEO planning.  
- **Email Capture** – Built-in form for lead generation and inquiries.  

---

## ⚡ How It Works

Because Google’s YouTube autocomplete endpoint blocks direct client requests (CORS), this tool uses a **Railway-hosted Python proxy** to fetch suggestions:

1. User enters keywords in the textarea.  
2. The frontend sends requests to the **Railway proxy**.  
3. Proxy fetches suggestions from Google and returns them.  
4. Results are displayed with keyword scores and suggested titles.  

This architecture allows the entire tool to run on **GitHub Pages** without CORS issues.

---

## 🔧 Deployment

### 1. Deploy the Railway Proxy

Create a Python app (`app.py`) for autocomplete:

```python
from flask import Flask, request, jsonify
import requests

app = Flask(__name__)

@app.route('/autocomplete')
def autocomplete():
    q = request.args.get('q')
    if not q:
        return jsonify([])
    url = "https://suggestqueries.google.com/complete/search"
    params = {"client": "firefox", "ds": "yt", "q": q}
    try:
        r = requests.get(url, params=params, timeout=5)
        return jsonify(r.json()[1])
    except:
        return jsonify([])

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

Create `requirements.txt`:

```
Flask==2.3.2
requests==2.31.0
```

Push to GitHub (optional) and deploy on [Railway](https://railway.app/). Copy your Railway URL, e.g., `https://your-railway-app.up.railway.app`.

---

### 2. Update `index.html`

Replace `RAILWAY_URL` in the script section:

```javascript
const RAILWAY_URL = "https://your-railway-app.up.railway.app";
```

Push `index.html` to your GitHub Pages repo.  

---

## 🖥 Usage

1. Open your GitHub Pages site in a browser.  
2. Enter one or multiple keywords in the textarea.  
3. Click **Generate Keywords**.  
4. View keywords, scores, and suggested titles.  
5. Optionally, download the results as CSV.  
6. Use the contact form to capture leads or inquiries.  

---

## 📈 Analytics & SEO

- Google Analytics (GA4) included for tracking; replace the GA ID with your own if needed.  
- Meta tags optimized for SEO, including description, keywords, and Open Graph.  

---

## 📧 Lead Generation

- Built-in contact form using [Formspree](https://formspree.io/).  
- Form submissions redirect to a custom **thank-you page**.  
- Fully customizable for email capture and Gumroad product promotion.  

---

## 📝 License

Open-source and free to use. Attribution appreciated:  
Mate Technologies – [https://matetools.gumroad.com](https://matetools.gumroad.com)

---

## ⚠️ Notes

- GitHub Pages can only serve **static sites**, so the Railway proxy is required for fetching live YouTube autocomplete keywords.  
- The keyword “score” is a **fake metric for UX purposes**, not actual YouTube ranking data.  

---

## 🔗 Links

- [Railway](https://railway.app/) – Free backend hosting  
- [Formspree](https://formspree.io/) – Email capture service  
- [Gumroad](https://matetools.gumroad.com/) – Promote your digital products  

---

**Ready to deploy:** Clone the repo, deploy the Railway proxy, update `RAILWAY_URL`, and push to GitHub Pages. Your full YouTube Keyword Generator will be live and CORS-free!
