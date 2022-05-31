FROM tomcat:9-jdk17-openjdk-slim

# EXPOSE 8080 # useless as it's the same as the FROM image
# CMD ["catalina.sh", "run"] # useless as it's the same as the FROM image

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
HEALTHCHECK --interval=5s --timeout=10s --start-period=20s CMD curl -f http://localhost:8080/ || exit 1

# Might be useful to wait for DB startup - see https://docs.docker.com/compose/startup-order/
ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh .
RUN chmod +x wait-for-it.sh

RUN rm -rf ${CATALINA_HOME}/webapps/*
ADD http://svn.ensisa.uha.fr/bd/vg/todo-app.war ${CATALINA_HOME}/webapps/ROOT.war
