FROM node:19-alpine AS builder

# Let's make an app folder
RUN mkdir /app

# [OPTIONAL] if we have a data folder we can also replace the command above for: (eg. if we have sqlite db in the data folder)
#RUN mkdir /app && mkdir /app/data

# Copy everything from the current directory to the /app folder
COPY . /app

RUN cd /app && yarn install && yarn build

# [OPTIONAL] if we have our database in the data folder and want to copy the database:
# RUN cd /app && yarn install && echo "DB_PATH=/app/data/db.sqlite" > /app/.env && yarn build


# Final container
FROM node:19-alpine

# Let's make an app folder
RUN mkdir /app

# copy the build from the builder container to the app folder in this container
COPY --from=builder /app/build /app/build
COPY --from=builder /app/package.json /app/yarn.lock /app/

RUN cd /app && yarn install --production && yarn cache clean

WORKDIR /app
CMD ["node", "build/index.js"]





