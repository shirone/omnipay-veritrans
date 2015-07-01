# Omnipay: Veritrans

[![Build Status](https://travis-ci.org/andylibrian/omnipay-veritrans.svg)](https://travis-ci.org/andylibrian/omnipay-veritrans)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/andylibrian/omnipay-veritrans/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/andylibrian/omnipay-veritrans/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/andylibrian/omnipay-veritrans/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/andylibrian/omnipay-veritrans/?branch=master)
[![Latest Stable Version](https://poser.pugx.org/andylibrian/omnipay-veritrans/v/stable.svg)](https://packagist.org/packages/andylibrian/omnipay-veritrans)

**[Veritrans](https://www.veritrans.co.id/) driver for the Omnipay PHP payment processing library**

[Omnipay](https://github.com/thephpleague/omnipay) is a framework agnostic, multi-gateway payment
processing library for PHP 5.3+. This package implements Veritrans support for Omnipay.

*This is a third party package maintained by [the author](https://github.com/andylibrian) and community.
If you want to use Veritrans Payment API without Omnipay, we suggest you check out The official [PHP wrapper for Veritrans Payment API](https://github.com/veritrans/veritrans-php).*

## Installation

Omnipay is installed via [Composer](http://getcomposer.org/). To install, simply run:

    $ php composer.phar require andylibrian/omnipay-veritrans


## Basic Usage

The following gateways are provided by this package:

- VT-Web


```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use Omnipay\Omnipay;
use Omnipay\Common\CreditCard;

$gateway = Omnipay::create('Veritrans_VTWeb');
$gateway->setServerKey('VT-server-eEpn68iOEtiwFHJIU2fOWYWS');
$gateway->setEnvironment('sandbox'); // [production|sandbox] default to production
 // Optional
$item1_details = array(
    'id' => 'a1',
    'price' => 50000,
    'quantity' => 2,
    'name' => "Apple"
    );

// Optional
$item2_details = array(
    'id' => 'a2',
    'price' => 45000,
    'quantity' => 1,
    'name' => "Orange"
    );

// Optional
$item_details = array ($item1_details, $item2_details);

// Optional
$shipping_address = array(
    'first_name'    => "Obet",
    'last_name'     => "Supriadi",
    'address'       => "Manggis 90",
    'city'          => "Jakarta",
    'postal_code'   => "16601",
    'phone'         => "08113366345",
    'country_code'  => 'IDN'
    );

// Optional
$customer_details = array(
    'first_name'    => "Andri",
    'last_name'     => "Litani",
    'email'         => "andri@litani.com",
    'phone'         => "081122334455",
    // 'billing_address'  => $billing_address,
    'shipping_address' => $shipping_address
    );

$data = array(
    'transactionId' => '1234569',
    'amount'        => '145000.00',
    'card'          => new CreditCard(),
    'vtwebConfiguration' => array(
        'credit_card_3d_secure' => true,
    ),  
    'currency'      => 'IDR',
    'itemDetails'   => $item_details
);


$response = $gateway->purchase($data)->send();

if ($response->isSuccessful()) {
    // payment success, update database
    // using VT-Web, you will always get redirected to offsite (veritrans page)
    // so here won't be reached.
} elseif ($response->isRedirect()) {
    // redirect to offsite payment gateway
    $response->redirect();
} else {
    echo $response->getMessage();
}
```


For general usage instructions, please see the main [Omnipay](https://github.com/thephpleague/omnipay)
repository.
And for more information about Veritrans features, please see [Veritrans Documentation](http://docs.veritrans.co.id/welcome/welcome.html)

## Support

If you are having general issues with Omnipay, we suggest posting on
[Stack Overflow](http://stackoverflow.com/). Be sure to add the
[omnipay tag](http://stackoverflow.com/questions/tagged/omnipay) so it can be easily found.

If you want to keep up to date with release anouncements, discuss ideas for the project,
or ask more detailed questions, there is also a [mailing list](https://groups.google.com/forum/#!forum/omnipay) which
you can subscribe to.

If you believe you have found a bug, please report it using the [GitHub issue tracker](https://github.com/andylibrian/omnipay-veritrans/issues),
or better yet, fork the library and submit a pull request.

