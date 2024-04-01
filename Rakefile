# frozen_string_literal: true

require "bundler/gem_tasks"
require "rake/testtask"

Rake::TestTask.new do |t|
  t.ruby_opts = %w[-w]
  t.ruby_opts << "-rdevkit" if RbConfig::CONFIG["host_os"].include?("mingw")

  t.libs << "test"
  t.test_files = FileList["test/**/test_*.rb"]
end

task default: :test
