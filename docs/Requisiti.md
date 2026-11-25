# Vista generale e Glossario
Il sistema è un'applicazione desktop dotata di un'interfaccia grafica che non prevede accesso remoto o integrazioni con sistemi esterni. L'unico ad interfacciarsi con l'applicazione è l'Operatore che si occupa di inserire sull'applicazione le informazioni relative ai docenti, le aule e le prenotazioni.
| Termine                  | Definizione                                                                                           |
| ----------------------- | ----------------------------------------------------------------------------------------------------- |
| Archivio | Insieme persistente di aule, docenti e prenotazioni. |
| Aula | Luogo fisico soggetto alla prenotazione. |
| Conflitto | Sovrapposizione temporale con un'altra prenotazione della stessa aula o dello stesso docente. |
| Docente | Colui che richiede la prenotazione. Identificato dall'insieme di dati: email univoca, nome e cognome. |
| Fascia oraria | Intervallo di tempo compreso tra una data e ora di inizio e una data e ora di fine. |
| Operatore | Utente che gestisce aule, docenti e prenotazioni attraverso l'interfaccia. |
| Prenotazione | Occupazione di un aula per un tempo definito. |
| Prenotazione ricorrente | Prenotazione che si ripete ad intervalli settimanali fino a una data di termine. |


# Casi d'uso (UC)

## 1. Gestione aula
### UC1 - Inserire aula
Attore: Operatore<br />
Precondizioni: L'archivio è stato caricato<br />
Flusso di eventi:<br />
1. L'operatore sceglie 'nuova aula'. 
2. Il sistema mostra il form di creazione. 
3. L'operatore inserisce il codice univoco, nome, edificio, piano e capienza. 
4. L'operatore invia il form. 
5. Il sistema convalida i dati. 
6. Il sistema crea l'aula. 
7. Il sistema salva l'archivio. 
8. Il sistema mostra la lista aggiornata. 

Flussi alternativi:<br />
- 4a. L'operatore annulla l'operazione
    - Nessuna modifica effettuata all'archivio.
    - L'esecuzione riprende dal passo 1
- 5a. Il codice è già stato utilizzato
    - Il sistema segnala l'errore e non salva l'operazione.
    - L'esecuzione riprende dal passo 2
- 5b. Uno dei campi è mancante o non valido
    - Il sistema segnala l'errore e non salva l'operazione.
    - L'esecuzione riprende dal passo 2

Postcondizioni: Esiste una nuova aula<br />
### UC2 - Modifica aula
Attore: Operatore<br />
Precondizioni: Esiste un'aula<br />
Flusso di eventi:<br />
1. L'Operatore seleziona un'aula dalla lista e sceglie 'Modifica' 
2. Il sistema mostra i dati correnti 
3. L'Operatore modifica uno o più campi. 
4. L'Operatore conferma. 
5. Il sistema convalida i nuovi campi. 
6. Il sistema aggiorna l'archivio. 
7. Il sistema mostra la lista aggiornata. 

Flussi alternativi:<br />
- 4a. L'Operatore annulla l'operazione
    - Nessuna modifica effettuata all'archivio
    - L'esecuzione riprende dal passo 1
- 5a. Uno dei campi è mancante o non valido
    - Il sistema segnala l'errore e non salva l'operazione
    - L'esecuzione riprende dal passo 2

Postcondizioni: I dati dell'aula sono aggiornati<br />
### UC3 - Cancellare un'aula
Attore: Operatore<br />
Precondizioni: Esiste almeno un'aula<br />
Flusso di eventi:<br />
1. L'Operatore seleziona un'aula e sceglie 'Cancella' 
2. Il sistema chiede conferma 
3. L'operatore conferma 
4. Il sistema elimina l'aula 
5. Il sistema salva 
6. Il sistema mostra la lista aggiornata 

Flussi alternativi:<br />
- 3a. L'operatore annulla l'operazione
    - Nessuna modifica effettuata all'archivio
    - L'esecuzione riprende dal passo 1

Postcondizioni: L'aula non è più presente nell'archivio<br />
### UC4 - Visualizzare la lista delle aule
Attore: Operatore<br />
Precondizioni: L'archivio è caricato<br />
Flusso di eventi:<br />
1. L'Operatore apre la sezione Aule 
2. Il sistema mostra tutte le aule con codice, nome, edificio, piano e capienza 

Flussi alternativi:<br />
- 2a. Nessuna aula è presente nell'archivio
    - Il sistema mostra un messaggio di notifica.

Postcondizioni: Nessuna modifica ai dati effettuata<br />
### UC5 - Cercare un'aula
Attore: Operatore<br />
Precondizioni: L'archivio è caricato<br />
Flusso di eventi:<br />
1. L'Operatore inserisce uno o più criteri di ricerca 
2. Il sistema mostra le aule che soddisfano tutti i criteri inseriti 

Flussi alternativi:<br />
- 1a. Nessun criterio
    - L'esecuzione riprende da UC4
- 1b. Criteri non validi
    - Messaggio di errore che segnala il criterio non valido
- 2a. Nessun risultato
    - Messaggio di errore 'nessuna aula trovata'

Postcondizioni: Nessuna modifica ai dati effettuata<br />

## 2. Gestione docente
### UC6 - Inserire un docente
Attore: Operatore<br />
Precondizioni: L'archivio è stato caricato<br />
Flusso di eventi:<br />
1. L'operatore sceglie 'nuovo docente'. 
2. Il sistema mostra il form di creazione. 
3. L'operatore inserisce l'email istituzionale univoca, nome e cognome. 
4. L'operatore invia il form. 
5. Il sistema convalida i dati. 
6. Il sistema crea il docente. 
7. Il sistema salva l'archivio. 
8. Il sistema mostra la lista aggiornata. 

Flussi alternativi:<br />
- 4a. L'operatore annulla l'operazione
    - Nessuna modifica effettuata all'archivio.
    - L'esecuzione riprende dal passo 1
- 5a. L'email è già stata utilizzata
    - Il sistema segnala l'errore e non salva l'operazione.
    - L'esecuzione riprende dal passo 3
- 5b. Uno dei campi è mancante o non valido
    - Il sistema segnala l'errore e non salva l'operazione.
    - L'esecuzione riprende dal passo 3

Postcondizioni: Esiste un nuovo docente<br />
### UC7 - Modificare un docente
Attore: Operatore<br />
Precondizioni: Esiste un docente<br />
Flusso di eventi:<br />
1. L'Operatore seleziona un docente dalla lista e sceglie 'Modifica' 
2. Il sistema mostra i dati correnti 
3. L'Operatore modifica uno o più campi. 
4. L'Operatore conferma. 
5. Il sistema convalida i nuovi campi. 
6. Il sistema aggiorna l'archivio. 
7. Il sistema mostra la lista aggiornata. 

Flussi alternativi:<br />
- 4a. L'Operatore annulla l'operazione
    - Nessuna modifica effettuata all'archivio
    - L'esecuzione riprende dal passo 1
- 5a. Uno dei campi è mancante o non valido
    - Il sistema segnala l'errore e non salva l'operazione
    - L'esecuzione riprende dal passo 3

Postcondizioni: I dati del docente sono aggiornati<br />
### UC8 - Cancellare un docente
Attore: Operatore<br />
Precondizioni: Esiste almeno un docente<br />
Flusso di eventi:<br />
1. L'Operatore seleziona un docente e sceglie 'Cancella' 
2. Il sistema chiede conferma 
3. L'operatore conferma 
4. Il sistema elimina il docente 
5. Il sistema salva 
6. Il sistema mostra la lista aggiornata 

Flussi alternativi:<br />
- 3a. L'operatore annulla l'operazione
    - Nessuna modifica effettuata all'archivio
    - L'esecuzione riprende dal passo 1

Postcondizioni: Il docente non è più presente nell'archivio<br />
### UC9 - Visualizzare la lista dei docenti
Attore: Operatore<br />
Precondizioni: L'archivio è caricato<br />
Flusso di eventi:<br />
1. L'Operatore apre la sezione Docenti 
2. Il sistema mostra tutti i docenti con email istituzionale, cognome e nome. 

Flussi alternativi:<br />
- 2a. Nessun docente è presente nell'archivio
    - Il sistema mostra un messaggio di notifica.

Postcondizioni: Nessuna modifica ai dati effettuata<br />
### UC10 - Cercare un docente
Attore: Operatore<br />
Precondizioni: L'archivio è caricato<br />
Flusso di eventi:<br />
1. L'Operatore inserisce uno o più criteri di ricerca 
2. Il sistema mostra i docenti che soddisfano tutti i criteri inseriti 

Flussi alternativi:<br />
- 1a. Nessun criterio
    - L'esecuzione riprende da UC9
- 1b. Criteri non validi
    - Messaggio di errore che segnala il criterio non valido
    - L'esecuzione riprende dal passo 1
- 2a. Nessun risultato
    - Messaggio di errore 'nessun docente trovato'

Postcondizioni: Nessuna modifica ai dati effettuata<br />

## 3. Gestione prenotazioni
### UC11 - Cercare aule disponibili
Attore: Operatore<br />
Precondizioni: Esiste almeno un'aula<br />
Flusso di eventi:<br />
1. L'operatore inserisce i criteri di ricerca quali data, ora di inizio e ora di fine e/o capienza. 
2. Il sistema calcola le aule non occupate in quell'intervallo 
3. Il sistema mostra l'elenco delle aule libere 

Flussi alternativi:<br />
- 1a. Campi non validi (es. Ora di fine precedente all'ora di inizio, capienza negativa)
    - Visualizza un messaggio di errore
    - L'esecuzione riprende dal passo 1
- 3a. Nessuna aula libera
    - Visualizza un messaggio di errore

Postcondizioni: Nessuna<br />
### UC12 - Inserire una prenotazione singola
Attore: Operatore<br />
Precondizioni: Esistono almeno un'aula e un docente<br />
Flusso di eventi:<br />
1. L'Operatore sceglie 'Nuova prenotazione' 
2. Il sistema mostra il form 
3. Compila il form inserendo data e ora di inizio e fine attività, selezionando un'aula, selezionando il docente responsabile, inserendo tipo di attività e denominazione. 
4. Il sistema convalida i dati e verifica le sovrapposizioni (**UC21**)
5. Se non ci sono conflitti, il sistema crea la prenotazione e salva 

Flussi alternativi:<br />
- 3a. Campi inseriti non validi (es. Ora di fine precedente all'ora di inizio, capienza negativa)
    - Visualizza un messaggio di errore
    - Non crea alcuna prenotazione
    - L'esecuzione riprende dal passo 2
- 3b. L'operatore seleziona 'prenotazione ricorrente'
    - L'esecuzione riprende da UC13
- 4a. Si verifica un conflitto
    - La prenotazione non è salvata
    - Viene visualizzato un messaggio di errore
    - L'esecuzione riprende dal passo 2

Postcondizioni: Nessuna<br />
### UC13 - Inserire una prenotazione ricorrente
Attore: Operatore<br />
Precondizioni: Esistono almeno un'aula e un docente.<br />
Flusso di eventi:<br />
1. L'operatore seleziona 'prenotazione ricorrente'. 
2. L'operatore indica la data di termine 
3. Il sistema genera le occorrenze: stesso giorno della settimana e stessa fascia oraria, dalla data di inizio alla data di termine inclusa. 
4. Il sistema verifica le sovrapposizioni per ogni occorrenza (**UC21**)
5. Se nessuna occorrenza è in conflitto il sistema crea l'intera serie e salva 

Flussi alternativi:<br />
- 1a. Campi inseriti non validi
    - Visualizza un messaggio di errore
    - L'esecuzione riprende dal passo 1
- 2a. Data di termine precedente alla data di inizio
    - Visualizza un messaggio di errore
    - L'esecuzione riprende dal passo 1
- 4a. Il sistema rileva delle sovrapposizioni
    - Visualizza un messaggio di errore elencando le date in conflitto
    - Non effettua la creazione della serie di eventi
    - L'esecuzione riprende dal passo 1

Postcondizioni: Nessuna<br />
### UC14 - Visualizzare le prenotazioni
Attore: Operatore<br />
Precondizioni: L'archivio è caricato<br />
Flusso di eventi:<br />
1. L'operatore apre la sezione 'Prenotazioni' 
2. Il sistema mostra le prenotazioni ordinate per data e ora 
3. L'operatore può filtrare per aula e per docente 
4. Il sistema aggiorna la lista 

Flussi alternativi:<br />
- 3a. La visualizzazione filtrata non trova alcuna corrispondenza
    - Visualizza un messaggio di errore

Postcondizioni: Nessuna modifica effettuata<br />
### UC15 - Cancellare la prenotazione singola
Attore: Operatore<br />
Precondizioni: Esiste almeno una prenotazione<br />
Flusso di eventi:<br />
1. L'operatore seleziona una prenotazione e sceglie 'Cancella' (**UC14**)
2. Il sistema chiede conferma 
3. L'operatore conferma 
4. Il sistema elimina solo quella occorrenza e salva. 

Flussi alternativi:<br />
- 1a. La prenotazione appartiene a una serie
    - Il sistema mostra la scelta 'elimina prenotazione singola' o 'elimina serie'
    - L'operatore sceglie 'elimina prenotazione singola'
    - L'esecuzione riprende dal passo 2
- 1b. La prenotazione appartiene a una serie
    - Il sistema mostra la scelta 'elimina prenotazione singola' o 'elimina serie'
    - L'operatore sceglie 'elimina serie'
    - L'esecuzione riprende dal passo UC20.2
- 3a. L'operatore annulla
    - L'esecuzione riprende dal passo 1

Postcondizioni: La prenotazione non è più presente; le altre occorrenze della serie restano<br />
### UC16 - Modificare la prenotazione singola
Attore: Operatore<br />
Precondizioni: Esiste almeno una prenotazione singola<br />
Flusso di eventi:<br />
1. L'operatore seleziona una prenotazione singola e sceglie 'Modifica' (**UC14**)
2. Il sistema mostra i dati correnti 
3. L'operatore modifica i campi 
4. L'operatore conferma 
5. Il sistema verifica la validità dei dati inseriti 
6. Il sistema aggiorna i dati 

Flussi alternativi:<br />
- 3a. L'operatore modifica la prenotazione da singola a ricorrente
    - L'esecuzione riprende da UC17
- 4a. L'operatore annulla
    - L'esecuzione riprende dal passo 1

Postcondizioni: Nessuna<br />
### UC17 - Modificare la prenotazione da singola a ricorrente
Attore: Operatore<br />
Precondizioni: Esiste almeno una prenotazione singola. L'operatore sta modificando una prenotazione singola<br />
Flusso di eventi:<br />
1. L'operatore seleziona 'prenotazione ricorrente'. 
2. L'operatore indica la data di termine 
3. Il sistema genera le occorrenze: stesso giorno della settimana e stessa fascia oraria, dalla data di inizio alla data di termine inclusa. 
4. Il sistema verifica le sovrapposizioni per ogni occorrenza (**UC21**)
5. Se nessuna occorrenza è in conflitto il sistema crea l'intera serie e salva 

Flussi alternativi:<br />
- 1a. Campi inseriti non validi
    - Visualizza un messaggio di errore
    - L'esecuzione riprende dal passo 1
- 1b. L'operatore deseleziona 'prenotazione ricorrente'
    - Nessuna modifica effettuata da questo caso d'uso.
    - L'esecuzione riprende da UC16
- 2a. Data di termine precedente alla data di inizio
    - Visualizza un messaggio di errore
    - L'esecuzione riprende dal passo 1
- 4a. Il sistema rileva delle sovrapposizioni
    - Visualizza un messaggio di errore elencando le date in conflitto
    - Non effettua la creazione della serie di eventi
    - L'esecuzione riprende dal passo 1

Postcondizioni: Nessuna<br />
### UC18 - Modificare la prenotazione ricorrente
Attore: Operatore<br />
Precondizioni: Esiste almeno una prenotazione ricorrente<br />
Flusso di eventi:<br />
1. L'operatore seleziona una prenotazione ricorrente e sceglie 'Modifica' (**UC14**)
2. Il sistema mostra i dati correnti 
3. L'operatore modifica i campi 
4. L'operatore conferma 
5. Il sistema verifica la validità dei dati inseriti 
6. Il sistema aggiorna i dati 

Flussi alternativi:<br />
- 3a. L'operatore modifica la prenotazione da ricorrente a singola
    - L'esecuzione riprende da UC19
- 4a. L'operatore annulla
    - L'esecuzione riprende dal passo 1
- 5a. L'operatore ha modificato la data di termine anticipandola
    - Il sistema verifica se ci sono prenotazioni da rimuovere
    - Il sistema avvisa e chiede conferma
    - Se l'operatore conferma si procede con l'eliminazione delle prenotazioni e l'esecuzione riprende dal passo 6.
    - Se l'operatore annulla l'esecuzione riprende dal passo 3.
- 5b. L'operatore ha modificato la data di termine posticipandola
    - Il sistema verifica se è possibile effettuare le nuove prenotazioni
    - Se possibile, il sistema avvisa e chiede conferma: se l'operatore conferma si procede con la creazione degli eventi, se annulla l'esecuzione riprende dal passo 3.
    - Se non è possibile, il sistema avvisa e l'operazione viene annullata, l'esecuzione riprende dal passo 3.

Postcondizioni: Nessuna<br />
### UC19 - Modificare la prenotazione da ricorrente a singola
Attore: Operatore<br />
Precondizioni: Esiste almeno una prenotazione ricorrente. L'operatore sta modificando una prenotazione ricorrente<br />
Flusso di eventi:<br />
1. L'operatore deseleziona 'prenotazione ricorrente'. 
2. Il sistema verifica se esistono prenotazioni successive, in tal caso le mostra e avvisa che saranno eliminate. 
3. L'operatore conferma. 
4. Il sistema verifica la correttezza dei dati (**UC21**)
5. Il sistema elimina le occorrenze con data non uguale alla data dell'occorrenza modificata. 
6. Il sistema aggiorna i dati. 

Flussi alternativi:<br />
- 1a. Campi inseriti non validi
    - Visualizza un messaggio di errore
    - L'esecuzione riprende dal passo 1
- 1b. L'operatore seleziona 'prenotazione ricorrente'
    - Nessuna modifica effettuata da questo caso d'uso.
    - L'esecuzione riprende da UC18
- 3a. L'operatore annulla
    - L'esecuzione riprende dal passo UC18.1

Postcondizioni: Nessuna<br />
### UC20 - Cancellare tutte le prenotazioni future di una serie
Attore: Operatore<br />
Precondizioni: Esiste una prenotazione appartenente a una serie ricorrente<br />
Flusso di eventi:<br />
1. L'operatore seleziona una prenotazione della serie e sceglie 'Cancella' e poi 'elimina serie'. 
2. Il sistema mostra le occorrenze che saranno eliminate. 
3. Il sistema chiede conferma. 
4. L'operatore conferma. 
5. Il sistema elimina le occorrenze con data successiva o uguale alla data dell'occorrenza eliminata 
6. Il sistema aggiorna i dati. 

Flussi alternativi:<br />
- 2a. Non ci sono occorrenze future
    - Visualizza un messaggio
    - L'esecuzione riprende dal passo 3
- 4a. L'operatore annulla
    - L'esecuzione riprende dal passo 1

Postcondizioni: Nessuna<br />

## 4. Gestione dati
### UC21 - Verificare le sovrapposizioni
Attore: Nessuno<br />
Precondizioni: Note le informazioni di una prenotazione di cui controllare eventuali sovrapposizioni con un insieme di note prenotazioni.<br />
Flusso di eventi:<br />
1. Il sistema cerca prenotazioni della stessa aula con intervallo temporale sovrapposto 
2. Il sistema cerca prenotazioni dello stesso docente con intervallo temporale sovrapposto 
3. Se non trova nulla il risultato è 'nessun conflitto' 

Flussi alternativi:<br />
- 1a. Trovata una prenotazione
    - Esito: 'conflitto'
- 2a. Trovata una prenotazione
    - Esito: 'conflitto'

Postcondizioni: Nessuna modifica ai dati<br />
### UC22 - Salvare e caricare dati nell'archivio
Attore: Nessuno<br />
Precondizioni: Nessuna<br />
Flusso di eventi:<br />
1. All'avvio il sistema legge il file di archivio e carica aule, docenti e prenotazioni 
2. Dopo ogni operazione che modifica i dati, il sistema salva l'archivio su file e aggiorna i propri valori caricati 

Flussi alternativi:<br />
- 1a. File assente
    - Il sistema inizializza l'archivio creando una struttura iniziale dei suoi schemi
- 1b. Errore nella lettura del file
    - Il sistema segnala l'errore e non sovrascrive il file esistente
- 1c. Salvataggio non riuscito
    - Il sistema avvisa l'Operatore

Postcondizioni: Il file riflette lo stato corrente dei dati<br />


# Business flow
| ID   | Business flow                                                       | Priorità    |
| ---- | ------------------------------------------------------------------- | ----------- |
| BF-1 | Inserimento, modifica o eliminazione dei dati relativi a un'aula    | MUST-HAVE   |
| BF-2 | Inserimento, modifica o eliminazione dei dati relativi a un docente | MUST-HAVE   |
| BF-3 | Inserimento o eliminazione dei dati relativi a una prenotazione     | MUST-HAVE   |
| BF-4 | Modifica di una prenotazione                                        | SHOULD-HAVE |

# Requisiti funzionali
| ID | Requisito | Priorità | Caso d'uso |
|----|-----------|----------|------------|
| FI-1 | Il sistema deve consentire di inserire un'aula con codice univoco, nome, edificio, piano e capienza. | MustHave | UC1|
| FI-2 | Il sistema deve consentire di modificare i dati di un'aula | ShouldHave | UC2|
| FI-3 | Il sistema deve consentire l'eliminazione di un'aula | ShouldHave | UC3|
| FI-4 | Il sistema deve visualizzare la lista delle aule | MustHave | UC4|
| FI-5 | Il sistema deve permettere la ricerca di aule per nome, codice o capienza minima | ShouldHave | UC5|
| FI-6 | Il sistema deve consentire di inserire un docente con e-mail istituzionale univoca, nome e cognome | MustHave | UC6|
| FI-7 | Il sistema deve consentire di modificare nome e cognome di un docente | ShouldHave | UC7|
| FI-8 | Il sistema deve consentire di cancellare un docente | NiceToHave | UC8|
| FI-9 | Il sistema deve visualizzare la lista dei docenti ordinata per cognome e nome | NiceToHave | UC9|
| FI-10 | Il sistema deve permettere la ricerca di docenti per cognome, nome o per email | NiceToHave | UC10|
| FI-11 | Il sistema deve permettere di cercare le aule disponibili in una data e fascia oraria | NiceToHave | UC11|
| FI-12 | Il sistema deve consentire di inserire una prenotazione singola con aula, docente, tipo e denominazione attività, data e ora di inizio e fine | MustHave | UC12|
| FI-13 | Il sistema deve consentire di inserire una prenotazione con ricorrenza settimanale e data di termine | MustHave | UC13|
| FI-14 | Il sistema deve visualizzare le prenotazioni ordinate per data e ora | ShouldHave | UC14|
| FI-15 | Il sistema deve permettere di filtrare le prenotazioni per aula o per docente | NiceToHave | UC14|
| FI-16 | Il sistema deve consentire di cancellare una singola prenotazione | ShouldHave | UC15|
| FI-17 | Il sistema deve consentire di cancellare tutte le prenotazioni future di una serie ricorrente | ShouldHave | UC20|
| ED-18 | Il sistema non deve ammettere due prenotazioni sovrapposte per la stessa aula | MustHave | UC21|
| ED-19 | Il sistema non deve ammettere due prenotazioni sovrapposte per lo stesso docente | MustHave | UC21|
| ED-20 | Il sistema deve garantire l'unicità del codice aula e dell'e-mail docente | MustHave | UC1, UC6|
| ED-21 | Il sistema deve validare la correttezza dei dati in ingresso | ShouldHave | UC1, UC2, UC6, UC7, UC12, UC13|
| UI-22 | Il sistema deve chiedere conferma prima di ogni cancellazione | NiceToHave | UC3, UC8, UC15, UC19, UC20|
| UI-23 | Il sistema deve mostrare messaggi di errore comprensibili qualora il sistema necessiti di segnalare un errore | NiceToHave | UC1, UC2, UC4, UC5, UC6, UC7, UC9, UC10, UC11, UC12, UC13, UC14, UC15, UC20|
| ED-24 | Il sistema deve caricare l'archivio da file all'avvio e salvarlo dopo ogni modifica | MustHave | UC22|
| FI-25 | Il sistema deve consentire la modifica delle informazioni di una prenotazione | ShouldHave | UC16, UC17, UC18, UC19|
| FI-26 | Il sistema deve gestire la conversione di una prenotazione singola in una prenotazione ricorrente | NiceToHave | UC17|
| FI-27 | Il sistema deve gestire la conversione di una prenotazione ricorrente in una prenotazione singola | NiceToHave | UC19|

# Requisiti non funzionali
| ID | Requisito | Categoria | Priorità | Verifica |
|----|-----------|-----------|----------|----------|
| NF-1 | L'applicazione deve avere un'interfaccia grafica per tutte le funzionalità | MustHave | Test manuale |
| NF-2 | L'archivio (aule, docenti e prenotazioni) deve essere salvato su file | MustHave |  |
| NF-3 | Il sistema non deve sovrascrivere il file esistente se il caricamento fallisce | MustHave | Test |
| NF-4 | Non è necessaria alcuna preparazione tecnica per usare il programma, i messaggi di errore devono essere chiari affinché sia possibile correggere le operazioni facilmente | ShouldHave |  |
| NF-5 | L'applicazione deve funzionare su differenti piattaforme desktop | NiceToHave |  |
| NF-6 | L'applicazione deve funzionare senza connessione di rete o server esterni | NiceToHave |  |
| NF-7 | Il codice deve essere strutturato in moduli con alta coesione e basso accoppiamento. In particolare si mira a separare interfaccia utente e logica applicativa. | ShouldHave |  |
| NF-8 | Le interfacce dei componenti devono essere documentate con commenti di documentazioni | NiceToHave |  |
| NF-9 | La logica applicativa deve essere coperta da test automatici | MustHave |  |

# Matrice di tracciabilità
|Caso d'uso| Requisiti funzionali | Requisiti non funzionali | Design | Codice | Test |
|----------|----------------------|--------------------------|--------|--------|------|
| UC1| ED-20, UI-23, FI-1, ED-21| NF-4, NF-1||||
| UC2| FI-2, UI-23, ED-21| NF-4, NF-1||||
| UC3| FI-3, UI-22| NF-1||||
| UC4| UI-23, FI-4| NF-4, NF-1||||
| UC5| UI-23, FI-5| NF-4, NF-1||||
| UC6| ED-20, UI-23, FI-6, ED-21| NF-4, NF-1||||
| UC7| UI-23, FI-7, ED-21| NF-4, NF-1||||
| UC8| FI-8, UI-22| NF-1||||
| UC9| UI-23, FI-9| NF-4, NF-1||||
| UC10| FI-10, UI-23| NF-4, NF-1||||
| UC11| UI-23, FI-11| NF-4, NF-1||||
| UC12| UI-23, FI-12, ED-21| NF-4, NF-1||||
| UC13| FI-13, UI-23, ED-21| NF-4, NF-1||||
| UC14| UI-23, FI-15, FI-14| NF-4, NF-1||||
| UC15| FI-16, UI-23, UI-22| NF-1||||
| UC16| FI-25| NF-4, NF-1||||
| UC17| FI-25, FI-26| NF-4, NF-1||||
| UC18| FI-25| NF-4, NF-1||||
| UC19| FI-25, FI-27, UI-22| NF-4, NF-1||||
| UC20| UI-23, FI-17, UI-22| NF-4, NF-1||||
| UC21| ED-18, ED-19| NF-4||||
| UC22| ED-24| NF-4, NF-3, NF-2, NF-6||||
