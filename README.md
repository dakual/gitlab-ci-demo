docker run -d --name gitlab-runner --restart always \
-v ~/Genel/gitlab/config:/etc/gitlab-runner \
-v /var/run/docker.sock:/var/run/docker.sock \
gitlab/gitlab-runner:latest

docker exec -it gitlab-runner bash
docker logs gitlab-runner -f

gitlab-runner register -n \
--description "Sample Runner 1" \
--url <GITLAB-URL> \
--registration-token <GITLAB-REGISTRATION-TOKEN> \
--executor docker \
--docker-image "docker:latest" \
--docker-volumes /var/run/docker.sock:/var/run/docker.sock \
--docker-privileged \
--tag-list prod


gitlab-runner list
gitlab-runner stop
gitlab-runner start
gitlab-runner restart
gitlab-runner unregister --name <runner-name>
gitlab-runner unregister --all-runners
