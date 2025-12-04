# Deploy Instructions for TikSpyder

## Deploying to Streamlit Community Cloud

### Prerequisites
1. A GitHub account
2. SerpAPI key (get it from https://serpapi.com/)
3. Apify API token (optional, get it from https://apify.com/)

### Step-by-Step Deployment

#### 1. Fork or Push to Your GitHub Repository

If you haven't already, push this repository to your GitHub account:

```bash
# Initialize git if not already done
git init
git add .
git commit -m "Prepare for Streamlit Cloud deployment"

# Add your GitHub repository as remote
git remote add origin https://github.com/YOUR_USERNAME/tik-spyder.git
git branch -M main
git push -u origin main
```

Or simply fork the original repository at: https://github.com/estebanpdl/tik-spyder

#### 2. Sign Up for Streamlit Community Cloud

1. Go to https://streamlit.io/cloud
2. Sign in with your GitHub account
3. Authorize Streamlit to access your repositories

#### 3. Deploy Your App

1. Click "New app" button
2. Select your repository: `YOUR_USERNAME/tik-spyder`
3. Set the main file path: `app.py`
4. Click "Deploy"

#### 4. Configure Secrets

After deployment, you need to configure your API keys:

1. Go to your app's dashboard on Streamlit Cloud
2. Click on "Settings" (⚙️ icon)
3. Go to "Secrets" section
4. Add the following secrets in TOML format:

```toml
[serpapi]
api_key = "your_actual_serp_api_key_here"

[apify]
token = "your_actual_apify_token_here"
```

5. Click "Save"

#### 5. Access Your Deployed App

Your app will be available at:
```
https://YOUR_USERNAME-tik-spyder-app-RANDOM.streamlit.app
```

### Important Notes

- **Free Tier Limitations**: Streamlit Community Cloud free tier has resource limitations
- **API Keys**: Never commit your actual API keys to the repository
- **Secrets Management**: Always use Streamlit's secrets management for sensitive data
- **Updates**: Any push to your main branch will automatically redeploy the app

### Modifying the App to Use Streamlit Secrets

The app needs to be modified to read API keys from Streamlit secrets instead of config.ini. 

In your Python code, replace config file reading with:

```python
import streamlit as st

# Read from Streamlit secrets
serp_api_key = st.secrets["serpapi"]["api_key"]
apify_token = st.secrets["apify"]["token"]
```

### Alternative Deployment Options

If Streamlit Cloud doesn't meet your needs, consider:

1. **Heroku** (with Streamlit buildpack)
2. **Railway.app** (supports Python apps)
3. **Render.com** (free tier available)
4. **Google Cloud Run** (pay-as-you-go)
5. **AWS EC2** (requires more setup)
6. **DigitalOcean App Platform** (simple deployment)

### Troubleshooting

- **App crashes**: Check the logs in Streamlit Cloud dashboard
- **Missing dependencies**: Ensure all packages are in requirements.txt
- **System dependencies**: Add them to packages.txt (e.g., ffmpeg)
- **Secrets not working**: Verify TOML format in secrets configuration

### Support

For issues related to:
- TikSpyder functionality: https://github.com/estebanpdl/tik-spyder/issues
- Streamlit Cloud: https://docs.streamlit.io/streamlit-community-cloud
