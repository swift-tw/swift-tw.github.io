require "rubygems"

task :parse_file do
  require 'nokogiri'
  filename = ENV['f']
  outputname = ENV['o']
  f = File.read(filename)
  doc = Nokogiri::Slop(f)
  header = <<-HEADER
---
layout: page
title: 
---
HEADER
  html = doc.css('article').children.to_html
  File.write(outputname,header+html)
end

