# Sets the base image
FROM node:24-alpine

# Create a user with perms to run the app
# -S : system user
# -G : add to a group
# Avoids running as root (avoid exploits)
RUN addgroup app && adduser -S -G app app

# set the working dir
WORKDIR /app

# copy package.json & lock to the workdir
# done before copying to use Docker's cache
COPY package*.json ./

# fix ownership / EACCESS perm denied
USER root

# change ownership of /app to app user
# chown -R user:group dir
RUN chown -R app:app .

USER app

RUN npm install

COPY . . 

EXPOSE 5173

CMD ["npm", "run", "dev"]