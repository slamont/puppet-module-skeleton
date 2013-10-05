require 'puppetlabs_spec_helper/rake_tasks'

# Configured to be recognizable by Jenkins warnings plugin
require 'puppet-lint/tasks/puppet-lint'
PuppetLint.configuration.ignore_paths = ["vendor/**/*.pp", "spec/**/*.pp"]
PuppetLint.configuration.log_format =
  "%{path}:%{linenumber}:%{check}:%{KIND}:%{message}"

# Used by Jenkins to show tests report.
require 'ci/reporter/rake/rspec'
ENV['CI_REPORTS'] = 'reports'

# Invoked by Jenkins to validate manifest syntax
require 'puppet/face'
desc "Perform puppet parser's validation on manifests"
task :validate do
  Puppet::Face[:parser, '0.0.1'].validate(FileList['**/*.pp'].exclude('vendor/**/*.pp', 'spec/**/*.pp').join())
end

require 'erb'
require 'open3'

desc "Check erb syntax for template"
task :erb do
  FileList['**/*.erb'].each do |template|
    # exclude the vendor/ dir
    next if template =~ /vendor/

      puts "Evaluating (erb) template syntax -  #{template}"
      Open3.popen3('ruby -Ku -c') do |stdin, stdout, stderr|
        stdin.puts(ERB.new(File.read(template), nil, '-').src)
        stdin.close
        if error = ((stderr.readline rescue false))
          puts template + error[1..-1].sub(/^[^:]*:\d+: /, '')
        end
        stdout.close rescue false
        stderr.close rescue false
      end
  end
end

task :default => [:lint, :erb, :validate, :spec ]

desc "Run all tasks for a release"
task :release => [:spec_prep, :spec_standalone, :spec_clean, :clean, :build ]

