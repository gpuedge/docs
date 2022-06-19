---
id: wallet
title: Wallet
---

GPUX uses a cryptographic (ed25519) settlement system. 

Because node providers must be able to operate independently to not be affected by central outages, it becomes complex
to settle payment for jobs using traditional concurrent database methods.

## Wallet Rules {#wallet-rules}

- Access using email or ED25519 secret-key
- Buy `credits` using Stripe
- Earn `earned credits` completing jobs
- `credits` nor `earned credits` cannot be transferred

---

## Email {#wallet-email}

Email accounts have the ED25519 secret key stored on our backend, this is for ease of use. 
For small amounts of credits they are perfectly fine and safe. When you login with an email account
we lookup the keypair and send it back to the device you are logging in from.

---

## ED25519 {#wallet-ed25519}

ED25519 keypair accounts put you in full custody of your secret key. You must keep it safe
and backed up. Only the `wallet.gpux.ai` domain has access to the key when you use the GUI. When you
use purely the API you can keep your key off `wallet.gpux.ai` even. 

---

## Recommended use {#wallet-recommended}

If you use GPUX sporadically/to-trial feel perfectly comfortable using the `Email` login method.
If you are a power user, higher tier node operator or pedantic, take full custody of your keys.

---

## Credits {#credits-wallet}

Credits can only be bought through Stripe checkout, which supports bank cards, credit cards, wechat pay and alipay.

---

## Earned Credits {#earned-wallet}

Earned credits are the result of paying a node provider for compute.  They cannot be converted into regular credits, they can only be withdrawn into fiat. For withdrawals contact us, we can pay to bank, DAI, or credit card.

