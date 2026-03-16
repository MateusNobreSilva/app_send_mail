# PHPMailer

**PHPMailer** – A full-featured email creation and transfer class for PHP.

## Features

- Probably the world's most popular code for sending email from PHP!
- Used by many open-source projects: **WordPress, Drupal, 1CRM, SugarCRM, Yii, Joomla!**, and many more.
- Integrated **SMTP** support – send emails without a local mail server.
- Send emails with multiple **To**, **CC**, **BCC**, and **Reply-to** addresses.
- **Multipart/alternative** emails for mail clients that do not read HTML email.
- Add attachments, including inline attachments for images.
- Supports **UTF-8** content and various encodings like **8bit, base64, binary, and quoted-printable**.
- **SMTP authentication** with mechanisms such as **LOGIN**, **PLAIN**, **CRAM-MD5**, and **XOAUTH2** over SMTPS and SMTP+STARTTLS.
- Validates email addresses automatically.
- Protects against header injection attacks.
- **Error messages** in over 50 languages.
- Supports **DKIM** and **S/MIME** signing.
- Compatible with **PHP 5.5** and later, including **PHP 8.1**.
- Namespaced to prevent name clashes.

## Why You Might Need PHPMailer

Many PHP developers need to send emails from their code, but the built-in `mail()` function offers limited functionality, lacking features such as encryption, authentication, HTML emails, and attachments. **PHPMailer** simplifies these tasks, while also making sure that emails are formatted and sent correctly according to complex email standards.

### Example Scenarios:

- **Sending from Windows**: Windows does not include a local mail server by default. PHPMailer's integrated **SMTP** client works on all platforms, including Windows, allowing you to send emails without a local mail server.
- **Security**: When sending sensitive data, **SMTP over TLS** provides encryption and authentication, which is not supported by the native `mail()` function.

> **Note**: It is both safer and faster to use **SMTP** than the native `mail()` function when sending emails from PHP.

### Alternatives to PHPMailer

While PHPMailer is widely used and robust, other libraries you can consider include **SwiftMailer, Laminas/Mail**, and **ZetaComponents**.

## License

This software is distributed under the **LGPL 2.1** license, along with the **GPL Cooperation Commitment**.  
Please refer to the LICENSE file for detailed information.

## Installation & Loading

### Composer Installation

PHPMailer is available on **Packagist**, and installation via **Composer** is the recommended way to install it. Add the following line to your `composer.json` file:

```
"phpmailer/phpmailer": "^6.5"
```

Or run the following command:

```
composer require phpmailer/phpmailer
```

### Manual Installation

Alternatively, if you’re not using Composer, you can download PHPMailer as a zip file, extract it, and copy the **PHPMailer** folder into one of the `include_path` directories specified in your PHP configuration. Then, load the required classes manually:
```
use PHPMailer\PHPMailer\PHPMailer;  
use PHPMailer\PHPMailer\Exception;

require 'path/to/PHPMailer/src/Exception.php';  
require 'path/to/PHPMailer/src/PHPMailer.php';  
require 'path/to/PHPMailer/src/SMTP.php';
```

> **Note**: You need to include the **Exception** class even if you're not using exceptions because PHPMailer uses it internally.

### Minimal Installation

For projects where you don’t need the full package, the minimal files required are:

- **src/PHPMailer.php**
- **src/SMTP.php** (if using **SMTP**)
- **src/OAuth.php** (if using **XOAUTH2**)
- You can skip the **language** folder if English-only errors are sufficient.

## A Simple Example

Here's how you can send an email using **PHPMailer** with **SMTP**:
```
use PHPMailer\PHPMailer\PHPMailer;  
use PHPMailer\PHPMailer\SMTP;  
use PHPMailer\PHPMailer\Exception;

// Load Composer's autoloader  
require 'vendor/autoload.php';

// Create an instance; passing `true` enables exceptions  
$mail = new PHPMailer(true);

try {  
    // Server settings  
    $mail->SMTPDebug = SMTP::DEBUG_SERVER; // Enable verbose debug output  
    $mail->isSMTP();                       // Send using SMTP  
    $mail->Host       = 'smtp.example.com'; // Set the SMTP server  
    $mail->SMTPAuth   = true;               // Enable SMTP authentication  
    $mail->Username   = 'user@example.com'; // SMTP username  
    $mail->Password   = 'secret';           // SMTP password  
    $mail->SMTPSecure = PHPMailer::ENCRYPTION_SMTPS; // Enable TLS encryption  
    $mail->Port       = 465;                // TCP port to connect to

    // Recipients  
    $mail->setFrom('from@example.com', 'Mailer');  
    $mail->addAddress('joe@example.net', 'Joe User');  
    $mail->addReplyTo('info@example.com', 'Information');  
    $mail->addCC('cc@example.com');  
    $mail->addBCC('bcc@example.com');

    // Attachments  
    $mail->addAttachment('/var/tmp/file.tar.gz');  
    $mail->addAttachment('/tmp/image.jpg', 'new.jpg');

    // Content  
    $mail->isHTML(true);                   // Set email format to HTML  
    $mail->Subject = 'Here is the subject';  
    $mail->Body    = 'This is the HTML message body <b>in bold!</b>';  
    $mail->AltBody = 'This is the plain text for non-HTML mail clients';

    $mail->send();  
    echo 'Message has been sent';  
} catch (Exception $e) {  
    echo "Message could not be sent. Mailer Error: {$mail->ErrorInfo}";  
}
```

This example shows how to send an HTML email with attachments. Modify the settings to suit your **SMTP** server.

## Localization

PHPMailer defaults to English but includes error message translations in over 50 languages. To set a specific language, use the following method:

```
$mail->setLanguage('fr', '/optional/path/to/language/directory/');
```

You can find the translations in the **language** folder, and you’re encouraged to contribute new languages or corrections.

## Documentation

For comprehensive documentation, check out the GitHub wiki. There’s also a troubleshooting guide for common problems.

- PHPMailer API Documentation
- Complete PHPMailer Examples
- Unit Tests

You can generate complete API-level documentation by running `phpdoc` in the top-level folder.

## Tests

PHPMailer uses **PHPUnit 9**, with a polyfill for older versions. You can run tests to ensure the correct behavior of the system.

## Security

Please disclose any vulnerabilities responsibly. Report security issues to the maintainers privately.  
See PHPMailer's security advisories on GitHub.

## Contributing

Submit bug reports, suggestions, or pull requests via GitHub's issue tracker. Contributions to translations or edge case handling are always appreciated.

## Sponsorship

Development resources for PHPMailer are provided by **Smartmessages.net**, a privacy-first email marketing platform.  
Sponsorship via GitHub is welcome. Consider supporting the maintainers through Tidelift’s enterprise support program.

Donations are very welcome, whether in beer 🍺, T-shirts 👕, or cold, hard cash 💰. Sponsorship through GitHub is a simple and convenient way to say "thank you" to PHPMailer's maintainers and contributors – just click the "Sponsor" button on the project page. If your company uses PHPMailer, consider taking part in Tidelift's enterprise support programme.

## PHPMailer For Enterprise
Available as part of the Tidelift Subscription.

The maintainers of PHPMailer and thousands of other packages are working with Tidelift to deliver commercial support and maintenance for the open source packages you use to build your applications. Save time, reduce risk, and improve code health, while paying the maintainers of the exact packages you use. Learn more.

Formatting email correctly is surprisingly difficult. There are myriad overlapping (and conflicting) standards, requiring tight adherence to horribly complicated formatting and encoding rules – the vast majority of code that you'll find online that uses the mail() function directly is just plain wrong, if not unsafe!

The PHP mail() function usually sends via a local mail server, typically fronted by a sendmail binary on Linux, BSD, and macOS platforms, however, Windows usually doesn't include a local mail server; PHPMailer's integrated SMTP client allows email sending on all platforms without needing a local mail server. Be aware though, that the mail() function should be avoided when possible; it's both faster and safer to use SMTP to localhost.

Please don't be tempted to do it yourself – if you don't use PHPMailer, there are many other excellent libraries that you should look at before rolling your own. Try SwiftMailer , Laminas/Mail, ZetaComponents etc.

## Changelog
See changelog.

## History
- PHPMailer was originally written in 2001 by Brent R. Matzelle as a SourceForge project.
- Marcus Bointon (coolbru on SF) and Andy Prevost (codeworxtech) took over the project in 2004.
- Became an Apache incubator project on Google Code in 2010, managed by Jim Jagielski.
- Marcus created his fork on GitHub in 2008.
- Jim and Marcus decide to join forces and use GitHub as the canonical and official repo for PHPMailer in 2013.
- PHPMailer moves to the PHPMailer organisation on GitHub in 2013.

## What's changed since moving from SourceForge?
- Official successor to the SourceForge and Google Code projects.
- Test suite.
- Continuous integration with Github Actions.
- Composer support.
- Public development.
- Additional languages and language strings.
- CRAM-MD5 authentication support.
- Preserves full repo history of authors, commits and branches from the original SourceForge project.
