FROM jpbp/ambientecentral:1.0
WORKDIR /app
RUN apt-get update && apt install nano git -y
RUN mkdir /root/.ssh/
COPY .ssh/ /root/.ssh/
RUN ssh-keyscan -H https://gitlab.ti.lemaf.ufla.br/ >> ~/.ssh/known_hosts
RUN git ls-remote --tags --heads git@gitlab.ti.lemaf.ufla.br:utilitarios/mapa-geo-car-wc.git
COPY ./ ./ 
RUN echo '{ "allow_root": true }' > /root/.bowerrc && chown -R $(whoami) $HOME/.npm && npm install grunt -g
RUN cd frontend && npm install && bower install 
#Rodar dentro do container por conta da task watching cd frontend && rm -rf node_modules/grunt-connect-proxy && npm install eventemitter3@0.1.6 && npm install grunt-connect-proxy && grunt
#exexutar a aplicação ENTRYPOINT JAVA_HOME=/opt/jdk1.7.0_80 /opt/play-1.4.5/play run /app/backend
