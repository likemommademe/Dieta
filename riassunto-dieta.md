# Riassunto progetto Dieta – "Il Menù di Oggi - Massa"

_Ultimo aggiornamento: 11 novembre 2026_

---

## 1. Cosa abbiamo fatto finora

### Collegamento a GitHub (21 ottobre 2026)
1. **Installata la CLI di GitHub (`gh`)** versione 2.103.0 sul Mac.
   - Non c'era Homebrew, quindi è stata scaricata dal sito ufficiale GitHub:
     https://github.com/cli/cli/releases
   - Si trova in: `~/.local/bin/gh`
   - Aggiunta la riga `export PATH="$HOME/.local/bin:$PATH"` al file `~/.zshrc`, così il Terminale la trova.
2. **Login fatto** con `gh auth login` (GitHub.com → HTTPS → login dal browser con codice monouso).
   - Account collegato: **likemommademe**
   - Pagina usata per il codice: https://github.com/login/device
3. **Scaricato (clonato) il repository** `likemommademe/Dieta`, prima in Documenti.
4. **Spostata la cartella sulla Scrivania**: ora è in `~/Desktop/Dieta`.

### Decisioni prese
- Il progetto si modifica **direttamente da qui con Claude**, sul file del Mac.
- Flusso di lavoro concordato:
  1. Tu dici cosa cambiare, in parole semplici.
  2. Claude modifica `index.html` sulla Scrivania.
  3. Lo apriamo nel browser e controlli il risultato.
  4. **Solo quando dici tu** le modifiche vengono salvate su GitHub (commit + push).
  5. Se qualcosa non piace, si torna alla versione precedente.
- Le istruzioni passo passo includono sempre il **link diretto** di ogni pagina da aprire.

---

## 2. Link utili

| Cosa | Link |
|---|---|
| Repository su GitHub | https://github.com/likemommademe/Dieta |
| **App online (GitHub Pages)** | https://likemommademe.github.io/Dieta/ |
| Impostazioni GitHub Pages | https://github.com/likemommademe/Dieta/settings/pages |
| Storico modifiche | https://github.com/likemommademe/Dieta/commits/main |
| Login GitHub con codice | https://github.com/login/device |

GitHub Pages è **già attivo**: pubblica il ramo `main`, cartella principale `/`. Ogni modifica salvata su GitHub va online da sola dopo 1–2 minuti.

---

## 3. Struttura del progetto

```
~/Desktop/Dieta/
├── .git/                 ← collegamento a GitHub (non toccare)
├── index.html            ← TUTTA l'app (~1.180 righe: HTML + CSS + JavaScript)
└── riassunto-dieta.md    ← questo file
```

L'app è **un unico file**, `index.html`, diviso così:

| Righe circa | Contenuto |
|---|---|
| 1–9 | Intestazione: titolo, font **Work Sans** (Google Fonts), libreria grafici **Chart.js** |
| 10–180 | **Stile (CSS)**: colori, card, pulsanti, menu in basso |
| 180–205 | **Schermata di login** ("Il Menù di Oggi") |
| 207–410 | **Le 5 sezioni** dell'app |
| 410–430 | **Menu di navigazione** in basso (5 pulsanti) |
| 431–660 | **Dati**: piani alimentari e liste della spesa |
| 660–745 | **Login, logout e password** |
| 745–1183 | **Logica dell'app**: calendario, calorie, peso, foto, impostazioni |

### Le 5 sezioni (menu in basso)
1. 🍽️ **Diario Oggi** (`view-plan`): calendario settimanale, scelta giorno *Allenamento* o *Riposo*, card dei pasti con opzioni da scegliere e "Segna completato", sezione **🔥 Allenamento di Oggi** (corsa, pesi, piscina, casa + minuti).
2. 📅 **Calendario Mensile** (`view-month`): vista del mese, tocchi un giorno per aprirlo.
3. 🛒 **Lista Spesa** (`view-shop`): lista per categorie (frutta e verdura, carboidrati, proteine, pesce, latticini, legumi e grassi, integrazione) con spunte, divisa per settimane.
4. 📈 **Progressi** (`view-weight`): riepilogo calorie di oggi, grafico calorie degli ultimi 7 giorni, media calorie, aggiornamento peso con grafico, **📸 foto fisico**.
5. ⚙️ **Impostazioni** (`view-settings`): profilo attivo, esci/cambia profilo, cambia password, obiettivi di massa (peso di partenza e obiettivo), dati fisici (altezza, età, sesso), caricamento di un nuovo piano dalla nutrizionista in formato `.json`, azzeramento dei dati del profilo.

### Profili e piani alimentari
- Due profili già pronti: **Emanuele** e **Andrea**, ognuno con il suo piano (`EMANUELE_PLAN`, `ANDREA_PLAN`) e la sua lista spesa (`EMANUELE_SHOP`, `ANDREA_SHOP`).
- Ogni piano ha due tipi di giornata: **train** (Allenamento) e **rest** (Riposo).
- Pasti: Colazione, Spuntino mattina, Pranzo, Spuntino pomeriggio, Cena, Condimenti & integrazione.
- Ogni alimento ha un testo e le sue calorie (`{t: "...", k: 170}`): le calorie del giorno si sommano da sole.
- Si possono creare nuovi profili dal login: basta scrivere un nome nuovo.

### Calcoli
- **Metabolismo basale (BMR)** con la formula Mifflin-St Jeor, usando peso, altezza, età e sesso.
- **Calorie dell'allenamento** con i valori MET: corsa 8, pesi 5, piscina 7, casa 4,5.

### Dove vengono salvati i dati
Tutto è salvato **nel browser** (`localStorage`), separato per profilo:
- `menu-oggi-state-v21-<Nome>`: calendario, scelte dei pasti, profilo
- `menu-oggi-weight-v21-<Nome>`: storico del peso
- `menu-oggi-photos-v21-<Nome>`: foto del fisico
- `menu-oggi-custom-plan-<Nome>`: piano `.json` caricato a mano
- `menu-oggi-pwd-<Nome>`: password

⚠️ Questo significa che:
- i dati **restano solo sul dispositivo e sul browser** dove li inserisci: telefono e computer non si sincronizzano;
- se cancelli i dati del browser, **perdi tutto**;
- la password iniziale **1900** è scritta nel codice e il file è pubblico, quindi è solo un "lucchetto" di comodità, non una vera protezione;
- le foto occupano molto spazio, e il browser ha un limite di circa 5 MB.

---

## 4. Stato attuale

- Versione sul Mac **uguale** a quella su GitHub (ultima modifica: 23/09/2026, *"Refactor login UI and enhance button functionality"*).
- Nessuna modifica in sospeso.
- App online su https://likemommademe.github.io/Dieta/

---

## 5. Prossimi passi possibili

1. **Aprire l'app** e fare un giro completo per capire cosa sistemare:
   - dal Mac: doppio clic su `~/Desktop/Dieta/index.html`
   - online: https://likemommademe.github.io/Dieta/
2. **Scrivere la lista delle modifiche** desiderate (pasti, grafica, funzioni, errori).
3. **Modifiche una alla volta** con il flusso del punto 1: modifica → controllo nel browser → salvataggio su GitHub solo quando sei d'accordo.
4. **Sull'iPhone/Android:** aprire il link online e usare "Aggiungi a schermata Home" per averla come un'app.
5. **Idee da valutare:**
   - un pulsante **"Esporta/Importa backup"** dei dati, per non perderli e passarli da un dispositivo all'altro;
   - fissare la versione di Chart.js (ora carica sempre l'ultima, e un aggiornamento potrebbe rompere i grafici);
   - togliere la password predefinita "1900" dal codice;
   - dividere `index.html` in più file (stile, dati, logica) se cresce ancora.

---

## 6. Comandi utili (Terminale)

```bash
cd ~/Desktop/Dieta            # entra nella cartella del progetto
git status                    # vedi se ci sono modifiche non salvate
git pull                      # scarica le ultime modifiche da GitHub
~/.local/bin/gh auth status   # controlla di essere collegato a GitHub
open index.html               # apri l'app nel browser
```

> Non serve scriverli a mano: basta chiedere a Claude.
