FROM mcr.microsoft.com/playwright:v1.31.2-jammy

RUN apt-get update -qqy \
  && apt-get -qqy install \
       dumb-init gnupg wget ca-certificates apt-transport-https \
       ttf-wqy-zenhei \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN npx playwright install-deps chromium

RUN ln -s /ms-playwright/chromium-1048/chrome-linux/chrome /usr/bin/google-chrome