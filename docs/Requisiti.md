Richiesta informale
>Il programma gestisce i docenti, le aule e le relative prenotazioni per un dipartimento universitario.
>Per ogni docente devono essere registrate le seguenti informazioni: 
>	E-mail istituzionale (univoca) 
>	Nome e cognome 
>Per ogni aula devono essere registrate le seguenti informazioni: 
>	Codice identificativo univoco 
>	Nome, edificio, piano e capienza
>Per ogni prenotazione devono essere registrate le seguenti informazioni: 
>	 Aula prenotata 
>	 Docente responsabile 
>	 Tipo di attività (lezione, esame, seminario, ecc.) 
>	 Denominazione attività (nome del corso, titolo del seminario) 
>	 Data e ora di inizio e di fine 
>	 Eventuale ricorrenza settimanale e relativa data di termine 
>L’applicazione deve avere un’interfaccia grafica (GUI)
>Usando l’interfaccia deve essere possibile:
>	Inserire, modificare e cancellare i dati delle aule 
>	Visualizzare la lista delle aule 
>	Cercare un’aula per nome, codice o capienza minima 
>	Inserire, modificare e cancellare i dati dei docenti 
>	Visualizzare la lista dei docenti, ordinata per cognome e nome 
>	Cercare un utente per cognome o codice identificativo
>	… (continua)
>Usando l’interfaccia deve essere possibile: 
>	Cercare le aule disponibili in una data e fascia oraria 
>	Inserire una prenotazione singola o ricorrente 
>	Visualizzare le prenotazioni ordinate per data e ora, filtrandole per aula o docente
>	Cancellare una singola prenotazione oppure tutte le prenotazioni future di una serie ricorrente
>Non sono ammesse sovrapposizioni 
>	L’aula non può essere occupata contemporaneamente da più docenti
>	Il docente non può essere contemporaneamente in più aule
>L’archivio (aule, docenti, prenotazioni) è salvato su file

---
# Domande su cui fare chiarezza
1. L'operatore conosce il codice univoco dell'aula o deve essere generato all'inserimento?
2. Se l'aula ha prenotazioni associate è possibile eliminarla? Si->le prenotazioni annesse a quell'aula vanno eliminate. No -> segnala e evita che possa essere eliminata se esiste almeno una prenotazione.
3. Il sistema deve rifiutare la cancellazione di un docente con prenotazioni associate?

---
# Vista generale e Glossario
Il sistema è un'applicazione desktop dotata di un'interfaccia grafica che non prevede accesso remoto o integrazioni con sistemi esterni. L'unico ad interfacciarsi con l'applicazione è l'Operatore che si occupa di inserire sull'applicazione le informazioni relative ai docenti, le aule e le prenotazioni.

| Parola                  | Definizione                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------ |
| Docente                 | Colui che richiede la prenotazione. Identificato dall'insieme di dati: (email univoca, nome e cognome) |
| Prenotazione            | Occupazione di un aula per un tempo definito                                                           |
| Prenotazione ricorrente | Prenotazione che si ripete ad intervalli settimanali fino a una data di termine                        |
| Fascia oraria           | Intervallo di tempo compreso tra una data e ora di inizio e una data e ora di fine                     |
| Aula                    | Luogo fisico soggetto alla prenotazione                                                                |

# Casi d'uso (UC)
## 1. Gestione aula
### UC1 - Inserire aula
Attore: Operatore
Precondizioni: L'archivio è stato caricato
Flusso di eventi:
1. L'operatore sceglie "nuova aula".
2. Il sistema mostra il form di creazione.
3. L'operatore inserisce il codice univoco, nome, edificio, piano e capienza.
4. L'operatore invia il form.
5. Il sistema convalida i dati.
6. Il sistema crea l'aula.
7. Il sistema salva l'archivio.
8. Il sistema mostra la lista aggiornata.
Flussi alternativi;
- 4a. L'operatore annulla l'operazione:
	- Nessuna modifica effettuata all'archivio.
	- L'esecuzione riprende dal passo 1.
- 5a.  Il codice è già stato utilizzato:
	- Il sistema segnala l'errore e non salva l'operazione
	- L'esecuzione riprende dal passo 2.
- 5b. Uno dei campi è mancante o non valido:
	- Il sistema segnala l'errore e non salva l'operazione
	- L'esecuzione riprende dal passo 2.
Postcondizione: Esiste una nuova aula

### UC2 - Modifica aula
Attore: Operatore
Precondizione: Esiste un'aula
Flusso di eventi:
1. L'Operatore seleziona un'aula dalla lista e sceglie "Modifica"
2. Il sistema mostra i dati correnti
3. L'Operatore modifica uno o più campi.
4. L'Operatore conferma.
5. Il sistema convalida i nuovi campi.
6. Il sistema aggiorna l'archivio.
7. Il sistema mostra la lista aggiornata.
Flussi alternativi:
- 4a. L'Operatore annulla l'operazione:
	- Nessuna modifica effettuata all'archivio
	- L'esecuzione riprende dal passo 1.
- 5b. Uno dei campi è mancante o non valido:
	- Il sistema segnala l'errore e non salva l'operazione
	- L'esecuzione riprende dal passo 2.
Postcondizione: I dati dell'aula sono aggiornati

### UC3 - Cancellare un aula
Attore: Operatore
Precondizione: Esiste almeno un'aula
Flusso di eventi:
1. L'Operatore seleziona un'aula e sceglie "Cancella"
2. Il sistema chiede conferma
3. L'operatore conferma
4. Il sistema elimina l'aula
5. Il sistema salva
6. Il sistema mostra la lista aggiornata
Flussi alternativi:
- 3a. L'operatore annulla l'operazione:
	- Nessuna modifica effettuata all'archivio
	- L'esecuzione riprende dal passo 1.
Postcondizioni: L'aula non è più presente nell'archivio

### UC4 - Visualizzare la lista delle aule
Attore: Operatore
Precondizione: L'archivio è caricato
Flusso di eventi:
1. L'Operatore apre la sezione Aule
2. Il sistema mostra tutte le aule con codice, nome, edificio, piano e capienza
Flussi alternativi:
- 2a. Nessuna aula è presente nell'archivio:
	- Il sistema mostra un messaggio di notifica.
Postcondizioni: Nessuna modifica ai dati effettuata

### UC5 - Cercare un'aula
Attore: Operatore
Precondizione: L'archivio è caricato
Flusso di eventi:
1. L'Operatore inserisce uno o più criteri di ricerca
2. Il sistema mostra le aule che soddisfano tutti i criteri inseriti
Flussi alternativi:
- 1a. Nessun criterio:
	- Equivale a **UC4**
- 1b. Criteri non validi
	- Messaggio di errore che segnala il criterio non valido
- 2a. Nessun risultato:
	- Messaggio di errore "nessuna aula trovata"
Postcondizioni: Nessuna modifica ai dati effettuata
## 2. Gestione docente
### UC6 - Inserire un docente
Attore: Operatore
Precondizioni: L'archivio è stato caricato
Flusso di eventi:
1. L'operatore sceglie "nuovo docente".
2. Il sistema mostra il form di creazione.
3. L'operatore inserisce il email istituzionale univoca, nome e cognome.
4. L'operatore invia il form.
5. Il sistema convalida i dati.
6. Il sistema crea il docente.
7. Il sistema salva l'archivio.
8. Il sistema mostra la lista aggiornata.
Flussi alternativi;
- 4a. L'operatore annulla l'operazione:
	- Nessuna modifica effettuata all'archivio.
	- L'esecuzione riprende dal passo 1.
- 5a.  L'email è già stata utilizzata:
	- Il sistema segnala l'errore e non salva l'operazione
	- L'esecuzione riprende dal passo 3.
- 5b. Uno dei campi è mancante o non valido:
	- Il sistema segnala l'errore e non salva l'operazione
	- L'esecuzione riprende dal passo 3.
Postcondizione: Esiste un nuovo docente

### UC7 - Modificare un docente
Attore: Operatore
Precondizione: Esiste un docente
Flusso di eventi:
1. L'Operatore seleziona un docente dalla lista e sceglie "Modifica"
2. Il sistema mostra i dati correnti
3. L'Operatore modifica uno o più campi.
4. L'Operatore conferma.
5. Il sistema convalida i nuovi campi.
6. Il sistema aggiorna l'archivio.
7. Il sistema mostra la lista aggiornata.
Flussi alternativi:
- 4a. L'Operatore annulla l'operazione:
	- Nessuna modifica effettuata all'archivio
	- L'esecuzione riprende dal passo 1.
- 5b. Uno dei campi è mancante o non valido:
	- Il sistema segnala l'errore e non salva l'operazione
	- L'esecuzione riprende dal passo 3.
Postcondizione: I dati del docente sono aggiornati

### UC8 - Cancellare un docente
Attore: Operatore
Precondizione: Esiste almeno un docente
Flusso di eventi:
1. L'Operatore seleziona un docente e sceglie "Cancella"
2. Il sistema chiede conferma
3. L'operatore conferma
4. Il sistema elimina il docente
5. Il sistema salva
6. Il sistema mostra la lista aggiornata
Flussi alternativi:
- 3a. L'operatore annulla l'operazione:
	- Nessuna modifica effettuata all'archivio
	- L'esecuzione riprende dal passo 1.
Postcondizioni: Il docente non è più presente nell'archivio

### UC9 - Visualizzare la lista dei docenti
Attore: Operatore
Precondizione: L'archivio è caricato
Flusso di eventi:
1. L'Operatore apre la sezione Docenti
2. Il sistema mostra tutte i docenti con email istituzionale, cognome e nome.
Flussi alternativi:
- 2a. Nessun docente è presente nell'archivio:
	- Il sistema mostra un messaggio di notifica.
Postcondizioni: Nessuna modifica ai dati effettuata

### UC10 - Cercare un docente
Attore: Operatore
Precondizione: L'archivio è caricato
Flusso di eventi:
1. L'Operatore inserisce uno o più criteri di ricerca
2. Il sistema mostra i docenti che soddisfano tutti i criteri inseriti
Flussi alternativi:
- 1a. Nessun criterio:
	- Equivale a **UC9**
- 1b. Criteri non validi
	- Messaggio di errore che segnala il criterio non valido
	- L'esecuzione riprende dal passo 1.
- 2a. Nessun risultato:
	- Messaggio di errore "nessuna docente trovato"
Postcondizioni: Nessuna modifica ai dati effettuata
# 3. Gestione prenotazioni
### UC11 - Cercare aule disponibili
Attore: Operatore
Precondizioni: Esiste almeno un'aula
Flusso di eventi:
1. L'operatore inserisce i criteri di ricerca quali data, ora di inizio e ora di fine e/o capienza.
2. Il sistema calcola le aule non occupate in quell'intervallo
3. Il sistema mostra l'elenco delle aule libere
Flussi alternativi:
- 1a. Campi non validi (es. Ora di fine precedente all'ora di inizio, capienza negativa):
	- Visualizza un messaggio di errore
	- L'esecuzione riprende dal passo 1.
- 3a. Nessuna aula libera:
	- Visualizza un messaggio di errore
### UC12 - Inserire una prenotazione singola
Attore: Operatore
Precondizioni: Esistono almeno un'aula e un docente
Flusso di eventi:
1. L'Operatore sceglie "Nuova prenotazione"
2. Il sistema mostra il form
3. Compila il form inserendo data e ora di inizio e fine attività, selezionando un'aula, selezionando il docente responsabile, inserendo tipo di attività e denominazione.
4. Il sistema convalida i dati e verifica le sovrapposizioni (**UC21**)
5. Se non ci sono conflitti, il sistema crea la prenotazione e salva
Flussi alternativi:
- 3a. Campi inseriti non validi (es. Ora di fine precedente all'ora di inizio, capienza negativa):
	- Visualizza un messaggio di errore
	- Non crea alcuna prenotazione
	- L'esecuzione riprende dal passo 2.
- 3b. L'operatore selezione "prenotazione ricorrente":
	- Si prosegue con **UC13**
- 4a. Si verifica un conflitto:
	- La prenotazione non è salvata
	- Viene visualizzato un messaggio di errore
	- L'esecuzione riprende dal passo 2.
### UC13 - Inserire una prenotazione ricorrente (estende UC12)
Attore: Operatore 
Precondizioni: Esistono almeno un'aula e un docente. 
Flusso di eventi:
1. L'operatore seleziona "prenotazione ricorrente" in **UC12**.
2. L'operatore indica la data di termine
3. Il sistema genera le occorrenze: stesso giorno della settimana e stessa fascia oraria, dalla data di inizio alla data di termine inclusa.
4. Il sistema verifica le sovrapposizioni per ogni occorrenza (**UC21**)
5. Se nessuna occorrenza è in conflitto il sistema crea l'intera serie e salva
Flussi alternativi:
- 1a. Campi inseriti non validi:
	- Visualizza un messaggio di errore
	- L'esecuzione riprende dal passo 1.
- 2a. Data di termine precedente alla data di inizio:
	- Visualizza un messaggio di errore
	- L'esecuzione riprende dal passo 1.
- 4a. Il sistema rileva delle sovrapposizioni (**UC21**):
	- Visualizza un messaggio di errore elencando le date in conflitto
	- Non effettua la creazione della serie di eventi
	- L'esecuzione riprende dal passo 1.
### UC14 - Visualizzare le prenotazioni
Attore: Operatore
Precondizioni: L'archivio è caricato
Flusso di eventi:
1. L'operatore apre la sezione "Prenotazioni"
2. Il sistema mostra le prenotazioni ordinate per data e ora
3. L'operatore può filtrare per aula e per docente
4. Il sistema aggiorna la lista
Flusso alternativo:
- 3a. La visualizzazione filtrata non trova alcuna corrispondenza:
	- Visualizza un messaggio di errore
Postcondizioni: Nessuna modifica effettuata

### UC15 - Cancellare la prenotazione singola
Attore: Operatore
Precondizioni: Esiste almeno una prenotazione
Flusso di eventi: 
1. L'operatore seleziona una prenotazione (**UC14**) e sceglie "Cancella"
2. Il sistema chiede conferma
3. L'operatore conferma
4. Il sistema elimina solo quella occorrenza e salva.
Flusso alternativo:
- 1a. Se la prenotazione appartiene a una serie il sistema mostra la scelta "elimina prenotazione singola" o "elimina serie":
	- "elimina prenotazione singola": L'esecuzione riprende dal passo 2.
	- "elimina serie": L'esecuzione riprende da **UC20.2**.
- 3a. L'operatore annulla:
	- L'esecuzione riprende dal passo 1.
Postcondizioni: La prenotazione non è più presente; le altre occorrenze della serie restano

### UC16 - Modificare la prenotazione singola
Attore: Operatore
Precondizioni: Esiste almeno una prenotazione singola
Flusso di eventi:
1. L'operatore seleziona una prenotazione singola (**UC14**) e sceglie "Modifica"
2. Il sistema mostra i dati correnti
3. L'operatore modifica i campi
4. L'operatore conferma
5. Il sistema verifica la validità dei dati inseriti
6. Il sistema aggiorna i dati
Flussi alternativi:
- 3a. L'operatore modifica la prenotazione da singola a ricorrente:
	- L'esecuzione prosegue con **UC17**.
- 4a. L'operatore annulla:
	- L'esecuzione riprende dal passo 1.
### UC17 - Modificare la prenotazione da singola a ricorrente
Attore: Operatore
Precondizioni: Esiste almeno una prenotazione singola. L'operatore sta modificando una prenotazione singola (**UC16**)
Flusso di eventi:
1. L'operatore seleziona "prenotazione ricorrente" in **UC16**.
2. L'operatore indica la data di termine
3. Il sistema genera le occorrenze: stesso giorno della settimana e stessa fascia oraria, dalla data di inizio alla data di termine inclusa.
4. Il sistema verifica le sovrapposizioni per ogni occorrenza (**UC21**)
5. Se nessuna occorrenza è in conflitto il sistema crea l'intera serie e salva
Flussi alternativi:
- 1a. Campi inseriti non validi:
	- Visualizza un messaggio di errore
	- L'esecuzione riprende dal passo 1.
- 1b. L'operatore deseleziona "prenotazione ricorrente":
	- Nessuna modifica effettuata da **UC17**.
	- L'esecuzione ritorna a **UC16**.
- 2a. Data di termine precedente alla data di inizio:
	- Visualizza un messaggio di errore
	- L'esecuzione riprende dal passo 1.
- 4a. Il sistema rileva delle sovrapposizioni (**UC21**):
	- Visualizza un messaggio di errore elencando le date in conflitto
	- Non effettua la creazione della serie di eventi
	- L'esecuzione riprende dal passo 1.
### UC18 - Modificare la prenotazione ricorrente
Attore: Operatore
Precondizioni: Esiste almeno una prenotazione ricorrente
Flusso di eventi:
1. L'operatore seleziona una prenotazione ricorrente (**UC14**) e sceglie "Modifica"
2. Il sistema mostra i dati correnti
3. L'operatore modifica i campi
4. L'operatore conferma
5. Il sistema verifica la validità dei dati inseriti
6. Il sistema aggiorna i dati
Flussi alternativi:
- 3a. L'operatore modifica la prenotazione da singola a ricorrente:
	- L'esecuzione prosegue con **UC19**.
- 4a. L'operatore annulla:
	- L'esecuzione riprende dal passo 1.
- 5a. Se l'operatore ha modificato la data di termine anticipandola:
	- Il sistema verifica se ci sono prenotazioni da rimuovere
	- Il sistema avvisa e chiede conferma
		- Se l'operatore conferma si procede con l'eliminazione delle prenotazioni e l'esecuzione riprende dal passo 6.
		- Se l'operatore annulla l'esecuzione riprende dal passo 3.
- 5b. Se l'operatore ha modificato la data di termine posticipandola:
	- Il sistema verifica se è possibile effettuare le nuove prenotazioni
		- Se possibile, il sistema avvisa e chiede conferma
			- Se l'operatore conferma si procede con la creazione degli eventi
			- Se l'operatore annulla l'esecuzione riprende dal passo 3.
		- Se non è possibile, il sistema avvisa e l'operazione viene annullata, l'esecuzione riprende dal passo 3.
### UC19 - Modificare la prenotazione da ricorente a singola
Attore: Operatore
Precondizioni: Esiste almeno una prenotazione ricorrente. L'operatore sta modificando una prenotazione ricorrente (**UC18**)
Flusso di eventi:
1. L'operatore deseleziona "prenotazione ricorrente" in **UC16**.
2. Il sistema verifica se esistono prenotazioni successive, in tal caso le mostra e avvisa che saranno eliminate.
3. L'operatore conferma.
4. Il sistema verifica la correttezza dei dati (**UC21**)
5. Il sistema elimina le occorrenze con data successiva alla data dell'occorrenza eliminata.
6. Il sistema aggiorna i dati.
Flussi alternativi:
- 1a. Campi inseriti non validi:
	- Visualizza un messaggio di errore
	- L'esecuzione riprende dal passo 1.
- 1b. L'operatore seleziona "prenotazione ricorrente":
	- Nessuna modifica effettuata da **UC19**.
	- L'esecuzione ritorna a **UC18**.
- 3a. L'operatore annulla:
	- L'esecuzione riprende dal passo **UC18.1**

### UC20 - Cancellare tutte le prenotazioni future di una serie
Attore: Operatore
Precondizioni: Esiste una prenotazione appartenente a una serie ricorrente
Flusso di eventi:
1. L'operatore seleziona una prenotazione della serie e sceglie "Cancella" e poi "elimina serie".
2. Il sistema mostra le occorrenze che saranno eliminate.
3. Il sistema chiede conferma.
4. L'operatore conferma.
5. Il sistema elimina le occorrenze con data successiva o uguale alla data dell'occorrenza eliminata
6. Il sistema aggiorna i dati.
Flussi alternativi:
- 2a. Non ci sono occorrenze future:
	- Visualizza un messaggio
	- L'esecuzione riprende dal passo 3.
- 4a. L'operatore annulla:
	- L'esecuzione riprende dal passo 1.

### UC21 - Verificare le sovrapposizioni
Attore: Nessuno
Precondizioni: Note le informazioni di una prenotazione di cui controllare eventuali sovrapposizioni con un insieme di note prenotazioni.
Flusso di eventi:
1. Il sistema cerca prenotazioni della stessa aula con intervallo temporale sovrapposto
2. Il sistema cerca prenotazioni dello stesso docente con intervallo temporale sovrapposto
3. Se non trova nulla il risultato è "nessun conflitto"
Flussi alternativi:
- 1a. Trovata una prenotazione:
	- Esito: "conflitto"
- 2a. Trovata una prenotazione:
	- Esito: "conflitto"
Postcondizioni: Nessuna modifica ai dati
## 4. Gestione dati
### UC21 - Salvare e caricare dati nell'archivio
Attore: Nessuno
Precondizioni: Nessuna
Flusso di eventi:
1. All'avvio il sistema legge il file di archivio e carica aule, docenti e prenotazioni
2. Dopo ogni operazione che modifica i dati, il sistema salva l'archivio su file e aggiorna i propri valori caricati
Flussi alternativi:
- 1a. File assente:
	- il sistema inizializza l'archivio creando una struttura iniziale dei suoi schemi
- 1b. Errore nella lettura del file:
	- Il sistema segnala l'errore e non sovrascrive il file esistente
- 2a. Salvataggio non riuscito:
	- Il sistema avvisa l'Operatore
Postcondizioni: Il file riflette lo stato corrente dei dati

# Business flow

| ID   | Business flow                                                       | Priorità    |
| ---- | ------------------------------------------------------------------- | ----------- |
| BF-1 | Inserimento, modifica o eliminazione dei dati relativi a un'aula    | MUST-HAVE   |
| BF-2 | Inserimento, modifica o eliminazione dei dati relativi a un docente | MUST-HAVE   |
| BF-3 | Inserimento o eliminazione dei dati relativi a una prenotazione     | MUST-HAVE   |
| BF-4 | Modifica di una prenotazione                                        | SHOULD-HAVE |



# Requisiti funzionali

| ID     | Requisito                                                                                                                                     | Priorità      | Caso d'uso                                                                  |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | --------------------------------------------------------------------------- |
| FI-1.1 | Il sistema deve consentire di inserire un'aula con codice univoco, nome, edificio, piano e capienza.                                          | MUST - HAVE   | UC1                                                                         |
| FI-1.2 | Il sistema deve consentire di modificare i dati di un'aula                                                                                    | SHOULD - HAVE | UC2                                                                         |
| FI-1.3 | Il sistema deve consentire l'eliminazione di un'aula                                                                                          | SHOULD - HAVE | UC3                                                                         |
| FI-1.4 | Il sistema deve visualizzare la lista delle aule                                                                                              | MUST - HAVE   | UC4                                                                         |
| FI-1.5 | Il sistema deve permettere la ricerca di aule per nome, codice o capienza minima                                                              | SHOULD - HAVE | UC5                                                                         |
| FI-2.1 | Il sistema deve consentire di inserire un docente con e-mail istituzionale univoca, nome e cognome                                            | MUST-HAVE     | UC6                                                                         |
| FI-2.2 | Il sistema deve consentire di modificare nome e cognome di un docente                                                                         | SHOULD - HAVE | UC7                                                                         |
| FI-2.3 | Il sistema deve consentire di cancellare un docente                                                                                           | NICE TO HAVE  | UC8                                                                         |
| FI-2.4 | Il sistema deve visualizzare la lista dei docenti ordinata per cognome e nome                                                                 | NICE TO HAVE  | UC9                                                                         |
| FI-2.5 | Il sistema deve permettere la ricerca di docenti per cognome, nome o per email                                                                | NICE TO HAVE  | UC10                                                                        |
| FI-3.1 | Il sistema deve permettere di cercare le aule disponibili in una data e fascia oraria                                                         | NICE TO HAVE  | UC11                                                                        |
| FI-3.2 | Il sistema deve consentire di inserire una prenotazione singola con aula, docente, tipo e denominazione attività, data e ora di inizio e fine | MUST - HAVE   | UC12                                                                        |
| FI-3.3 | Il sistema deve consentire di inserire una prenotazione con ricorrenza settimanale e data di termine                                          | MUST - HAVE   | UC13                                                                        |
| FI-3.4 | Il sistema deve visualizzare le prenotazioni ordinate per data e ora                                                                          | SHOULD - HAVE | UC14                                                                        |
| FI-3.5 | Il sistema deve permettere di filtrare le prenotazioni per aula o per docente                                                                 | NICE TO HAVE  | UC14                                                                        |
| FI-3.6 | Il sistema deve consentire di cancellare una singola prenotazione                                                                             | SHOULD HAVE   | UC15                                                                        |
| FI-3.7 | Il sistema deve consentire di cancellare tutte le prenotazioni future di una serie ricorrente                                                 | SHOULD HAVE   | UC20                                                                        |
| ED-4.1 | Il sistema non deve ammettere due prenotazioni sovrapposte per la stessa aula                                                                 | MUST - HAVE   | UC21                                                                        |
| ED-4.2 | Il sistema non deve ammettere due prenotazioni sovrapposte per lo stesso docente                                                              | MUST - HAVE   | UC21                                                                        |
| ED-4.3 | Il sistema deve garantire l'unicità del codice aula e dell'e-mail docente                                                                     | MUST - HAVE   | UC1, UC6                                                                    |
| ED-4.4 | Il sistema deve validare la correttezza dei dati in ingresso                                                                                  | SHOULD - HAVE | UC1, UC2, UC6, UC7, UC12, UC13                                              |
| UI-4.5 | Il sistema deve chiedere conferma prima di ogni cancellazione                                                                                 | NICE TO HAVE  | UC3, UC8, UC15, UC20                                                        |
| UI-4.6 | Il sistema deve mostrare messaggi di errore comprensibili qualora il sistema necessiti di segnalare un errore                                 | NICE TO HAVE  | UC1, UC2, UC4, UC5, UC6, UC7, UC9, UC10, UC11, UC12, UC13, UC14, UC15, UC20 |
| ED-4.7 | Il sistema deve caricare l'archivio da file all'avvio e salvarlo dopo ogni modifica                                                           | MUST -HAVE    | UC21                                                                        |
# Requisiti non funzionali

| ID    | Requisito                                                                                                                                                                 | Categoria            | Priorità     | Verifica     |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | ------------ | ------------ |
| NF-01 | L'applicazione deve avere un'interfaccia grafica per tutte le funzionalità                                                                                                | Interfaccia grafica  | MUST-HAVE    | Test manuale |
| NF-02 | L'archivio (aule, docenti e prenotazioni) deve essere salvato su file                                                                                                     | Persistenza dei dati | MUST-HAVE    |              |
| NF-03 | Il sistema non deve sovrascrivere il file esistente se il caricamento fallisce                                                                                            | Affidabilità         | SHOULD-HAVE  | Test         |
| NF-04 | Le operazioni comuni (ricerca, verifica sovrapposizioni, inserimento, modifica, salvataggio) devono completarsi in tempi rapidi                                           | Prestazioni          | SHOULD-HAVE  | Test         |
| NF-05 | Non è necessaria alcuna preparazione tecnica per usare il programma, i messaggi di errore devono essere chiari affinché sia possibile correggere le operazioni facilmente | Usabilità            | SHOULD-HAVE  |              |
| NF-06 | L'applicazione deve funzionare su differenti piattaforme desktop                                                                                                          | Portabilità          | NICE TO HAVE |              |
| NF-07 | L'applicazione deve funzionare senza connessione di rete o server esterni                                                                                                 |                      | NICE TO HAVE |              |
| NF-08 | Il codice deve essere strutturato in moduli con alta coesione e basso accoppiamento. In particolare si mira a separare interfaccia utente e logica applicativa.           | Manutenibilità       | SHOULD-HAVE  |              |
| NF-09 | Le interfacce dei componenti devono essere documentate con commenti di documentazioni                                                                                     | Manutenibilità       | NICE TO HAVE |              |
| NF-10 | La logica applicativa deve essere coperta da test automatici                                                                                                              | Testabilità          | MUST-HAVE    |              |
# Matrice di tracciabilità

| Caso d'uso | Requisiti funzionali           | Requisiti non funzionali   | Design | Codice | Test |
| ---------- | ------------------------------ | -------------------------- | ------ | ------ | ---- |
| UC1        | FI-1.1, ED-4.3, ED-4.4, UI-4.6 | NF-01, NF-05               |        |        |      |
| UC2        | FI-1.2, ED-4.4, UI-4.6         | NF-01, NF-05               |        |        |      |
| UC3        | FI-1.3, UI-4.5                 | NF-01                      |        |        |      |
| UC4        | FI-1.4, UI-4.6                 | NF-01, NF-05               |        |        |      |
| UC5        | FI-1.5, UI-4.6                 | NF-01, NF-05               |        |        |      |
| UC6        | FI-2.1, ED-4.3, ED-4.4, UI-4.6 | NF-01, NF-05               |        |        |      |
| UC7        | FI-2.2, ED-4.4, UI-4.6         | NF-01, NF-05               |        |        |      |
| UC8        | FI-2.3, UI-4.5                 | NF-01                      |        |        |      |
| UC9        | FI-2.4, UI-4.6                 | NF-01, NF-05               |        |        |      |
| UC10       | FI-2.5, UI-4.6                 | NF-01, NF-05               |        |        |      |
| UC11       | FI-3.1, UI-4.6                 | NF-01, NF-05               |        |        |      |
| UC12       | FI-3.2, ED-4.4, UI-4.6         | NF-01, NF-05               |        |        |      |
| UC13       | FI-3.3, ED-4.4, UI-4.6         | NF-01, NF-05               |        |        |      |
| UC14       | FI-3.4, FI-3.5, UI-4.6         | NF-01, NF-05               |        |        |      |
| UC15       | FI-3.6, UI-4.5, UI-4.6         | NF-01, NF-05               |        |        |      |
| UC20       | FI-3.7, UI-4.5, UI-4.6         | NF-01, NF-05               |        |        |      |
| UC21       | FI-4.1, ED-4.2                 | NF-04,                     |        |        |      |
| UC21       | ED-4.7                         | NF-02, NF-03, NF-04, NF-07 |        |        |      |
