# docker-compose for Rasa NLU boilerplate

## Getting started

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
