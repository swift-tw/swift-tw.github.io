require "rubygems"
require "pry-byebug"
require 'nokogiri'
require 'uri'

def header(layout: "page")
  <<-HEADER
---
layout: #{layout}
title: 
---
HEADER
end

def post_header(time)
  <<-HEADER
---
layout: post
title: 
date: #{time}
comments: true
paginate: true
categories: [Swift blog, Swift, Xcode]
---
HEADER
end

def parse_article(filename)
  f = File.read(filename)
  doc = Nokogiri::Slop(f)
  html = doc.css('article').children.to_html
  html
end

task :parse_file do
  filename = ENV['f']
  outputname = ENV['o']
  parsed_html = parse_article(filename)
  File.write(outputname,header + parsed_html)
end

task :download_post do
  url = ENV['url']
  `aria2c -s 16 -x 16 -j 16 #{url}`
  uri = URI(url)
  filename = File.basename(uri.path)
  origin_post_filename = "_origin_posts/#{filename}.html"
  `mv index.html.1 #{origin_post_filename}`
  html = parse_article(origin_post_filename)
  doc = Nokogiri::HTML(html)
  ts = doc.css('time').attribute('datetime').value
  t = DateTime.parse(ts)
  outputname = "_posts/"+ t.strftime("%Y-%m-%d") + "-#{filename}.html"
  File.write(outputname, post_header(t)+html)
end
