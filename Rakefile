require 'html/proofer'
require 'rspec/core/rake_task'

RSpec::Core::RakeTask.new(:spec)

SITE_DIR = './_site'

def jekyll(cmd)
  sh "bundle exec jekyll #{cmd}"
end

def remove_site
  sh "rm -rf #{SITE_DIR}" if Dir.exists?(SITE_DIR)
end

def build_site
  remove_site
  jekyll 'build'
end

'Run the Markdown specs and HTML Proofer'
task :ci do
  build_site
  sh 'grunt test'
  Rake::Task['spec'].invoke
  HTML::Proofer.new(SITE_DIR, cache: { timeframe: '2w' } ).run
end

'Run the site locally on localhost:4000'
task :dev do
  remove_site
  build_site
  jekyll 'serve --watch --drafts'
end

task default: :ci