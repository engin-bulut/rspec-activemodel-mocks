source "https://rubygems.org"

gemspec

%w[rspec rspec-core rspec-expectations rspec-mocks rspec-support].each do |lib|
  library_path = File.expand_path("../../#{lib}", __FILE__)
  if File.exist?(library_path) && !ENV['USE_GIT_REPOS']
    gem lib, :path => library_path
  else
    gem lib, :git => "git://github.com/rspec/#{lib}.git"
  end
end

gem 'sqlite3'

### deps for rdoc.info
group :documentation do
  gem 'yard',          '0.8.7.3', :require => false
  gem 'redcarpet',     '2.3.0'
  gem 'github-markup', '1.0.0'
end

case version = ENV.fetch('RAILS_VERSION', '4.2.4')
when /\Amaster\z/, /stable\z/
  gem "activerecord", :github => "rails/rails", :branch => version
  gem "activemodel", :github => "rails/rails", :branch => version
  gem "activesupport", :github => "rails/rails", :branch => version
else
  gem "activerecord", version
  gem "activemodel", version
  gem "activesupport", version
end

if version < '4.0.0'
  gem "test-unit", '~> 3' if (version >= '3.2.22' || version == '3-2-stable')
else
  gem "minitest", :require => false
end

if RUBY_VERSION < '2.0.0' && !!(RbConfig::CONFIG['host_os'] =~ /cygwin|mswin|mingw|bccwin|wince|emx/)
  gem 'ffi', '< 1.9.15' # allow ffi to be installed on older rubies on windows
elsif RUBY_VERSION < '1.9'
  gem 'ffi', '< 1.9.19' # ffi dropped Ruby 1.8 support in 1.9.19
else
  gem 'ffi', '~> 1.9.25'
end

gem "i18n", '< 0.7.0' if RUBY_VERSION < '1.9.3'
