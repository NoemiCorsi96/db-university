### TESTO DELL'ES
Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d'Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;
per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

Utilizzare https://www.drawio.com/ per la creazione dello schema.
Esportare quindi il diagramma in png e caricarlo nella repo inserendolo anche in un file index.html tramite il tag img per poterne vedere al volo un anteprima come mostrato a lezione.
### FINE TESTO 

### Tables 
-dipartimenti
-corsi_laurea
-corsi
-insegnanti
-appelli_esame
-studenti
### Possibili relazioni: 
---dipartimenti- corsi_laurea 1-* un dipartimento offre più corsi di laurea e un corso di laurea è di un solo dipartimento
----corsi_laurea-corsi un corso di laurea ha molti corsi e un corso può appartenere a più corsi di laurea *-* TABELLA PIVOT
---corsi_insegnanti un corso può essere tenuto da più insegnanti e un insegnate può fare piu di un corso *-* TABELLA PIVOT
----corsi- appelli_esame un corso ha più appelli di esame e un appello appartiene ad un corso 1-*
---studenti-corsi_laurea uno studente può frequentare un corso di laurea, ma un cors odi laurea è frequentato da più studenti *-1 
---studenti-appelli_esame uno studente può partecipare a più appelli e ad un appello posono partecipare più studenti *-* TABELLA PIVOT

### Table: dipartimenti
id: INT|| BIGINT  AI NOTNULL UNIQUE PK INDEX
nome: VARCHAR(100) UNIQUE NOT NULL
indirizzo_sede: VARCHAR(75) NULL 


### Table: corsi_laurea
id: PK BIGINT UNIQUE INDEX
dipartimento_id: NOT NULL FK BIGINT UNIQUE INDEX
nome: VARCHAR(30) NOT NULL INDEX 

### Table: corsi
id:PK BIGINT UNIQUE INDEX PK INDEX
codice: VARCHAR(15) UNIQUE NOT NULL INDEX
cfu: SMALLINT 
nome: VARCHAR(100) NOT NULL 
prerequisiti: VARCHAR(200) NULL 
tipo_esame: VARCHAR(200) NULL
appelli_id FK NOT NULL UNIQUE

### Table: insegnanti 
id:PK BIGINT UNIQUE INDEX PK INDEX
nome: VARCHAR(50)
COGNOME: varchar(50)
matricola: VARCHAR(20) UNIQUE NOT NULL INDEX
email: VARCHAR(60) UNIQUE NOT NULL INDEX

## Table: studenti 
id:PK BIGINT UNIQUE INDEX PK INDEX
corsi_laurea.id: FK BIGINT
nome: VARCHAR(50)
COGNOME: varchar(50)
matricola: VARCHAR(20) UNIQUE NOT NULL INDEX
email: VARCHAR(60) UNIQUE NOT NULL INDEX

## Table: appelli_esame

id:PK BIGINT UNIQUE INDEX PK INDEX
semestre: SMALLINT 
straordinario: BOOLEANO 
remoto: DEFAULT


### Pivot tables 

ponte corsi-insegnanti 

name_table: corso_insegnante 
corso_id: FK BIGINT NOTNULL 
docente_id: FK BIGINT NOTNULL 
ruolo: VARCHAR(30) NULL 

ponte corsi_laurea-corsi

name_table:corso_corso_laurea  
cdl_id: FK BIGINT NOTNULL 
corso_id: FK BIGINT NOTNULL 
anno: SMALLINT 
frequenza_obbligatoria: BOOLEANO 
semestre: SMALLINT 


pote studenti-appelli_esame

name_table:appello_esame_studente 

studente_id: FK BIGINT NOTNULL
appello_id: FK BIGINT NOTNULL
esito: VARCHAR(20) NOT NULL 
voto: SMALLINT  NOT NULL 
lode: BOOLEANO 

