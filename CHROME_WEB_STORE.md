# Chrome Web Store: Datenschutzangaben

Diese Texte beschreiben die aktuelle Implementierung. Bei Änderungen der Datenverarbeitung müssen sie zusammen mit `PRIVACY.md` aktualisiert werden.

## Beschreibung des alleinigen Zwecks

TUWien Autologin erleichtert die Anmeldung bei TU-Wien-Diensten, indem die Erweiterung passende Anmeldeformulare mit vom Nutzer gespeicherten Zugangsdaten ausfüllt und auf Wunsch automatisch absendet. Optional erzeugt sie lokal zeitbasierte Einmalcodes (TOTP) aus einem vom Nutzer hinterlegten Einrichtungsschlüssel und trägt diese in die MFA-Formulare ein. Die Funktion ist auf HTTPS-Seiten unter tuwien.ac.at und tuwien.at einschließlich ihrer Subdomains beschränkt.

## Begründung für storage

Die Berechtigung storage wird benötigt, um den vom Nutzer eingegebenen Benutzernamen bzw. die E-Mail-Adresse, das Passwort, den optionalen TOTP-Einrichtungsschlüssel und die Konfiguration lokal im Browserprofil zu speichern. Dadurch funktioniert die eingerichtete Anmeldung auch nach Browserneustarts. Außerdem werden technische Daten zur Begrenzung wiederholter Anmeldeversuche und zur Vermeidung mehrfacher automatischer Verwendung desselben TOTP-Codes lokal gespeichert. Die Erweiterung nutzt storage.local, keine Gerätesynchronisierung. Nutzer können die gespeicherten Daten auf der Einstellungsseite löschen.

## Begründung für Hostberechtigung

Der Zugriff auf https://*.tuwien.ac.at/* und https://*.tuwien.at/* ist erforderlich, um Anmeldeformulare auf TU-Wien-Seiten zu erkennen, die vom Nutzer gespeicherten Zugangsdaten und lokal erzeugten TOTP-Codes einzutragen und bei aktivierter automatischer Anmeldung abzusenden. Dazu prüft die Erweiterung die aktuelle Seitenadresse, Formularziele und relevante Formularfelder. Subdomains werden benötigt, da TU-Wien-Dienste verschiedene Hosts verwenden. Es wird kein Zugriff auf fremde Domains oder den allgemeinen Browserverlauf angefordert. Technische Anmeldekennungen und Zeitpunkte werden lokal zur Begrenzung wiederholter Anmeldeversuche verwendet.

## Remote Code

Auswahl: **Nein, ich verwende „Remote Code“ nicht**.

Falls ein Begründungsfeld verfügbar ist:

Der gesamte ausführbare Code ist im Erweiterungspaket enthalten. Die Erweiterung lädt keine externen JavaScript- oder WebAssembly-Dateien und führt keinen nachgeladenen Code über eval() aus. TOTP-Codes werden lokal mit den integrierten Web-Crypto-Funktionen des Browsers erzeugt.

## Datennutzung

Für die aktuelle Implementierung ankreuzen:

- **Personenidentifizierbare Informationen:** eingegebener Benutzername bzw. E-Mail-Adresse.
- **Authentifizierungsdaten:** Passwort, TOTP-Einrichtungsschlüssel, erzeugte Einmalcodes und technische Anmeldekennungen.
- **Webprotokoll:** konservative Offenlegung der lokal verarbeiteten TU-Wien-Seitenadressen und gespeicherten Website-Ursprünge mit Zeitpunkten automatischer Anmeldeversuche; kein allgemeiner Browserverlauf.
- **Websitecontent:** lokale Verarbeitung relevanter Anmeldeformulare, Formularfelder und Beschriftungen; keine Archivierung von Seiteninhalten.

Nicht ankreuzen: Gesundheitsinformationen, Finanzdaten und Zahlungsinformationen, persönliche Kommunikation, Ort und Nutzeraktivität. Die Erweiterung überwacht keine Klicks, Mausbewegungen oder Tastatureingaben zur Aufzeichnung des Nutzerverhaltens. Automatisches Ausfüllen und Absenden sowie technische Wiederholungsgrenzen sind in den Angaben oben offengelegt.

Diese Einordnung legt Googles Definition von Datenverarbeitung zugrunde, die auch ausschließlich lokale Verarbeitung und Speicherung einschließt. Die Kategorien Webprotokoll und Websitecontent sind wegen dieser weiten Definition vorsorglich enthalten.

Alle drei Bestätigungen zur Datennutzung ankreuzen: Es gibt keinen Datenverkauf oder zweckfremden Transfer, keine zweckfremde Verwendung und keine Verwendung zur Bonitätsprüfung oder für Darlehenszwecke. Die Übermittlung von Anmeldedaten an TU Wien dient ausschließlich der vom Nutzer eingerichteten Anmeldung.

## Datenschutzbestimmungen

Datei: [PRIVACY.md](PRIVACY.md).

Nach Veröffentlichung dieser Datei in einem öffentlichen Repository kann die öffentliche GitHub-Dateiseite als URL eingetragen werden. Den tatsächlichen Branch verwenden, zum Beispiel:

`https://github.com/ThomasW2005/tuwien-auto-login/blob/main/PRIVACY.md`

Vor Einreichung prüfen, dass die URL ohne Anmeldung erreichbar ist. Eine lokale Datei oder eine noch nicht gepushte Datei reicht nicht aus.

## Referenzen

- [Google: Datenschutzfelder ausfüllen](https://developer.chrome.com/docs/webstore/cws-dashboard-privacy)
- [Google: User Data FAQ, einschließlich lokaler Verarbeitung](https://developer.chrome.com/docs/webstore/program-policies/user-data-faq)
