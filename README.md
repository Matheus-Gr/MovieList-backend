# README
Project using rails as banckend api, vue as frontend, postgres as datbase and docker to cotainerize

to run project, first you need to have this folder structure:

backend
frontend
.env
docker-compose.yml

sample of .env file:

```env
VITE_API_URL=your_db
RAILS_ENV=your_enviroment
POSTGRES_HOST=your_db
POSTGRES_DB=your_production
POSTGRES_USER=your_user
POSTGRES_PASSWORD=your_password
RAILS_MASTER_KEY=your_rails_master_key
SECRET_KEY_BASE=your_rails_secret_key_base
```
