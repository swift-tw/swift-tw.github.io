require "rubygems"

task :parse_file do
  require 'nokogiri'
  filename = ENV['f']
  outputname = ENV['o']
  f = File.read(filename)
  doc = Nokogiri::Slop(f)
  h = doc.css('article').children.to_html
  File.write(outputname,h)
end

