# Konten und Stämme einrichten (Firebase, kostenlos)

Dauert etwa 10 Minuten und geht komplett im Browser.

1. Öffne https://console.firebase.google.com und melde dich mit einem Google-Konto an.
2. **Projekt hinzufügen**, einen Namen vergeben (z. B. `stamm-lager`), Google Analytics kannst du ausschalten.
3. **Build → Authentication → Los geht's → Anmeldemethode → E-Mail/Passwort** aktivieren (nur den ersten Schalter) und speichern.
4. **Build → Firestore Database → Datenbank erstellen**, Standort `eur3 (europe-west)` wählen, **Produktionsmodus** starten.
5. In Firestore den Tab **Regeln** öffnen, den gesamten Inhalt durch den Text aus `firebase-rules.txt` ersetzen und **Veröffentlichen** tippen.
6. Auf der Projektübersicht das Symbol **</>** (Web-App) wählen, einen Namen vergeben, **App registrieren**. Firebase zeigt dir ein Objekt `firebaseConfig = { ... }`.
7. Öffne `firebase-config.js` und ersetze `null` durch dieses Objekt:
   `window.FIREBASE_CONFIG = { apiKey: "...", authDomain: "...", projectId: "...", appId: "..." };`
8. Lade alle Dateien auf GitHub hoch (wie beim letzten Update) und öffne die App neu.

Danach erscheint im Tab **👥 Stamm** die Anmeldung. Der erste Nutzer registriert sich, gründet den Stamm und zeigt den QR-Code zum Einladen.

## Rollen
- **Stammesleitung** und **Materialwart**: gleiche Rechte. Sie bearbeiten das Material (hinzufügen, ändern, löschen), geben Beitrittsanfragen frei, legen Rollen fest und erlauben Beobachtern befristet das Bearbeiten.
- **Beobachter**: sehen alles live, ändern aber nichts. Mit einer befristeten Erlaubnis (1 Stunde bis 7 Tage) können sie bearbeiten, danach wieder nur lesen.
- Der **Ersteller** wählt beim Gründen, ob er Stammesleitung oder Materialwart ist. Jeder mit diesen beiden Rollen kann seine eigene Rolle zwischen beiden wechseln und die Rollen der anderen ändern. Nur der Ersteller kann von anderen nicht herabgestuft oder entfernt werden.

## Gut zu wissen
- Als Benutzername dient „Vorname Nachname“ (intern wird daraus eine technische Adresse gebildet). Zwei Personen mit gleichem Namen brauchen eine kleine Unterscheidung im Nachnamen (z. B. „Müller2“).
- Es gibt keine „Passwort vergessen“-Funktion, weil keine echte E-Mail-Adresse hinterlegt ist. Im Firebase-Projekt (Authentication → Benutzer) kann ein Konto gelöscht werden, die Person registriert sich dann neu.
- Die Konfigurationswerte in `firebase-config.js` sind nicht geheim. Geschützt sind die Daten durch die Regeln aus Schritt 5. Veröffentliche sie deshalb unbedingt.
- Gleichzeitige Änderungen mehrerer Personen werden automatisch zusammengeführt. Ändern zwei Personen genau dasselbe Objekt, gewinnt die zuletzt gespeicherte Änderung.
