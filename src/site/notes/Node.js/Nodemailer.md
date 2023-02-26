---
{"dg-publish":true,"permalink":"/node-js/nodemailer/"}
---

# Nodemailer

---

## Node module for off-the-shelf solutions

02-24-2023

Nodemailer is a project that was started in 2010 when there was no easy option to send email messages, and today it is the solution most Node.js users turn to by default.

With Nodemailer, you can use a number of supported email services to send emails. Nodemailer supports popular email services such as Gmail, Outlook.com, Yahoo Mail, and many others. It also supports custom SMTP servers, sendmail, and Amazon SES (Simple Email Service).

To use Nodemailer with a specific [email service](https://nodemailer.com/smtp/well-known/), you will need to provide the necessary credentials and settings for that service. 

***Some services like [iCloud](https://support.apple.com/en-us/HT202304) will also require SSL and SMTP authentication. This typically includes the SMTP server address, port number, authentication method, username, and password.***

---

The Nodemailer documentation is very well organized and easy to follow, making it simple for developers to learn how to use and implement the module. The documentation includes a comprehensive Getting Started guide that walks through the basics of setting up a transport object and sending emails.

```npm install nodemailer```

For example, to use Nodemailer with Gmail, you can create a transport object with the following settings:

```js
const nodemailer = require('nodemailer');
// no need to set up host or port for well-known services
const transporter = nodemailer.createTransport({
  service: 'gmail',
  auth: {
    user: '<your-gmail-username>',
    pass: '<your-gmail-password>'
  }
});
```

One great feature of Nodemailer is that it comes with a built-in way to test your emails without actually sending them. I like to use this during development and testing when I don't want to spam users with test emails. To test Nodemailer, you can use [Ethereal.email](http://ethereal.email/), a free email testing service that allows you to receive and view emails sent from your application.
```javascript
app.post("/servicerequest", async (req, res) => {

	let testAccount = await nodemailer.createTestAccount();
	const transporter = nodemailer.createTransport({
		host: "smtp.ethereal.email",
		port: 587,
		auth: {
			user: testAccount.user,
			pass: testAccount.pass,
		},
	});
```

Sending an email response to the user with their form details.
```javascript
const mailOptions = {
	from: testAccount.user,
	to: req.body.email,
	subject: "Service Request Submitted",
	html: `
	<p>Thank you for submitting a service request!</p>
	<p>Here are the details you submitted:</p>
	<ul>
		<li>Name: ${req.body.name}</li>
		<li>Phone: ${req.body.phone}</li>
		<li>Email: ${req.body.email}</li>
		<li>Service: ${req.body.service}</li>
		<li>Date: ${req.body.date}</li>
		<li>Time: ${req.body.time}</li>
	</ul>`,
};

transporter.sendMail(mailOptions, (error, info) => {
	if (error) {
		console.log(error);
	} else {
		console.log("Email sent: " + info.response);
	}
});
```

By using Nodemailer with a supported email service, you can send emails from your application without having to set up your own email server. This makes it easy to integrate email functionality into your application and ensures that your emails are delivered reliably and securely.