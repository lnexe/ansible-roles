FROM node:12
LABEL name="AUTOMATION-TEST"

# Install Chrome

RUN echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' > /etc/apt/sources.list.d/chrome.list

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -

RUN set -x \
    && apt-get update \
    && apt-get install -y \
    google-chrome-stable

ENV CHROME_BIN /usr/bin/google-chrome

# Log versions

RUN set -x \
    && node -v \
    && npm -v \
    && google-chrome --version

RUN mkdir dwp-test

COPY . /dwp-test
RUN chmod 755 -R /dwp-test

WORKDIR /dwp-test

RUN npm install
RUN npm run webdriver
RUN npm run build

ENTRYPOINT [ "/bin/bash", "-c" ]
CMD [ "./built/test/akerbp/config/conf.docker.js" ]
