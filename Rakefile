def log(string)
  color = 33
  puts "\033[#{color}m * #{string}\033[0m"
end

desc 'Compiles LESS from source/stylesheets into home.css'
task :less do
  require 'bundler/setup'
  require 'less'

  log 'Compiling LESS...'

  parser = Less::Parser.new :paths => 'lib/assets/stylesheets', :filename => '_home.less'
  css = ''

  File.open 'lib/assets/stylesheets/_home.less' do |f|
    css = parser.parse(f.read).to_css(:compress => true)
  end

  File.open 'lib/assets/stylesheets/home.css', 'w' do |f|
    f.write css
  end
end

desc 'Install dependencies and clone the library'
task :install do
  log 'Installing dependencies...'
  sh 'bundle install --deployment'

  library_dir = "source"
  unless Dir.exists? library_dir
    log 'Getting latest version of the Library...'
    sh "git clone git@github.com/displague/library.git #{library_dir}"
  end
end

desc 'Update to the latest version of docsmith'
task :update do
  log 'Pulling the latest version of docsmith...'
  sh 'git pull origin master'

  log 'Updating dependencies...'
  sh 'bundle install --deployment'
end

desc 'Start a local docsmith development server'
task :server do
  log 'Starting docsmith development server...'
  sh 'bundle exec middleman server --reload-paths=lib/partials,lib/layouts,lib/assets/stylesheets'
end

task :default => [:less]
