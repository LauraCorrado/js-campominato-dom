# TRACCIA (old)
L'utente clicca su un bottone che genererà una griglia di gioco quadrata.
Ogni cella ha un numero progressivo, da 1 a 100.
Ci saranno quindi 10 caselle per ognuna delle 10 righe.
Quando l'utente clicca su ogni cella, la cella cliccata si colora di azzurro ed emetto un messaggio in console con il numero della cella cliccata.

# Flow (old)
- Recupero dal DOM l'elemento entro cui creare gli altri elementi e lo salvo in una costante
- Recupero dal DOM il button a cui voglio aggiungere il click event tramite id e lo salvo in una costante
- Dichiaro una funzione nominata con ritorno e senza parametri
    - Istruzioni:
        - Crea un elemento HTML (createElement() method) e lo salvo in una variabile
        - Aggiungo le classi necessarie all'elemento
        - Restituisco l'elemento HTML
- Dichiaro una funzione "newGame()" senza ritorno e senza parametri
    - Istruzioni:
    - Svuoto la griglia
        - Dichiaro una variabile "square" per i quadrati
        - Eseguo un ciclo di 100 iterazioni per creare una griglia 10x10
            - Invoco la funzione di creazione dell'elemento HTML e la memorizzo nella variabile "square"
            - Aggiungo a ciascun elemento creato in "square" un evento click
                - Nella callback function:
                    - Aggiungo all'elemento clickato la classe "clicked-azure"
                    - Stampo su console "Hai cliccato su " + (indice + 1)
            - Aggiungo del testo a ogni elemento creato
            - Aggiungo in coda l'elemento creato all'interno del contenitore recuperato dal DOM
- Aggiungo l'evento click al bottone e invoco la funzione newGame
        

# TRACCIA (new)
Il computer deve generare 16 numeri casuali nello stesso range della difficoltà prescelta: le bombe. Attenzione: **nella stessa cella può essere posizionata al massimo una bomba, perciò nell’array delle bombe non potranno esserci due numeri uguali.
In seguito l'utente clicca su una cella: se il numero è presente nella lista dei numeri generati - abbiamo calpestato una bomba - la cella si colora di rosso e la partita termina. Altrimenti la cella cliccata si colora di azzurro e l'utente può continuare a cliccare sulle altre celle.
La partita termina quando il giocatore clicca su una bomba o quando raggiunge il numero massimo possibile di numeri consentiti (ovvero quando ha rivelato tutte le celle che non sono bombe).
Al termine della partita il software deve comunicare il punteggio, cioè il numero di volte che l’utente ha cliccato su una cella che non era una bomba.
# SUPERBONUS
## 1
Quando si clicca su una bomba e finisce la partita, evitare che si possa cliccare su altre celle.
## 2
Quando si clicca su una bomba e finisce la partita, il software scopre tutte le bombe nascoste

# Flow (new) + SUPERBONUS (1) + SUPERBONUS (2)
.........
- Recupero dal DOM l'elemento h3.score
- Recupero dal DOM le schermate di vittoria e di sconfitta
- Creo una costante BOMBS e le assegno il valore numerico 16
- Creo una variabile flag impostata su true: il gioco è interattivo // SUPERBONUS 1
- Dichiaro un array vuoto (bombsArr)
- Dichiaro una variabile per il punteggio ("score") e la inizializzo a 0
- Creo una funzione "bombsGenerator" con parametro "cells" (numero di celle)
    - Istruzioni:
        - Richiamo la variabile globale (bombsArr) e la svuoto a ogni nuovo ciclo
        - Ciclo l'array finché non contiene lo stesso numero presente in BOMBS
            - Prendo un numero randomico da 1 al numero delle celle e lo salvo nella variabile "random"
            - ? SE il numero random non è già incluso nell'array
                - => inserisco il numero random nell'array
        - Stampo in console l'array per controllare quali celle presenteranno la bomba
.........
- Creo una funzione che riveli tutte le bombe // SUPERBONUS 2
    - Istruzioni:
        - Recupero tutti i div creati restituendoli in una nodelist
        - Creo un ciclo per iterare le bombe contenute nell'array percorrendo il numero totale dei div.square
            - ? SE all'indice del div corrisponde una bomba
                - => Crea una variabile che salvi quella posizione
                - => Rendila visibile aggiungendo la classe .clicked-red
- Creo una funzione per il Game Over // SUPERBONUS 1
    - Istruzioni:
        - Imposto la flag su false: il gioco non è più interattivo
        - Invoco la funzione per rivelare tutte le altre bombe
        - Aggiungo la schermata di sconfitta
- All'inizio della funzione newGame() creata nel primo progetto
    - Aggiungo la classe .d-none alle schermate di sconfitta e di vittoria
    - Inizializzo la variabile flag su true a ogni inizio partita // SUPERBONUS 1
    - Imposto il punteggio a 0
    - Aggiungo come base per ogni start la variabile "score" all'h3.score
    - ...........
    - Invoco la funzione bombsGenerator e, in questo caso, passo come parametro il valore numerico 100 (100 celle per l'esercizio base)
    - All'interno del ciclo for con k < 100 come condizione di uscita
        - Al click del quadrato
            - ? SE la variabile flag è su true // SUPERBONUS 1
                - ? SE l'array delle bombe include la cella clickata
                    - => aggiungo all'elemento clickato la classe "clicked-red"
                    - chiamo la funzione di Game Over
                    - Stampo sul DOM il punteggio
                    - Stampo "Hai pestato una bomba"
                - : ALTRIMENTI
                    - => aggiungo all'elemento clickato la classe "clicked-azure"
                    - Incremento di 1 lo score
                    - Stampo sul DOM il punteggio
                    - Stampo su console "Hai clickato su " + (numero cella)
                    - ? SE il punteggio è uguale alla lunghezza delle caselle meno il numero delle bombe
                        - => Aggiungo la schermata di vittoria
            - : ALTRIMENTI
                - Stampo su console "Il gioco non è attivo. Ricomincia da capo"