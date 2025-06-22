# Contact Form Setup Guide

## 🎯 Overview
This setup will allow your contact form to:
1. Save submissions to Google Forms
2. Send email notifications to your Gmail
3. Show success notifications to users

## 📋 Step-by-Step Setup

### Step 1: Create Google Form

1. **Go to Google Forms**: https://forms.google.com
2. **Create a new form** with these fields:
   - Name (Short answer)
   - Email (Short answer)
   - Subject (Short answer)
   - Message (Paragraph)

3. **Get Form ID**:
   - Click "Send" button
   - Copy the form URL
   - Extract the form ID from the URL
   - Example: `https://docs.google.com/forms/d/e/1FAIpQLSd.../formResponse`
   - The ID is: `1FAIpQLSd...`

4. **Get Entry IDs**:
   - Right-click on your form and "View page source"
   - Search for `entry.` to find the entry IDs
   - Note down the entry IDs for each field

### Step 2: Update HTML Form

Replace the placeholder values in `index.html`:

```html
<!-- Replace YOUR_FORM_ID with your actual Google Form ID -->
<form id="contactForm" action="https://docs.google.com/forms/d/e/YOUR_FORM_ID/formResponse" method="POST" target="hidden_iframe">

<!-- Replace entry.1234567890 with your actual entry IDs -->
<input type="text" id="name" name="entry.1234567890" placeholder="Your Name" required>
<input type="email" id="email" name="entry.0987654321" placeholder="Your Email" required>
<input type="text" id="subject" name="entry.1122334455" placeholder="Subject" required>
<textarea id="message" name="entry.5566778899" placeholder="Your Message" rows="6" required></textarea>
```

### Step 3: Setup EmailJS

1. **Go to EmailJS**: https://www.emailjs.com
2. **Create account** and verify your email
3. **Add Email Service**:
   - Click "Add New Service"
   - Choose "Gmail"
   - Connect your Gmail account
   - Note down the Service ID

4. **Create Email Template**:
   - Go to "Email Templates"
   - Create new template
   - Use this template:

```html
Subject: New Contact Form Submission from {{from_name}}

Name: {{from_name}}
Email: {{from_email}}
Subject: {{subject}}

Message:
{{message}}

---
This message was sent from your portfolio contact form.
```

5. **Get Template ID** and update `script.js`:

```javascript
emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', {
    from_name: name,
    from_email: email,
    subject: subject,
    message: message,
    to_email: 'vigneshhemanthrao@gmail.com'
})
```

### Step 4: Update Configuration

1. **In `index.html`**:
   - Replace `YOUR_PUBLIC_KEY` with your EmailJS public key

2. **In `script.js`**:
   - Replace `YOUR_SERVICE_ID` with your EmailJS service ID
   - Replace `YOUR_TEMPLATE_ID` with your EmailJS template ID

### Step 5: Gmail App Password (Optional but Recommended)

For better security, use an App Password:

1. **Enable 2-Factor Authentication** on your Google account
2. **Generate App Password**:
   - Go to Google Account settings
   - Security → App passwords
   - Generate password for "Mail"
   - Use this password in EmailJS instead of your regular password

## 🔧 Testing

1. **Test Google Forms**:
   - Submit a test form
   - Check if it appears in your Google Forms responses

2. **Test EmailJS**:
   - Submit a test form
   - Check if you receive email notification
   - Check browser console for any errors

## 🚀 Features

✅ **Google Forms Integration**: All submissions saved to Google Forms
✅ **Email Notifications**: Instant email alerts to your Gmail
✅ **Success Notifications**: User-friendly success messages
✅ **Loading States**: Visual feedback during submission
✅ **Form Validation**: Required field validation
✅ **Mobile Responsive**: Works on all devices

## 📱 Mobile Optimization

The form is fully responsive and includes:
- Touch-friendly input fields
- Proper keyboard types for mobile
- Loading states for better UX
- Success notifications

## 🔒 Security Notes

- EmailJS uses your Gmail account securely
- Form data is encrypted in transit
- No sensitive data stored on your server
- Google Forms provides secure data storage

## 🆘 Troubleshooting

**Form not submitting?**
- Check if Google Form ID is correct
- Verify entry IDs match your form fields
- Check browser console for errors

**Emails not sending?**
- Verify EmailJS configuration
- Check if Gmail account is properly connected
- Ensure template variables match

**Mobile issues?**
- Test on different devices
- Check responsive design
- Verify touch interactions

## 📞 Support

If you need help:
1. Check EmailJS documentation
2. Verify Google Forms setup
3. Test step by step
4. Check browser console for errors

Your contact form will now save data to Google Forms and send email notifications to your Gmail! 