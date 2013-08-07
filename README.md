# Muskox

A JSON Parser-Generator that takes a json-schema and converts it into a parser.

## Why?

Using a parser to handle inputs makes your app safe from attacks that rely on passing disallowed params, because disallowed params will either be ignored or rejected.

> Be definite about what you accept.(*) 
>
> Treat inputs as a language, accept it with a matching computational
> power, generate its recognizer from its grammar.
>
> Treat input-handling computational power as privilege, and reduce it
> whenever possible.

http://www.cs.dartmouth.edu/~sergey/langsec/postel-principle-patch.txt

## Installation

Add this line to your application's Gemfile:

    gem 'muskox'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install muskox

## Usage

```ruby
    # to generate a parser, call generate w/ a JSON-Schema
    parser = Muskox.generate({
        "title" => "Schema",
        "type" => "object",
        "properties" => {
          "number" => {
            "type" => "integer"
          }
        },
        "required" => ["number"]
      })

    # then call parse with the string you want to have parsed
    n = parser.parse "{\"number\": 1}"
    # => {"number" => 1}
    
    # invalid types are disallowed
    parser.parse "{\"number\": true}" rescue puts $!
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
