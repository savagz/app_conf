# app_conf

Carpeta de datos, sin código. Solo `app_php` la lee (vía `CONF_DIR`, ver `app_php/README.md`). No define variables de entorno propias.

## Archivos

| Archivo          | Keys                                                                 |
|-------------------|-----------------------------------------------------------------------|
| `database.conf`   | `host`, `port`, `name`, `user`, `password`, `pool_size`, `timeout`    |
| `server.conf`      | `host`, `port`, `threads`, `max_connections`, `timeout`               |
| `app.conf`         | `name`, `version`, `environment`, `debug`, `locale`                   |
| `users.conf`       | `admin_user`, `admin_email`, `max_users`, `default_role`              |
| `features.conf`    | `feature_dark_mode`, `feature_beta_api`, `feature_new_dashboard`, `rollout_percentage` |

Formato: `key=value` por línea, estilo INI plano (`parse_ini_file` con `INI_SCANNER_TYPED`, tipa bool/int automático).

Agregar un `.conf` nuevo acá lo expone en `app_php` solo si se agrega su nombre a `CONF_NAMES` en `app_php/src/Router.php`.

## CI/CD

`.github/workflows/ci-cd.yml`: valida que cada `.conf` tenga solo líneas `key=value` en push/PR a `main` -> deploy por SSH (`git pull` dentro del contenedor `labs-php`, en `/opt/app_conf`) solo en push a `main`.

Secrets requeridos en el repo: `DEPLOY_HOST`, `DEPLOY_USER`, `DEPLOY_SSH_KEY`.
