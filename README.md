# GitHub Pages Deployment Guide

This guide will help you deploy the PDF to Excel AI Converter to GitHub Pages for a fully client-side, serverless experience.

## 🚀 Quick Deployment

### Step 1: Fork or Clone the Repository

1. **Fork this repository** to your GitHub account, or
2. **Clone and push** to your own repository:
   ```bash
   git clone https://github.com/your-username/PDF-To-Excel-AI-Converter.git
   cd PDF-to-Excel-ai-converter
   git remote set-url origin https://github.com/your-username/your-repo-name.git
   git push -u origin main
   ```

### Step 2: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click on **Settings** tab
3. Scroll down to **Pages** section
4. Under **Source**, select **GitHub Actions**
5. The deployment workflow will automatically trigger

### Step 3: Access Your Application

After deployment completes (usually 2-5 minutes):
- Your app will be available at: `https://your-username.github.io/your-repo-name/`
- The deployment status can be seen in the **Actions** tab

## 📁 File Structure

```
docs/                    # GitHub Pages source directory
├── index.html          # Main application file (complete standalone app)
├── README.md          # Documentation for the GitHub Pages version
└── .nojekyll          # Disables Jekyll processing

.github/
└── workflows/
    └── deploy-pages.yml # GitHub Actions workflow for automatic deployment
```

## 🛠️ How It Works

### Client-Side Architecture

The GitHub Pages version is completely different from the server-based version:

1. **PDF Processing**: Uses PDF.js to convert PDF pages to images in the browser
2. **AI Processing**: Makes direct calls to Google Gemini AI API from the browser
3. **Excel Generation**: Uses SheetJS to create Excel files client-side
4. **File Handling**: Uses modern File System Access API or fallback download methods

### Key Differences from Server Version

| Feature | Server Version | GitHub Pages Version |
|---------|----------------|---------------------|
| **Architecture** | Flask backend + frontend | Single HTML file |
| **PDF Processing** | Python pdf2image | Browser PDF.js |
| **AI API** | Server-side calls | Direct browser calls |
| **Excel Generation** | Python pandas | Browser SheetJS |
| **File Storage** | Server filesystem | Browser downloads |
| **Privacy** | Files stored on server | No server storage |
| **Deployment** | Requires hosting | Free GitHub Pages |

## 🔧 Customization

### Updating the Application

The main application is in `docs/index.html`. This is a complete, standalone HTML file that includes:
- All CSS styles
- All JavaScript code
- External library imports (PDF.js, SheetJS)

To customize:
1. Edit `docs/index.html`
2. Commit and push changes
3. GitHub Actions will automatically redeploy

### Changing Repository Links

Update the following in `docs/index.html`:
- Line ~652: Update the GitHub repository link in the footer
- `docs/README.md`: Update all repository URLs

### Adding Custom Domain

1. In your repository, go to **Settings** → **Pages**
2. Under **Custom domain**, enter your domain
3. Create a `CNAME` file in the `docs/` directory with your domain name

## 🔑 API Key Management

The GitHub Pages version requires users to provide their own Google Gemini API key:

### For Users:
1. Get a free API key from [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Enter it in the application interface
3. The key is stored locally in browser localStorage

### For Developers:
- API keys are never sent to GitHub or stored in the repository
- Each user manages their own API key
- No server-side API key management needed

## 🚨 Important Security Notes

### API Key Exposure
- ⚠️ **NEVER** hardcode API keys in the HTML file
- ✅ Always require users to enter their own API keys
- ✅ Store API keys only in browser localStorage

### CORS Considerations
- Google Gemini AI API supports CORS for browser requests
- No proxy server needed for API calls
- Direct browser-to-API communication

## 📊 Performance Considerations

### Browser Requirements
- **Minimum RAM**: 4GB recommended for large PDFs
- **Modern Browser**: ES6+ support required
- **File Size Limits**: 50MB PDF limit (browser memory constraints)

### Optimization Tips
1. **PDF Quality**: Balance between quality and processing speed
2. **Batch Processing**: Pages processed sequentially to manage memory
3. **Progress Indicators**: Real-time feedback for user experience

## 🔍 Troubleshooting

### Deployment Issues

**Workflow fails**:
```bash
# Check if docs/ directory exists and contains index.html
ls -la docs/

# Verify workflow file is correct
cat .github/workflows/deploy-pages.yml
```

**Pages not updating**:
1. Check the Actions tab for deployment status
2. Verify GitHub Pages is enabled in repository settings
3. Clear browser cache and try again

### Runtime Issues

**API calls fail**:
- Verify API key is valid and has Gemini AI access
- Check browser console for CORS or network errors
- Ensure stable internet connection

**PDF processing fails**:
- Check PDF file size (< 50MB)
- Verify PDF is not password protected
- Try a different PDF file to isolate the issue

## 🔄 Updates and Maintenance

### Automatic Updates
- GitHub Actions automatically deploys on every push to main branch
- No manual deployment steps required
- Deployment typically takes 2-5 minutes

### Manual Deployment
If needed, you can manually trigger deployment:
1. Go to **Actions** tab in your repository
2. Select **Deploy to GitHub Pages** workflow
3. Click **Run workflow**

### Library Updates
The application uses CDN links for external libraries:
- PDF.js: `https://cdnjs.cloudflare.com/ajax/libs/pdf.js/4.0.379/`
- SheetJS: `https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/`

To update versions, modify the CDN URLs in `docs/index.html`.

## 🆘 Support

### Getting Help
1. **Check the browser console** for error messages
2. **Review the documentation** in `docs/README.md`
3. **Test with a simple PDF** to isolate issues
4. **Check GitHub Actions logs** for deployment issues

### Reporting Issues
When reporting issues, please include:
- Browser and version
- PDF file characteristics (size, type, source)
- Console error messages
- Steps to reproduce

---

**Ready to deploy?** Follow the Quick Deployment steps above to get your PDF to Excel converter running on GitHub Pages! 🚀
