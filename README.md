

# Get a Highest Score with reCaptcha v3 Using CapSolver

![How to solve reCaptcha v3](https://assets.capsolver.com/prod/images/post/2023-10-18/24e2fc61-c832-429c-8f50-a12f27e0d6cb.png)

## 🤙 Step 1: Sign Up for CapSolver

To start using [CapSolver](https://www.capsolver.com/?utm_source=github&utm_medium=repo&utm_campaign=recaptchav3score)., you need to sign up for an account. Visit the website and click on the ‘Sign Up’ button. You will be prompted to enter your email address and create a password. Once you have provided the necessary information, click on the ‘Sign Up’ button to create your account.

![Sign up CapSolver](https://assets.capsolver.com/prod/images/post/2023-07-18/ba8e903b-d96a-4ac4-aab7-6bfb6a2a4112.gif)

## 🔖 Step 2: Add Funds to Your Account

Before you can start solving reCaptcha v3, you need to add funds to your CapSolver account. Click on the ‘Add Funds’ button and select your preferred payment method. Follow the on-screen instructions to complete the payment process.

![Add Funds CapSolver](https://assets.capsolver.com/prod/images/post/2023-12-14/2c8f6971-07d7-4324-b29e-c3d6e24b581a.png)

## 🤖 How to Solve reCaptcha v3 and Achieve a Human-like Score

### Requisites

- **CapSolver Key:** Your API key from CapSolver.
- **Proxy (Optional):** While optional, it's recommended to use your own proxy for reCaptcha v3 as IP quality is crucial for obtaining a high score.

### Important Considerations

- **`pageAction`:** Must be accurate. Refer to [this blog](https://www.capsolver.com/blog/how-to-identify-and-find-values-of-recaptchav3) for guidance on obtaining the correct `pageAction`.
- **`websiteURL`:** Must be correct.
- **Proxy Quality:** If using `ReCaptchaV3TaskProxyLess`, a proxy isn’t required, but if using `ReCaptchaV3Task`, a good proxy is essential. Poor proxy quality or incorrect `pageAction` and `websiteURL` can result in a low score, affecting the outcome.

### Task Types

- **`ReCaptchaV3Task`:** Requires your own proxies.
- **`ReCaptchaV3TaskProxyLess`:** Uses the server's built-in proxy.

For this example, we'll use **ReCaptchaV3TaskProxyLess** to test our token score using [this page](https://antcpt.com/score_detector).

### ⚡ Step 1: Submit the Required Information to CapSolver

Send the following request to CapSolver to create a task:

```json
POST https://api.capsolver.com/createTask
{
  "clientKey":"yourapiKey",
  "task": {
    "type": "ReCaptchaV3TaskProxyLess",
    "websiteURL": "https://antcpt.com/score_detector",
    "websiteKey": "6LcR_okUAAAAAPYrPe-HK_0RULO1aZM15ENyM-Mf",
    "pageAction": "homepage"
  }
}
```

### 🪄 Step 2: Retrieve the Captcha Solution

Use the `getTaskResult` method to retrieve the solution:

```json
POST https://api.capsolver.com/getTaskResult
{
    "clientKey":"YOUR_API_KEY",
    "taskId": "TASKID_OF_CREATETASK"
}
```

Check every 3 to 5 seconds to see if the captcha has been solved.

### 📝 Example: Submitting the Captcha Token to the Test Website

```js
var request = require('request');
var options = {
  method: 'POST',
  url: 'https://antcpt.com/score_detector/verify.php',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    "g-recaptcha-response": "here the token of capsolver"
  })
};

request(options, function (error, response) {
  if (error) throw new Error(error);
  console.log(response.body);
});
```

The test page will respond with the score of the token.

### Troubleshooting

If the token returns a low score or isn’t accepted, review the earlier points about ensuring correct parameters. If issues persist, refer to this [blog post](https://www.capsolver.com/blog/How-to-bypass-all-the-versions-reCAPTCHA-v2-v3) for additional guidance.

## 🏁 Conclusion

Achieving a human-like score when solving reCaptcha v3 can be challenging, but with CapSolver, it's streamlined. By following the steps outlined, you can easily achieve scores in the 0.7–0.9 range, mimicking human behavior effectively.

## 📢 Disclaimer

Using CapSolver or similar tools to bypass CAPTCHA protections should always comply with the terms of service of the website you are interacting with. Misuse of these tools can result in legal consequences. Always ensure you have the necessary permissions before employing such techniques.

