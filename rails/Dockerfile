FROM ruby:3.3.9

# 開発に必要なパッケージをインストール
RUN apt-get update -qq && \
    apt-get install --no-install-recommends -y \
    build-essential \
    default-libmysqlclient-dev \
    git \
    curl \
    libjemalloc2 \
    libvips \
    nodejs \
    libyaml-dev \
    pkg-config \
    vim

# 作業ディレクトリを設定
RUN mkdir /myapp
WORKDIR /myapp

# 開発環境の設定
ENV RAILS_ENV="development" \
    BUNDLE_PATH="/usr/local/bundle"

# Gemfileをコピーしてインストール
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN bundle install

# アプリケーションコードをコピー
COPY . .

# Entrypointに実行権限を付与して上書き
COPY entrypoint.sh /usr/bin/entrypoint.sh
RUN chmod +x /usr/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]
