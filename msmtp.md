▇▅▃▆▂▁▄▆▅▇▇▁▂▅▆▆▃▂▄▆▃▁▂▄▅█▄▂▁▆▃▆▃▃▁▂▄▇▄▅▁▁▄▅▄▅▅▁▂▄▆▇▇▇▂▃▇▃▁



Certainly! I'll guide you through using msmtp in the
 terminal and provide advanced examples. Let's start with
 the basics and then move on to more advanced usage.

### Basic Usage

1. Install msmtp:

On Ubuntu/Debian:
``
sudo apt-get install msmtp
```

On macOS (using Homebrew):                                 ``
brew install msmtp
```

2. Configure msmtp:

Create a configuration file named ~/.msmtprc:

``
account default
host smtp.example.com
port 587
auth username
user your_email@example.com
password your_password
tls on
```

Replace the values with your SMTP server details.

3. Send an email:

```bash
echo "Subject: Test Email" | msmtp -a default recipient
@example.com
```

This command sends a simple text email.

### Advanced Examples

#### 1. Sending HTML Emails

To send HTML emails, use the -t flag:

```bash
cat << EOF > email.html
<html>
<body>
<h1>Hello from msmtp!</h1>
<p>This is an HTML email.</p>
</body>
</html>
EOF

msmtp -t -a default recipient@example.com < email.html
```

#### 2. Using Attachments

Add attachments using the -i flag:

```bash
msmtp -a default recipient@example.com -i /path/to/file.txt

```

For multiple attachments:

```bash
msmtp -a default recipient@example.com -i file1.txt -i file
2.pdf
```

#### 3. Setting Custom Headers

Use the -h flag to set custom headers:

```bash
msmtp -a default recipient@example.com -h "X-Mailer: msmtp/
1.6.0"
```

Multiple headers:

```bash
msmtp -a default recipient@example.com \
      -h "X-Mailer: msmtp/1.6.0" \
      -h "Precedence: bulk"
```

#### 4. Using SSL/TLS

Specify SSL/TLS settings explicitly:

```bash
msmtp -a default recipient@example.com --ssl-cipher=DHE-RSA
-AES256-GCM-SHA384
```

#### 5. Retry Mechanism

Set retry intervals:

``
account default
...
timeout 60
retry 15
maxretries 3
```

#### 6. Using Environment Variables

Store sensitive information in environment variables:

```bash
export MSMTPOPTIONS="-a default"
export MSMTPEMAIL="your_email@example.com"
export MSMTPSERVER="smtp.example.com"

echo "Subject: Test Email" | msmtp $MSMTPOPTIONS $MSMTPE
MAIL
```

#### 7. Logging

Enable verbose logging:

```bash
msmtp -v -a default recipient@example.com
```

#### 8. Using Multiple Accounts

Define multiple accounts in ~/.msmtprc:

``
account default
...
account backup
...
```

Send using a specific account:

```bash
msmtp -a backup recipient@example.com
```

These examples cover various aspects of using msmtp in the
 terminal. Remember to replace placeholder values with your
 actual SMTP server details and credentials.

 ✔  [08:40:54 PM][Wed Jul 16]u0_a23@localhost:~
$
