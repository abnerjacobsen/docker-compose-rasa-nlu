# docker-compose for Rasa NLU boilerplate

.. contents::

1. Setup
--------

Requirements for the tutorial:

    - A text editor of your choice
    - Docker
    - Docker-compose

If you are not sure whether Docker is installed on your machine execute the
following command:

  .. code-block:: bash

    docker -v && docker-compose -v
    # Docker version 18.06.1-ce, build e68fc7a
    # docker-compose version 1.21.2, build a133471

If your output is not similar to the one above, please install Docker.
See `this instruction page <https://docs.docker.com/install/>`_ for the
instructions.

2. Quick Start
--------------

This section will cover the following:

    - Clone this repository
    - Start Docker container with default sample data
    - Test if the Rasa NLU is working
    
## Quick Start

```bash
# 1. Clone the repository.
git clone https://github.com/abnerjacobsen/docker-compose-rasa-nlu.git nlu-new-project

# 2. Enter your newly-cloned folder.
cd nlu-new-project

# 3. Start docker containers usiong docker-compose.
docker-compose up -d

# 4. Test it.
curl --request POST --url http://localhost:5000/parse --header 'content-type: application/json' --data '{"q": "very good", "project": "default"}'
curl --request POST --url http://localhost:5000/parse --header 'content-type: application/json' --data '{"q": "sad", "project": "default"}'

# 5. Test Duckling.
curl --request POST --url http://localhost:5000/parse --header 'content-type: application/json' --data '{"q": "My email is user@domain.com", "project": "default"}'
curl --request POST --url http://localhost:5000/parse --header 'content-type: application/json' --data '{"q": "Amount to pay is US$ 1,000.00", "project": "default"}'
```

## Training with your own data

```bash
# 1. Edit the training data to fit your needs.
nano -w rasa/nlu/app/projects/default/nlu_data.json

# 2. Train Rasa NLU with the changed data file.
curl --request POST --url 'http://localhost:5000/train?project=default' -H'Content-Type: application/json' --data @rasa/nlu/app/projects/default/nlu_data.json
```
