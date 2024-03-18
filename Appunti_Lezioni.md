# APPUNTI DEL CORSO _RETI DI CALCOLATORI_ DEL CORSO DI INFORMATICA (UNIMI)

## Indice
- [Lezione 1 - Introduzione](#lezione-1---introduzione)  
- [Lezione 2](#lezione-2)
    - [Introduzione ai router](#introduzione-ai-router)
    - [Il concetto di pacchetto](#il-concetto-di-pacchetto)


### LEZIONE 1 - INTRODUZIONE
Per prima cosa va introdotto il concetto di **_rete_**: sistema distribuito di computer.  

![first img](img/img1.jpg)

A, B, C e D sono macchine distribuite geograficamente e non necessariamente connesse fra di loro, ma interconnettibili attraverso un **sistema di rete**.  

#### Cosa fa un sistema di rete:
un sistema di rete crea i canali che consentono ad un calcolatore di entrare in connessione con un server per effettuare operazioni come lo scambio di file.  
Per creare questo sistema di rete bisogna capire cosa aggiungere al **sistema operativo** di ogni macchina.  

Un sistema di rete è possibile considerarlo come un vero e proprio grafo e i suoi nodi sono i cosiddetti **apparati di rete**.  

Tutto ciò che interagisce con l'utente finale fa riferimento ad un host computer.  

Un dispositivo molto importante che vedremo durante il corso è il **router**, che sono apparati dedicati a svolgere solo funzioni di rete. 


### LEZIONE 2
#### Introduzione ai router
**_HOP_ -->** "Salto". Si tratta di un passaggio un nodo ad un altro. Ogni hop ha un costo, poiché la trasmissione ha bisogno di tempo per essere attuata.  

Vediamo l'interno di un **router**:

![interno router](img/interno_router.png)

Il collegamento fra una porta del router e un dispositivo connesso è chiamato ***link di ingresso/uscita**. Essi hanno dei **buffer** gestiti esattamente come delle code.  
Sono i dati all'interno dei buffer che necessitano della gestione da parte dell'**interprete** e conseguentemente anche delle **tabelle di routing**, capendo quindi qual è la porta associata al canale verso il mandare il pacchetto.

I router rappresentano un vero e proprio collo di bottiglia per quanto riguarda le reti internet, anche se in passato era rappresentato proprio dai link di ingresso/uscita.  

I router non fanno altro che decidere il cammino delle informazioni lungo la rete, ma questa decisione può essere presa in più di un modo.  
Nelle situazioni più semplici, la metrica è il numero di nodi, mentre nelle situazioni più "raffinate" è necessario che venga considerato anche il *tempo* come discriminante.  

Definiamo $T_x$ la velocità di trasmissione di un **link**.  

Supponiamo di avere 2 nodi, che chiamiammo $N_1$ e $N_2$, connessi da un canale di comunicazione a 1 MegaBit al secondo (*Mbps*), ovvero 1000000 *bit al secondo*.  
Ecco una rappresentazione grafica:

![connessione nodi](img/connessione_nodi.png)
![clock](img/clock.png)

Semplificando, un impulso elettrico di *5V* equivale al segnale di *1*, mentre quello di *0V* equivale a quello di *0*.

**Quesito:** se voglio passare un'informazione di 1000 *bit* su questo canale (su cui può passare 1*Mbps*), cosa ci interessa sapere?  
È necessario conoscere il **_tempo necessario_** alla porta *I/O* per trasmettere il numero di *bit* specificato. Ci viene in supporto un calcolo:  
$T_x = \frac{1000 bit}{1000000 bps} = \frac{10^3 bit} {10^6 bit} = 10^{-3} bps = 1 ms $  

#### Il concetto di pacchetto
Supponiamo di voler scambiare tra due **host** *A* e *B* un file di dimensione di 1 *Mb*.  
Non è ragionevole inviare il contenuto dell'intero file all'interno della sottorete, poiché ogni router si può trovare dinanzi ad una dimensione potenzialmente enorme di dati rischiando un **_overflow_** in pochissimi *millisecondi*.  
La soluzione più sensata in questo caso sarebbe quella di prendere l'intero file, frammentarlo e trasmettere da *A* a *B* un frammento alla volta: ecco che prende piede il concetto di **_pacchetto_**.  

In rete non passa quindi l'intero file, ma solo i frammenti necessari per poi costruire, a fine trasmissione, il tutto; i pacchetti trasmessi sono vere e proprie *unità dati*, che devono rispettare delle regole ben precise per garantire una trasmissione sicura.  

Il pacchetto è suddiviso in 2 parti fondamentali:
![pacchetto](img/pacchetto.png)

L'*host di provenienza* del pacchetto si occupa chiaramente della frammentazione del file da trasmettere, mentre l'*host di destinazione* si occupa di riassemblare tutti i pacchetti per avere a disposizione il file originale.  

Ovviamente quest'operazione deve essere sicura, nel senso che tutti i dati da trasmettere devono correttametne arrivare a destinazione. Questo aspetto è garantito da 3 fattori:  
1. Il $1^o$ fattore garantisce che i pacchetti vengano ricevuti nell'ordine corretto;  
2. Il $2^o$ fattore garantisce che i pacchetti arrivati non presentino duplicati. Potremmo, ad esempio, introdurre una funzione adibita al controllo di correttezza di una certa sequenza di bit, imponendone inoltre la ritrasmissione nel caso in cui qualcosa fosse andato storto;  
3. Il $3^o$ fattore garantisce l'effettiva correttezza del pacchetto arrivato a destinazione.  

