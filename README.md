README.md

## Drupal project

### Dmitry Shevtsov

***

### Project steps:
```
1.    Push to GitHub repo reaction (Webhook).
2.    Running Jenkins pipeline with the following tasks:
2.1.    Clone Git repo.
2.2.    Verification of the configuration.
2.3.    Building an environment.
2.4.    Checking start page.
2.5.    Folding the environment.
2.6.    Cleaning up.
2.7.    Sending Job status message to the Slack.
```



### Jenkns Pipeline stages


|       Step1       |            Step2            |          Step3          |            Step4             |        Step5         |            Step6            |          Step7          |           Step8           |
|-------------------|-----------------------------|-------------------------|------------------------------|----------------------|-----------------------------|-------------------------|---------------------------|
| Clone repository  | Checks for Docker-compose file  | UP with Docker-compose  | Wait prior starting testing  | Checking start page  | Stopping Docker containers  | Removing Docker images  | Declarative: Post Actions |


