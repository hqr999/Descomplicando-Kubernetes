
# ---Stage 1: build---
FROM  cgr.dev/chainguard/python:latest-dev AS buildando 
WORKDIR /app 
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt
#---Stage 2: runtime---
FROM cgr.dev/chainguard/python:latest 

WORKDIR /app 

#Copia apenas as libs instaladas
COPY --from=buildando /home/nonroot/.local /home/nonroot/.local

#Copia a aplicação
COPY app.py .
COPY templates templates/
COPY static static/

#PATH para reconhecer pacotes instalados com --user 
ENV PATH="/home/nonroot/.local/bin:$PATH"



ENTRYPOINT ["flask","run","--host=0.0.0.0"]
