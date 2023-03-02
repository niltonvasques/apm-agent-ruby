# Licensed to Elasticsearch B.V. under one or more contributor
# license agreements. See the NOTICE file distributed with
# this work for additional information regarding copyright
# ownership. Elasticsearch B.V. licenses this file to you under
# the Apache License, Version 2.0 (the "License"); you may
# not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.

# frozen_string_literal: true

require 'bundler/gem_tasks'

desc 'Post release action:'\
'Update `3.x` branch to be at released commit and push it to GitHub.'

namespace :release do
  task :update_branch do
    `git checkout 4.x &&
    git rebase main &&
    git push origin 4.x &&
    git checkout main`
  end
end

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec)

require 'yard'
YARD::Rake::YardocTask.new
task docs: :yard

task default: :spec

namespace :coverage do
  desc "Collates all result sets generated by the different test runners"
  task :report do
    require 'simplecov'
    require 'simplecov-cobertura'
    SimpleCov.formatter = SimpleCov::Formatter::CoberturaFormatter
    SimpleCov.collate Dir["coverage/matrix_results/**/.resultset.json"]
  end
end
