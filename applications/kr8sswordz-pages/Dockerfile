FROM docker pull registry.cn-hangzhou.aliyuncs.com/labikyo/node-yarn:7-alpine

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json gulpfile.js yarn.lock /usr/src/app/
RUN yarn config set registry https://registry.npm.taobao.org
RUN yarn --pure-lockfile

# Bundle app source
COPY . /usr/src/app

EXPOSE 3002

CMD [ "npm", "run", "start" ]
