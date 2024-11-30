# Thabora Lame Orchestration

thaboralame_orchestration/
│
├── docker-compose.dev.yml
│
├── thaboralame_auth/
│   ├── Dockerfile.dev
│   └── ... (autres fichiers)
│
├── thaboralame_user/
│   ├── Dockerfile.dev
│   └── ... (autres fichiers)
│
├── thaboralame_cart/
│   ├── Dockerfile.dev
│   └── ... (autres fichiers)
│
├── thaboralame_product/
│   ├── Dockerfile.dev
│   └── ... (autres fichiers)
│
├── thaboralame_gateway/
│   ├── Dockerfile.dev
│   └── ... (autres fichiers)
│
└── thaboralame_frontend/
    ├── Dockerfile.dev
    └── ... (autres fichiers)


# Commandes

docker-compose -f docker-compose.dev.yml down && \
docker volume ls -q --filter "name=thaboralame_" | xargs docker volume rm && \
docker images -q --filter "reference=thaboralame_*" | xargs docker rmi && \
docker ps -a -q --filter "name=thaboralame_" | xargs docker rm && \
docker image prune -a -f