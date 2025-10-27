# Digital Ocean Deployment Guide

## Prerequisites

1. **Digital Ocean Account**: Sign up at [digitalocean.com](https://digitalocean.com)
2. **GitHub Repository**: Push your code to GitHub
3. **Database**: Set up a PostgreSQL database (can be done through Digital Ocean)

## Deployment Steps

### 1. Create Digital Ocean App

1. Go to [Digital Ocean App Platform](https://cloud.digitalocean.com/apps)
2. Click "Create App"
3. Choose "GitHub" as source
4. Connect your GitHub account and select the `IntegratedLensSystem` repository
5. Select the `main` branch

### 2. Configure App Settings

1. **App Name**: Integrated Lens System
2. **Source Directory**: `/` (root)
3. **Build Command**: `npm run build`
4. **Run Command**: `npm start`
5. **Environment**: Node.js

### 3. Set Environment Variables

In the Digital Ocean dashboard, add these environment variables:

```
NODE_ENV=production
PORT=5000
DATABASE_URL=postgresql://username:password@host:port/database
ADMIN_SETUP_KEY=your-secure-admin-setup-key
RESEND_API_KEY=your-resend-api-key
```

### 4. Database Setup

1. In Digital Ocean, go to "Databases"
2. Create a new PostgreSQL database
3. Copy the connection string and use it as `DATABASE_URL`
4. Run database migrations:
   ```bash
   npm run db:push
   ```

### 5. Domain Configuration

1. In your app settings, go to "Settings" > "Domains"
2. Add your custom domain or use the provided Digital Ocean domain
3. Configure SSL certificate (automatic with Digital Ocean)

## Environment Variables Reference

| Variable | Description | Required |
|----------|-------------|----------|
| `DATABASE_URL` | PostgreSQL connection string | Yes |
| `ADMIN_SETUP_KEY` | Secret key for admin account creation | Yes |
| `RESEND_API_KEY` | API key for email service | Yes |
| `NODE_ENV` | Environment (production/development) | Yes |
| `PORT` | Server port (default: 5000) | No |

## Post-Deployment

1. **Test the application**: Visit your deployed URL
2. **Create admin account**: Use the admin setup key to create the first admin user
3. **Configure email**: Set up Resend API key for email notifications
4. **Database migration**: Ensure all tables are created properly

## Monitoring

- Use Digital Ocean's built-in monitoring
- Check application logs in the Digital Ocean dashboard
- Monitor database performance and usage

## Scaling

- Increase instance size in Digital Ocean dashboard
- Add load balancers if needed
- Monitor resource usage and scale accordingly

## Troubleshooting

### Common Issues

1. **Build Failures**: Check build logs in Digital Ocean dashboard
2. **Database Connection**: Verify DATABASE_URL is correct
3. **Environment Variables**: Ensure all required variables are set
4. **Port Issues**: Make sure PORT is set to 5000

### Logs

Access logs through:
- Digital Ocean App Platform dashboard
- Command line: `doctl apps logs <app-id>`

## Security Considerations

1. **Environment Variables**: Keep sensitive data in Digital Ocean's secure environment variables
2. **Database**: Use Digital Ocean's managed database service
3. **SSL**: Enable SSL certificates for HTTPS
4. **Admin Key**: Use a strong, unique admin setup key
