source "https://rubygems.org"

# Same versions GitHub Pages uses to build the site
gem "github-pages", group: :jekyll_plugins

# Needed to run `jekyll serve` on Ruby 3+
gem "webrick"

# Windows and JRuby do not include zoneinfo files
platforms :windows, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end
