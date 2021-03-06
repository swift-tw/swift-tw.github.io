require "rubygems"
require "pry-byebug"
require 'nokogiri'
require 'uri'

def header(layout: "page", title:"")
  <<-HEADER
---
layout: #{layout}
title: #{title}
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
  doc.css('footer').remove
  html = doc.css('article').children.to_html
  html
end

task :parse_file do
  filename = ENV['f']
  outputname = ENV['o']
  parsed_html = parse_article(filename)
  File.write(outputname,header + parsed_html)
end

task :download_page do
  url = ENV['url']
  `aria2c -s 16 -x 16 -j 16 #{url}`
  uri = URI(url)
  filename = File.basename(uri.path)
  origin_post_filename = "_origin_html/#{filename}.html"
  `mv index.html.1 #{origin_post_filename}`
  html = parse_article(origin_post_filename)
  File.write("#{filename}.html",header + html)
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

def replace_at_css(old_doc, new_doc, css)
    latest_builds = new_doc.css(css)
    current_latest_builds = old_doc.css(css)[0]
    current_latest_builds.replace(latest_builds)
end

def extract_time_node(timenode)
 timenode.to_h.merge({"content" => timenode.content})
end

def extract_osx_build_node(n)
  {
    "release" => {"href" => "http://swift.org" + n.css(".download .release a")[0]['href'] },
    "debug" => {"href" => "http://swift.org" + n.css(".download .debug a")[0]['href'] },
    "time" => extract_time_node(n.css(".date time")[0])
  }
end

def extract_ubuntu_build_node(n)
  {
    "release" => {"href" => "http://swift.org" + n.css(".download .release a")[0]['href'],
                  "content" => n.css(".download .release a")[0].content },
    "pgp" => {"href" => "http://swift.org" + n.css(".download .release a")[1]['href']},
    "time" => extract_time_node(n.css(".date time")[0])
  }
end

task :update_download_page do
  url = "https://swift.org/download/"
  `aria2c -s 16 -x 16 -j 16 #{url}`
  uri = URI(url)
  filename = File.basename(uri.path)
  origin_post_filename = "_origin_html/#{filename}.html"
  `mv index.html.1 #{origin_post_filename}`
  html = parse_article(origin_post_filename)
  doc = Nokogiri::HTML(html)
  latest_builds = doc.css("#latest-builds .download a").map{|n| "http://swift.org#{n['href']}"}
  File.write("_data/latest_build_urls.yml", latest_builds.to_yaml)
  latest_build_times = doc.css("#latest-builds .date time").map{|n| extract_time_node(n)}
  File.write("_data/latest_build_times.yml", latest_build_times.to_yaml)
  osx_build_nodes = doc.css("#osx-builds > tbody > tr")
  osx_build_infos = osx_build_nodes.map{|n| extract_osx_build_node(n)}
  File.write("_data/osx_builds.yml", osx_build_infos.to_yaml)
  ubuntu_15_builds_nodes = doc.css("#linux-builds")[0].css("tbody tr")
  ubuntu_15_builds = ubuntu_15_builds_nodes.map{|n| extract_ubuntu_build_node(n)}
  File.write("_data/ubuntu_15_builds.yml", ubuntu_15_builds.to_yaml)
  ubuntu_14_builds_nodes = doc.css("#linux-builds")[1].css("tbody tr")
  ubuntu_14_builds = ubuntu_14_builds_nodes.map{|n| extract_ubuntu_build_node(n)}
  File.write("_data/ubuntu_14_builds.yml", ubuntu_14_builds.to_yaml)
end
