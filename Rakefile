require 'rubygems'
require 'net/ssh'
require File.expand_path(File.dirname(__FILE__) + '/lib/moby')

desc 'update site from remote repo'
task :update do

 user = 'jeffkreeftmeijer'
 repo = 'jeffkreeftmeijer.com'

 Net::SSH.start('67.23.79.117', 'jeff') do |ssh|
   ssh.exec(
    "rm -rf #{repo} && " <<
    "git clone -q git://github.com/#{user}/#{repo}.git && " <<
    "/opt/ruby-enterprise/bin/jekyll #{repo} _new_site --pygments && " <<
    "rm -rf _site && " <<
    "mv _new_site _site && " <<
    "rake -f #{repo}/Rakefile moby:fetch")
  end
end

namespace :moby do
  desc 'fetch the newest image from mobypicture'
  task :fetch do
    Moby.fetch
  end

  desc 'fetch the newest image every fifteen minutes'
  task :loop do
    loop { Moby.fetch; sleep 900 }
  end
end
