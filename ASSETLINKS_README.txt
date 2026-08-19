# Configurare assetlinks.json (OBLIGATORIU pentru a ascunde bara de adresă în APK)

## De ce apare bara de adresă în APK?
Android TWA (Trusted Web Activity) arată bara de adresă când aplicația
NU poate verifica că domeniul web îți aparține. Verificarea se face prin
fișierul assetlinks.json.

## Pași:

### 1. Generează APK cu PWABuilder
- Mergi pe pwabuilder.com → Package for stores → Android
- PWABuilder generează un keystore și îți arată SHA-256 fingerprint
- Copiază SHA-256 fingerprint (arată ca: AB:CD:12:34:...)
- SALVEAZĂ fișierul keystore (.jks) — îl vei folosi la fiecare update

### 2. Actualizează assetlinks.json
Deschide fișierul `.well-known/assetlinks.json` și înlocuiește:
  "PLACEHOLDER_SHA256_FROM_PWABUILDER_KEYSTORE"
cu fingerprint-ul real, ex:
  "AB:CD:12:34:56:78:90:AB:CD:EF:..."

### 3. Urcă pe Netlify
Folderul `.well-known/` trebuie urcat pe hosting.
Netlify servește fișierele din subfolderuri automat.

### 4. Verifică
Deschide în browser:
  https://DOMENIUL_TAU/.well-known/assetlinks.json
Trebuie să returneze JSON, nu 404.

### 5. Testează APK-ul
Reinstalează APK-ul pe telefon. Bara de adresă dispare.

## Notă despre package_name
Asigură-te că în PWABuilder ai setat:
  Package ID: ro.codmedro.app
(același ca în assetlinks.json)
