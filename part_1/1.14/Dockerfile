FROM ruby:2.6.0

WORKDIR /usr/app/ruby

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs
RUN git clone https://github.com/docker-hy/rails-example-project.git /usr/app/ruby
RUN gem install bundler
RUN bundle install
RUN rails db:migrate

EXPOSE 3000

CMD rails s
