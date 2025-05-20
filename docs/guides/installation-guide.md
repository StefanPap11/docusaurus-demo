---
sidebar_position: 1
---

# Installációs útmutató: Minta Projekt

## Bevezetés

Ez a dokumentum részletesen ismerteti a Minta Projekt telepítésének lépéseit különböző operációs rendszereken. A telepítés előtt győződjön meg arról, hogy rendelkezik az összes szükséges előfeltétellel.

**Fontos**: Olvassa el figyelmesen az egész dokumentumot a telepítés megkezdése előtt.

## Előfeltételek

A szoftver futtatásához szükséges:

- Operációs rendszer: Windows 10/11, macOS 10.14+, vagy Linux (Ubuntu 20.04+ ajánlott)
- Processzor: Legalább 2 GHz dual-core
- Memória: Minimum 4 GB RAM
- Tárhely: Legalább 2 GB szabad hely
- [.NET Core 6.0 Runtime](https://dotnet.microsoft.com/download/dotnet/6.0) vagy újabb
- [Node.js 16.x](https://nodejs.org/) (csak webes felülethez)

## 1. Windows telepítés

### 1.1 Letöltés

1. Látogasson el a [letöltési oldalunkra](https://example.com/download)
2. Kattintson a "Windows Installer" gombra
3. Mentse a `MintaProjekt_Setup.exe` fájlt

### 1.2 Telepítés

```powershell
Start-Process -FilePath "MintaProjekt_Setup.exe" -ArgumentList "/quiet", "/norestart" -Wait
```

Vagy manuálisan:

1. Kattintson duplán a letöltött EXE fájlra
2. Fogadja el a licencszerződést
3. Válassza telepítési útvonalat (alapértelmezett ajánlott)
4. Várja meg a telepítés befejezését (kb. 5-10 perc)

### 1.3 Verzió ellenőrzése

Nyisson meg egy parancssort és futtassa:

```cmd
mintaprojekt --version
```

## 2. macOS telepítés

### 2.1 Homebrew használata

```bash
brew tap example/mintaprojekt
brew install mintaprojekt
```

### 2.2 Kézi telepítés

1. Töltse le a `.pkg` fájlt
2. Nyissa meg a letöltött csomagot
3. Kövesse a telepítővarázsló utasításait

## 3. Linux telepítés

### 3.1 Debian/Ubuntu

```bash
wget https://example.com/releases/mintaprojekt_1.0.0_amd64.deb
sudo apt install ./mintaprojekt_1.0.0_amd64.deb
```

### 3.2 RHEL/CentOS

```bash
sudo yum install https://example.com/releases/mintaprojekt-1.0.0.el7.x86_64.rpm
```

## Konfiguráció

A telepítés után szükség lehet az alábbi konfigurációs fájl szerkesztésére:

```yaml
# /etc/mintaprojekt/config.yaml
database:
  host: localhost
  port: 5432
  username: admin
  password: securepassword
```

## Hibaelhárítás

**Probléma**: A program nem indul el
- Megoldás: Ellenőrizze, hogy fut-e az adatbázis szolgáltatás

**Probléma**: Hiányzó függőségek
- Megoldás: Futtassa a `mintaprojekt --install-deps` parancsot

További segítségért látogasson el a [támogatási oldalunkra](https://example.com/support) vagy nyisson egy ticketet a [GitHub repositorynkon](https://github.com/example/mintaprojekt/issues).

## Frissítés

A legújabb verzióra frissítés:

```bash
mintaprojekt --update
```

Vagy használja a natív csomagkezelőt:

```bash
# Ubuntu/Debian
sudo apt update && sudo apt upgrade mintaprojekt

# RHEL/CentOS
sudo yum update mintaprojekt
```

## Eltávolítás

### Windows
- Vezérlőpult → Programok és szolgáltatások → Minta Projekt → Eltávolítás

### macOS
```bash
brew uninstall mintaprojekt
```

### Linux
```bash
# Debian/Ubuntu
sudo apt remove mintaprojekt

# RHEL/CentOS
sudo yum remove mintaprojekt
```

## Következő lépések

A sikerres telepítés után:

1. Indítsa el a programot
2. Hajtsa végre a kezdeti beállításokat
3. Ismerkedjen meg a [felhasználói kézikönyvvel](https://example.com/docs)

## További információk

- [API dokumentáció](https://example.com/api-docs)
- [Közösségi fórum](https://forum.example.com)
- [Fejlesztői dokumentáció](https://dev.example.com)
