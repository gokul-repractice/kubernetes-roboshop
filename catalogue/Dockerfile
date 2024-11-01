FROM node:20.18.0-alpine3.20
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S appuser -G appgroup
WORKDIR /opt/server
#ENV MONGO=true  #We can pass this from kubernetes env, instead of here
RUN chown roboshop:roboshop /opt/server
USER roboshop
COPY package.json /opt/server/
COPY server.js /opt/server/
RUN npm install
CMD [ "node", "server.js" ]


FROM node:20.18.0-alpine3.20
EXPOSE 8080

# Create the roboshop group and appuser user under this group
RUN addgroup -S roboshop && adduser -S appuser -G roboshop

WORKDIR /opt/server
# ENV MONGO=true  #We can pass this from kubernetes env, instead of here

# Set ownership of the working directory to the roboshop group and appuser
RUN chown roboshop:roboshop /opt/server

# Switch to the roboshop user
USER appuser

# Copy application files and install dependencies
COPY package.json /opt/server/
COPY server.js /opt/server/
RUN npm install

# Start the application
CMD ["node", "server.js"]
