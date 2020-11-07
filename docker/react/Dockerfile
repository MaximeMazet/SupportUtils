# pull official base image
FROM node:14.15.0-slim


WORKDIR /var/www/html

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# start app
CMD ["npm", "start"]
