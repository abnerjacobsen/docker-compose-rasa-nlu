FROM rasa/rasa_nlu:latest-full
MAINTAINER Abner G Jacobsen - http://daspanel.com <admin@daspanel.com>

# A little bit of metadata management.
# See http://label-schema.org/  
LABEL org.label-schema.schema-version="1.0" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.version=$VERSION \
      org.label-schema.vcs-url=$VCS_URL \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.name="abnerjacobsen/dizendo-dev-rasa-nlu" \
      org.label-schema.description="Dizendo.ai dev RASA NLU server"

WORKDIR ${RASA_NLU_HOME}

RUN python -m spacy download pt

COPY . ${RASA_NLU_HOME}
WORKDIR ${RASA_NLU_HOME}

# Copy as early as possible so we can cache ...
COPY requirements.txt .

RUN pip install -r requirements.txt --no-cache-dir

EXPOSE 5000

ENTRYPOINT []

