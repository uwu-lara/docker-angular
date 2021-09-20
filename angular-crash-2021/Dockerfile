ARG WORK_DIR=/build

FROM node:14.17 as builder

ARG WORK_DIR

ENV PATH ${WORK_DIR}/node_modules/.bin:$PATH

RUN mkdir ${WORK_DIR}

WORKDIR ${WORK_DIR}

COPY package.json ${WORK_DIR}
COPY package-lock.json ${WORK_DIR}

# RUN npm install @angular/cli
RUN npm install

COPY . ${WORK_DIR}

# RUN ng build --prod
RUN npm run build --prod

FROM nginx:latest

ARG WORK_DIR

COPY --from=builder ${WORK_DIR}/dist/angular-crash /usr/share/nginx/html

COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD nginx -g "daemon off;"

# # Stage 1: Compile and Build angular codebase

# # Use official node image as the base image
# FROM node:latest as build

# # Set the working directory
# WORKDIR /usr/local/app

# # Add the source code to app
# COPY ./ /usr/local/app/

# # Install all the dependencies
# RUN npm install

# # Generate the build of the application
# RUN npm run build


# # Stage 2: Serve app with nginx server

# # Use official nginx image as the base image
# FROM nginx:latest

# # Copy the build output to replace the default nginx contents.
# COPY --from=build /usr/local/app/dist/sample-angular-app /usr/share/nginx/html

# # Expose port 80
# EXPOSE 80