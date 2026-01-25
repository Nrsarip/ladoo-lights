# Security Guide for Admin Page

## Current Security Implementation

The admin page (`admin.html`) now includes password protection to prevent unauthorized access.

### Password Protection

- **Default Password**: `admin123`
- **Storage**: Authentication is stored in `sessionStorage` (clears when browser closes)
- **Hashing**: Passwords are hashed using SHA-256 before comparison

### How to Change the Password

1. **Generate a new password hash**:
   - Go to: https://emn178.github.io/online-tools/sha256.html
   - Enter your desired password
   - Copy the SHA-256 hash

2. **Update the password hash in `admin.html`**:
   - Open `admin.html` in a text editor
   - Find the line: `const PASSWORD_HASH = '240be518fabd2724ddb6f04eeb1da5967448d7e831c08c8fa822809f74c720a9';`
   - Replace the hash with your new one
   - **Remove or change the default password hint** in the login form

3. **Save and test**:
   - Save the file
   - Test login with your new password

## Security Limitations

⚠️ **Important**: This is client-side password protection. It provides basic security but has limitations:

1. **Source Code Visibility**: 
   - The password hash is visible in the HTML source code
   - Anyone who views the page source can see the hash
   - However, they cannot easily reverse the hash to get the password

2. **GitHub Token Exposure**:
   - The GitHub token is still visible in the source code
   - Anyone with access to the file can see it

3. **No Server-Side Validation**:
   - Authentication only happens in the browser
   - A determined attacker could bypass it

## Better Security Options

### Option 1: Use Environment Variables (Recommended for Hosting Services)

If you're using a hosting service that supports environment variables (like Netlify, Vercel, etc.):

1. Store credentials in environment variables
2. Use a serverless function to handle authentication
3. Keep credentials out of the client-side code

### Option 2: Use GitHub OAuth

Instead of personal access tokens:

1. Implement GitHub OAuth flow
2. Users authenticate through GitHub
3. No tokens stored in code

### Option 3: Backend Authentication Service

For production use:

1. Create a simple backend API
2. Handle authentication server-side
3. Use secure session management
4. Store credentials in environment variables

### Option 4: Use a Password Manager with URL Restrictions

1. Use a service like Cloudflare Access or similar
2. Restrict access to the admin URL
3. Require authentication before the page loads

### Option 5: Host Admin Page Separately

1. Host the admin page on a different domain/subdomain
2. Use HTTP Basic Auth (if supported by hosting)
3. Or use a service like Netlify Identity

## Best Practices

1. **Change Default Password**: Immediately change from `admin123`
2. **Use Strong Passwords**: Use a long, random password
3. **Rotate GitHub Token**: Periodically create new tokens and revoke old ones
4. **Limit Token Permissions**: Use fine-grained tokens with minimal required permissions
5. **Monitor Access**: Check GitHub repository activity logs regularly
6. **Don't Share URLs**: Keep the admin page URL private
7. **Use HTTPS**: Always access the admin page over HTTPS
8. **Logout When Done**: Always click logout when finished

## Quick Security Checklist

- [ ] Changed default password
- [ ] Removed password hint from login form
- [ ] Using HTTPS for the website
- [ ] GitHub token has minimal required permissions
- [ ] Admin page URL is not publicly linked
- [ ] Regular token rotation scheduled
- [ ] Monitoring repository access logs

## Emergency: If Token is Compromised

1. **Immediately revoke the token**:
   - Go to: https://github.com/settings/tokens
   - Find the token and click "Revoke"

2. **Generate a new token**:
   - Create a new token with the same permissions
   - Update `admin.html` with the new token

3. **Review repository activity**:
   - Check for any unauthorized changes
   - Review commit history

4. **Change password**:
   - Update the admin password hash
   - Notify authorized users

## Support

For security concerns or questions, contact: ladooandlights@gmail.com
