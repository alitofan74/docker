FROM node:20-slim

# Install Puppeteer dependencies
RUN apt-get update && apt-get install -y \
    wget curl unzip fontconfig locales libnss3 libatk1.0-0 libatk-bridge2.0-0 \
    libcups2 libx11-xcb1 libxcomposite1 libxdamage1 libxrandr2 libgbm1 libasound2 \
    libpangocairo-1.0-0 libpango-1.0-0 libxss1 libgtk-3-0 libxshmfence1 \
    --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN npm install -g pm2

RUN npm install

WORKDIR /app

# Copy all node service files
COPY node-services/ /app/

# Install dependencies for each service (safe install)
RUN cd /app/wa-service && npm install || true
# RUN cd /app/notifier-service && npm install || true
# RUN cd /app/converter-service && npm install || true

CMD ["pm2-runtime", "pm2.config.js"]