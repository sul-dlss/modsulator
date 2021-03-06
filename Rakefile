require 'rspec/core/rake_task'
require 'yard'

RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = 'spec/**/*_spec.rb'
  spec.exclude_pattern = 'spec/integration_tests/**/*_spec.rb'
end


# Larger integration/acceptance style tests (take several minutes to complete)
RSpec::Core::RakeTask.new(:integration_tests) do |spec|
  spec.pattern = 'spec/integration_tests/**/*_spec.rb'
end


YARD::Rake::YardocTask.new(:yard) do |t|
  t.files   = ['lib/**/*.rb']                # optional
  t.stats_options = ['--list-undoc']         # optional
end

task :lint do
  sh "ruby-lint lib/ bin/"
end

task :default  => :spec     # Default task is to just run shorter (unit) tests

task :all do
  Rake::Task["spec"].invoke
  Rake::Task["yard"].invoke
  Rake::Task["integration_tests"].invoke
  Rake::Task["lint"].invoke
end




# Set up default Rake tasks for cutting gems etc.
begin
  require 'bundler/setup'
rescue LoadError
  puts 'You must `gem install bundler` and `bundle install` to run rake tasks'
end
Bundler::GemHelper.install_tasks
