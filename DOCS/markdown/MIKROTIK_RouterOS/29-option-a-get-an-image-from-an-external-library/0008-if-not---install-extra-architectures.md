## If not - install extra architectures: 

```
docker run --privileged --rm tonistiigi/binfmt --install all
```

pull or create your project with Dockerfile included  and build, extract image (adjust --platform if needed): 

```
git clone https://github.com/pi-hole/docker-pi-hole.git
cd docker-pi-hole
```

```
docker buildx build  --no-cache --platform arm64 --output=type=docker -t pihole .
docker save pihole > pihole.tar
```
