FROM mcr.microsoft.com/playwright:v1.31.2-jammy

RUN apt-get update -qqy \
  && apt-get -qqy install \
       dumb-init gnupg wget ca-certificates apt-transport-https \
       ttf-wqy-zenhei \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN npx playwright install-deps chromium

RUN ln -s /ms-playwright/chromium-1048/chrome-linux/chrome /usr/bin/google-chrome

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

# ENTRYPOINT ["tail", "-f", "/dev/null"]