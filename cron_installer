#!/usr/bin/env ruby
require 'fileutils'

class Cronjob
  
  def self.install
    root = `pwd`.gsub("\n",'')
    root = root.split('/')
    root = "#{root[0..root.size-3].join('/')}/current"
    env = 'development'
    backup_crontab = 'crontab -l > log/my_crontab'
    puts 'backuping previous crontab..'
    system(backup_crontab)
    system("crontab -l > log/crontab_backup_#{Time.now.to_s.gsub(' ','_')}")

    script_execute = "
0 * * * * /bin/bash -l -c 'cd #{root} && ./script/update_point.rb #{env} >> log/update_point.log 2>&1'
    "

    File.open("log/my_crontab", 'w+') {|f| f.write(script_execute) }
    system('crontab log/my_crontab')
    puts "done"
    puts 'crontab list'
    system('crontab -l')
  end
end

Cronjob.install
