# Use the latest stable Node.js Debian-based slim version
FROM node:22-slim

# Install common dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    software-properties-common

# Install Google Chrome
RUN curl -sSL https://dl-ssl.google.com/linux/linux_signing_key.pub | gpg --dearmor -o /usr/share/keyrings/google-chrome-keyring.gpg \
    && echo "deb [arch=amd64 signed-by=/usr/share/keyrings/google-chrome-keyring.gpg] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update \
    && apt-get install -y google-chrome-stable

# Install Firefox
RUN apt-get update \
    && apt-get install -y firefox-esr

# Install Microsoft Edge
RUN curl -sSL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o /usr/share/keyrings/microsoft-edge-keyring.gpg \
    && echo "deb [arch=amd64 signed-by=/usr/share/keyrings/microsoft-edge-keyring.gpg] https://packages.microsoft.com/repos/edge stable main" > /etc/apt/sources.list.d/microsoft-edge.list \
    && apt-get update \
    && apt-get install -y microsoft-edge-stable

# Cleanup
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set environment variables for each browser to be recognized by Selenium or other tools
ENV CHROME_BIN=/usr/bin/google-chrome
ENV FIREFOX_BIN=/usr/bin/firefox
ENV EDGE_BIN=/usr/bin/microsoft-edge

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .
