# Cyberattacchi in Italia – dataviz Radar QN

Sette dataviz interattive (HTML + D3 v7) per l'articolo di Radar – QN sui cyberattacchi in Italia, da incorporare nel CMS con un iframe. Ogni pagina legge il proprio CSV da `data/`: per aggiornare un grafico basta cambiare il CSV.

Indice con anteprime desktop e mobile e snippet da copiare: `index.html` (https://lorenzobuonarosa.github.io/cyberattacchi/, quando GitHub Pages sarà attivo dalla root di `main`).

| # | Cartella | Titolo | Dati | Fonte |
|---|---|---|---|---|
| 1 | `crescita/` | In Italia gli attacchi gravi sono cresciuti più che nel resto del mondo | `data/crescita.csv` | Clusit, Rapporto 2026 sulla sicurezza ICT in Italia |
| 2 | `tipi-attacco/` | Metà degli attacchi sono DDoS, ma i danni li fa il ransomware | `data/tipi-attacco.csv`, `data/tipi-attacco-riepilogo.csv` | ENISA, Threat Landscape 2026 (dati 1 gennaio – 31 dicembre 2025) |
| 3 | `provenienza/` | Tre attacchi attribuiti su quattro portano a Russia, Cina, Iran e Corea del Nord | `data/provenienza.csv`, `data/provenienza-riepilogo.csv` | EuRepoC, dati estratti il 17/11/2026 |
| 4 | `paesi-colpiti/` | L'Italia è il settimo Paese più colpito al mondo e il terzo in Europa | `data/paesi-colpiti.csv` | EuRepoC, dati estratti il 17/11/2026 |
| 5 | `ddos/` | Gli attacchi DDoS degli hacktivisti fanno sempre meno danni | `data/ddos.csv` | ACN, Operational Summary mensili |
| 6 | `attacchi-italia/` | Ospedali, Comuni e fornitori fermi per settimane | `data/attacchi-italia.csv` | EuRepoC; ACN, Operational Summary mensili; Il Piccolo, Rai News |
| 7 | `settori/` | Nel 2026 gli attacchi si spostano dalla pubblica amministrazione alle imprese | `data/settori.csv` | ACN, Operational Summary mensili |

## Note sui dati e trasformazioni

1. **Crescita** – Numero indice calcolato nella pagina: valore dell'anno / valore 2021 × 100, per ciascuna serie. Big number = Italia 2025 / Italia 2021 (507 / 70 = ×7,2); confronto Mondo 5.265 / 2.049 = ×2,6. Variazioni annue nel tooltip calcolate dal CSV.
   **Da verificare sul PDF originale Clusit**: la serie viene da un'infografica del Rapporto Clusit 2026.
   Il dato "4.911 incidenti nel mondo nel primo semestre 2026" dell'annotazione è scritto nel testo, non nel CSV.
2. **Tipi di attacco** – Le righe con `ricavato = sì` (Altro / non determinato 13%, Altro 10%) sono ricavate per differenza: ENISA dà percentuali arrotondate. Sono disegnate tratteggiate, con "≈" e nota nel tooltip. "Motivazione economica" ha la nota "ENISA: quasi il 30%". Il 51% di DDoS del big number è in `data/tipi-attacco-riepilogo.csv`.
3. **Provenienza** – Quota senza responsabile = (incidenti_totali − incidenti_attribuiti) / incidenti_totali = 2.139 / 2.871 = 74,5%, mostrata arrotondata a 75%. Percentuali delle barre come da CSV (una cifra decimale). Russia + Cina + Iran + Corea del Nord = 73,5% degli attribuiti (≈ tre su quattro, titolo).
4. **Paesi colpiti** – Vista Mondo: i primi 25 Paesi del CSV per numero di attacchi; vista Unione europea: righe con `area = ue`. Posizioni in classifica calcolate dal CSV (Italia 7ª al mondo, 3ª nell'Ue). Area delle bolle proporzionale agli attacchi; la vista Ue usa una scala più grande (indicato nella nota sotto il grafico). Colori: Italia rosso, Ue blu, altri Paesi europei blu chiaro, resto del mondo grigio.
5. **DDoS** – Punti senza linea di collegamento (dati sporadici e non omogenei). Ogni punto è la quota di attacchi DDoS del mese che hanno causato disservizi. Il mese con `approssimato = sì` (maggio 2026) è un punto vuoto con "≈". La fascia giugno–agosto 2026 non ha dati. Dicembre 2024 (circa 30%, campagna di NoName057(16)) è stato tolto dal grafico e dal CSV su richiesta della redazione.
6. **Attacchi in Italia** – Carosello a scorrimento orizzontale con aggancio (swipe su mobile, frecce e tastiera su desktop). La parte evidenziata di ogni scheda è la colonna `evidenza`, cercata nel testo di `conseguenza` (se non si trova, la scheda resta senza evidenza).
7. **Settori** – Su mobile (sotto i 520 px) la griglia si divide in due blocchi, 2025 sopra e 2026 sotto, ciascuno con il proprio totale. Righe ordinate per numero totale di presenze nei primi tre (a parità, in ordine alfabetico: Tecnologico e PA locale hanno 11 presenze ciascuno). Totali 2025 e 2026 calcolati dal CSV. Luglio 2026: tre settori a pari merito al 2° posto, tutti mostrati come 2°. La riga del Manifatturiero (1 presenza nel 2025, 8 nel 2026) è in rosso.

## Snippet per il CMS

Ogni snippet è l'iframe seguito dallo script di `assets/embed.min.js` (inline, con `https://lorenzobuonarosa.github.io` come origine accettata). Lo script adatta l'altezza dell'iframe e manda il tema e il colore di sfondo del sito; se in un articolo ci sono più dataviz può restare in ognuna (lavora una volta sola grazie a `__radarQNv2`). Gli snippet completi sono in `index.html`.

```html
<iframe src="https://lorenzobuonarosa.github.io/cyberattacchi/crescita/" width="100%" height="660" frameborder="0" scrolling="no" title="In Italia gli attacchi gravi sono cresciuti più che nel resto del mondo"></iframe>
<iframe src="https://lorenzobuonarosa.github.io/cyberattacchi/tipi-attacco/" width="100%" height="840" frameborder="0" scrolling="no" title="Metà degli attacchi sono DDoS, ma i danni li fa il ransomware"></iframe>
<iframe src="https://lorenzobuonarosa.github.io/cyberattacchi/provenienza/" width="100%" height="700" frameborder="0" scrolling="no" title="Tre attacchi attribuiti su quattro portano a Russia, Cina, Iran e Corea del Nord"></iframe>
<iframe src="https://lorenzobuonarosa.github.io/cyberattacchi/paesi-colpiti/" width="100%" height="790" frameborder="0" scrolling="no" title="L'Italia è il settimo Paese più colpito al mondo e il terzo in Europa"></iframe>
<iframe src="https://lorenzobuonarosa.github.io/cyberattacchi/ddos/" width="100%" height="670" frameborder="0" scrolling="no" title="Gli attacchi DDoS degli hacktivisti fanno sempre meno danni"></iframe>
<iframe src="https://lorenzobuonarosa.github.io/cyberattacchi/attacchi-italia/" width="100%" height="500" frameborder="0" scrolling="no" title="Ospedali, Comuni e fornitori fermi per settimane"></iframe>
<iframe src="https://lorenzobuonarosa.github.io/cyberattacchi/settori/" width="100%" height="580" frameborder="0" scrolling="no" title="Nel 2026 gli attacchi si spostano dalla pubblica amministrazione alle imprese"></iframe>
```

Anteprime senza CMS: `?bg=grigio`, `?bg=bianco`, `?bg=nero`, `?bg=notte` nell'URL forzano lo sfondo (e il tema).
