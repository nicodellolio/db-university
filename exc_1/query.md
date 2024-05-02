
## 1.Selezionare tutti gli studenti nati nel 1990 (160)
### query: 
- SELECT * FROM `students` WHERE date_of_birth LIKE '1990-%';

## 2.Selezionare tutti i corsi che valgono più di 10 crediti (479)
### query:
- SELECT * FROM `courses` WHERE cfu > 10;

## 3.Selezionare tutti gli studenti che hanno più di 30 anni
### query:
- SELECT * FROM `students` WHERE date_of_birth < '1994-%';

## 4.Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
### query:
- SELECT * FROM `courses` WHERE year = 1 AND period = 'I semestre';

## 5.Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
### query:
- SELECT * FROM `exams` WHERE date = '2020-06-20' AND hour > '13-59%';
<!-- ho escluso l'edge case dell'esame alle 14 in punto -->

## 6.Selezionare tutti i corsi di laurea magistrale (38)
### query:
- SELECT * from `degrees` WHERE level = 'magistrale';

## 7.Da quanti dipartimenti è composta l'università? (12)
### query:
- SELECT COUNT(*) FROM `departments`;

## 8.Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
### query:
- SELECT * from `teachers` WHERE phone IS NULL;
