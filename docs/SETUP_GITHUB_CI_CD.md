# GitHub CI/CD Setup Guide

This guide will help you set up the complete CI/CD pipeline with branch protection rules for your Expo React Native project.

## 🚀 Quick Setup

### 1. GitHub Repository Settings

#### Branch Protection Rules

**For MAIN branch:**

1. Go to your GitHub repository
2. Navigate to Settings → Branches
3. Click "Add rule" for the `main` branch
4. Configure the following settings:
   - ✅ **Require a pull request before merging**
   - ✅ **Require approvals**: 1 (swapnilgupta14)
   - ✅ **Dismiss stale PR approvals when new commits are pushed**
   - ✅ **Require status checks to pass before merging**
   - ✅ **Require branches to be up to date before merging**
   - ✅ **Require linear history**
   - ✅ **Restrict pushes that create files that are larger than 100 MB**
   - ❌ **Allow force pushes**: Disabled
   - ❌ **Allow deletions**: Disabled
   - **Required status checks**: `CI` (from the CI workflow)

**For DEVELOP branch:**

1. Click "Add rule" for the `develop` branch
2. Configure the same settings as main branch

### 2. Required GitHub Secrets

Add these secrets in your GitHub repository (Settings → Secrets and variables → Actions):

#### For Expo Builds:

- `EXPO_TOKEN`: Your Expo access token
  - Get it from: https://expo.dev/accounts/[username]/settings/access-tokens

#### For Vercel Deployment:

- `VERCEL_TOKEN`: Your Vercel access token
  - Get it from: https://vercel.com/account/tokens
- `VERCEL_PROJECT_ID`: Your Vercel project ID
  - Get it from your Vercel project settings
- `VERCEL_ORG_ID`: Your Vercel organization ID
  - Get it from your Vercel account settings

### 3. Vercel Setup

1. **Connect your repository to Vercel:**

   - Go to https://vercel.com
   - Import your GitHub repository
   - Configure the build settings:
     - Framework Preset: Expo
     - Build Command: `bun run expo export --platform web`
     - Output Directory: `dist`
     - Install Command: `bun install`

2. **Get Vercel credentials:**
   - Project ID: Found in your Vercel project settings
   - Organization ID: Found in your Vercel account settings
   - Access Token: Create at https://vercel.com/account/tokens

### 4. Expo Setup

1. **Create Expo account** (if not already done):

   - Go to https://expo.dev
   - Sign up and create an account

2. **Get Expo access token:**

   - Go to https://expo.dev/accounts/[username]/settings/access-tokens
   - Create a new access token

3. **Configure app.json for builds:**
   ```json
   {
     "expo": {
       "build": {
         "development": {
           "developmentClient": true,
           "distribution": "internal"
         },
         "preview": {
           "distribution": "internal"
         },
         "production": {}
       }
     }
   }
   ```

## 🔄 Workflow

### Development Workflow:

1. **Create feature branch** from `develop`

   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/your-feature-name
   ```

2. **Make changes and commit**

   ```bash
   git add .
   git commit -m "feat: your feature description"
   git push origin feature/your-feature-name
   ```

3. **Create Pull Request** to `develop`

   - Go to GitHub and create PR from your feature branch to `develop`
   - Fill out the PR template
   - CI checks will run automatically

4. **Review and Merge**
   - `swapnilgupta14` must approve the PR
   - All CI checks must pass
   - PR gets merged to `develop`

### Release Workflow:

1. **Create release PR** from `develop` to `main`

   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b release/v1.0.0
   # Update version in package.json
   git add package.json
   git commit -m "chore: bump version to 1.0.0"
   git push origin release/v1.0.0
   ```

2. **Create Pull Request** to `main`

   - PR from `develop` to `main`
   - `swapnilgupta14` must approve
   - All checks must pass

3. **Merge to main triggers release**
   - Android APK build and release
   - iOS build and release
   - Web deployment to Vercel
   - GitHub release created automatically

## 📋 Checklist

### GitHub Setup:

- [ ] Branch protection rules configured for `main`
- [ ] Branch protection rules configured for `develop`
- [ ] Required reviewers set to `swapnilgupta14`
- [ ] Status checks required: `CI`
- [ ] Linear history enabled

### Secrets Configuration:

- [ ] `EXPO_TOKEN` added
- [ ] `VERCEL_TOKEN` added
- [ ] `VERCEL_PROJECT_ID` added
- [ ] `VERCEL_ORG_ID` added

### Vercel Setup:

- [ ] Repository connected to Vercel
- [ ] Build settings configured
- [ ] Domain configured (optional)

### Expo Setup:

- [ ] Expo account created
- [ ] Access token generated
- [ ] App configuration updated

## 🛠️ Troubleshooting

### Common Issues:

1. **CI checks failing:**

   - Check that all linting passes: `bun run lint`
   - Check that formatting is correct: `bun run format:check`
   - Check that tests pass: `bun run test`

2. **Build failures:**

   - Verify Expo token is correct
   - Check that app.json is properly configured
   - Ensure all dependencies are installed

3. **Vercel deployment issues:**
   - Verify Vercel tokens are correct
   - Check that vercel.json is properly configured
   - Ensure build command works locally

### Local Testing:

```bash
# Test CI checks locally
bun run lint
bun run format:check
bun run test

# Test build locally
bun run expo export --platform web
```

## 📞 Support

If you encounter any issues:

1. Check the GitHub Actions logs for detailed error messages
2. Verify all secrets are correctly configured
3. Test the build process locally first
4. Contact the development team for assistance
