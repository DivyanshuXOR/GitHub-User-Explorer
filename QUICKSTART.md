# 🚀 Quick Start Guide

Get GitHub Profile Shop running in 2 minutes!

## Prerequisites
- Node.js v14+ installed
- npm or yarn
- Internet connection

## Installation

### 1. Clone the Repository
```bash
git clone https://github.com/DivyanshuXOR/GitHub-User-Explorer.git
cd GitHub-User-Explorer
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Start the Server
```bash
npm run dev
```

### 4. Open Your Browser
Navigate to: **http://localhost:3000**

That's it! 🎉

---

## Optional: Add GitHub Token (Recommended)

For higher API rate limits (5000 requests/hour vs 60):

1. **Get a GitHub Token**
   - Visit: https://github.com/settings/tokens
   - Click "Generate new token (classic)"
   - Give it a name (no scopes needed for public data)
   - Copy the token

2. **Create/Edit .env file** in the `server/` folder:
   ```env
   PORT=3000
   NODE_ENV=development
   GITHUB_TOKEN=ghp_your_token_here
   ```

3. **Restart the server**
   ```bash
   # Press Ctrl+C to stop
   npm run dev
   ```

---

## First Steps

### 1. Search for Users
- Use the search bar in the hero section
- Type a GitHub username and press Enter or click "Explore"

### 2. Browse Profiles
- Scroll through the profile grid
- Click on any card to view full details

### 3. Follow Users
- Click the + button on profile cards
- View your following list via the "Following" dropdown

### 4. Use Quick Actions
- Click the hamburger menu (☰)
- Try Random, Popular, Most Repos, or A-Z sorting

### 5. Easter Egg
- Press: ↑↑↓↓←→←→BA for a surprise!

---

## Project Structure
```
├── server/
│   ├── config/         # Configuration
│   ├── middleware/     # Rate limiting
│   ├── routes/         # API routes
│   ├── services/       # GitHub service
│   └── server.js       # Main server
├── public/
│   ├── pages/
│   │   └── index.html  # Main page
│   └── assets/
│       ├── css/        # Styles
│       └── js/         # Frontend logic
└── package.json
```

---

## Available Commands

```bash
# Development (auto-reload)
npm run dev

# Production
npm start
```

---

## Quick API Test

```bash
# Health check
curl http://localhost:3000/api/health

# Get users
curl http://localhost:3000/api/github/users

# Search users
curl "http://localhost:3000/api/github/search?q=octocat"

# Get specific user
curl http://localhost:3000/api/github/user/octocat
```

---

## Features at a Glance

✅ Dark theme with Webflow animations  
✅ GitHub user search by username  
✅ Detailed profile view with repos & followers  
✅ Follow/unfollow system with dropdown  
✅ Full-screen navigation menu  
✅ Quick actions (Random, Popular, A-Z)  
✅ Category filters (All, Developers, Organizations)  
✅ Responsive design  
✅ Server-side caching  
✅ Rate limiting  
✅ Easter eggs!  

---

## Need Help?

- 📖 **Full documentation**: See [README.md](README.md)
- 🔧 **API details**: See [API_DOCUMENTATION.md](API_DOCUMENTATION.md)
- 🎨 **Feature guide**: See [FEATURES.md](FEATURES.md)
- 🐛 **Troubleshooting**: See [TROUBLESHOOTING.md](TROUBLESHOOTING.md)

---

## Tips

💡 **Tip 1**: Add a GitHub token for 5000 requests/hour  
💡 **Tip 2**: Use the menu for quick sorting options  
💡 **Tip 3**: Click "Following" to manage your list  
💡 **Tip 4**: Press ESC to close menus and modals  
💡 **Tip 5**: Try the Konami code for fun!  

---

**Enjoy exploring GitHub profiles!** 🎉
