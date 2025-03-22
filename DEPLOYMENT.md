# Deployment Guide for Commodity Trading Web Application

This document provides instructions for deploying the Commodity Trading Web Application to Cloudflare Pages with D1 database integration.

## Prerequisites

- Cloudflare account
- Node.js and npm installed
- Wrangler CLI (installed as a dev dependency)

## Local Development Setup

1. Clone the repository
2. Install dependencies:
   ```
   npm install
   ```
3. Start the development server:
   ```
   npm run dev
   ```
4. Access the application at http://localhost:3000

## Database Setup

1. Initialize the D1 database:
   ```
   npx wrangler d1 create commodity-trading-db
   ```

2. Update the `wrangler.toml` file with your database ID

3. Apply the database migrations:
   ```
   npx wrangler d1 migrations apply DB --local
   ```

## Deployment Steps

1. Build the application:
   ```
   npm run build
   ```

2. Deploy to Cloudflare Pages:
   ```
   npx wrangler pages deploy out
   ```

3. Bind the D1 database to your deployment:
   ```
   npx wrangler pages deployment update --branch main --d1 DB=commodity-trading-db
   ```

## Continuous Deployment

For continuous deployment, you can connect your GitHub repository to Cloudflare Pages:

1. Go to Cloudflare Dashboard > Pages
2. Click "Create a project"
3. Connect your GitHub repository
4. Configure build settings:
   - Build command: `npm run build`
   - Build output directory: `out`
5. Add environment variables if needed
6. Deploy

## Troubleshooting

- If you encounter database connection issues, verify your database bindings in the Cloudflare dashboard
- For deployment errors, check the build logs in the Cloudflare Pages dashboard
- For local development issues, ensure wrangler is properly configured with your account

## Maintenance

- To update the application, push changes to your repository or run the deployment command again
- To backup the database, use `wrangler d1 backup`
- To monitor performance, use Cloudflare Analytics
