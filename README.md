## SMTP-Notes
### Check connection
```
$telnet <smtp-host-ip> 25
```
### Install nmap to check ports and connections
```
$apt-get install nmap
```
### Check SMTP available ports
```
$nmap <smtp-host-ip>

Nmap scan report for 10.xx.xx.xxx
Host is up (0.0047s latency).
Not shown: 995 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
25/tcp   open  smtp
110/tcp  open  pop3
587/tcp  open  submission
1720/tcp open  h323q931
```
### Check SMTP port
```
$nmap -p<port> <smtp-host-ip>
```
### PHP Test Script
```
<?php
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;

require 'vendor/autoload.php';

$mail = new PHPMailer(true);

try {
    $mail->SMTPDebug = SMTP::DEBUG_SERVER;
    $mail->isSMTP();
    $mail->Host       = '10.xx.xx.xxx';
    $mail->AuthType = 'PLAIN';
    $mail->SMTPAuth   = false;
    $mail->Username   = null;
    $mail->Password   = null;
    $mail->Port       = 25;
    $mail->SMTPAutoTLS = false;
    $mail->SMTPOptions = array(
        'ssl' => array(
                'verify_peer' => false,
                'verify_peer_name' => false,
                'allow_self_signed' => true
                )
   );

    $mail->setFrom('noreply@gmail.com', 'Sender From');
    $mail->addAddress('recipient@gmail.com', 'Recipient'); 

    $mail->isHTML(true);                                  
    $mail->Subject = 'Here is the subject';
    $mail->Body    = 'This is the HTML message body <b>in bold!</b>';
    $mail->AltBody = 'This is the body in plain text for non-HTML mail clients';

    $mail->send();
    echo 'Message has been sent';
} catch (Exception $e) {
    echo "Message could not be sent. Mailer Error: {$mail->ErrorInfo}";
}
```
### Remember
```
Relay Access Denied: 
1. SMTP hosts, Authentication Type, Username and Password
2. Recipient email and Sender email should be allowed by smtp
3. smtp in-bound accept sender email
4. smtp out-bound sent the email to recipient (note if this is blocked)
```
### Links Debugging
```
1. https://github.com/PHPMailer/PHPMailer/issues/1322
2. https://itsyndicate.org/blog/relay-access-denied-solution/
3. https://serversitters.com/how-to-correct-554-5-7-1-relay-access-denied-email-errors-and-prevent-them-in-the-future.html
```
