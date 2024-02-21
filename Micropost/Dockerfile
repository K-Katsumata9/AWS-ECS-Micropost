FROM ruby:3.3.0
RUN apt-get update -qq && apt-get install -y build-essential nodejs default-mysql-client
# Create app user
RUN groupadd -g 1000 app && useradd -u 1000 app -g app

# Set working directory and Bundle Install
WORKDIR /micropost
COPY Gemfile .
COPY Gemfile.lock .
RUN bundle install

# Copy source code
COPY --chown=app:app . /micropost

# Create public volume
RUN mkdir /public
RUN chown app:app /public
VOLUME /public

# Set working directory and application user
WORKDIR /micropost
USER app
