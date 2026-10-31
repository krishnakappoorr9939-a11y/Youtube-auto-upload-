# YouTube Auto Uploader – தினசரி தானியங்கி Upload (Starter)

## இந்த App என்ன செய்யும்?
1. பல YouTube சேனல்களைத் தனித்தனியாக Google மூலம் இணைக்கலாம்.
2. Android மொபைலில் வீடியோவைத் தேர்வு செய்யலாம்.
3. வீடியோ தலைப்பு/Topic கொடுத்தால் AI மூலம் Title, Description, Tags உருவாக்கலாம்.
4. எந்த சேனலில் upload செய்ய வேண்டும் என்பதைத் தேர்வு செய்யலாம்.
5. தினமும் எந்த நேரத்தில் upload செய்ய வேண்டும் என்பதை அமைக்கலாம்.
6. வீடியோவை Daily Queue-ல் சேர்க்கலாம்.
7. Server தினமும் குறிப்பிட்ட நேரத்தில் Queue-யில் உள்ள அடுத்த வீடியோவை upload செய்ய முயற்சிக்கும்.

## முக்கியமான விஷயம்
இது source code மட்டுமே; தயாரான APK அல்ல. Flutter மூலம் APK உருவாக்க வேண்டும். மேலும் தினசரி upload நடக்க backend server 24 மணி நேரமும் இயங்க வேண்டும். மொபைல் off-ஆக இருந்தாலும் server இயங்கினால் schedule தொடரும். Server-ல் நிரந்தர storage அவசியம்.

## அமைப்பது எப்படி?
### Google Cloud
- Google Cloud Console-ல் project உருவாக்கவும்.
- YouTube Data API v3 enable செய்யவும்.
- OAuth consent screen அமைக்கவும்.
- Web application OAuth Client உருவாக்கவும்.
- `https://உங்கள்-server-domain/oauth2callback` callback URL சேர்க்கவும்.

### Server
- Node.js 20 அல்லது அதற்கு மேல் நிறுவவும்.
- `server/.env.example`-ஐ `.env` என்று copy செய்து Google OAuth விவரங்களை நிரப்பவும்.
- `npm install` செய்து `npm start` இயக்கவும்.
- எப்போதும் இயங்கும் HTTPS server-ல் deploy செய்யவும்; persistent disk தேவை.

### Android
- Flutter நிறுவவும்.
- `mobile/lib/main.dart`-ல் `apiBase`-ஐ உங்கள் server HTTPS URL-ஆக மாற்றவும்.
- `flutter pub get` மற்றும் `flutter run` இயக்கவும்.

## பாதுகாப்பு
ஒவ்வொரு YouTube சேனலுக்கும் உரிமையாளர் Google authorization தேவை. OAuth token-களை பாதுகாப்பாக சேமிக்க வேண்டும். இந்த demo-வில் local JSON token/queue storage மட்டுமே உள்ளது; பொதுப் பயன்பாட்டுக்கு முன் encrypted database, user login, OAuth state validation, HTTPS, retry/monitoring போன்றவை சேர்க்கப்பட வேண்டும்.
