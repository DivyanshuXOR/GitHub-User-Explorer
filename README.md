# 🚀 GitHub Profile Shop

A stunning, modern web application that showcases GitHub profiles in a beautiful dark-themed interface. Built with Webflow animations, server-side API handling, and amazing interactive features.

![GitHub Profile Shop](https://img.shields.io/badge/GitHub-Profile%20Shop-blue?style=for-the-badge&logo=github)
![Node.js](https://img.shields.io/badge/Node.js-v14+-green?style=for-the-badge&logo=node.js)
![License](https://img.shields.io/badge/License-ISC-purple?style=for-the-badge)

## ✨ Features

### Core Features
- 🔍 **Advanced Search**: Real-time search with debouncing - search any GitHub user by username
- 📊 **Sort & Filter**: Sort by followers, repos, or name; Filter by user type (Developers, Organizations)
- 🎯 **Detailed Profile View**: View comprehensive user profiles with repositories, followers, and statistics
- 💾 **Server Caching**: 10-minute cache for improved performance
- 🛡️ **Rate Limiting**: Built-in protection against API abuse

### UI/UX Features
- 🌙 **Dark Theme**: Beautiful dark interface with gradient accents
- 🎬 **Webflow Animations**: Smooth hero section with video background
- 📱 **Fully Responsive**: Works perfectly on desktop, tablet, and mobile
- ✨ **Modern Design**: Clean interface with Orbitron & IBM Plex Mono fonts

### Navigation
- **Explore**: Browse GitHub profiles in a stunning card grid
- **Following**: Track users you're interested in with a dropdown list
- **Hamburger Menu**: Full-screen menu with:
  - Quick search
  - Category filters with live counts
  - Navigation links
  - Quick actions (Random, Popular, Most Repos, A-Z)
  - Following list with statistics

### Profile Features
When you search for or click on a user:
- 📱 Complete user information (bio, location, company, email, Twitter)
- 📊 Statistics (repos, followers, following, stars, forks)
- 📚 Top repositories with language tags and star counts
- 👥 Followers list with avatars
- 📝 Gists and contributions
- 🔗 Direct links to GitHub profile

### Statistics Dashboard
- 100M+ Developers worldwide
- 400M+ Repositories
- 4M+ Organizations
- 1B+ Contributions

## 🏗️ Architecture

### Project Structure
```
├── server/
│   ├── config/
│   │   └── config.js          # Configuration management
│   ├── middleware/
│   │   └── rateLimiter.js     # Rate limiting middleware
│   ├── routes/
│   │   └── github.js          # GitHub API routes
│   ├── services/
│   │   └── githubService.js   # GitHub API service layer
│   └── server.js              # Main server file
├── public/
│   ├── pages/
│   │   └── index.html         # Main application page
│   └── assets/
│       ├── css/
│       │   └── styles.css     # Custom styles
│       └── js/
│           └── script.js      # Frontend logic
└── package.json
```

### API Endpoints

#### Users
- `GET /api/github/users?since=0&per_page=30` - Fetch list of users
- `GET /api/github/user/:username` - Get detailed user profile
- `GET /api/github/search?q=query&page=1` - Search users

#### Repositories & Social
- `GET /api/github/user/:username/repos` - Get user's repositories
- `GET /api/github/user/:username/followers` - Get user's followers
- `GET /api/github/user/:username/following` - Get users being followed
- `GET /api/github/user/:username/gists` - Get user's gists
- `GET /api/github/trending` - Get trending repositories

#### System
- `GET /api/health` - Health check
- `DELETE /api/github/cache` - Clear cache

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/DivyanshuXOR/GitHub-User-Explorer.git
cd GitHub-User-Explorer
```

2. **Install dependencies**
```bash
npm install
```

3. **Configure environment variables**
Create a `.env` file in the `server/` directory:
```env
PORT=3000
NODE_ENV=development

# Optional: Add GitHub token for higher rate limits (5000/hour vs 60/hour)
# Get your token from: https://github.com/settings/tokens
GITHUB_TOKEN=your_github_personal_access_token_here
```

4. **Start the development server**
```bash
npm run dev
```

5. **Open in browser**
Navigate to: `http://localhost:3000`

## 🎯 Usage

1. **Hero Section**: Enter a GitHub username in the search bar and click "Explore"
2. **Browse Profiles**: Scroll through the profile grid
3. **Search Users**: Use the search bar to find specific GitHub users
4. **Sort & Filter**: Use the dropdown or menu to sort/filter profiles
5. **View Details**: Click on any profile card to see full details
6. **Follow Users**: Click the + button to add users to your following list
7. **Menu**: Click the hamburger icon for full navigation and quick actions

## 🎮 Easter Eggs

- **Konami Code**: Press `↑↑↓↓←→←→BA` for a surprise!
- **Confetti**: Available through special interactions

## 🛡️ Security & Performance

### Security
- Rate Limiting: 100 requests per 15 minutes per IP
- Server-side API calls (no exposed tokens)
- Input validation and sanitization
- CORS enabled

### Performance
- 10-minute server-side caching
- Lazy loading images
- Debounced search (500ms)
- Parallel API requests
- Staggered animations

## 🎨 Design System

- **Colors**: GitHub-inspired dark theme with blue (#0969da), purple (#8250df), and pink (#bf3989) gradients
- **Fonts**: Orbitron (headings), IBM Plex Mono (code), Work Sans (body)
- **Animations**: Webflow-powered smooth transitions
- **Icons**: Font Awesome 6.5.1

## 📦 Dependencies

### Production
- `express` - Web server framework
- `axios` - HTTP client
- `express-rate-limit` - Rate limiting
- `node-cache` - In-memory caching
- `cors` - CORS middleware
- `dotenv` - Environment variables

### Development
- `nodemon` - Auto-reload

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 👤 Author

**Divyanshu**

- GitHub: [@DivyanshuXOR](https://github.com/DivyanshuXOR)

## 🙏 Acknowledgments

- GitHub for their amazing API
- Webflow for animation inspiration
- Font Awesome for icons
- Canvas Confetti for celebration effects

---

Made with ❤️ for the developer community
