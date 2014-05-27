require 'rake'
require 'rspec/core/rake_task'
task default: :spec
task spec: 'spec:all'

namespace :spec do
  roles = %w(app proxy)
  task all: roles

  roles.each do |role|
    RSpec::Core::RakeTask.new(role.to_sym) do |t|
      ENV['ROLE'] = role
      t.pattern = "spec/#{role}/*_spec.rb"
    end
  end
end



