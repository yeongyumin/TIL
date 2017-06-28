# 헤로쿠

## 사전 준비

버전관리가 `git`이어야 함.

heroku의 데이터베이스는 postgre를 사용하므로 젬파일을 production을 분리한다.

```ruby

source 'https://rubygems.org'

gem 'rails',        '5.0.3'
gem 'puma',         '3.9.1'
gem 'sass-rails',   '5.0.6'
gem 'uglifier',     '3.2.0'
gem 'coffee-rails', '4.2.2'
gem 'jquery-rails', '4.3.1'
gem 'turbolinks',   '5.0.1'
gem 'jbuilder',     '2.6.4'

group :development, :test do
  gem 'sqlite3', '1.3.13'
  gem 'byebug',  '9.0.6', platform: :mri
end

group :development do
  gem 'web-console',           '3.5.1'
  gem 'listen',                '3.0.8'
  gem 'spring',                '2.0.2'
  gem 'spring-watcher-listen', '2.0.1'
end

group :production do
  gem 'pg', '0.20.0'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]

```

## 커맨드

`heroku version`

`heroku login`

`heroku keys:add`

`git push heroku master`

`heroku run rails db:migrate`

## help

`heroku help`