# Custom SMTP for WordPress (Without Plugin)

This project provides a custom SMTP configuration for WordPress using Gmail's SMTP server. It modifies the `functions.php` file to send emails without relying on plugins.

## Features

- Uses Gmail's SMTP server for email delivery.
- No need for additional plugins.
- Secure authentication with an App Password.
- Easily configurable within `functions.php`.

## Prerequisites

- A Gmail account.
- An App Password generated from your Gmail account ([Google App Password Guide](https://support.google.com/accounts/answer/185833)).
- A WordPress website with access to `functions.php`.

## Installation

1. **Generate a Gmail App Password:**

   - Go to [Google App Passwords](https://myaccount.google.com/apppasswords).
   - Generate a password for "Mail" and "Other (Custom name)".
   - Copy the generated password.

2. **Edit ****\`\`**** in Your Theme:**

   - Open your WordPress theme's `functions.php` file.
   - Add the following code:

   ```php
   // SMTP mail configuration
   function custom_smtp_mail_config($phpmailer) {
       $phpmailer->isSMTP();
       $phpmailer->Host = 'smtp.gmail.com';
       $phpmailer->SMTPAuth = true;
       $phpmailer->Port = 587;
       $phpmailer->Username = 'your-email@gmail.com';
       $phpmailer->Password = 'your-app-password';
       $phpmailer->SMTPSecure = 'tls';
       $phpmailer->From = 'your-email@gmail.com';
       $phpmailer->FromName = 'Your Name';
   }
   add_action('phpmailer_init', 'custom_smtp_mail_config');
   ```

   - Replace `your-email@gmail.com` with your Gmail address.
   - Replace `your-app-password` with the generated App Password.

3. **Test Email Sending:**

   - Add the following function in `functions.php`:

   ```php
   function send_test_email() {
       $to = 'recipient-email@example.com'; // Replace with the recipient's email
       $subject = 'Test Email from WordPress';
       $message = 'This is a test email sent using custom SMTP settings.';
       $headers = array('Content-Type: text/html; charset=UTF-8');

       if (wp_mail($to, $subject, $message, $headers)) {
           echo 'Test email sent successfully!';
       } else {
           echo 'Failed to send test email.';
       }
   }
   // Uncomment the line below to send a test email
   // add_action('init', 'send_test_email');
   ```

   - Replace `recipient-email@example.com` with your desired email address.
   - Uncomment `add_action('init', 'send_test_email');` to send a test email.

## Security Note

- Never hardcode sensitive credentials in public repositories.
- Use environment variables or a WordPress configuration file to securely store credentials.
- Avoid exposing your App Password in any public forum or repository.

## License

This project is open-source and licensed under the MIT License.

