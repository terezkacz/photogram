source 'http://rubygems.org'

require 'open3'

class << File
  alias_method :old_symlink, :symlink
  alias_method :old_symlink?, :symlink?

  def symlink(old_name, new_name)
    #if on windows, call mklink, else self.symlink
    if RUBY_PLATFORM =~ /mswin32|cygwin|mingw|bccwin/
      #windows mklink syntax is reverse of unix ln -s
      #windows mklink is built into cmd.exe
      #vulnerable to command injection, but okay because this is a hack to make a cli tool work.
      stdin, stdout, stderr, wait_thr = Open3.popen3('cmd.exe', "/c mklink #{new_name} #{old_name}")
      wait_thr.value.exitstatus
    else
      self.old_symlink(old_name, new_name)
    end
  end

  def symlink?(file_name)
    #if on windows, call mklink, else self.symlink
    if RUBY_PLATFORM =~ /mswin32|cygwin|mingw|bccwin/
      #vulnerable to command injection because calling with cmd.exe with /c?
      stdin, stdout, stderr, wait_thr = Open3.popen3("cmd.exe /c dir #{file_name} | find \"SYMLINK\"")
      wait_thr.value.exitstatus
    else
      self.old_symlink?(file_name)
    end
  end
end

gem 'rails','~> 4.2'
gem 'tzinfo-data'
gem 'pg'
gem 'sass-rails'
gem 'uglifier'
gem 'coffee-rails'
gem 'jquery-rails'
gem 'turbolinks'
gem 'jbuilder'
gem 'sdoc', group: :doc
gem 'haml'
gem 'paperclip'
gem 'simple_form'
gem 'bootstrap-sass','~> 3.3.5'
gem 'devise', '~> 4.2'
gem 'acts_as_votable'
gem 'kaminari'
gem 'jquery-turbolinks'

group :development, :test do
  gem 'byebug'
  gem 'web-console'
  gem 'spring'

  gem 'capybara'
  gem 'rspec-rails'
  gem 'factory_girl_rails'
end
