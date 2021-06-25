### docker for rbenv的配置参考
```dockerfile
FROM swift:5.3.3-bionic-slim

COPY bin/linux/*.so /usr/lib/

COPY bin/linux/clang-format bin/linux/swiftlint RubySwiftlint/RubySwiftlint-0.1.0.gem  /usr/bin/

ENV PATH=/usr/local/rbenv/bin:$PATH \
    RBENV_ROOT=/usr/local/rbenv \
    CONFIGURE_OPTS=--disable-install-doc \
    PATH=/usr/local/rbenv/bin:/usr/local/rbenv/shims:$PATH

RUN apt-get update && apt-get install -y \ 
    curl \
    gcc \
    g++ \
    git \
    git-lfs \
    libssl-dev \
    make \
    zlib1g-dev && \
    git clone git://github.com/rbenv/rbenv.git /usr/local/rbenv && \
    git clone git://github.com/rbenv/ruby-build.git /usr/local/rbenv/plugins/ruby-build && \
    /usr/local/rbenv/plugins/ruby-build/install.sh && \
    echo 'export RBENV_ROOT=/usr/local/rbenv' >> /etc/profile.d/rbenv.sh && \
    echo 'export PATH=/usr/local/rbenv/bin:$PATH' >> /etc/profile.d/rbenv.sh && \
    echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh && \
    echo 'export RBENV_ROOT=/usr/local/rbenv' >> /root/.bashrc && \
    echo 'export PATH=/usr/local/rbenv/bin:$PATH' >> /root/.bashrc && \
    echo 'eval "$(rbenv init -)"' >> /root/.bashrc && \
    echo 'export CONFIGURE_OPTS=--disable-install-doc' >> /root/.bashrc && \
    echo 'export PATH=/usr/local/rbenv/bin:/usr/local/rbenv/shims:$PATH' >> /root/.bashrc && \
    eval "$(rbenv init -)"; rbenv install 3.0.1 && \
    eval "$(rbenv init -)"; rbenv global 3.0.1 && \
    eval "$(rbenv init -)"; gem update --system && \
    eval "$(rbenv init -)"; gem install /usr/bin/RubySwiftlint-0.1.0.gem && \
    rbenv rehash && \
    rm -r /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    rm -rf /usr/bin/RubySwiftlint-0.1.0.gem
```
