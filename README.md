# Mail

The mail package provides a straightforward email client for sending emails using SMTP in Go applications. It supports sending individual emails, bulk emails, and personalized emails with template substitution.

## Installation

```zsh
go get github.com/gosuit/mail
```

## Features

• SMTP Authentication: Securely send emails using SMTP authentication.

• Single Email Sending: Send emails to a single recipient with specified subject and message.

• Bulk Email Sending: Send the same message to multiple recipients at once.

• Personalized Emails: Send personalized messages to each recipient by substituting values into a template.

## Usage

```golang
package main

import (
    "log"

    "github.com/gosuit/mail"
)

func main() {
    cfg := &mail.Config{
        Host:     "smtp.example.com",
        Port:     587,
        Username: "your-email@example.com",
        Password: "your-email-password",
        Identity: "your-email@example.com",
    }

    client := mail.New(cfg)

    // One recipient.
    err := client.Send("recipient@example.com", "Hello, this is a test email!", "Test Subject", "text/plain")
    if err != nil {
        log.Fatalf("failed to send email: %v", err)
    }

    // A lot of recipients.
    recipients := []string{"recipient1@example.com", "recipient2@example.com"}
    message := "This is a bulk email message."
    subject := "Bulk Email Subject"

    err = client.Mailing(recipients, message, subject, "text/plain")
    if err != nil {
        log.Fatalf("failed to send bulk emails: %v", err)
    }

    // Personalized Greeting
    template := "Hello %s, welcome to our service!"
    values := map[string][]interface{}{
        "recipient1@example.com": {"Alice"},
        "recipient2@example.com": {"Bob"},
    }

    subject := "Personalized Greeting"
    err = client.PersonalMailing(values, template, subject, "text/plain")
    if err != nil {
        log.Fatalf("failed to send personalized emails: %v", err)
    }
}
```

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue for any enhancements or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
