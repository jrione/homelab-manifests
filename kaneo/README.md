# TUTORIAL HOWTO:

>  PRE REQ:
>
> - PostgreSQL 16.4
> - Nginx Ingress Controller
> - Cert Manager

1. Kita clone dulu si repositori kaneo

   ```shell
   git clone https://github.com/usekaneo/kaneo.git kaneo_repo
   ```
2. Siapkan DB nya dulu:

   ```pgsql
    CREATE DATABASE kaneo;
    CREATE USER kaneo_user WITH PASSWORD 'apacoba';
    GRANT ALL PRIVILEGES ON DATABASE kaneo TO kaneo_user;
    \c kaneo;
    GRANT USAGE ON SCHEMA public TO kaneo_user;
    GRANT CREATE ON SCHEMA public TO kaneo_user;
    ALTER SCHEMA public OWNER TO kaneo_user;
   ```
3. Langsung hantam pake helm install

   ```shell
   helm upgrade  --install kaneo kaneo_repo/charts/kaneo -f kaneo_repo/charts/kaneo/values.yaml -f values.yaml --namespace kaneo --create-namespace
   ```
