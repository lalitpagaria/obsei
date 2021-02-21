# Obsei: OBserve, SEgment and Inform

<p align="center">
    <a href="https://github.com/lalitpagaria/obsei/actions">
        <img alt="CI" src="https://github.com/lalitpagaria/obsei/workflows/CI/badge.svg?branch=master">
    </a>
    <a href="https://github.com/lalitpagaria/obsei/blob/master/LICENSE">
        <img alt="License" src="https://img.shields.io/github/license/lalitpagaria/obsei?color=blue">
    </a>
    <a href="https://pypi.org/project/obsei">
        <img src="https://img.shields.io/pypi/pyversions/obsei" alt="PyPI - Python Version" />
    </a>
    <a href="https://pypi.org/project/obsei/">
        <img alt="Release" src="https://img.shields.io/pypi/v/obsei">
    </a>
    <a href="https://pepy.tech/project/obsei">
        <img src="https://pepy.tech/badge/obsei/month" alt="Downloads" />
    </a>
    <a href="https://hub.docker.com/r/lalitpagaria/obsei">
        <img src="https://img.shields.io/docker/pulls/lalitpagaria/obsei" alt="Docker Pulls" />
    </a>
    <a href="https://github.com/lalitpagaria/obsei/commits/master">
        <img alt="Last commit" src="https://img.shields.io/github/last-commit/lalitpagaria/obsei">
    </a>
</p>

**Note: There are major breaking changes are on the way. Please use released version instead of master branch. To track progress of next release refer [Release Progress](#release-progress).**


`Obsei` is intended to be a workflow automation tool for text segmentation need. `Obsei` consist of -
 - **OBserver**, observes platform like Twitter, Facebook, App Stores, Google reviews, Amazon reviews and feed that information to,
 - **SEgmenter**, which perform text classification and sentiment analysis and feed that information to,
 - **Informer**, which send it to ticketing system, data store or other places for further action and analysis.

Current flow -

![](https://raw.githubusercontent.com/lalitpagaria/obsei/master/images/Obsei-flow-diagram.png)

A future concept (Coming Soon! :slightly_smiling_face:)

![](https://raw.githubusercontent.com/lalitpagaria/obsei/master/images/Obsei-future-concept.png)


## Installation

### To use as SDK
Install via PyPi:
```shell
pip install obsei
```
Install from master branch (if you want to try the latest features):
```shell
git clone https://github.com/lalitpagaria/obsei.git
cd obsei
pip install --editable .
```

To update your installation, just do a `git pull`. The `--editable` flag
will update changes immediately.

### To use as Rest interface
Start docker with default configuration file:
```shell
docker run -d --name obesi -p 9898:9898 lalitpagaria/obsei:latest
```
Start docker with custom configuration file (Assuming you have configfile `config.yaml` at `/home/user/obsei/config` at host machine):
```shell
docker run -d --name obesi -v "/home/user/obsei/config:/home/user/config" -e "OBSEI_CONFIG_PATH=/home/user/config" -e "OBSEI_CONFIG_FILENAME=config.yaml" -p 9898:9898 lalitpagaria/obsei:latest
```
Start docker locally with `docker-compose`:
```shell
docker-compose up --build
```
Following environment variables are useful to customize various parameters -
- `OBSEI_CONFIG_PATH`: Configuration file path (default: ../config)
- `OBSEI_CONFIG_FILENAME`: Configuration file name (default: rest.yaml)
- `OBSEI_NUM_OF_WORKERS`: Number of workers for rest API server (default: 1)
- `OBSEI_WORKER_TIMEOUT`: Worker idle timeout in seconds (default: 180)
- `OBSEI_SERVER_PORT`: Rest API server port (default: 9898)
- `OBSEI_WORKER_TYPE`: Gunicorn worker type (default: uvicorn.workers.UvicornWorker)

## Components and Integrations

- **Source/Observer**: Twitter, Play Store Reviews, Apple App Store Reviews, Reddit, Email (Facebook, Instagram, Google reviews, Amazon reviews, Slack, Microsoft Team, Chat-bots etc planned in future)
- **Analyzer/Segmenter**: Sentiment and Text classification (QA, Natural Search, FAQ, NER etc planned in future)
- **Sink/Informer**: HTTP API, ElasticSearch, DailyGet, Slack and Jira (Salesforce, Zendesk, Hubspot, Slack, Microsoft Team, etc planned in future)
- **Processor/WorkflowEngine**: Simple integration between Source, Analyser and Sink (Rich workflows using rule engine planned in future)
- **Convertor**: Very important part, which convert data from analyzer format to the format sink understand. It is very helpful in any customizations, refer `dailyget_sink.py` and `jira_sink.py`.

**Note:** In order to use some integrations you would need credentials, refer following list -
- [Twitter](https://twitter.com/): To make authorized API call, get access from [dev portal](https://developer.twitter.com/en/apply-for-access). Read about [search api](https://developer.twitter.com/en/docs/twitter-api/tweets/search/introduction) for more details. 
- [Play Store](https://play.google.com/): To make authorized API calls, get [service account's credentials](https://developers.google.com/identity/protocols/oauth2/service-account). Read about [review api](https://googleapis.github.io/google-api-python-client/docs/dyn/androidpublisher_v3.reviews.html) for more details.
- [Reddit](https://www.reddit.com/): To make authorized API calls, create [client app](https://www.reddit.com/prefs/apps). For more detail refer [link](https://praw.readthedocs.io/en/latest/getting_started/authentication.html).
- [Slack](https://slack.com/): To send message to Slack channel, get bot or user token. Refer [link](https://api.slack.com/authentication/token-types#bot).
- [Email]: Email read only via IMAP servers are supported. Refer [link](https://www.systoolsgroup.com/imap/) for popular IMAP servers (like for Gmail).

## Model selection
Any model listed in [Named Entity Recognition](https://huggingface.co/models?filter=token-classification), [Text Classification](https://huggingface.co/models?filter=text-classification) and [Zero-Shot Classification](https://huggingface.co/models?filter=zero-shot-classification) can be used in Segmenter.

## Examples and Screenshots
Refer [example](https://github.com/lalitpagaria/obsei/tree/master/example) and [config](https://github.com/lalitpagaria/obsei/tree/master/config) folders for `obsei` usage and configurations.

### Jira
![](https://raw.githubusercontent.com/lalitpagaria/obsei/master/images/jira_screenshot.png)

## Changelog
Refer [releases](https://github.com/lalitpagaria/obsei/releases) and [projects](https://github.com/lalitpagaria/obsei/projects).