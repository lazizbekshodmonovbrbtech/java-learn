# Keycloak laboratoriyasi (41-modul)

## Ishga tushirish
```
docker compose up -d
curl -s localhost:9000/health/ready
```
Admin konsol: http://localhost:8080 — admin / admin

`realm/bank-realm.json` birinchi ishga tushishda avtomatik import qilinadi:
- realm `bank`, rollar MIJOZ / KASSIR / ADMIN
- client'lar: `internet-bank` (confidential + PKCE), `mobile-app` (public + PKCE), `tolov-service` (service account)
- foydalanuvchi: `otabek` / `otabek123` (MIJOZ, filial_id=12)

## Birinchi token (client_credentials)
```
curl -s -X POST http://localhost:8080/realms/bank/protocol/openid-connect/token \
  -d grant_type=client_credentials -d client_id=tolov-service -d client_secret=svc-secret-change-me
```

## Keyingi qadamlar
- 45-modul: `filial` client scope + User Attribute mapper qo'shing
- 46-modul: Spring resource server'da `issuer-uri: http://localhost:8080/realms/bank`
- 47-modul: `internet-bank` client'ida Backchannel logout URL

⚠ Faqat lokal o'rganish uchun: sirlar va parollar ochiq yozilgan, `start-dev` rejimi.
