## Local Development Setup with Custom Domain

### Prerequisites
1. A custom domain (in this case: generart.fit)
2. Cloudflare account for tunneling
3. Node.js and npm installed

### Setup Steps

1. **Configure Cloudflare Tunnel**
   - Set up a Cloudflare tunnel for your domain
   - Create a subdomain for the app (e.g., discount.generart.fit)
   - Configure the tunnel to point to your local development server (usually port 3000)
   - Start the tunnel from a terminal, you will get the details on the cloudflared when setting it up

2. **Update Shopify App Configuration**
   - In `shopify.app.toml`, set the following:
   ```toml
   application_url = "https://discount.generart.fit:3000"
   
   [auth]
   redirect_urls = [ "https://discount.generart.fit:3000/api/auth" ]

3. **Update Shopify Partner Dashboard**
   - Go to your app in the Shopify Partner Dashboard
   - Update the App URL to: `https://discount.generart.fit:3000`
   - Update the Allowed redirection URL(s) to: `https://discount.generart.fit:3000/api/auth`

4. **Start Development Server**
   ```bash
   npm run dev -- --tunnel-url https://discount.generart.fit:3000
   ```

### Troubleshooting
- If you see `ERR_BLOCKED_BY_CLIENT` errors in the console, these are related to ad blockers and can be safely ignored
- If the app shows a blank page, check:
  1. Cloudflare tunnel is running and accessible
  2. App URLs are correctly configured in  `shopify.app.toml`
  3. All redirect URLs match exactly

### Notes
- The `monorail-edge.shopifysvc.com` errors in console are from Shopify's analytics and don't affect app functionality
- Always ensure your tunnel is running before starting the development server
- Use `shopify app config reset` if you need to reset the configuration