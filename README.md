# CloudPayments

CloudPayments ruby client (http://cloudpayments.eu/Docs/Integration)

[![Build Status](https://travis-ci.org/undr/cloud_payments.svg)](https://travis-ci.org/undr/cloud_payments)

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'cloud_payments'
```

And then execute:

```
$ bundle
```

Or install it yourself as:

```
$ gem install cloud_payments
```

## Usage

### Configuration

```ruby
CloudPayments.configure do |c|
  c.host = 'http://localhost:3000'    # By default, it is https://api.cloudpayments.ru
  c.public_key = ''
  c.secret_key = ''
  c.log = false                       # By default. it is true
  c.logger = Logger.new('/dev/null')  # By default, it writes logs to stdout
end
```

### Test method

```ruby
CloudPayments.client.ping
# => true
```

### Cryptogram-based payments

```ruby
tansaction = CloudPayments.client.payments.cards.charge(
  amount: 120,
  currency: 'RUB',
  ip_address: request.remote_ip,
  name: params[:name],
  card_cryptogram_packet: params[:card_cryptogram_packet]
)
# => {:metadata=>nil,
# :id=>12345,
# :amount=>120,
# :currency=>"RUB",
# :currency_code=>0,
# :invoice_id=>"1234567",
# :account_id=>"user_x",
# :email=>nil,
# :description=>"Payment for goods on example.com",
# :created_at=>#<DateTime: 2014-08-09T11:49:41+00:00 ((2456879j,42581s,0n),+0s,2299161j)>,
# :authorized_at=>#<DateTime: 2014-08-09T11:49:42+00:00 ((2456879j,42582s,0n),+0s,2299161j)>,
# :confirmed_at=>#<DateTime: 2014-08-09T11:49:42+00:00 ((2456879j,42582s,0n),+0s,2299161j)>,
# :auth_code=>"123456",
# :test_mode=>true,
# :ip_address=>"195.91.194.13",
# :ip_country=>"RU",
# :ip_city=>"Ufa",
# :ip_region=>"Bashkortostan Republic",
# :ip_district=>"Volga Federal District",
# :ip_lat=>54.7355,
# :ip_lng=>55.991982,
# :card_first_six=>"411111",
# :card_last_four=>"1111",
# :card_type=>"Visa",
# :card_type_code=>0,
# :issuer_bank_country=>"RU",
# :status=>"Completed",
# :status_code=>3,
# :reason=>"Approved",
# :reason_code=>0,
# :card_holder_message=>"Payment successful",
# :name=>"CARDHOLDER NAME",
# :token=>"a4e67841-abb0-42de-a364-d1d8f9f4b3c0"}
tansaction.class
# => CloudPayments::Transaction
tansaction.token
# => "a4e67841-abb0-42de-a364-d1d8f9f4b3c0"
```

## Contributing

1. Fork it ( https://github.com/undr/cloud_payments/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
