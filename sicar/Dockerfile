#trocar o ubuntu 18.04lts na imagem base
FROM jpbp/ambientesicar:1.0 

WORKDIR /app
RUN apt update && apt install nano -y
COPY backend backend

COPY frontend frontend
COPY frontend_gestao_acesso frontend_gestao_acesso
COPY car-ui-components car-ui-components
COPY site site

RUN echo '{ "allow_root": true }' > /root/.bowerrc && chown -R $(whoami) $HOME/.npm && npm install grunt -g
RUN cd site && npm install
RUN cd frontend_gestao_acesso && npm install
RUN cd frontend && npm install && bower install && grunt
# build do backend e grunt da bagaca
# salvar o arquivo pdf-0.9
RUN wget https://www.playframework.com/modules/pdf-0.9.zip -O /tmp/pdf-0.9.zip
RUN mkdir -p backend/modules/pdf-0.9 && cd backend && ls
RUN unzip /tmp/pdf-0.9.zip -d backend/modules/pdf-0.9
RUN echo "/opt/play-1.2.7/modules/secure" > backend/modules/secure.txt

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get upgrade -y 
RUN apt install python-minimal -y 
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && apt-get update && apt-get install apt-utils tzdata -y

RUN ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata

RUN mkdir -p /app/arquivos/analise/
RUN mkdir -p /app/arquivos/demonstrativo/
RUN mkdir -p /app/arquivos/portal_seguranca/oficios_solicitacao/
RUN mkdir -p /app/arquivos/portal_seguranca/planilhas/
RUN mkdir -p /app/arquivos/portal_seguranca/termo_compromisso/
RUN mkdir -p /app/arquivos/documentos_cancelamento/
RUN mkdir -p /app/arquivos/imovel_car/sucesso/
RUN mkdir -p /app/arquivos/documentos_cancelamento/
RUN mkdir -p /app/arquivos/centralMensagem/anexos/
RUN mkdir -p /app/arquivos/integracao_sfb/shapefiles/


#ENTRYPOINT JAVA_HOME=/opt/jdk1.7.0_80 /opt/play-1.2.7/play run /app/backend

EXPOSE 9003/tcp

