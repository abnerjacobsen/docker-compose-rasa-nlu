FROM python:3.6-slim
MAINTAINER Abner G Jacobsen - http://daspanel.com <admin@daspanel.com>

ENV RASA_NLU_DOCKER="YES" \
    RASA_NLU_HOME=/app \
    RASA_NLU_PYTHON_PACKAGES=/usr/local/lib/python3.6/dist-packages

# A little bit of metadata management.
# See http://label-schema.org/  
LABEL org.label-schema.schema-version="1.0" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.version=$VERSION \
      org.label-schema.vcs-url=$VCS_URL \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.name="abnerjacobsen/dizendo-dev-rasa-nlu" \
      org.label-schema.description="Dizendo.ai dev RASA NLU server"

# Run updates, install basics and cleanup
# - build-essential: Compile specific dependencies
# - git-core: Checkout git repos
RUN apt-get update -qq \
    && apt-get install -y --no-install-recommends build-essential git-core openssl libssl-dev libffi6 libffi-dev curl  \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR ${RASA_NLU_HOME}

# Get latest RASA NLU sources
RUN git clone https://github.com/RasaHQ/rasa_nlu.git

# use bash always
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN pip install -r rasa_nlu/alt_requirements/requirements_full.txt
RUN pip install -e rasa_nlu/.

RUN apt-get update -qq \
    && apt-get install -y --no-install-recommends wget \
    && wget -P data/ https://s3-eu-west-1.amazonaws.com/mitie/total_word_feature_extractor.dat \
    && apt-get remove -y wget \
    && apt-get autoremove -y

RUN pip install https://github.com/explosion/spacy-models/releases/download/en_core_web_md-2.0.0/en_core_web_md-2.0.0.tar.gz --no-cache-dir > /dev/null \
    && python -m spacy link en_core_web_md en \
    && pip install https://github.com/explosion/spacy-models/releases/download/de_core_news_sm-2.0.0/de_core_news_sm-2.0.0.tar.gz --no-cache-dir > /dev/null \
    && python -m spacy link de_core_news_sm de

RUN python -m spacy download pt

COPY . ${RASA_NLU_HOME}
#COPY ./app ${RASA_NLU_HOME}
WORKDIR ${RASA_NLU_HOME}

# Copy as early as possible so we can cache ...
COPY requirements.txt .
#COPY entrypoint.sh .

RUN pip install -r requirements.txt --no-cache-dir

EXPOSE 5000

#ENTRYPOINT ["./entrypoint.sh"]

ENTRYPOINT []

#CMD ["start", "-c", "/app/config/config_spacy_duckling.yml", "--path", "/app/projects", "--response_log", "/app/logs"]
