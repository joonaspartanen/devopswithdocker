FROM ruby:2.6.0

COPY ./rails-example-project .
#RUN apt-get update && apt-get install -y nodejs
RUN bundle install
RUN gem install execjs
RUN gem install therubyracer
RUN rails db:migrate
RUN rails s
#RUN gem update --system 1.8.7
#RUN apt-get update && apt-get install -y curl
#RUN curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash
#RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
#RUN gem install bundler:1.17.2
#RUN bundle install

CMD ["/bin/bash"]
