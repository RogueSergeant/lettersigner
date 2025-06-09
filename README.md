# Sign the Formal Complaint Website

A secure petition website where residents can sign a formal complaint digitally. The site allows admin to upload a PDF complaint, residents to sign it, and generates a final PDF with all signatures.

## Features

- Secure password protection using GitHub secrets
- PDF upload functionality for admin
- Digital signature canvas
- Real-time signature display
- Mobile-responsive design
- Download complaint with signatures as PDF
- Firebase integration for signature storage (with local storage fallback)

## Setup Instructions

### 1. Set up GitHub Secrets

1. Go to your GitHub repository
2. Navigate to Settings > Secrets and variables > Actions
3. Add the following secrets:
   - `SITE_PASSWORD`: Password for regular users to access the site
   - `ADMIN_PASSWORD`: Password for admin users to upload/download PDFs

### 2. Set up Firebase (optional but recommended)

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project
3. Enable Realtime Database
4. Set database rules to allow read/write (for testing):
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
5. Get your config from Project Settings > General > Web Apps
6. Replace the `firebaseConfig` object in `index.html`

### 3. Deploy to GitHub Pages

The GitHub Actions workflow (`.github/workflows/deploy.yml`) will automatically:
- Replace password placeholders with your GitHub secrets
- Deploy to GitHub Pages when you push to the main branch

To enable:
1. Go to repository Settings > Pages
2. Set source to "GitHub Actions"
3. Your site will be available at `https://yourusername.github.io/repositoryname`

### 4. Custom Domain (optional)

- Add your domain in GitHub Pages settings
- Configure your domain's DNS to point to GitHub Pages

## Usage

1. **Admin**: Visit the site, enter admin password, upload complaint PDF
2. **Residents**: Visit site, enter user password, view complaint, sign with name/flat/building
3. **Admin**: Download the final PDF with all signatures attached

## Technical Details

- **Frontend**: Pure HTML/CSS/JavaScript
- **PDF Handling**: PDF-lib.js for merging PDFs
- **Signatures**: HTML5 Canvas for drawing
- **Storage**: Firebase Realtime Database (with localStorage fallback)
- **Security**: Environment variables via GitHub Actions
- **Hosting**: GitHub Pages with automated deployment

## Security Features

- Passwords are stored as GitHub repository secrets
- No hardcoded passwords in the source code
- Secure build process replaces placeholders with actual values
- Client-side validation suitable for community use