# kriss.cc

Personal website hosted on AWS S3 and served via CloudFront.

## Structure

- **index.html**: Main landing page
- **404.html**: Custom error page
- **gauntlet/**: Directory for project demos
  - **index.html**: Overview of all Gauntlet AI projects
  - **ChatGenius/**: Modern, AI-enhanced chat messaging platform for teams - [Live Demo](https://chatgenius.kriss.cc/)
  - **AutoCRM/**: AI-powered Customer Relationship Management platform - [Live Demo](https://autocrm.kriss.cc/)
  - **ReelAI/**: Native iOS app for creating AI-generated viral videos
  - **MCPMonkey/**: Browser extension that bridges AI language models and browser interactions - [Website](https://mcpmonkey.com)
  - **sana-mobile/**: React Native healthcare app with HIPAA-compliant security
  - **DreamUp/**: Gaming platform - [Live Site](https://dreamup.gg)
- **s3-website-config.json**: Configuration for S3 redirects

## Projects

### ChatGenius (Weeks 1-2)
Modern, AI-enhanced chat messaging platform built for teams. Combines familiar features of popular platforms with advanced AI capabilities for enhanced communication. Built with React, TypeScript, Tailwind CSS, and Supabase for real-time functionality.

### AutoCRM (Weeks 3-4)
AI-powered Customer Relationship Management platform that minimizes human workload in customer support while enhancing customer experience. Features include AI-powered ticket resolution, real-time management, and automated routing built with React, TypeScript, and Supabase.

### ReelAI (Weeks 5-6)
Native iOS application built with Swift that transforms ideas into engaging, AI-generated videos designed for viral meme culture. Integrates with Firebase for authentication, storage, and performance monitoring.

### MCPMonkey (Week 7)
A browser extension that extends userscript capabilities to support Model Context Protocol servers, bridging the gap between AI language models and browser interactions for more effective AI assistance.

### sana-mobile (Week 8)
React Native mobile application for Android and iOS providing access to healthcare providers and insurance information. Features secure authentication with PIN and biometric options, chat functionality, and HIPAA-compliant security.

### DreamUp (Week 9)
An innovative gaming platform that aims to transform the gaming experience by leveraging modern web technologies and AI integration.

## Adding New Project Pages

### Option 1: Static HTML with embedded video

1. Create a new HTML file in the appropriate directory (e.g., `gauntlet/project-name/index.html`)
2. Use the template from existing pages to maintain consistent styling
3. Replace `VIDEO_ID` in the YouTube embed URL with your actual YouTube video ID
4. Update content and descriptions

### Option 2: Direct redirect to YouTube

1. Edit `s3-website-config.json` to add a new routing rule:
```json
{
    "Condition": {
        "KeyPrefixEquals": "redirect/your-project-name"
    },
    "Redirect": {
        "Protocol": "https",
        "HostName": "www.youtube.com",
        "ReplaceKeyWith": "watch?v=YOUR_VIDEO_ID",
        "HttpRedirectCode": "302"
    }
}
```

## Deployment

To deploy changes to AWS:

```
aws s3 sync . s3://krissdotcc --profile personal-kriss --exclude ".git/*"
aws s3 website s3://krissdotcc --profile personal-kriss --website-configuration file://s3-website-config.json
```

This uploads all files to S3 and configures the website redirects.