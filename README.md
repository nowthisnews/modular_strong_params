# ModularStrongParams

This is `StrongParameters` from Ruby on Rails, just... without ActionController. It was literally copied from [the source](https://github.com/rails/rails/blob/master/actionpack/lib/action_controller/metal/strong_parameters.rb) and reorganized so it can be used as module.

Error classes are now namespaced with `StrongParameters::Error`. Other explicit references to ActionController have been removed. Please get in touch if anything lingers.

## Installation

In your gemfile:

```
gem 'modular_strong_params', '~> 1.0.0'
```

## Usage

`lib/action_controller.rb` more or less demonstrates its use.

```ruby

require 'strong_parameters'

class MyAppClass
  include StrongParameters

  def params
    @_params ||= Parameters.new(method_that_returns_base_params_hash)
  end

  def params=(value)
    @_params = value.is_a?(Hash) ? Parameters.new(value) : value
  end
end
```

Those methods and the `method_that_returns_base_params_hash` will need to be adapted to your environment. Alternatively, you can turn any hash into a Parameters:

```
StrongParameters::Parameters.new(hash)
```

## Credit Where Credit's Due

Full credit for this code goes to those who contributed to this code in Rails.

### Maintenance

Since this code has been copied from Rails, it will need to be maintained separately. We cannot claim to keep up on that constantly. If you come across changes to the source that are not reflected here, please submit a PR with passing tests.

## License

Released under the [MIT License](http://www.opensource.org/licenses/MIT).
