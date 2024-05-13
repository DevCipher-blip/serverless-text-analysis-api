# Serverless text analysis

## Understand the handler before deployment

This repository demonstrates a small text-analysis service and its serverless packaging workflow. Keep local request behavior separate from deployment configuration, credentials, and provider-side limits.

Use the existing setup and test commands below to inspect the application first. For an engineering walkthrough, show a normal request, empty or malformed text, and the behavior when a required NLP resource is missing; deployment success alone is not a text-quality evaluation.

This is a small Flask project that lets you run NLP on AWS Lambda hosting Spacy models on S3 and therefore not running into the 250MB Lambda limit.

## Installing

`pipenv install`

## Activating environment
`pipenv shell`

## Testing

`pipenv install -d` to install also dev dependencies
`pytest`

## Before running it
Create an .env file in the root folder where `settings.py` is with these variables
```
FLASK_ENV=development
SENTRY_DSN=your_sentry_dsn
SPACY_MODEL_MEDIUM=en_core_web_md-2.3.1 # or whatever you want
SPACY_MODEL_SMALL=en_core_web_sm-2.3.1 # same
S3_BUCKET=your_bucket
```

## Deploying it
Delete `zappa_settings.json` and create one from scratch if you want, or change the S3 bucket name in the JSON provided. I used different buckets to store the models and the lambda code but you can probably use the same one.

Then, do `zappa deploy dev` and it should be deployed in a couple minutes
