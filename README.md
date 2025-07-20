# Min-Max Ant System per Maximum Flow Problem

## Descrizione

Questo progetto implementa l'algoritmo **Min-Max Ant System (MMAS)** per risolvere il problema del **Maximum Flow** su grafi diretti. L'implementazione è fornita sotto forma di Jupyter Notebook e include analisi statistiche complete con visualizzazioni grafiche.

## Caratteristiche Principali

### Algoritmo MMAS
- ✅ **Deposito selettivo**: Solo la miglior formica può depositare feromone
- ✅ **Controllo limiti**: Valori τ_min e τ_max per evitare stagnazione
- ✅ **Inizializzazione ottimizzata**: Tutti gli archi iniziano con τ_max per favorire l'esplorazione
- ✅ **Evaporazione controllata**: Convergenza stabile e graduale
- ✅ **Prevenzione cicli**: Evita percorsi ciclici durante la costruzione delle soluzioni

### Funzionalità
- Esecuzione automatica di 10 run indipendenti
- Calcolo statistiche complete (best, mean, std dev, iterazioni medie, valutazioni)
- Visualizzazione grafica della convergenza
- Salvataggio automatico dei risultati
- Monitoraggio dettagliato dell'algoritmo (opzionale)

## Struttura del Progetto

```
├── ScriptMMAS.ipynb                    # Notebook principale con implementazione MMAS
├── network_160.txt                     # File di istanza di esempio
├── README.md                           # Questo file
├── istanze/                            # Cartella contenente reti di esempio per il testing
├── risultati_grafici/                  # Cartella contenente i risultati delle istanze testate
└── Francesco_Prospero_Antonio_VIRZI_1000.pdf  # Documentazione completa del progetto
```

## Prerequisiti

### Librerie Python Richieste
```bash
pip install networkx matplotlib numpy statistics random
```

### Versioni Consigliate
- Python 3.8+
- NetworkX 2.8+
- Matplotlib 3.5+
- NumPy 1.21+

## Installazione e Configurazione

### 1. Clona o scarica il progetto
```bash
git clone <repository-url>
cd mmas-maximum-flow
```

### 2. Installa le dipendenze
```bash
pip install -r requirements.txt
```

### 3. Utilizza le istanze fornite o prepara nuove istanze

Il progetto include diverse **reti di esempio** nella cartella `istanze/`

I **risultati delle istanze testate** sono disponibili nella cartella `risultati_grafici/` con i grafici di convergenza corrispondenti.

Per creare nuove istanze, il file di input deve seguire questo formato:
```
<numero_nodi>
<numero_archi>
<nodo_sorgente>
<nodo_pozzo>
<u1> <v1> <capacità1>
<u2> <v2> <capacità2>
...
```

**Esempio (network_160.txt):**
```
6
10
0
5
0 1 16
0 2 13
1 2 4
1 3 12
2 1 4
2 4 14
3 2 9
3 5 20
4 3 7
4 5 4
```

## Documentazione Completa

📄 **Documentazione dettagliata**: Consultare il file `Francesco_Prospero_Antonio_VIRZI_1000.pdf` per:
- Analisi teorica approfondita dell'algoritmo MMAS
- Risultati sperimentali completi
- Comparazione con altri approcci
- Analisi della complessità computazionale
- Bibliografia e riferimenti accademici

## Istanze di Test Fornite

Il progetto include diverse reti di test nella cartella `istanze/`:


### Risultati Pre-calcolati
La cartella `risultati_grafici/` contiene i grafici di convergenza per tutte le istanze testate, permettendo confronti immediati delle prestazioni.

## Utilizzo

### Esecuzione Standard con Istanze Fornite

1. **Apri il notebook** `ScriptMMAS.ipynb` in Jupyter
2. **Scegli un'istanza** dalla cartella `istanze/` o configura il percorso nel Blocco 3:
   ```python
   # Esempi di istanze disponibili:
   file_path = "istanze/network_160.txt"     # Rete standard
   file_path = "istanze/network_small.txt"   # Rete piccola  
   file_path = "istanze/network_large.txt"   # Rete complessa
   ```
3. **Esegui tutti i blocchi** in sequenza (Cells → Run All)
4. **Confronta i risultati** con quelli in `risultati_grafici/`

### Configurazione Parametri

Nel **Blocco 1**, modifica i parametri MMAS secondo necessità:

```python
# Parametri principali
alpha = 1.0      # Importanza del feromone (α)
beta = 2.0       # Importanza dell'euristica (β) 
rho = 0.1        # Tasso di evaporazione (ρ)
Q = 100.0        # Costante per deposito feromone

# Parametri specifici MMAS
tau_max = 10.0   # Valore massimo feromone
tau_min = 0.01   # Valore minimo feromone
```

Nel **Blocco 11**, configura l'esperimento:

```python
runs = 10           # Numero di esecuzioni indipendenti
iter_max = 20000    # Massimo iterazioni per run
```

### Modalità Verbose

Per visualizzare il tracciamento dettagliato:
- Nel **Blocco 8**, imposta `verbose=True` nella chiamata a `MMAS_single_run()`
- Verrà mostrato il percorso di ogni formica e gli aggiornamenti del feromone

## Output e Risultati

### Statistiche Quantitative
L'algoritmo produce automaticamente:

1. **Valore massimo del flusso trovato (best)**
2. **Media dei valori massimi su 10 run (mean)**
3. **Deviazione standard (std dev)**
4. **Numero medio di iterazioni per migliore soluzione**
5. **Numero medio di valutazioni funzione obiettivo**

### Visualizzazioni
- **Grafico di convergenza**: Mostra l'evoluzione del flusso per tutti i 10 run
- **Annotazioni iterazioni**: Numero di iterazioni necessarie per ogni run
- **Evidenziazione run migliore**: Il run con convergenza più veloce
- **Salvataggio automatico**: File PNG in `risultati_grafici/`

### Esempio Output
```
📊 RISULTATI FINALI - STATISTICHE MIN-MAX ANT SYSTEM (10 RUNS)
==============================================================
(1) Valore massimo del flusso trovato (best): 23.00
(2) Media dei valori massimi (mean): 22.80
(3) Deviazione standard (std dev): 0.42
(4) Numero medio di iterazioni per migliore soluzione: 145.3
(5) Numero medio di valutazioni funzione obiettivo: 2847.2
```

## Struttura dell'Algoritmo

### Fasi Principali

1. **Inizializzazione**: Tutti gli archi con feromone = τ_max
2. **Costruzione soluzioni**: Regola di transizione probabilistica
3. **Valutazione**: Calcolo flusso per ogni cammino valido
4. **Aggiornamento feromone**: Solo dalla miglior formica
5. **Applicazione limiti**: Mantenimento τ_min ≤ τ ≤ τ_max

### Regola di Transizione
```
P(i,j) = [τ(i,j)^α × η(i,j)^β] / Σ[τ(i,k)^α × η(i,k)^β]
```
Dove:
- τ(i,j) = livello di feromone sull'arco (i,j)
- η(i,j) = informazione euristica (capacità dell'arco)

## Personalizzazione

### Modifica Parametri Algoritmo
Sperimenta con diversi valori per ottimizzare le prestazioni:

- **α più alto**: Maggiore importanza al feromone (intensificazione)
- **β più alto**: Maggiore importanza alla capacità (greedy)
- **ρ più basso**: Evaporazione più lenta (memoria più lunga)
- **τ_max/τ_min più stretti**: Convergenza più controllata

### Aggiunta Nuove Istanze
1. Crea file di testo nel formato richiesto
2. Modifica `file_path` nel Blocco 3
3. Esegui l'esperimento

### Estensioni Possibili
- Implementazione di altre varianti ACO (AS, ACS, etc.)
- Aggiunta di operatori di ricerca locale
- Parallelizzazione delle formiche
- Adattamento dinamico dei parametri

## Troubleshooting

### Errori Comuni

**File not found**
```
FileNotFoundError: [Errno 2] No such file or directory
```
→ Verificare il percorso del file di istanza

**Formato file non valido**
```
ValueError: invalid literal for int()
```
→ Controllare che il file rispetti esattamente il formato richiesto

**Convergenza lenta**
→ Ridurre `rho` o aumentare `tau_max`

**Stagnazione precoce**
→ Aumentare `rho` o ridurre `tau_min`

### Ottimizzazione Prestazioni

- **Run troppo lunghi**: Ridurre `iter_max`
- **Qualità insufficiente**: Aumentare numero di run
- **Memory issues**: Ridurre dimensione grafo o `iter_max`

## Contributi

Sono benvenuti contributi per:
- Ottimizzazioni algoritmiche
- Nuove funzionalità di visualizzazione
- Supporto per formati di input aggiuntivi
- Documentazione migliorata

## Licenza

Questo progetto è rilasciato sotto licenza MIT. Vedi il file LICENSE per dettagli.

## Riferimenti

1. Stützle, T., & Hoos, H. H. (2000). MAX–MIN ant system. Future generation computer systems, 16(8), 889-914.
2. Dorigo, M., & Gambardella, L. M. (1997). Ant colony system: a cooperative learning approach to the traveling salesman problem. IEEE Transactions on evolutionary computation, 1(1), 53-66.
3. Ford, L. R., & Fulkerson, D. R. (1956). Maximal flow through a network. Canadian journal of Mathematics, 8(3), 399-404.

---

**Autore**: [Nome Autore]  
**Data**: [Data]  
**Versione**: 1.0