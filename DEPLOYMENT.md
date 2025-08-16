# CalcHub Pro - Deployment Guide

This guide provides step-by-step instructions for deploying CalcHub Pro to various hosting platforms.

## 🚀 Quick Deployment Options

### Option 1: Vercel (Recommended)
**Best for:** Production deployments with automatic CI/CD

1. **Connect Repository**
   ```bash
   # Push your code to GitHub
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/your-username/calchub-pro.git
   git push -u origin main
   ```

2. **Deploy to Vercel**
   - Visit [vercel.com](https://vercel.com)
   - Click "New Project" and import your GitHub repository
   - Configure environment variables (see below)
   - Click "Deploy"

3. **Environment Variables**
   ```env
   NEXT_PUBLIC_SITE_URL=https://your-domain.vercel.app
   NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
   NEXT_PUBLIC_PLAUSIBLE_DOMAIN=your-domain.com
   NEXT_PUBLIC_DISABLE_ADS=false
   NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION=your-verification-code
   ```

### Option 2: Netlify
**Best for:** Static hosting with form handling

1. **Build the Project**
   ```bash
   pnpm build
   pnpm export
   ```

2. **Deploy to Netlify**
   - Visit [netlify.com](https://netlify.com)
   - Drag and drop the `out` folder
   - Configure environment variables in site settings

### Option 3: Static Hosting
**Best for:** Any static hosting provider (GitHub Pages, Cloudflare Pages, etc.)

1. **Configure for Static Export**
   ```bash
   # Add to next.config.js
   /** @type {import('next').NextConfig} */
   const nextConfig = {
     output: 'export',
     trailingSlash: true,
     images: {
       unoptimized: true
     }
   }
   ```

2. **Build and Export**
   ```bash
   pnpm build
   ```

3. **Upload the `out` folder** to your hosting provider

## 🔧 Environment Configuration

### Required Variables
```env
# Site Configuration
NEXT_PUBLIC_SITE_URL=https://your-domain.com

# Analytics (Optional)
NEXT_PUBLIC_GA_ID=G-XXXXXXXXXX
NEXT_PUBLIC_PLAUSIBLE_DOMAIN=your-domain.com

# Features (Optional)
NEXT_PUBLIC_DISABLE_ADS=false
NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION=your-verification-code
```

### Variable Descriptions

**NEXT_PUBLIC_SITE_URL**
- Your website's base URL
- Used for SEO meta tags and canonical URLs
- Example: `https://calchub.pro`

**NEXT_PUBLIC_GA_ID**
- Google Analytics 4 tracking ID
- Format: `G-XXXXXXXXXX`
- Leave empty to disable Google Analytics

**NEXT_PUBLIC_PLAUSIBLE_DOMAIN**
- Domain for Plausible Analytics
- Example: `calchub.pro`
- Leave empty to disable Plausible Analytics

**NEXT_PUBLIC_DISABLE_ADS**
- Set to `true` to hide ad banners
- Set to `false` to show ad placeholders
- Default: `false`

**NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION**
- Google Search Console verification code
- Used for SEO and search engine indexing
- Optional but recommended for production

## 📋 Pre-Deployment Checklist

### ✅ Code Quality
- [ ] All tests pass: `pnpm test`
- [ ] Build succeeds: `pnpm build`
- [ ] No TypeScript errors
- [ ] ESLint warnings reviewed

### ✅ Configuration
- [ ] Environment variables configured
- [ ] Site URL updated in all configs
- [ ] Analytics tracking IDs added
- [ ] Google Search Console verification

### ✅ SEO & Analytics
- [ ] Meta tags customized for your brand
- [ ] Google Analytics configured
- [ ] Sitemap.xml accessible
- [ ] Robots.txt configured
- [ ] Schema.org markup verified

### ✅ Legal & Privacy
- [ ] Privacy Policy updated with your details
- [ ] Terms of Use customized
- [ ] Cookie consent banner configured
- [ ] GDPR compliance verified

### ✅ Performance
- [ ] Images optimized
- [ ] Lighthouse scores checked
- [ ] Core Web Vitals optimized
- [ ] Mobile responsiveness verified

## 🔍 Post-Deployment Verification

### 1. Functionality Testing
```bash
# Test key pages
https://your-domain.com/
https://your-domain.com/calculators/age
https://your-domain.com/calculators/bmi
https://your-domain.com/category/finance
https://your-domain.com/blog
```

### 2. SEO Verification
- [ ] Google Search Console setup
- [ ] Sitemap submitted to search engines
- [ ] Meta tags displaying correctly
- [ ] Structured data validated

### 3. Analytics Verification
- [ ] Google Analytics tracking events
- [ ] Plausible Analytics (if enabled)
- [ ] Cookie consent working
- [ ] Event tracking functional

### 4. Performance Testing
```bash
# Run Lighthouse audit
npx lighthouse https://your-domain.com --view

# Check Core Web Vitals
# Use Google PageSpeed Insights
```

## 🛠️ Custom Domain Setup

### Vercel Custom Domain
1. Go to Project Settings → Domains
2. Add your custom domain
3. Configure DNS records as instructed
4. Update `NEXT_PUBLIC_SITE_URL` environment variable

### Netlify Custom Domain
1. Go to Site Settings → Domain Management
2. Add custom domain
3. Configure DNS records
4. Enable HTTPS (automatic)

## 🔄 Continuous Deployment

### GitHub Actions (Optional)
Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Vercel
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '18'
      - run: npm install -g pnpm
      - run: pnpm install
      - run: pnpm build
      - run: pnpm test
```

## 📊 Monitoring & Maintenance

### Regular Tasks
- [ ] Monitor analytics for user behavior
- [ ] Update calculator functions as needed
- [ ] Review and respond to user feedback
- [ ] Update dependencies monthly
- [ ] Backup data and configurations

### Performance Monitoring
- [ ] Set up uptime monitoring
- [ ] Monitor Core Web Vitals
- [ ] Track conversion rates
- [ ] Analyze user engagement

## 🆘 Troubleshooting

### Common Issues

**Build Fails**
```bash
# Clear cache and rebuild
rm -rf .next node_modules
pnpm install
pnpm build
```

**Environment Variables Not Working**
- Ensure variables start with `NEXT_PUBLIC_`
- Restart development server after changes
- Check Vercel/Netlify dashboard for correct values

**Analytics Not Tracking**
- Verify tracking IDs are correct
- Check cookie consent is accepted
- Ensure ad blockers aren't interfering

**SEO Issues**
- Verify meta tags in page source
- Check sitemap.xml accessibility
- Ensure robots.txt allows crawling

## 📞 Support

### Resources
- [Next.js Deployment Docs](https://nextjs.org/docs/deployment)
- [Vercel Documentation](https://vercel.com/docs)
- [Netlify Documentation](https://docs.netlify.com)

### Getting Help
- Check the README.md for setup instructions
- Review GitHub Issues for common problems
- Contact support through project repository

---

**Deployment completed successfully!** 🎉

Your CalcHub Pro website is now live and ready to serve users worldwide with professional-grade online calculators.

*Last updated: January 15, 2024*

