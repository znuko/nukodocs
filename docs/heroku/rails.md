---
title: Rails for Heroku
---

# 参考

- [Heroku スターターガイド (Rails 6.x) | Heroku Dev Center](https://devcenter.heroku.com/ja/articles/getting-started-with-rails6#create-a-new-rails-app-or-upgrade-an-existing-one)



# 初期設定

Heroku 用アプリのデータベースは progresql を使う；

```
rails new myapp --database=postgresql
cd myapp
```

database を作成；

```
rails db:create
```

ここまでで、`rails s` で Yay! You’re on Rails! のページが表示される。

# デプロイ

多分 `rails new` のときに自動で `git init` はされている。

あとは今までの変更をコミットする；

```
git add .
git commit -m "init"
```

```
bundle exec rake -P
```