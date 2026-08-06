source "https://rubygems.org"

# Siteyi Netlify derler; bu dosya hem oradaki derleme hem de
# `bundle exec jekyll serve` ile yerel önizleme için kullanılır.
gem "jekyll", "~> 4.3"

# Ruby 3+ ile birlikte gelmediği için gerekli (jekyll serve)
gem "webrick", "~> 1.8"

# Aşağıdaki sabitler YALNIZCA eski Ruby'ler içindir.
# Bu makinede yalnızca sistem Ruby'si (2.6) var ve yeni sürümler Ruby 3+ istiyor.
# Netlify daha yeni bir Ruby kullanırsa bu blok atlanır ve güncel sürümler kurulur.
if RUBY_VERSION < "3.0"
  gem "ffi", "< 1.17"
  gem "jekyll-sass-converter", "~> 2.2"
  gem "sassc", "~> 2.4"
end
