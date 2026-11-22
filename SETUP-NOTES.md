# wacrm — deployment notes (Vikas)

Open-source WhatsApp CRM (ArnasDon/wacrm), deployed free on Vercel + Supabase.

## Live
- App (production): https://wacrm-five-pied.vercel.app
- Vercel project: wacrm (team vikas162202-stack, Hobby/free)
- GitHub fork: https://github.com/vikas162202-stack/wacrm

## Supabase
- Project: wacrm  (ref: kxakwmgrzrihdyctysej)
- URL: https://kxakwmgrzrihdyctysej.supabase.co
- Region: Northeast Asia (Tokyo)
- Schema: 58 migrations applied → 37 tables
- Keys page: dashboard → Project Settings → API Keys (Legacy)

## Vercel env vars (set)
- NEXT_PUBLIC_SUPABASE_URL ............ set
- NEXT_PUBLIC_SUPABASE_ANON_KEY ....... set (pasted by Vikas)
- SUPABASE_SERVICE_ROLE_KEY ........... set (pasted by Vikas)
- ENCRYPTION_KEY ...................... set (AES-256, stored in .env.local)
- META_APP_SECRET .................... PLACEHOLDER — replace after Meta setup, then redeploy

## Remaining (final phase): Meta WhatsApp Cloud API
1. Create a Meta app (developers.facebook.com) → add WhatsApp product.
2. Get: phone number ID + WhatsApp business account ID (use the free TEST number),
   a permanent access token, and the App Secret (App Settings → Basic).
3. In Vercel → wacrm → Settings → Environment Variables: replace META_APP_SECRET
   placeholder with the real App Secret → Redeploy.
4. In the CRM (app → connect WhatsApp): paste phone number ID, WABA ID, access token,
   and a webhook verify token (any string).
5. In Meta app → WhatsApp → Configuration: set callback URL to
   https://wacrm-five-pied.vercel.app/api/whatsapp/webhook  + the same verify token;
   subscribe webhook fields: messages, message_template_status, message_template_quality.

## Meta WhatsApp Cloud API (connected 22 Nov 2026)
- Meta app: wacrm  (App ID: 1961775291896589)
- Business portfolio: The Geopolitical Economist (unverified — OK for test number)
- Test number: +1 555 174 9182  (free, up to 5 recipients, 90 days)
- Phone Number ID: 1425643260637895
- WhatsApp Business Account ID (Messaging account ID): 2336221127150880
- Webhook callback URL: https://wacrm-five-pied.vercel.app/api/whatsapp/webhook
- Webhook verify token: wacrmverify2026gpe
- Webhook field subscribed: messages (v27.0)
- App Secret: set in Vercel META_APP_SECRET (replaced placeholder) + redeployed
- Access token: TEMPORARY (24h). For 24/7 use, create a permanent System User token
  (Meta Business settings → Users → System users) and re-paste it in the CRM.

## Status
Fully wired: credentials valid, WABA subscribed to app, webhook verified, messages
subscribed, app secret live. CRM: https://wacrm-five-pied.vercel.app (login vikas162202@gmail.com).

## To test
In Meta → WhatsApp → API Setup, add your own WhatsApp number as a test recipient (verify
with the code Meta sends). Then message the test number from your phone — it should appear
in the CRM Inbox. Or use the CRM to send (test number can message the 5 verified recipients).

## Caveats / next steps for production
- Temporary token expires in ~24h → swap for a permanent token.
- Test number only reaches 5 verified recipients; app is in Development mode.
- To go live to anyone on a real number: complete Meta Business verification, add/register a
  real phone number, and publish the app.
