FROM python:3.10.0-slim-buster

# Set a variable for workdir
ENV APP_HOME=/app
# Create a work dir
RUN mkdir $APP_HOME
# create a staticfiles dir in ./app
RUN mkdir $APP_HOME/staticfiles
# set /app as workdir  
WORKDIR $APP_HOME

# Image metadata
LABEL maintainer="tankoraphael@gmail.com"
LABEL description="Development image for Real Estate Project" 

# prevents python .pyc files to written to docker
ENV PYTHONDONTWRITEBYTECODE 1
# python output is transmitted directly to the terminal without being bufferred and allows 
# displays of application output in real time
ENV PYTHONUNBUFFERED 1

# RUN apt-get update \
#     && apt-get install -y build-essential \
# # psycopg dependencies to work with postgres
#     && apt-get install -y libpd-dev \
# # translation dependencies
#     && apt-get install -y gettext \
# # postgres dependencies
#     && apt-get install -y netcat gcc postgresql \
# # clean up unused file
#     && apt-get purge -y  --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
#     && rm -rf /var/lib/apt/lists/*


RUN pip3 install --upgrade pip
COPY ./requirements.txt /app/requirements.txt

RUN pip3 install -r requirements.txt

COPY ./docker/local/django/entrypoint /entrypoint
# process line endings of shell script by converting windows lines endings into unix lines endings
RUN sed -i 's/\r$//g' /entrypoint
# Make entry shell script executable
RUN chmod +x /entrypoint

# start shell script
COPY ./docker/local/django/start /start
RUN sed -i 's/\r$//g' /start
RUN chmod +x /start

# dir for entrypoint
ENTRYPOINT [ "/entrypoint" ]