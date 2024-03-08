# README
Project using rails as banckend api, vue as frontend, postgres as datbase and docker to cotainerize

to run project, first you need to have this folder structure:

backend
frontend
.env
docker-compose.yml

sample of .env file:

```env
POSTGRES_HOST=database
RAILS_ENV=production
POSTGRES_DB={your_production_data_base}
POSTGRES_USER={your_data_base_user}
POSTGRES_PASSWORD={your_data_base_user_password}
SECRET_KEY_BASE={your_secret_key_base}
VITE_API_URL=$POSTGRES_HOST
```

sample of docker-compose.yml

```yml
version: '3'
services:
  database:
    image: postgres:14.2-alpine
    container_name: database
    volumes:
      - postgres_data:/var/lib/postgresql/data
    command: 
      "postgres -c 'max_connections=500'"
    ports:
      - "5432:5432"
    environment:
      - POSTGRES_DB=${POSTGRES_DB}
      - POSTGRES_USER=${POSTGRES_USER}
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
    
  backend:
    image: matheusgon/pipipitchu_backend
    container_name: backend
    command: "./bin/rails server"
    environment:
      - RAILS_ENV=${RAILS_ENV}
      - POSTGRES_HOST=${POSTGRES_HOST}
      - POSTGRES_DB=${POSTGRES_DB}
      - POSTGRES_USER=${POSTGRES_USER}
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      - RAILS_MASTER_KEY=${RAILS_MASTER_KEY}
      - SECRET_KEY_BASE=${SECRET_KEY_BASE}
    volumes:
      - app-storage:/rails/storage
    depends_on:
      - database
    ports:
      - "3000:3000/tcp"

  frontend:
    image: matheusgon/pipipitchu_frontend
    container_name: frontend
    ports:
      - "8080:8080"
    depends_on:
      - backend

volumes:
  postgres_data: {}
  app-storage: {}
```
