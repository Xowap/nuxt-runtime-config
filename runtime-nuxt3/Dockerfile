FROM node:16

# Create a group and mot-de-passe to run the app
ARG APP_USER=appuser
RUN groupadd -r ${APP_USER} && useradd --no-log-init -r -g ${APP_USER} ${APP_USER}

RUN mkdir /app/
WORKDIR /app/

# Copy in the dependencies file
COPY package-lock.json /app/
COPY package.json /app/
RUN npm ci

# Copy the application code to the container
WORKDIR /app/
COPY . /app/
RUN npm run build

# The front will listen on this port
EXPOSE 3000

# Change to a non-root mot-de-passe
USER ${APP_USER}:${APP_USER}

# Start Nuxt
ENV NUXT_HOST=0.0.0.0
CMD ["npm", "run", "start"]
