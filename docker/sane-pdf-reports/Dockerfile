FROM demisto/python3-deb:3.8.2.6712

WORKDIR "/app"

COPY ./get_build_artifacts.py .

SHELL ["/bin/bash", "-c"]
RUN apt-get update -y -q && \
    apt-get install -y -q nodejs \
    npm gconf-service \
    libasound2 libatk1.0-0 libatk-bridge2.0-0 \
    libc6 libcairo2 libcups2 libdbus-1-3 \
    libexpat1 libfontconfig1 libgcc1 \
    libgconf-2-4 libgdk-pixbuf2.0-0 \
    libglib2.0-0 libgtk-3-0 libnspr4 \
    libpango-1.0-0 libpangocairo-1.0-0 \
    libstdc++6 libx11-6 libx11-xcb1 libxcb1 \
    libxcomposite1 libxcursor1 libxdamage1 \
    libxext6 libxfixes3 libxi6 libxrandr2 \
    libxrender1 libxss1 libxtst6 \
    ca-certificates fonts-liberation \
    libappindicator1 libnss3 lsb-release \
    xdg-utils wget \
    && rm -rf /var/lib/apt/lists/*
RUN npm i puppeteer@1.2.0 && ln -s /app/node_modules/puppeteer/.local-chromium/linux-*/chrome-linux/chrome /usr/bin/chromium-browser

RUN python get_build_artifacts.py --project sane-reports --branch master --filter "sane-report$" \
    && mv sane-report sane-report.tar && tar -xvf sane-report.tar && rm -f sane-report.tar
