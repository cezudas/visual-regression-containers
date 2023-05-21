FROM cezudas/playwright-latest-headless-chrome:latest

RUN useradd headless --shell /bin/bash --create-home \
  && usermod -a -G sudo headless \
  && echo 'ALL ALL = (ALL) NOPASSWD: ALL' >> /etc/sudoers \
  && echo 'headless:nopassword' | chpasswd

RUN mkdir /data && chown -R headless:headless /data

USER headless

ENTRYPOINT ["/usr/bin/dumb-init", "--", \
            "/usr/bin/google-chrome", \
            "--disable-gpu", \
            "--headless", \
            "--disable-dev-shm-usage", \
            "--remote-debugging-address=0.0.0.0", \
            "--remote-debugging-port=9222", \
            "--user-data-dir=/data"]