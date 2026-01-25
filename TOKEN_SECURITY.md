# ⚠️ CRITICAL: Token Security

## Why GitHub Keeps Removing Your Token

GitHub automatically scans repositories for exposed tokens and secrets. If a token is found in your code, GitHub will:
1. **Immediately revoke the token**
2. Send you a security alert
3. Require you to generate a new token

## Current Security Implementation

The admin page (`admin.html`) now uses a **secure approach**:

✅ **Tokens are NOT hardcoded** - No tokens in source code  
✅ **Client-side storage only** - Tokens stored in browser localStorage  
✅ **Never committed** - Tokens never go to GitHub  
✅ **User-entered** - You enter the token when needed  

## How to Use Securely

### First Time Setup

1. **Open `admin.html`** in your browser
2. **Enter your GitHub token** in the configuration section:
   - Token: `ghp_xxxxxxxxxxxx`
   - Repository: `nrsarip/ladoo-lights`
3. **The token will be saved** in your browser's localStorage
4. **It will auto-fill** next time you visit (only on your device)

### Important Notes

- ✅ Token is stored **only in your browser** (localStorage)
- ✅ Token is **never sent to GitHub** as part of the code
- ✅ Token is **not visible** in the HTML source code
- ✅ Each user enters their own token

## If Token Gets Revoked

If GitHub revokes your token:

1. **Generate a new token**:
   - Go to: https://github.com/settings/tokens
   - Click "Generate new token (classic)"
   - Name: "Ladoo Lights Gallery Admin"
   - Scopes: ✅ `repo` (Full control of private repositories)
   - Click "Generate token"
   - **Copy it immediately**

2. **Update in admin page**:
   - Open `admin.html`
   - Enter the new token
   - It will be saved automatically

## Best Practices

1. **Never hardcode tokens** in any file
2. **Never commit tokens** to Git
3. **Use fine-grained tokens** if available (more secure)
4. **Rotate tokens regularly** (every 90 days)
5. **Revoke old tokens** when creating new ones
6. **Limit token scope** to minimum required permissions

## For Production Use

For a production website, consider:

1. **Backend API** - Handle authentication server-side
2. **Environment Variables** - Use hosting service env vars
3. **GitHub OAuth** - Let users authenticate through GitHub
4. **Serverless Functions** - Use Netlify/Vercel functions
5. **Password Protection** - Add additional layer of security

## Current Token

Your current token: `ghp_xxxxxxxxxxxx`

⚠️ **Keep this private!** Only enter it in the admin page, never commit it to Git.

## Emergency: Token Compromised

If you suspect your token is compromised:

1. **Immediately revoke it**:
   - https://github.com/settings/tokens
   - Find the token and click "Revoke"

2. **Generate a new token** with the same permissions

3. **Update the admin page** with the new token

4. **Review repository activity** for any unauthorized changes
