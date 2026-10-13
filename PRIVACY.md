# Datenschutzerklärung für TUWien Autologin

Stand: 13. Oktober 2026

TUWien Autologin füllt Anmeldeformulare der TU Wien aus und kann diese automatisch absenden. Optional erzeugt die Erweiterung zeitbasierte Einmalcodes (TOTP) aus einem vom Nutzer eingegebenen Einrichtungsschlüssel. Diese Erklärung gilt für die Firefox- und Chrome-Version.

## Verarbeitete Daten und Zweck

- Vom Nutzer eingegebener Benutzername bzw. E-Mail-Adresse und Passwort zur Anmeldung bei TU Wien.
- Optional ein TOTP-Einrichtungsschlüssel und dessen Parameter zur lokalen Erzeugung von Einmalcodes.
- Einstellungen zur automatischen Anmeldung und optionale CSS-Selektoren zur Erkennung von Formularfeldern.
- Auf erlaubten TU-Wien-Seiten: aktuelle Seitenadresse, Formularziele, Formularfelder und relevante Beschriftungen zur Erkennung und sicheren Verarbeitung von Anmeldeformularen. Die Erweiterung archiviert keine Seiteninhalte.
- Technische Daten zur Begrenzung automatischer Anmeldeversuche: Website-Ursprung, gegebenenfalls die SimpleSAML-Anmeldekennung `AuthState`, Anmeldestufe und Zeitpunkte automatischer Versuche. Zusätzlich werden ein SHA-256-Fingerabdruck des TOTP-Schlüssels mit seinen Parametern und das Ende des reservierten Code-Zeitfensters gespeichert, um die automatische Wiederverwendung eines Codes zu vermeiden.

Die Erweiterung verarbeitet diese Daten ausschließlich für die vom Nutzer eingerichtete Anmeldung und deren technische Schutzmechanismen. Sie verwendet keine Analyse-, Werbe- oder Trackingdienste und erstellt keinen allgemeinen Browserverlauf. Ihre Websiteberechtigungen sind auf HTTPS-Seiten unter `tuwien.ac.at` und `tuwien.at` einschließlich ihrer Subdomains beschränkt.

## Speicherung und Sicherheit

Zugangsdaten, TOTP-Schlüssel, Einstellungen und technische Anmeldedaten werden lokal im Browserprofil über `storage.local` gespeichert. Die Erweiterung synchronisiert diese Daten nicht zwischen Geräten und verschlüsselt sie nicht selbst. Personen oder Programme mit Zugriff auf das Browserprofil können sie möglicherweise auslesen. Die gemeinsame Speicherung von Passwort und TOTP-Schlüssel verringert den Schutz durch getrennte Authentifizierungsfaktoren.

Einmalcodes werden lokal erzeugt. Der TOTP-Einrichtungsschlüssel wird nicht in Anmeldeformulare eingetragen. Die Erweiterung berücksichtigt für Wiederholungsgrenzen nur Versuche der letzten zehn Minuten; ältere Einträge werden bei späterer Verarbeitung bereinigt. Dies ist keine garantierte automatische Löschung nach zehn Minuten. Auch der zuletzt gespeicherte TOTP-Fingerabdruck kann bis zum Überschreiben oder Löschen gespeichert bleiben.

## Übermittlung und Empfänger

Die Erweiterung trägt Benutzername, Passwort und gegebenenfalls einen erzeugten Einmalcode in passende Anmeldeformulare auf erlaubten TU-Wien-Seiten ein. Bei aktivierter automatischer Anmeldung sendet sie diese Formulare über HTTPS an erlaubte TU-Wien-Ziele ab. Die weitere Verarbeitung durch TU Wien unterliegt deren eigenen Datenschutzbestimmungen.

Die Erweiterung sendet keine Zugangsdaten, TOTP-Schlüssel, Seiteninhalte oder technischen Anmeldedaten an den Entwickler, Werbeanbieter oder Analysedienste. Nutzerdaten werden weder verkauft noch für Werbung, Bonitätsbewertungen oder Darlehensentscheidungen verwendet. Der Entwickler hat über die Erweiterung keinen Zugriff auf die lokal gespeicherten Daten.

Browser, Erweiterungsstores und GitHub können beim Abruf von Updates bzw. beim Öffnen von Projektlinks Daten nach ihren eigenen Datenschutzbestimmungen verarbeiten. Dies ist von der hier beschriebenen lokalen Anmeldefunktion getrennt.

## Kontrolle und Löschung

Nutzer können ihre Konfiguration auf der Einstellungsseite ändern und die automatische Anmeldung deaktivieren. Ein leeres TOTP-Eingabefeld erhält einen bereits gespeicherten Schlüssel; zum Entfernen ist die entsprechende Option zum Entfernen des gespeicherten Schlüssels zu verwenden und zu speichern.

**Delete credentials** löscht sämtliche von der Erweiterung in `storage.local` gespeicherten Daten einschließlich Einstellungen und technischer Anmeldedaten. **Reset retry limits** löscht nur die gespeicherten Wiederholungsgrenzen. Zugangsdaten und Einstellungen bleiben grundsätzlich bis zum Ändern oder Löschen gespeichert. Bereits an TU Wien übermittelte Daten werden dadurch nicht dort gelöscht.

## Beschränkte Datennutzung / Limited Use

TUWien Autologin verwendet und übermittelt Nutzerdaten ausschließlich zur beschriebenen Anmeldefunktion und im Einklang mit der Chrome Web Store User Data Policy einschließlich der Limited-Use-Anforderungen. Die Erweiterung verwendet keine Nutzerdaten für personalisierte Werbung, überträgt sie nicht an Datenhändler und ermöglicht dem Entwickler keinen menschlichen Zugriff auf lokal gespeicherte Anmeldedaten.

## Kontakt und Änderungen

Projekt und Kontakt: [ThomasW2005 auf GitHub](https://github.com/ThomasW2005/tuwien-auto-login). Fragen können über die dortigen Kontaktmöglichkeiten bzw. Issues gestellt werden. Bitte niemals Passwörter, TOTP-Schlüssel oder andere vertrauliche Anmeldedaten in öffentliche Issues schreiben.

Bei Änderungen der Datenverarbeitung wird diese Datei aktualisiert und die Offenlegung im jeweiligen Erweiterungsstore entsprechend angepasst.
