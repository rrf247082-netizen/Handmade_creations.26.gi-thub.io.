# Contact API â€” Handmade Creations 26

This small Express app receives contact form submissions (JSON) and forwards them to an email address using SendGrid or SMTP.

Quick start (local):
1. Copy files into a folder.
2. Create a .env file from .env.example and fill values.
3. Install deps:
   npm install
4. Start server:
   npm run dev        # for development (nodemon)
   npm start          # for production

Endpoint:
- POST /contact
  - Accepts JSON: { name, email, message, website? }
  - 'website' is a honeypot; leave it empty in the real form.
  - Responds: { success: true } or error object.

Connect from your front-end:
- Update index.html form action to your server URL, e.g.:
  <form id="contactForm" action="https://yourdomain.com/contact" method="POST">

Security & production tips:
- Use SendGrid (SENDGRID_API_KEY) for reliable delivery and to avoid SMTP complexity.
- Use environment variables for API keys â€” do NOT commit .env to Git.
- If deploying on a public server, set ORIGIN to your site domain to restrict CORS.
- Add spam protections: reCAPTCHA v2/v3 or server-side rate limiting (already included).
- Ensure EMAIL_FROM is a verified sender if using SendGrid or the SMTP provider.
- Consider logging submissions to a database or service for audit/history (optional).
- When deploying to serverless platforms (Vercel/Netlify Functions), adapt to their handler format.

Test via curl:
curl -X POST https://yourdomain.com/contact \
  -H "Content-Type: application/json" \
  -d '{"name":"Alice","email":"alice@example.com","message":"Hi there"}'

Deployment suggestions:
- Render, Railway, Heroku, or Fly are straightforward for this small Express app.
- For serverless functions (Vercel/Netlify) copy handler logic into their function format (they use different packaging).
- For Docker: create a small Dockerfile using node:18-alpine, copy files, npm ci, EXPOSE 3000, CMD npm start.

If you'd like, I can:
- Provide a ready-to-deploy Dockerfile or Render/Heroku deployment steps.
- Adapt this to a Vercel/Netlify serverless function (if you prefer serverless).
- Add reCAPTCHA server verification and show front-end integration.
