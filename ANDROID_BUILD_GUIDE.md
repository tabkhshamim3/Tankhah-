# راهنمای تبدیل به اپلیکیشن اندروید

## روش اول: استفاده از Capacitor (توصیه شده)

### مراحل نصب:

```bash
# 1. نصب Capacitor
npm install @capacitor/core @capacitor/cli
npm install @capacitor/android

# 2. ساخت پروژه Capacitor
npx cap init تنخواه ir.shahin.pettycash --web-dir dist

# 3. افزودن پلتفرم اندروید
npx cap add android

# 4. ساخت پروژه
npm run build
npx cap sync

# 5. باز کردن در Android Studio
npx cap open android
```

### ساخت APK در Android Studio:

1. در Android Studio از منوی Build گزینه Build Bundle(s) / APK(s) را انتخاب کنید
2. سپس Build APK(s) را بزنید
3. فایل APK در مسیر `android/app/build/outputs/apk/debug/app-debug.apk` ذخیره می‌شود

### برای انتشار در Google Play (AABB):

1. Generate Signed Bundle / APK را انتخاب کنید
2. یک Keystore جدید بسازید
3. Release نسخه را انتخاب کنید
4. فایل AABB برای آپلود در Play Store آماده است

---

## روش دوم: استفاده از Cordova

```bash
# نصب Cordova
npm install -g cordova

# ساخت پروژه
cordova create android-app ir.shahin.pettycash تنخواه
cd android-app

# افزودن پلتفرم اندروید
cordova platform add android

# کپی فایل‌های build شده
cp -r ../dist/* www/

# ساخت APK
cordova build android
```

---

## روش سوم: استفاده از PWA Builder (آنلاین و ساده)

1. به سایت https://www.pwabuilder.com بروید
2. آدرس سایت خود را وارد کنید
3. گزینه Android را انتخاب کنید
4. فایل‌های آماده شده را دانلود کنید

---

## تنظیمات اضافی برای اندروید

### دسترسی‌های لازم (AndroidManifest.xml):

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

### تنظیمات صفحه کامل (Full Screen):

در `android/app/src/main/res/values/styles.xml`:

```xml
<style name="AppTheme.NoActionBar" parent="Theme.AppCompat.NoActionBar">
    <item name="android:windowNoTitle">true</item>
    <item name="android:windowFullscreen">true</item>
</style>
```

---

## نکات مهم:

1. **ذخیره‌سازی داده**: در حالت فعلی داده‌ها در LocalStorage مرورگر ذخیره می‌شوند. برای نسخه اندروید می‌توانید از SQLite استفاده کنید.

2. **بروزرسانی**: برای بروزرسانی اپلیکیشن، فایل‌های جدید را build کرده و مجدداً sync کنید.

3. **آیکون**: آیکون‌های مختلف سایز در پوشه `public` قرار دارند.

4. **امضای دیجیتال**: برای انتشار در Play Store باید اپلیکیشن را با Keystore امضا کنید.

---

## دستورات سریع:

```bash
# یک دستور برای همه مراحل
npm run build && npx cap sync && npx cap open android
```

## پشتیبانی:

برای اطلاعات بیشتر:
- مستندات Capacitor: https://capacitorjs.com/docs
- مستندات Android: https://developer.android.com/studio
