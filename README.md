# Spesa

Shared grocery list. Firebase Realtime Database, project `groceries-d6616`, node `lists/casa`.

- Repo: `stefanoamato93-wq/spesa` (GitHub Pages)
- Data: `lists/casa/cats/{catId}` = `{ name, order, collapsed, items: { {itemId}: { name, order, need } } }`

## Siri Shortcut "Aggiungi spesa"
1. Richiedi input ("Cosa compro?").
2. URL action: `https://groceries-d6616-default-rtdb.europe-west1.firebasedatabase.app/lists/casa/inbox.json`
3. Ottieni contenuti dell'URL: POST, JSON body `name` = Richiedi input, `source` = `siri`.

The app reads `lists/casa/inbox` when open. Each entry is claimed once with a transaction, then deleted.
"latte, uova e pane" becomes 3 items. Without commas ("acqua pomodori patate", Siri often drops them) `splitSpoken` reads word by word, longest known item first (up to 3 words), skips articles ("il", "le", "poi"...), and keeps neighbouring unknown words together as one new item. A name that matches an existing item (case, accents and the last vowel ignored, so "pomodoro" = "Pomodori") ticks it as "da comprare". Anything else is added, ticked, to the category "Altro" (created if missing).
Entries wait in the inbox until a device opens the app.

## Version
`APP_VER` in `index.html`, shown small next to the title. Bump it on every push (V1 -> V2 -> V3).

## Changelog
- V1 (1 Nov 2026): version label next to the title; Siri inbox + spoken lists.
- 1 Nov 2026: Siri inbox (`processInbox`).
- 1 Nov 2026: Siri lists without commas (`splitSpoken`).
