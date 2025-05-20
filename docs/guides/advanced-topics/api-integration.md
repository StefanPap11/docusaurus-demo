---
sidebar_position: 4
---

# API Integrációs Útmutató

## Bevezetés

Ez a dokumentum leírja, hogyan integrálhatja alkalmazását a **MintaAPI** szolgáltatással. Az API REST-alapú, JSON formátumban kommunikál, és OAuth 2.0 hitelesítést használ.

## Alapvető információk

- **API végpont**: `https://api.pelda.com/v1`
- **Hitelesítés**: OAuth 2.0 (Bearer token)
- **Válasz formátum**: JSON
- **Rate limit**: 100 kérés/percenként
- [API Referencia Dokumentáció](https://api.pelda.com/docs)

## Hitelesítés

1. Regisztráljon fejlesztői fiókot a [Fejlesztői Portálon](https://dev.pelda.com)
2. Szerezze meg API kulcsát és titkos kódját
3. Kérjen hozzáférési tokent:

```bash
curl -X POST https://api.pelda.com/oauth/token \
  -H "Content-Type: application/json" \
  -d '{
    "client_id": "YOUR_CLIENT_ID",
    "client_secret": "YOUR_SECRET",
    "grant_type": "client_credentials"
  }'
```

## Példa API Hívások

### Adat lekérése (GET)

```javascript
fetch('https://api.pelda.com/v1/products', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN',
    'Content-Type': 'application/json'
  }
})
.then(response => response.json())
.then(data => console.log(data));
```

### Adat küldése (POST)

```python
import requests

url = "https://api.pelda.com/v1/orders"
headers = {
    "Authorization": "Bearer YOUR_ACCESS_TOKEN",
    "Content-Type": "application/json"
}
data = {
    "product_id": "123",
    "quantity": 2,
    "customer_note": "Szürke színben kérem"
}

response = requests.post(url, json=data, headers=headers)
print(response.json())
```

## Hibakezelés

Az API szabványos HTTP státuszkódokat használ:

- `200 OK` - Sikeres kérés
- `400 Bad Request` - Érvénytelen kérés
- `401 Unauthorized` - Érvénytelen token
- `404 Not Found` - Nem létező erőforrás
- `429 Too Many Requests` - Túl sok kérés

Hiba esetén a válasz tartalmazza a hiba részleteit:

```json
{
  "error": {
    "code": "invalid_parameter",
    "message": "A quantity mező értéke minimum 1 kell legyen",
    "details": {
      "field": "quantity",
      "validation": "min_value"
    }
  }
}
```

## Pagináció

Nagy adathalmazok esetén a pagináció használata kötelező:

```http
GET /v1/products?page=2&page_size=25
```

Válasz szerkezete:

```json
{
  "data": [...],
  "pagination": {
    "total_items": 120,
    "total_pages": 5,
    "current_page": 2,
    "page_size": 25
  }
}
```

## Legjobb gyakorlatok

1. Mindig kezelje a hibákat
2. Implementáljon újratöltési mechanizmust token lejárat esetén
3. Cache-elje a statikus adatokat
4. Használjon exponenciális visszalépést (exponential backoff) rate limit túllépése esetén
5. Frissítse rendszeresen az API kliens könyvtárat

## SDK-k és Könyvtárak

Használja a hivatalos kliens könyvtárakat a fejlesztés megkönnyítésére:

- [JavaScript SDK](https://github.com/pelda/api-js)
- [Python Könyvtár](https://pypi.org/project/pelda-api/)
- [Java Wrapper](https://mvnrepository.com/artifact/com.pelda/api-client)

## Tesztelés

Használja a sandbox környezetet fejlesztés közben:  
`https://sandbox.api.pelda.com/v1`

A sandbox nem igényel valós adatokat és minden művelet szimulált.

## További információk

- [API Changelog](https://api.pelda.com/changelog)
- [Közösségi támogatás](https://forum.pelda.com/api-integration)
- [Integrációs Checklist](https://api.pelda.com/checklist)