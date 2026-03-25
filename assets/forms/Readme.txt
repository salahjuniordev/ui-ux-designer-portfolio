

<?php
/**
 * Requires the "PHP Email Form" library
 * The "PHP Email Form" library is available only in the pro version of the template
 * The library should be uploaded to: vendor/php-email-form/php-email-form.php
 * For more info and help: https://bootstrapmade.com/php-email-form/
 */

// Replace contact@example.com with your real receiving email address
$receiving_email_address = 'happinessjohn395gmail.com';

if (!file_exists($php_email_form = '../assets/vendor/php-email-form/php-email-form.php')) {
    die('Unable to load the "PHP Email Form" Library!');
}

include($php_email_form);

$contact = new PHP_Email_Form;
$contact->ajax = true;
$contact->to = $receiving_email_address;
$contact->from_name = filter_input(INPUT_POST, 'name');
$contact->from_email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
$contact->subject = filter_input(INPUT_POST, 'subject');

// SMTP config (uncomment and fill in your credentials)
// $contact->smtp = array(
//     'host' => 'example.com',
//     'username' => 'example',
//     'password' => 'pass',
//     'port' => '587'
// );

$contact->add_message(filter_input(INPUT_POST, 'name'), 'From');
$contact->add_message(filter_input(INPUT_POST, 'email'), 'Email');
isset($_POST['phone']) && $contact->add_message(filter_input(INPUT_POST, 'phone'), 'Phone');
$contact->add_message(filter_input(INPUT_POST, 'message'), 'Message', 10);

if (!$contact->send()) {
    echo 'Error sending message';
} else {
    echo 'Message sent successfully';
}
?>

