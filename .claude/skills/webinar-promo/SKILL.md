---
name: webinar-promo
description: B2B webinar promóciós csomag készítése (LinkedIn posztok, meghívó email, emlékeztetők, landing szöveg) egy webinar címéből és leírásából. Használd, ha a felhasználó webinárt, online eseményt vagy élő bemutatót akar promótálni.
---

# Webinar promóciós csomag

## Bemenet (kérdezd meg, ami hiányzik)
- Webinar címe, időpontja, előadói
- Célcsoport (szerep + iparág) – ha nincs megadva, a CLAUDE.md ICP-je
- A résztvevő 3 konkrét tanulsága

## Lépések
1. Olvasd be a CLAUDE.md hangját és tiltólistáját.
2. Írj landing oldal szöveget: cím, 3 tanulság felsorolásban, előadó-bio, CTA.
3. Írj 3 LinkedIn posztot: bejelentés (-14 nap), előadói sztori (-7 nap), utolsó hívás (-1 nap).
4. Írj meghívó emailt + 2 emlékeztetőt (-1 nap, -1 óra), mindegyikhez 2 tárgysor-változat.
5. Futtasd a `tartalom-qa` skillt minden szövegen.
6. Mentsd egy fájlba: `ugyfelek/<ugyfel>/kimenet/<ÉÉÉÉ-HH>/webinar-<slug>.md`.

## Szabályok
- Számot csak forrással.
- Egy CTA szövegenként.
