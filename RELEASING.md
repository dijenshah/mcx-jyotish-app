# નવું વર્ઝન બહાર પાડવાના પગલાં

1. `pubspec.yaml` માં `version: X.Y.Z+N` વધારો (N દર વખતે +1).
2. `flutter build apk --release --split-per-abi`
3. `tool/sign_release.sh app-*-release.apk` (હંમેશા એ જ release key; lineage જળવાઈ રહે).
4. GitHub Release બનાવો: `gh release create vX.Y.Z app-*-release.apk -R dijenshah/mcx-jyotish-app --title "vX.Y.Z" --notes-file notes_gu.txt`
5. Manifest બનાવો:
   `python3 tool/make_manifest.py --base https://github.com/dijenshah/mcx-jyotish-app/releases/download/vX.Y.Z/ --code N --name X.Y.Z --notes notes_gu.txt app-*-release.apk`
6. `update_manifest.json` આ રિપોમાં `main` પર commit/push કરો. **Release પછી જ** push કરવું, જેથી APK લિંક તૈયાર હોય.
7. ચકાસો: raw manifest URL અને APK લિંક HTTP 200 આપે અને sha256 મેળ ખાય.

Manifest URL (એપમાં બેક કરેલું):
https://raw.githubusercontent.com/dijenshah/mcx-jyotish-app/main/update_manifest.json

⚠️ Keystore (`mcx_release.jks`) અને પાસવર્ડ ક્યારેય અહીં મૂકવા નહીં; તેનો બેકઅપ સુરક્ષિત જગ્યાએ રાખવો – તે ખોવાઈ જાય તો અપડેટ બંધ થઈ જશે.
