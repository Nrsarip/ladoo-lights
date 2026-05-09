# Photo Upload Setup Guide

This guide explains how to set up and use the photo upload feature for the Ladoo and Lights website.

## Overview

The upload page (`upload.html`) allows authorized users to:
1. Upload photos directly to the GitHub repository
2. Automatically add watermarks to images
3. Update the gallery.html page with new images

## Setup Instructions

### 1. Create a GitHub Personal Access Token

1. Go to [GitHub Settings > Developer settings > Personal access tokens > Tokens (classic)](https://github.com/settings/tokens)
2. Click "Generate new token (classic)"
3. Give it a descriptive name (e.g., "Ladoo Lights Photo Upload")
4. Select the following scopes:
   - ✅ `repo` (Full control of private repositories)
5. Click "Generate token"
6. **Copy the token immediately** - you won't be able to see it again!

### 2. Configure the Upload Page

1. Open `upload.html` in your browser
2. Enter your GitHub Personal Access Token
3. Enter your repository name in the format: `username/repository-name`
   - Example: `nityantasaripalli/ladoo-lights`
4. (Optional) Customize the watermark text (default: "Ladoo and Lights")

The configuration will be saved in your browser's localStorage for future use.

## How to Use

### Uploading Photos

1. **Open the upload page**: Navigate to `upload.html` in your browser
2. **Configure GitHub credentials** (if not already saved)
3. **Select a category**: Choose the appropriate category for your photos:
   - All Projects (default)
   - Weddings
   - Floral Mandaps
   - Haldi Ceremonies
   - Receptions
   - Sangeet
4. **Select or drag photos**: 
   - Click the upload area to browse for files, OR
   - Drag and drop photos onto the upload area
   - **Note**: All photos in one upload session will be tagged with the selected category
5. **Preview**: Review the watermarked previews of your images
6. **Upload**: Click "Upload to GitHub" button
7. **Wait for completion**: The page will show progress for each file

**Tip**: To upload photos to different categories, complete one upload, then change the category and upload again.

### What Happens During Upload

For each photo you upload:

1. **Original image** is uploaded to `assets/gallery/[filename].jpeg`
2. **Watermarked version** is uploaded to `images_watermarked/[filename].jpeg`
3. **gallery.html** is automatically updated to include the new image with the selected category tag

The watermarked version uses a semi-transparent white text overlay in the bottom-right corner.

### Category Filtering

Photos are automatically tagged with the category you select during upload. Visitors to the gallery can filter photos by category using the filter buttons at the top of the gallery page. This makes it easy to browse specific types of events.

## File Structure

After uploading, your repository will have:

```
ladoo-lights/
├── assets/
│   └── gallery/
│       └── [uploaded-images].jpeg
├── images_watermarked/
│   └── [watermarked-images].jpeg
└── gallery.html (automatically updated)
```

## Security Considerations

⚠️ **Important Security Notes:**

1. **Token Storage**: The GitHub token is stored in browser localStorage. This means:
   - It's only accessible on the same browser/device
   - It's not encrypted
   - Anyone with access to your browser can see it

2. **Token Permissions**: The token has `repo` access, which means it can:
   - Read and write to your repository
   - Modify files
   - Create commits

3. **Best Practices**:
   - Use a token with minimal required permissions
   - Don't share the upload page URL publicly
   - Consider using GitHub's fine-grained tokens (if available) with more restricted permissions
   - Rotate tokens periodically
   - Revoke tokens if compromised

4. **Alternative Approach**: For production use, consider:
   - Using a backend service to handle uploads
   - Using GitHub Actions for automated processing
   - Implementing user authentication

## Troubleshooting

### "Upload failed" errors

- **Check token permissions**: Ensure the token has `repo` scope
- **Verify repository name**: Format should be `username/repo-name`
- **Check file size**: Very large images may fail (GitHub has file size limits)
- **Network issues**: Check your internet connection

### Images not appearing in gallery

- **Check file paths**: Ensure `assets/gallery/` folder exists in your repo
- **Verify gallery.html**: Check that the AUTOGALLERY markers are present
- **Browser cache**: Clear cache and refresh the gallery page

### Watermark not showing

- The watermark is applied during upload
- Check the preview before uploading
- Watermark appears in bottom-right corner with semi-transparent white text

## Technical Details

### Image Processing

- Images are processed client-side using HTML5 Canvas API
- Watermark is applied as a text overlay
- Original quality is preserved (JPEG quality: 90%)
- Watermarked images are saved as JPEG format

### GitHub API Integration

- Uses GitHub REST API v3
- Creates/updates files via PUT requests
- Automatically handles file updates (uses SHA for existing files)
- Commits are created with descriptive messages

## Support

For issues or questions, contact: ladooandlights@gmail.com
