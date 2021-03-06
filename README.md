IPv4 Subnet Calculator (PHP)
============================

Network calculator for subnet mask and other classless (CIDR) network information.

Features
--------
Given an IP address and CIDR network size, it calculates the network information and provides all-in-one aggregated reports.

### Calculations
 * IP address network subnet masks, network and host portions, and provides aggregated reports.
 * Subnet mask 
 * Network portion
 * Host portion
 * Number of IP addresses in the network
 * Number of addressable hosts in the network
 * IP address range
 * Broadcast address
Provides each data in dotted quads, hexadecimal, and binary formats, as well as array of quads.

### Aggregated Network Calculation Reports
 * Associative array
 * JSON
 * String
 * Printed to STDOUT

Setup
-----

 Add the library to your `composer.json` file in your project:

```javascript
{
  "require": {
      "markrogoyski/ipv4-subnet-calculator": "2.0.*"
  }
}
```

Use [composer](http://getcomposer.org) to install the library:

```bash
$ php composer.phar install
```

Composer will install IPv4 Subnet Calculator inside your vendor folder. Then you can add the following to your
.php files to the use library with Autoloading.

```php
require_once( __DIR__ . '/vendor/autoload.php' );
```

### Minimum Requirements
 * PHP 5.3.0

Usage
-----

### Create New SubnetCalculator Object
```php
// For network 192.168.112.203/23
$sub = new IPv4\SubnetCalculator( '192.168.112.203', 23 );
```

### Get Various Network Information
```php
$number_ip_addrssses = $sub->getNumberIPAddresses();      // 512
$number_hosts        = $sub->getNumberAddressableHosts(); // 510
$address_rage        = $sub->getIPAddressRange();         // [ 192.168.112.0, 192.168.113.255 ]
$network_size        = $sub->getNetworkSize();            // 23
$broadcast_address   = $sub->getBroadcastAddress();       // 192.168.113.255
```

### Get IP Address
```php
$ip_address        = $sub->getIPAddress();       // 192.168.112.203
$ip_address_quads  = $sub->getIPAddressQuads();  // [ 192, 168, 112, 203 ]
$ip_address_hex    = $sub->getIPAddressHex();    // C0A870CB
$ip_address_binary = $sub->getIPAddressBinary(); // 11000000101010000111000011001011
```

### Get Subnet Mask
```php
$subnet_mask        = $sub->getSubnetMask();       // 255.255.254.0
$subnet_mask_quads  = $sub->getSubnetMaskQuads();  // [ 255, 255, 254, 0 ]
$subnet_mask_hex    = $sub->getSubnetMaskHex();    // FFFFFE00
$subnet_mask_binary = $sub->getSubnetMaskBinary(); // 11111111111111111111111000000000
```

### Get Network Portion
```php
$network        = $sub->getNetworkPortion();       // 192.168.112.0
$network_quads  = $sub->getNetworkPortionQuads();  // [ 192, 168, 112, 0 ]
$network_hex    = $sub->getNetworkPortionHex();    // C0A87000
$network_binary = $sub->getNetworkPortionBinary(); // 11000000101010000111000000000000
```

### Get Host Portion
```php
$host        = $sub->getHostPortion();       // 0.0.0.203
$host_quads  = $sub->getHostPortionQuads();  // [ 0, 0, 0, 203 ]
$host_hex    = $sub->getHostPortionHex();    // 000000CB
$host_binary = $sub->getHostPortionBinary(); // 00000000000000000000000011001011
```

### Calculations
```php
$in_subnet   = $sub->ipInSubnet('192.168.112.33');			// 1
$in_subnet   = $sub->ipInSubnet('192.168.110.33');			// 0
$next_subnet = $sub->nextSubnetInRange(21,'192.168.96.0/20');		// 192.168.120.0/21
$next_subnet = $sub->->nextSubnetInRange(22,'192.168.112.0/20');	// 192.168.116.0/22
```

### Reports

#### Printed Report
```php
$sub->printSubnetReport();
/*
192.168.112.203/23           Quads      Hex                           Binary
------------------ --------------- -------- --------------------------------
IP Address:        192.168.112.203 C0A870CB 11000000101010000111000011001011
Subnet Mask:         255.255.254.0 FFFFFE00 11111111111111111111111000000000
Network Portion:     192.168.112.0 C0A87000 11000000101010000111000000000000
Host Portion:            0.0.0.203 000000CB 00000000000000000000000011001011

Number of IP Addresses:      512
Number of Addressable Hosts: 510
IP Address Range:            192.168.112.0 - 192.168.113.255
Broadcast Address:           192.168.113.255
*/
```

#### Array Report
```php
$sub->getSubnetArrayReport();
/*
Array
(
    [ip_address_with_network_size] => 192.168.112.203/23
    [ip_address] => Array
        (
            [quads] => 192.168.112.203
            [hex] => C0A870CB
            [binary] => 11000000101010000111000011001011
        )

    [subnet_mask] => Array
        (
            [quads] => 255.255.254.0
            [hex] => FFFFFE00
            [binary] => 11111111111111111111111000000000
        )

    [network_portion] => Array
        (
            [quads] => 192.168.112.0
            [hex] => C0A87000
            [binary] => 11000000101010000111000000000000
        )

    [host_portion] => Array
        (
            [quads] => 0.0.0.203
            [hex] => 000000CB
            [binary] => 00000000000000000000000011001011
        )

    [network_size] => 23
    [number_of_ip_addresses] => 512
    [number_of_addressable_hosts] => 510
    [ip_address_range] => Array
        (
            [0] => 192.168.112.0
            [1] => 192.168.113.255
        )

    [broadcast_address] => 192.168.113.255
)
*/
```

#### JSON Report
```php
$sub->getJSONReport();
/*
{
    "ip_address_with_network_size": "192.168.112.203/23",
    "ip_address": {
        "quads": "192.168.112.203",
        "hex": "C0A870CB",
        "binary": "11000000101010000111000011001011"
    },
    "subnet_mask": {
        "quads": "255.255.254.0",
        "hex": "FFFFFE00",
        "binary": "11111111111111111111111000000000"
    },
    "network_portion": {
        "quads": "192.168.112.0",
        "hex": "C0A87000",
        "binary": "11000000101010000111000000000000"
    },
    "host_portion": {
        "quads": "0.0.0.203",
        "hex": "000000CB",
        "binary": "00000000000000000000000011001011"
    },
    "network_size": 23,
    "number_of_ip_addresses": 512,
    "number_of_addressable_hosts": 510,
    "ip_address_range": [
        "192.168.112.0",
        "192.168.113.255"
    ],
    "broadcast_address": "192.168.113.255"
}
*/
```

#### String Report
```php
$string_report = $sub->getPrintableReport();
/*
192.168.112.203/23           Quads      Hex                           Binary
------------------ --------------- -------- --------------------------------
IP Address:        192.168.112.203 C0A870CB 11000000101010000111000011001011
Subnet Mask:         255.255.254.0 FFFFFE00 11111111111111111111111000000000
Network Portion:     192.168.112.0 C0A87000 11000000101010000111000000000000
Host Portion:            0.0.0.203 000000CB 00000000000000000000000011001011

Number of IP Addresses:      512
Number of Addressable Hosts: 510
IP Address Range:            192.168.112.0 - 192.168.113.255
Broadcast Address:           192.168.113.255
*/

// Printing the SubnetCalculator object will print the printable report.
print($sub);
/*
192.168.112.203/23           Quads      Hex                           Binary
------------------ --------------- -------- --------------------------------
IP Address:        192.168.112.203 C0A870CB 11000000101010000111000011001011
Subnet Mask:         255.255.254.0 FFFFFE00 11111111111111111111111000000000
Network Portion:     192.168.112.0 C0A87000 11000000101010000111000000000000
Host Portion:            0.0.0.203 000000CB 00000000000000000000000011001011

Number of IP Addresses:      512
Number of Addressable Hosts: 510
IP Address Range:            192.168.112.0 - 192.168.113.255
Broadcast Address:           192.168.113.255
*/
```

#### ipInSubnet
```php

$testIP = "192.168.112.1";
$sub = new IPv4\SubnetCalculator( '192.168.112.203', 23 );
$inSubnet = $sub->ipInSubnet($testIP);
echo $inSubnet ? "192.168.112.1 is in 192.168.112.203/23" : "192.168.112.1 is in 192.168.112.203/23";
```

#### nextSubnetInRange
```php

$nextIPSubnet = $sub->nextSubnetInRange(21,'192.168.96.0/19');
echo "The next /21 subnet up from 192.168.112.0/23 in the 192.168.96.0/19 is: $nextIPSubnet\n";
/*
The next /21 subnet up from 192.168.112.0/23 in the 192.168.96.0/19 is: 192.168.120.0/21
*/

```


Unit Tests
----------

```bash
$ cd tests
$ phpunit
```

[![Coverage Status](https://coveralls.io/repos/github/markrogoyski/ipv4-subnet-calculator-php/badge.svg?branch=master)](https://coveralls.io/github/markrogoyski/ipv4-subnet-calculator-php?branch=master)

Standards
---------

IPv4 Subnet Calculator (PHP) conforms to the following standards:

 * PSR-1 - Basic coding standard (http://www.php-fig.org/psr/psr-1/)
 * PSR-2 - Coding style guide (http://www.php-fig.org/psr/psr-2/)
 * PSR-4 - Autoloader (http://www.php-fig.org/psr/psr-4/)

License
-------

IPv4 Subnet Calculator (PHP) is licensed under the MIT License. 
