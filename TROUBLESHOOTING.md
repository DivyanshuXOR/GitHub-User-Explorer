# GitHub Profile Shop - Troubleshooting Guide

## Common Issues & Solutions

---

## 🚀 Server Issues

### Server Won't Start

**Symptoms:**
- `npm start` fails
- Port already in use error
- Module not found errors

**Solutions:**

1. **Port in use:**
   ```powershell
   # Windows - Find and kill process on port 3000
   netstat -ano | findstr :3000
   taskkill /PID <PID> /F
   ```

2. **Missing dependencies:**
   ```powershell
   cd server
   npm install
   ```

3. **Wrong directory:**
   ```powershell
   # Make sure you're in the server folder
   cd server
   npm start
   ```

---

### Rate Limit Exceeded

**Symptoms:**
- 429 Too Many Requests error
- "Rate limit exceeded" message
- API stops responding

**Solutions:**

1. **Wait for reset** - Rate limit resets every 15 minutes

2. **Add GitHub token** to increase limits:
   ```powershell
   # In server/.env
   GITHUB_TOKEN=ghp_your_token_here
   ```

3. **Check current limits:**
   ```javascript
   // Server shows rate limit in response headers
   X-RateLimit-Remaining: 95
   ```

---

### Cache Issues

**Symptoms:**
- Stale data showing
- Changes not reflecting
- Inconsistent results

**Solutions:**

1. **Clear server cache:**
   ```bash
   curl -X DELETE "http://localhost:3000/api/github/cache"
   ```

2. **Clear browser cache:**
   - Press `Ctrl + Shift + R` for hard refresh
   - Open DevTools > Application > Clear storage

3. **Restart server:**
   ```powershell
   # Press Ctrl+C to stop, then:
   npm start
   ```

---

## 🎨 UI Issues

### Dark Theme Not Working

**Symptoms:**
- White/light backgrounds showing
- Text hard to read
- Colors look washed out

**Solutions:**

1. **Hard refresh the page:**
   ```
   Ctrl + Shift + R
   ```

2. **Clear browser cache:**
   - DevTools > Application > Clear site data

3. **Check CSS loading:**
   - Open DevTools > Network
   - Verify `styles.css` loads without errors

---

### Following Dropdown Empty

**Symptoms:**
- Dropdown shows but no users
- "No users followed yet" always shown
- Follow button not working

**Solutions:**

1. **Check localStorage:**
   ```javascript
   // In browser console
   localStorage.getItem('followedUsers')
   ```

2. **Clear and refresh:**
   ```javascript
   // Reset followed users
   localStorage.setItem('followedUsers', '[]')
   location.reload()
   ```

3. **Ensure user exists** before following:
   - Search for the user first
   - Click the user card
   - Use the Follow button in modal

---

### Hamburger Menu Not Opening

**Symptoms:**
- Hamburger icon doesn't respond
- Menu opens but closes immediately
- Menu animations broken

**Solutions:**

1. **Check JavaScript console:**
   - Press F12 > Console tab
   - Look for red error messages

2. **Verify script loading:**
   - DevTools > Network
   - Check if `script.js` loads successfully

3. **Disable browser extensions:**
   - Some ad blockers interfere with menus

---

### Search Not Working

**Symptoms:**
- Search returns no results
- Loading spinner never stops
- Error on search

**Solutions:**

1. **Check server is running:**
   ```powershell
   curl http://localhost:3000/api/health
   ```

2. **Verify search endpoint:**
   ```powershell
   curl "http://localhost:3000/api/github/search?q=test"
   ```

3. **Check browser console** for JavaScript errors

---

## 🔌 API Issues

### GitHub API 403 Forbidden

**Symptoms:**
- API returns 403 error
- "API rate limit exceeded" message
- Requests blocked

**Solutions:**

1. **Add GitHub personal access token:**
   ```powershell
   # Create .env file in server folder
   echo "GITHUB_TOKEN=ghp_your_token" > server/.env
   ```

2. **Get a token:**
   - Go to https://github.com/settings/tokens
   - Generate new token (classic)
   - Select scopes: `public_repo`, `read:user`

3. **Restart server** after adding token

---

### CORS Errors

**Symptoms:**
- "Access-Control-Allow-Origin" errors
- Requests blocked in browser
- Works in Postman but not browser

**Solutions:**

1. **Check server CORS config:**
   - Server should have `cors` middleware enabled
   - Verify in `server/server.js`

2. **Use correct origin:**
   - Access via `http://localhost:3000`
   - Not via `file://` protocol

3. **Check browser extensions** that might block CORS

---

### 404 User Not Found

**Symptoms:**
- User profile returns 404
- "User not found" error
- Profile won't load

**Solutions:**

1. **Verify username exists:**
   - Go to `https://github.com/<username>`
   - Check spelling

2. **Check API response:**
   ```powershell
   curl "http://localhost:3000/api/github/user/<username>"
   ```

3. **Clear cache and retry:**
   ```powershell
   curl -X DELETE "http://localhost:3000/api/github/cache"
   ```

---

## 💻 Installation Issues

### npm install Fails

**Symptoms:**
- Package installation errors
- Permission denied
- Network errors

**Solutions:**

1. **Update npm:**
   ```powershell
   npm install -g npm@latest
   ```

2. **Clear npm cache:**
   ```powershell
   npm cache clean --force
   ```

3. **Delete node_modules and retry:**
   ```powershell
   Remove-Item -Recurse -Force node_modules
   npm install
   ```

---

### Node.js Version Issues

**Symptoms:**
- Syntax errors on server start
- Module compatibility issues
- "Unexpected token" errors

**Solutions:**

1. **Check Node version:**
   ```powershell
   node --version
   # Should be v14 or higher
   ```

2. **Install latest LTS:**
   - Download from https://nodejs.org
   - Or use nvm for Windows

---

## 🎯 Quick Debug Checklist

When something goes wrong, check these in order:

1. ✅ **Server running?**
   ```powershell
   curl http://localhost:3000/api/health
   ```

2. ✅ **Console errors?**
   - Press F12 > Console tab

3. ✅ **Network requests?**
   - F12 > Network tab > Look for red failures

4. ✅ **Cache cleared?**
   - Server: DELETE /api/github/cache
   - Browser: Ctrl + Shift + R

5. ✅ **Rate limited?**
   - Check response for 429 status
   - Add GitHub token if needed

---

## 📞 Getting Help

If issues persist:

1. **Check GitHub Issues:**
   https://github.com/DivyanshuXOR/GitHub-User-Explorer/issues

2. **Create new issue** with:
   - Browser name and version
   - Node.js version (`node --version`)
   - Error messages from console
   - Steps to reproduce

3. **Include screenshots** of errors when possible

---

## 🔄 Reset Everything

Nuclear option if nothing else works:

```powershell
# Stop server (Ctrl+C if running)

# Delete node_modules
Remove-Item -Recurse -Force server/node_modules

# Clear npm cache
npm cache clean --force

# Reinstall
cd server
npm install

# Clear any .env issues
# Make sure .env is correct (or delete it for defaults)

# Start fresh
npm start

# In browser - clear all data
# DevTools > Application > Clear site data
```
