# Handle SEPA like a king

[![Build Status](https://secure.travis-ci.org/salesking/sepa_king.png)](http://travis-ci.org/salesking/sepa_king)
[![Code Climate](https://codeclimate.com/github/salesking/sepa_king.png)](https://codeclimate.com/github/salesking/sepa_king)
[![Coverage Status](https://coveralls.io/repos/salesking/sepa_king/badge.png)](https://coveralls.io/r/salesking/sepa_king)

We love building payment applications! So after developing the [DTAUS library for Ruby](https://github.com/salesking/king_dtaus) we move on with SEPA!


## Features

* Credit transfer initiation (pain.001.002.03)
* Debit transfer initiation (pain.008.002.02)
* Tested with Ruby 1.9.3 or 2.0.0


## Installation

    gem install sepa_king


## Examples

How to create the XML for **Direct Debit Initiation** (in german: "Lastschrift")

```ruby
# First: Create the main object
dd = SEPA::DirectDebit.new name:       'Gläubiger GmbH',
                           bic:        'BANKDEFFXXX',
                           iban:       'DE87200500001234567890',
                           identifier: 'DE98ZZZ09999999999'

# Second: Add transactions
dd.add_transaction name:                      'Zahlemann & Söhne GbR',
                   bic:                       'SPUEDE2UXXX',
                   iban:                      'DE21500500009876543210',
                   amount:                    39.99,
                   reference:                 'XYZ/2013-08-ABO/6789',
                   remittance_information:    'Vielen Dank für Ihren Einkauf!',
                   mandate_id:                'K-02-2011-12345',
                   mandate_date_of_signature: Date.new(2011,1,25),
                   requested_date:            Date.new(2013,08,31), # optional
                   local_instrument:          'CORE', # optional
                   batch_booking:             true # optional
dd.add_transaction ...

# Last: create XML string
xml_string = dd.to_xml
```


How to create the XML for **Credit Transfer Initiation** (in german: "Überweisung")

```ruby
# First: Create the main object
ct = SEPA::CreditTransfer.new name: 'Schuldner GmbH',
                              bic:  'BANKDEFFXXX',
                              iban: 'DE87200500001234567890'

# Second: Add transactions
ct.add_transaction name:                   'Telekomiker AG',
                   bic:                    'PBNKDEFF370',
                   iban:                   'DE37112589611964645802',
                   amount:                 102.50,
                   reference:              'XYZ-1234/123',
                   remittance_information: 'Rechnung vom 22.08.2013',
                   requested_date:         Date.new(2013,08,31), # optional
                   batch_booking:          true # optional
ct.add_transaction ...

# Last: create XML string
xml_string = ct.to_xml
```

Make sure to read the code and the specs!


## Changelog

https://github.com/salesking/sepa_king/releases


## Resources

* http://www.ebics.de/index.php?id=77
* SalesKing: http://salesking.eu


## License

Released under the MIT license

Copyright (c) 2013 Georg Leciejewski (SalesKing), Georg Ledermann (https://github.com/ledermann)
