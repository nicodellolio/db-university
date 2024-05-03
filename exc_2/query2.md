# Group by

## 1. Contare quanti iscritti ci sono stati ogni anno
- query
    SELECT COUNT(`id`) AS `subs_count`, YEAR (`enrolment_date`) AS `enrolment_year`
    FROM `students`
    GROUP BY YEAR(`enrolment_date`);

- result 

    `subs_count` -> `enrolment_year`
    912          ->   2018
    1709         ->   2019
    1645         ->   2020
    734          ->   2021

## 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
- query
    SELECT COUNT(`teachers`.`id`) AS `teacher_count`, `office_address`
    FROM `teachers`
    GROUP BY `office_address`;

- result 
    `teacher_count` ->   `office_address`
    1             ->     Borgo Demis 1
    8             ->     Borgo Elga 89
    4             ->     Borgo Elio 234 Piano 4
    1             ->     Borgo Ippolito 5 Piano 5
    3             ->     Borgo Martino 82 Appartamento 07
    5             ->     Contrada Amato 58 Piano 2
    4             ->     Contrada Penelope 73
    3             ->     Contrada Rita 5 Appartamento 71
    3             ->     Contrada Santoro 17 Appartamento 30
    3             ->     Incrocio Marini 9
    2             ->     Incrocio Testa 142 Piano 7
    1             ->     Piazza Aroldo 8 Appartamento 85
    3             ->     Piazza Demian 856 Appartamento 63
    3             ->     Piazza Ferretti 619
    2             ->     Piazza Pellegrino 613 Piano 8
    6             ->     Rotonda Carmela 10 Piano 1
    9             ->     Rotonda Martinelli 309
    2             ->     Rotonda Teseo 9
    3             ->     Strada Concetta 6
    5             ->     Strada Kociss 997 Piano 8
    1             ->     Strada Lino 8
    3             ->     Strada Lombardi 855
    3             ->     Strada Neri 577
    5             ->     Strada Vitali 8 Piano 0
    1             ->     Via Elga 7 Piano 4

## 3. Calcolare la media dei voti di ogni appello d'esame
- query
    SELECT ROUND(AVG(`vote`), 2) AS `average_vote`, `exam_id`
    FROM `exam_student`
    GROUP BY `exam_id`;

- result 
    avg_vote -> exam_id
    16.88   ->  1
    16.46   ->  2
    20.33   ->  3
    27.00   ->  4
    17.50   ->  6
    19.60   ->  7
    6.50    ->  8
    12.00   ->  9
    17.43   ->  11
    14.89   ->  12
    22.00   ->  13
    18.05   ->  16
    19.00   ->  17
    5.50    ->  18
    22.00   ->  19
    16.62   ->  21
    15.00   ->  22
    12.75   ->  23
    12.00   ->  24
    3.00    ->  25
    19.17   ->  26
    24.50   ->  27
    16.96   ->  31
    17.25   ->  32
    20.18   ->  36

## 4. Contare quanti corsi di laurea ci sono per ogni dipartimento
- query
    SELECT COUNT(`id`) AS `degrees_count`, `department_id`
    FROM `degrees`
    GROUP BY `department_id`;

- result

    `degrees_count` -> `department_id`
    10              ->  1
    4               ->  2
    4               ->  3
    9               ->  4
    4               ->  5
    6               ->  6
    7               ->  7
    8               ->  8
    5               ->  9
    8               ->  10
    3               ->  11
    7               ->  12


# Joins
## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
- query 
    SELECT `students`.`id` AS `student_id`,`students`.`name`, `students`.`surname`, `students`.`email`
    FROM `students`
    JOIN `degrees` ON `degrees`.`id` = `degree_id`
    WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

- result: 
    - 68 student(s) found

## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
- query
    SELECT `degrees`.`id` AS `degree_id`, `degrees`.`name` AS `degree_name`, `degrees`.`department_id`, `degrees`.`level` AS `degree_level`, `degrees`.`address` AS `degree_address`
    FROM `degrees`
    JOIN `departments` ON `departments`.`id` = `department_id`
    WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
    AND `degrees`.`level` = 'magistrale';

- result
    - 1 degree(s) found
    `degree_id`      -> 44
    `degree_name`    -> Corso di Laurea Magistrale in Odontoiatria e Prote...
    `department_id`  -> 7
    `degree_level`   -> magistrale
    `degree_address` -> Via Mariani 185

## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
- query
    SELECT `course_teacher`.`course_id`
    FROM `course_teacher`
    JOIN `teachers`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`
    WHERE `teachers`.`id` = 44;

- result
    - 11 course(s) found

    `course id` |   `degree_name`                                       | `degree_level`|
    23          |   Corso di Laurea in Biologia molecolare              |   triennale   |
    155         |   Corso di Laurea Magistrale in Scienze della natura  |   magistrale  |   
    170         |   Corso di Laurea in Astronomia                       |   triennale   |   
    251         |   Corso di Laurea in Ingegneria Civile                |   triennale   |   
    489         |   Corso di Laurea in Informatica                      |   triennale   |   
    601         |   Corso di Laurea in Tecniche di Radiologia Medica    |   triennale   |
    725         |   Corso di Laurea in Logopedia                        |   triennale   |
    766         |   Corso di Laurea in Tecniche di Neurofisiopatologia  |   triennale   |
    1016        |   Corso di Laurea Magistrale in Economia e Diritto    |   magistrale  |
    1017        |   Corso di Laurea Magistrale in Economia e Diritto    |   magistrale  |
    1259        |   Corso di Laurea Magistrale in Lingue e Letterature  |   magistrale  |

## 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
- query
    SELECT `students`.`id` AS student_id,  `students`.`surname` AS `student_surname`, `students`.`name` AS `student_name`, `degrees`.`id` AS `degree_id`, `degrees`.`name` AS `degree_name`, `degrees`.`level` AS `degree_level`, `degrees`.`address` AS `degree_address`, `departments`.`name` AS `department_name`, `departments`.`address` AS `department_address`
    FROM `students` 
    JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
    JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
    ORDER BY `students`.`surname` ASC, `students`.`name` ASC;

- result
    - 5000 student(s) found

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
- query
    SELECT `degrees`.`id` AS `degrees_id`, `degrees`.`name` AS `degree_name`, `courses`.`id` AS `course_id`, `courses`.`name` AS `course_name`, `teachers`.`id` AS `teacher_id`,`teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`
    FROM `degrees`
    JOIN `courses` ON `courses`.`degree_id` = `degree`.`id`
    JOIN `course_teacher` ON `course_id` = `courses`.`id`
    JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`

- result
    - 1317 degree(s) found
 
## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
- query
    SELECT DISTINCT `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`, `teachers`.`email` AS `teacher_email`
    FROM `course_teacher`
    JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
    JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
    JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
    JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
    WHERE `departments`.`name` = 'Dipartimento di Matematica';

- result
    - 54 teacher(s) found


<!-- MI SONO RESO CONTO UN PO' TARDI DELLA POSSIBILITÀ DI FARE JOIN DI PIÙ TABELLE, PER QUESTO NEGLI ESERCIZI FINO AL 4, SEPPUR CORRETTI, MANCANO TANTE INFORMAZIONI RELATIVE ALLE ALTRE TABELLE. IN QUANTO VI SONO PRESENTI SOLTANTO GLI ID -->