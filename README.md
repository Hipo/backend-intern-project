# Intern Project Backend

## System Requirements

Docker 1.12 or higher.

## Docker

### Install

For mac install **docker for mac**.

## Deploying for local development

From the repo's root run `source tools/deploy_dev.sh`.

This will use `docker-compose-dev.yml` and `Dockerfile` to setup a development environment complete with all the needed services.
The first time the process might take a few minutes, after that Docker will use its cache to speed up things.

You should be bashed into the container. You must install django and django rest framework's latest version and update the `requirements.txt` 

If you are doing this for the first time run the followings.
 - **python manage.py migrate** (This might raise an error. Wait a few seconds for database to be ready. Then run it again.)

You can run **python manage.py runserver 0:8000** to run server.
    
**Now you can reach the app from your host machine at http://localhost:8000**

### Logging

If the containers are all started in detached mode (`-d` with docker-compose) the logs of each container can be monitored by running
`docker logs -f ${CONTAINER_NAME}`

## Git flow

We use a topic-branch approach while rebasing on top of the main branch and then merging into it. 
Assuming the main branch is `staging` and the topic is `users`:

- `git checkout staging`
- `git checkout -b users`
- Apply and commit changes (and push to the remote feature branch).
- Somebody makes changes to staging.
- `git fetch --all && git rebase staging` (from the topic branch)
- Changes are ready to be merged into the main branch.
- `git checkout staging && git merge users && git push`

This keeps the commit history clean and only creates a few "merge" commits where they are needed (i.e. **only** when a feature branch is merged into the main one).

For more details: http://engineering.hipolabs.com/how-to-work-in-a-team-version-control-and-git/ .
