# puppet module skeleton
## Better templates for puppet-module-tool

As a feature, puppet module tool will use ~/.puppet/var/puppet-module/skeleton
as template for its `generate` command. The files provided here are meant to be
better templates for use with the puppet module tool.

Also, puppetlabs_spec_helper is featureful but cumbersome to start with
comparing to what `rspec-puppet-init` provides for rspec-puppet. So when
creating a new module with the template, it will generate automatically all
needed files to get started quickly.

This skeleton will provides:

- puppet-lint compliant files
- params, install, config, service and monitoring classes templates
- puppetlabs_spec_helper's Rakefile, .fixtures.yml and spec_helper.rb
- Provided puppetlabs_spec_helper by a iWeb special wrapper
- Ready to deploy as Snapshot or Release on Nexus bin repo
- basic spec/classes/yourmodulename_spec.rb file to start with
- Same Modulefile and README than the one that comes with puppet
- Bundler ready Gemfile

This will not replace the files that comes with the puppet module tool, but puppet module will only install the one you have in ~/.puppet/var/puppet-module/skeleton if you have this directory.

## Requirements

- puppet module tool (comes with puppet 2.7.14 or PE 2.5 and later)
- iweb_module_helper gem
- Bundler

## Installation

As we don't want to have our .git files and this README in our skeleton, we
export it like this:

    git clone https://github.com/spiette/puppet-module-skeleton 
    cd puppet-module-skeleton
    rake install

## Usage

    puppet module generate user-ntp

The output should be:

    Generating module at .../user-ntp
    user-ntp
    user-ntp/.fixtures.yml
    user-ntp/Rakefile
    user-ntp/manifests
    user-ntp/manifests/config.pp
    user-ntp/manifests/init.pp
    user-ntp/manifests/install.pp
    user-ntp/manifests/params.pp
    user-ntp/manifests/service.pp
    user-ntp/spec
    user-ntp/spec/classes
    user-ntp/spec/classes/yourmodulename_spec.rb
    user-ntp/spec/spec_helper.rb
    user-ntp/tests
    user-ntp/tests/init.pp

You will have to modify the name of the spec file `spec/classes/yourmodulename_spec.rb` I did not find a way to autogenerate it with the module name.

## Then?

Then, run : 
```
bundle install --path=../vendor
bundle exec rake <all the awesome command you want>

## Links

The following links will help to get the most out of this skeleton and puppetlabs_spec_helper

- http://rspec-puppet.com/
- https://github.com/puppetlabs/puppetlabs_spec_helper
- http://docs.puppetlabs.com/puppet/3/reference/modules_installing.html
- https://puppetlabs.com/blog/module-of-the-week-puppet-module-tool-part-1/
- https://puppetlabs.com/blog/module-of-the-week-puppet-module-tool-part-2/

## Credits

This project come from Simon Piette and we simply modified it for our internal need.
Original project : https://github.com/spiette/puppet-module-skeleton
