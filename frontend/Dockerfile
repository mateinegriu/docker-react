# if we create a named builder like here, deploying to AWS will fail, so we'd just have to use the id of this phase like below
FROM node:alpine
WORKDIR "/app"
COPY package.json ./
RUN npm install
COPY ./ ./
RUN npm run build
# the above stuff was run at build

# the following phase is to just copy the results of the above npm run build to the nginx folder,
# so this container will only contain the /app/build folder from the above without all the artefacts from npm install etc.
# this way we'd have a much lighter container.
FROM nginx
#elastic beanstock looks at expose and maps this port automatically,
#even though in a normal environment this statement is just descriptive and does nothing.
EXPOSE 80 
# copy something from a different phase (in this case from the previous "builder" phase)
COPY --from=0 /app/build /usr/share/nginx/html
# default command of the nginx container is to run nginx so no need to call it here