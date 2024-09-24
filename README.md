# CarrierWave for Mongoid

[![Gem Version](http://img.shields.io/gem/v/carrierwave-mongoid.svg)](https://rubygems.org/gems/carrierwave-mongoid)
[![Build Status](https://github.com/carrierwaveuploader/carrierwave-mongoid/workflows/CI/badge.svg?branch=master)](https://github.com/carrierwaveuploader/carrierwave-mongoid/actions?query=workflow%3ACI)
[![Gem Downloads](https://img.shields.io/gem/dt/carrierwave-mongoid.svg)](https://rubygems.org/gems/carrierwave-mongoid)

This functionality used to be part of CarrierWave but has since been extracted
into this gem.

## Installation

Install the latest release:

    gem install carrierwave-mongoid

Require it in your code:

```ruby
require 'carrierwave/mongoid'
```

Or, in Rails you can add it to your Gemfile:

```ruby
gem 'carrierwave-mongoid', :require => 'carrierwave/mongoid'
```


## Getting Started

Follow the "Getting Started" directions in the main
[Carrierwave repository](https://github.com/carrierwaveuploader/carrierwave/).

Now you can cache files by assigning them to the attribute; they will
automatically be stored when the record is saved. Ex:

```ruby
u = User.new
u.avatar = File.open('somewhere')
u.save!
```

## Version differences

| Version   | Notes                                                                           |
|-----------|---------------------------------------------------------------------------------|
| ~> 1.1.0  | ([compare][compare-1.1], [dependencies][deps-1.1]) Mongoid 7.0 support          |
| ~> 1.0.0  | ([compare][compare-1.0], [dependencies][deps-1.0]) Carrierwave 1.x support      |
| ~> 0.10.0 | ([compare][compare-0.10], [dependencies][deps-0.10]) Mongoid 6.0  support       |
| ~> 0.9.0  | ([compare][compare-0.9], [dependencies][deps-0.9]) Carrierwave 0.11 support     |
| ~> 0.8.0  | ([compare][compare-0.8], [dependencies][deps-0.8]) Mongoid 5 support, bug fixes |
| ~> 0.7.0  | ([compare][compare-0.7], [dependencies][deps-0.7]) Mongoid 3 & 4, bug fixes     |
| ~> 0.6.0  | ([compare][compare-0.6], [dependencies][deps-0.6]) Mongoid 3 & 4, bug fixes     |
| ~> 0.5.0  | ([compare][compare-0.5], [dependencies][deps-0.5]) Mongoid::Paranoia support    |
| ~> 0.4.0  | ([compare][compare-0.4], [dependencies][deps-0.4]) Carrierwave bump             |
| ~> 0.3.0  | ([compare][compare-0.3], [dependencies][deps-0.3]) Mongoid >= 3.0               |
| ~> 0.2.0  | ([compare][compare-0.2], [dependencies][deps-0.2]) Rails >= 3.2, Mongoid ~> 2.0 |
| ~> 0.1.0  | ([compare][compare-0.1], [dependencies][deps-0.1]) Rails <= 3.1                 |

[compare-1.1]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v1.0.0...v1.1.0
[compare-1.0]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.10.0...v1.0.0
[compare-0.10]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.9.0...v0.10.0
[compare-0.9]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.8.1...v0.9.0
[compare-0.8]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.7.1...v0.8.1
[compare-0.7]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.6.3...v0.7.1
[compare-0.6]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.5.0...v0.6.3
[compare-0.5]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.4.0...v0.5.0
[compare-0.4]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.3.1...v0.4.0
[compare-0.3]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.2.1...v0.3.1
[compare-0.2]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.1.7...v0.2.2
[compare-0.1]: https://github.com/carrierwaveuploader/carrierwave-mongoid/compare/v0.1.1...v0.1.7

[deps-1.1]: https://rubygems.org/gems/carrierwave-mongoid/versions/1.1.0
[deps-1.0]: https://rubygems.org/gems/carrierwave-mongoid/versions/1.0.0
[deps-0.10]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.10.0
[deps-0.9]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.9.0
[deps-0.8]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.8.1
[deps-0.7]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.7.1
[deps-0.6]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.6.3
[deps-0.5]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.5.0
[deps-0.4]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.4.0
[deps-0.3]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.3.1
[deps-0.2]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.2.2
[deps-0.1]: https://rubygems.org/gems/carrierwave-mongoid/versions/0.1.7

### Changes from earlier versions of CarrierWave <= 0.5.6

CarrierWave used to have built-in Mongoid support. This gem replaces that
support and only supports Mongoid ~> 2.1

You can use `upload_identifier` to retrieve the original name of the uploaded file.

In the earlier version, the mount_uploader-method for mongoid had been defined
in lib/carrierwave/orm/mongoid. This code has been moved to
carrierwave/mongoid. If you update from earlier versions, don't forget to adjust
your require accordingly in your carrierwave-initializer.

The default mount column used to be the name of the upload column plus
`_filename`. Now it is simply the name of the column. Most of the time, the
column was called `upload`, so it would have been mounted to `upload_filename`.
If you'd like to avoid a database migration, simply use the `:mount_on` option
to specify the field name explicitly. Therefore, you only have to add a
`_filename` to your column name. For example, if your column is called
`:upload`:

```ruby
class Dokument
  mount_uploader :upload, DokumentUploader, mount_on: :upload_filename
end
```

## Known issues and limitations

Note that files mounted in embedded documents aren't saved when parent documents
are saved. By default, mongoid does not cascade callbacks on embedded
documents. In order to save the attached files on embedded documents, you must
either explicitly call save on the embedded documents or you must configure the
embedded association to cascade the callbacks automatically. For example:

```ruby
class User
  embeds_many :pictures, cascade_callbacks: true
end
```

You can read more about this [here](https://github.com/carrierwaveuploader/carrierwave/issues/81)
