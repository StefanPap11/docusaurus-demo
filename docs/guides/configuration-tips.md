---
sidebar_position: 2
---

# Konfigurációs Tippek és Best Practices

## Alapkonfiguráció Optimalizálása

A szoftver teljesítményének javításához ajánlott módosítani az alapértelmezett beállításokat:

```yaml
# config/app_settings.yaml
performance:
  cache_enabled: true
  cache_size: 512MB # 256MB helyett
  worker_threads: auto # vagy manuális beállítás processzor magok alapján
```

**Tipp**: Használja a `auto` értéket a worker_threads-nál a legjobb eredményért.

## Adatbázis Konfiguráció

### MySQL/MariaDB optimalizálás

```sql
-- Ajánlott my.cnf beállítások
[mysqld]
innodb_buffer_pool_size = 1G # Rendelkezésre álló RAM 50-75%-a
innodb_log_file_size = 256M
max_connections = 100
```

További adatbázis tippekért lásd a [MySQL Performance Tuning Guide](https://dev.mysql.com/doc/refman/8.0/en/optimization.html)-t.

## Biztonsági Beállítások

1. **SSL/TLS konfiguráció**:
   ```nginx
   # Nginx példa
   ssl_protocols TLSv1.2 TLSv1.3;
   ssl_ciphers 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384';
   ```

2. **Hozzáférés korlátozás**:
   - IP-alapú whitelist használata
   - API kulcsok rotációja 90 naponta

## Naplózás Beállításai

Optimalizált naplókonfiguráció JSON formátumban:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning",
      "System": "Error",
      "Microsoft": "Error"
    },
    "File": {
      "Path": "/var/logs/app.log",
      "MaxSize": 10485760,
      "RetainedFileCountLimit": 5
    }
  }
}
```

**Fontos**: Éles környezetben kerülje a "Debug" szint használatát!

## Gyakori Hibák és Megoldások

1. **Teljesítménycsökkenés**:
   - Ok: Túl sok egyidejű kérés
   - Megoldás: Rate limiting bevezetése
     ```yaml
     rate_limiting:
       requests_per_minute: 300
       burst_limit: 50
     ```

2. **Memória túlcsordulás**:
   - Ok: Nem optimalizált gyorsítótár
   - Megoldás: LRU cache algoritmus beállítása

További hibaelhárítási útmutatóért látogasson el a [Hivatalos Hibaelhárítási Oldalunkra](https://example.com/troubleshooting).

## Speciális Beállítások

### Kubernetes konfiguráció

```yaml
# deployment.yaml
resources:
  requests:
    cpu: "500m"
    memory: "1Gi"
  limits:
    cpu: "2"
    memory: "4Gi"
```

### CI/CD integráció

```bash
# .gitlab-ci.yml példa
stages:
  - test
  - deploy

test_job:
  script:
    - make test
    - config-validator --strict
```

## Konfiguráció Verziókövetése

Ajánlott eljárások:
- Konfig fájlok tárolása Git-ben
- Titkos adatok kezelése Vault-tal vagy hasonló megoldással
- Konfiguráció validálása telepítés előtt

Hasznos eszköz: [Config Validator Tool](https://github.com/example/config-validator)
