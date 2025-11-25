# Stripe Integration Setup Guide

## ✅ Your Test Key is Already Integrated!
Your publishable test key is already in the website files:
`pk_test_51SWkKaEJVDHtcC6HAgNkLtbYiyHaxmsODqHq4FhafJip7gWujLk41YlE0cJX13Vuu1t52h3jgWJ1U1hihCmJhIsh00Xl2h1QFW`

## 📝 Next Steps to Complete Stripe Setup:

### 1. Create Products in Stripe Dashboard

1. Log into [dashboard.stripe.com](https://dashboard.stripe.com)
2. Go to **Products** → **Add Product**
3. Create each peptide product:

| Product Name | Suggested Price | 
|-------------|----------------|
| BPC-157 | $89.00 |
| Semaglutide | $299.00 |
| TB-500 | $95.00 |
| CJC-1295 | $125.00 |
| Ipamorelin | $115.00 |
| MOTS-c | $175.00 |
| NAD+ | $225.00 |
| Tirzepatide | $399.00 |
| Epithalon | $145.00 |
| GHK-Cu | $135.00 |
| PT-141 | $155.00 |
| AOD-9604 | $165.00 |

### 2. Get Price IDs

After creating each product:
1. Click on the product
2. Copy the **Price ID** (starts with `price_`)
3. Update the shop-page.html file with these IDs

### 3. Set Up Webhooks

1. In Stripe Dashboard → **Developers** → **Webhooks**
2. Add endpoint: `https://yourdomain.com/webhook/stripe`
3. Select events:
   - `checkout.session.completed`
   - `payment_intent.succeeded`
   - `payment_intent.failed`

### 4. Test Checkout

Test card numbers:
- Success: `4242 4242 4242 4242`
- Decline: `4000 0000 0000 0002`
- 3D Secure: `4000 0025 0000 3155`

Use any future expiry date and any 3-digit CVC.

### 5. Create Checkout Session (Backend Required)

The frontend is ready, but you'll need a backend endpoint to create checkout sessions.
Here's a simple Node.js/Express example:

```javascript
app.post('/create-checkout-session', async (req, res) => {
  const session = await stripe.checkout.sessions.create({
    payment_method_types: ['card'],
    line_items: req.body.items,
    mode: 'payment',
    success_url: 'https://thecompoundpeptides.com/success',
    cancel_url: 'https://thecompoundpeptides.com/cancel',
  });
  
  res.json({ id: session.id });
});
```

## 🎯 Quick Test Mode

For immediate testing without backend:
1. Click "Add to Cart" on products
2. Cart will update (frontend working)
3. Checkout button will attempt to connect to backend
4. You'll see the cart functionality works!

## 📞 Need Help?

- Stripe Support: support@stripe.com
- Stripe Docs: stripe.com/docs
- Test Dashboard: dashboard.stripe.com/test

---

Ready to go LIVE? 
1. Get your LIVE publishable key
2. Replace test key in files
3. Switch products to live mode
4. You're in business! 💰
