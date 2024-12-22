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

docker-compose -f docker-compose.dev.yml build
docker exec -it thaboralame_auth /bin/sh
docker exec -it thaboralame_user /bin/sh
npx prisma db push // npx prisma migrate dev --name initial_setup // npx prisma migrate deploy // npx prisma migrate deploy
docker-compose -f docker-compose.dev.yml up

docker-compose -f docker-compose.dev.yml logs -f auth
docker-compose -f docker-compose.dev.yml logs -f gateway

npx prisma migrate dev --schema=thaboralame_auth/src/prisma/schema.prisma --name init_refresh_token

npx prisma migrate dev --schema=thaboralame_user/src/prisma/schema.prisma --name init_user