# frozen_string_literal: true

source "https://rubygems.org"

git_source(:github) do |repo_name|
  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
  "https://github.com/#{repo_name}.git"
end

# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
gem "jekyll", "~> 3.9"

gem "kramdown-parser-gfm" # needed for kramdown

# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "the-plain", github: "heiswayi/the-plain", tag: "v4.0.0"

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-compose" # add some useful commands to create new posts
  gem "jekyll-feed", "~> 0.12"
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem "tzinfo-data", platforms: %i[mingw mswin x64_mingw jruby]

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.0" if Gem.win_platform?
