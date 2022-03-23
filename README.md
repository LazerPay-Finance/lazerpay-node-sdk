<p>
<img title="Lazerpay" src= "https://res.cloudinary.com/njokuscript/image/upload/v1646279538/lazerpay_logo_no-bg_trkkye.png"/>
</p>
# Lazerpay v1 NodeJS SDK

### How to use

`npm install lazerpay-node-sdk`

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);
```

Use TEST API keys for testing, and LIVE API keys for production

## Lazerpay Methods exposed by the sdk

**1**. **Payment**

- Initialize Payment
- Confirm Payment

**2**. **Payout**

- Crypto Payout
- Bank Payout ~ This is coming to V2

**3**. **Payment Links**

- Create payment links
- Get all payment links
- Get a single payment link
- Update a payment Link

**4**. **Misc**

- Get all accepted coins

## Payment

#### `Initialize Payment`

This describes to allow your customers to initiate a crypto payment transfer.

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);

const payment_tx = async () => {
  try {
    const transaction_payload = {
      reference: 'YOUR_REFERENCE', // Replace with a reference you generated
      customer_name: 'Njoku Emmanuel',
      customer_email: 'kalunjoku123@gmail.com',
      coin: 'BUSD', // BUSD, DAI, USDC or USDT
      currency: 'USD', // NGN, AED, GBP, EUR
      fiatAmount: '10',
      accept_partial_payment: true, // By default it's false
    };

    const response = await lazer.Payment.initializePayment(transaction_payload);

    console.log(response);
  } catch (error) {
    console.log(error);
  }
};
```

#### `Confirm Payment`

This describes to allow you confirm your customers transaction after payment has been made.

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);

const confirm_tx = async () => {
  try {
    const payload = {
      identifier:
        'address generated or the reference generated by you from initializing payment',
    };

    const response = await lazer.Payment.confirmPayment(payload);

    console.log(response);
  } catch (error) {
    console.log(error);
  }
};
```

## Transfer

#### `Crypto Payout`

This describes to allow you withdraw the crypto in their lazerpay balance to an external address

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);

const crypto_payout_tx = async () => {
  const transaction_payload = {
    amount: 1,
    recipient: '0x0B4d358D349809037003F96A3593ff9015E89efA', // address must be a bep20 address
    coin: 'BUSD',
    blockchain: 'Binance Smart Chain',
  };
  try {
    const response = await lazer.Payout.transferCrypto(transaction_payload);
    console.log(response.error);
  } catch (e) {
    console.log(e);
  }
};
```

## Payment Links

#### `Create a payment link`

This describes to allow you create a Payment link programatically

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);

const create_paymentlink_tx = async () => {
  const transaction_payload = {
    title: 'Njoku Test',
    description: 'Testing this sdk',
    logo:
      'https://assets.audiomack.com/fireboydml/bbbd8710eff038d4f603cc39ec94a6a6c2c5b6f4100b28d62557d10d87246f27.jpeg?width=340&height=340&max=true',
    currency: 'USD',
    type: 'standard',
  };
  try {
    const response = await lazer.PaymentLinks.createPaymentLink(
      transaction_payload
    );
    console.log(response);
  } catch (e) {
    console.log(e);
  }
};
```

#### `Update a payment link`

This describes to allow you disable or enable a Payment Link by updating it

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);

const transaction_payload = {
  identifier: '7f2vrd8n',
  status: 'inactive', // status should either be active or inactive
};

const update_paymentLink = async () => {
  try {
    const response = await lazer.PaymentLinks.updatePaymentLink(
      transaction_payload
    );
    console.log(response);
  } catch (e) {
    console.log(e);
  }
};
```

#### `Get all payment links`

This describes to allow you get all Payment links created

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);

const get_all_paymentlinks = async () => {
  try {
    const response = await lazer.PaymentLinks.getAllPaymentLinks();
    console.log(response);
  } catch (e) {
    console.log(e);
  }
};
```

#### `Get a single payment link`

This describes to allow you get a Payment link by it's identifier

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);

const identifier = '7f2vrd8n';

const get_paymentlink = async () => {
  try {
    const response = await lazer.PaymentLinks.getPaymentLink(identifier);
    console.log(response);
  } catch (e) {
    console.log(e);
  }
};
```

## Misc

#### `Get Accepted Coins`

This gets the list of accepted cryptocurrencies on Lazerpay

```javascript
const Lazerpay = require('lazerpay-node-sdk');

const lazerpay = new Lazerpay(LAZER_PUBLIC_KEY, LAZER_SECRET_KEY);

const get_accepted_coins = async () => {
  try {
    const response = await lazer.Misc.getAcceptedCoins();
    console.log(response);
  } catch (error) {
    console.log(error);
  }
};
```
