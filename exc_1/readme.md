## Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.


Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

# DB_NAME: university

# Table name: departments
- id | INDEX | PK | NN | AI | UNIQUE | BIGINT
- name | VARCHAR(150) | NN
- address | VARCHAR(100) | N 
  
# Table name: degree 
- id | INDEX | PK | NN | AI | UNIQUE | BIGINT
- title | VARCHAR(255) | NN
- department_id | NN | FK
- length | VARCHAR(15) | N

# Table name: courses
- id | INDEX | PK | NN | AI | UNIQUE | BIGINT
- title | VARCHAR(150) | NN
- degree_id | FK | 
- hours | TINYINT | N
- start_date | DATE | N
- end_date | DATE | N
- teacher_id | FK

# Table name: teachers
- id | INDEX | PK | NN | AI | UNIQUE | BIGINT
- name | VARCHAR(100) | NN
- lastname | VARCHAR(100) | NN
- email | VARCHAR(255) | N

# Table name: appeals
- id | INDEX | PK | NN | AI | UNIQUE | BIGINT
- date | DATETIME | NN
- course_id | FK 

# Table name: students
- id | INDEX | PK | NN | AI | UNIQUE | BIGINT
- name | VARCHAR(100) | NN
- lastname | VARCHAR(100) | NN
- birth_date | DATE | NN 
- email | VARCHAR(255) | N
- student_register_number | VARCHAR(6) | NN 
- degree_id | FK  

# Table name: appeals-registration
- id | INDEX | PK | NN | AI | UNIQUE | BIGINT
- student_id | FK 
- appeal_id | FK 
- vote | TINYINT | N



