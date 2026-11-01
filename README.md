# Spesa

Shared grocery list. Firebase Realtime Database, project `groceries-d6616`, node `lists/casa`.

- Repo: `stefanoamato93-wq/spesa` (GitHub Pages)
- Data: `lists/casa/cats/{catId}` = `{ name, order, collapsed, items: { {itemId}: { name, order, need } } }`

## Siri Shortcut "Aggiungi spesa"
1. Richiedi input ("Cosa compro?").
2. URL action: `https://groceries-d6616-default-rtdb.europe-west1.firebasedatabase.app/lists/casa/inbox.json`
3. Ottieni contenuti dell'URL: POST, JSON body `name` = Richiedi input, `source` = `siri`.

The app reads `lists/casa/inbox` when open. Each entry is claimed once with a transaction, then deleted.
"latte, uova e pane" becomes 3 items. A name that matches an existing item (case, accents and the last vowel ignored, so "pomodoro" = "Pomodori") ticks it as "da comprare". Anything else is added, ticked, to the category "Altro" (created if missing).
Entries wait in the inbox until a device opens the app.

## Changelog
- 1 Nov 2026: Siri inbox (`processInbox`).
