# LocalNotifications
cd LocalNotifications
npm install
ionic serve
npx cap add android
npm run build
npx cap sync
npx cap open android
luego que abra android estudio esperar que instale las dependencias, buscar la opcion Build, luego Build blunde apk y build apk
Dependencias que se instalo
npm install @capacitor/core
npm install @capacitor/android
npm install @capacitor/local-notifications
cofigurar AndroidManifest.xml
ruta ==>> android\app\src\main\AndroidManifest.xml
<?xml version="1.0" encoding="utf-8"?>
<manifest 
    xmlns:tools="http://schemas.android.com/tools"
    >
    <!-- Permissions -->
    <uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM" />
    <uses-permission android:name="android.permission.INTERNET" />
</manifest>
