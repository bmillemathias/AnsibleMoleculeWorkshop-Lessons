# Molecule workshop lessons

Here you find the lessons where we start the parts of our workshops from.

Most of the lessons are also the target of their previous lessons.

Please start with a new folder for every lesson. Don't begin to work in the lessons folders.

* [Lesson 1](./LESSON1.md)
* [Lesson 2](./LESSON2.md)
* [Lesson 3](./LESSON3.md)
* [Lesson 4](./LESSON4.md)
* [Lesson 5](./LESSON5.md)

## Versions

This workshop was created with

* Python: 3.8.1
* Ansible: 2.9.4
* Molecule: 3.0.2

## Links

* [molecule documentation](https://molecule.readthedocs.io/en/latest/)
* [molecule github](https://github.com/ansible-community/molecule)
* [molecule docker](https://quay.io/repository/ansible/molecule)
* [testinfra documentation](https://testinfra.readthedocs.io/en/latest/)

## Running Molecule within a role with the latest image

IMPORTANT: If you want to run these tests locally your docker engine must use the storage-engine aufs

Just create or edit the config file /etc/docker/daemon.json with content

```json3.8.1
  "storage-driver": "aufs"
}
```

then run in a role directory

```bash
docker run \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $(pwd):$(pwd) -w $(pwd) \
  --user root \
  quay.io/ansible/molecule:3.0.2 \
  /bin/sh -c "pip3 install testinfra; molecule test -s default"
```

## you want to give us your power for the workshop

```bash
docker run -d --rm --name gitlab-runner \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /home/gitlab-runner:/home/gitlab-runner \
  -v /buiilds:/builds \
  --privileged \
  gitlab/gitlab-runner:latest
```

```bash
docker exec -it gitlab-runner /bin/bash
```

```bash
gitlab-runner register -n \
  --url https://gitlab.com/ \
  --registration-token GZqpz8aRxUqiY3FsNqAz \
  --executor docker --description "MYRUNNERNAME" \
  --docker-image "docker:19.03.1" \
  --docker-volumes /var/run/docker.sock:/var/run/docker.sock \
  --docker-volumes /home/gitlab-runner:/home/gitlab-runner \
  --docker-volumes /builds:/builds --tag-list molecule-workshop
```

This registeres a gitlab-runner on your local machine that can be used in the workshop. This is for careful use and should be killed after the workshop.
