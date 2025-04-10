# Query SQL

## Soluzione

-- 1. Selezionare tutti gli studenti nati nel 1990

SELECT COUNT(id)
FROM `students`
WHERE `date_of_birth` >= '1990-01-01'
AND `date_of_birth` < '1991-01-01'

-- 2. Selezionare tutti i corsi che valgono più di 10 crediti

SELECT COUNT(id)
FROM `courses`
WHERE `cfu` > '10'

-- 3. Selezionare tutti gli studenti che hanno più di 30 anni

SELECT COUNT(id)
FROM `students`
WHERE `date_of_birth` <= '1995-04-10'

-- 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea

SELECT COUNT(id)
FROM `courses`
WHERE `period` = 'I semestre'
AND `year` = '1'

-- 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020

SELECT COUNT(id)
FROM `exams`
WHERE `date` = '2020-06-20'
AND `hour` > '14:00:00'

-- 6. Selezionare tutti i corsi di laurea magistrale

SELECT COUNT(id)
FROM `degrees`
WHERE `level` = 'magistrale'

-- 7. Da quanti dipartimenti è composta l'università?

SELECT COUNT(id)
FROM `departments`

-- 8. Quanti sono gli insegnanti che non hanno un numero di telefono?

SELECT COUNT(id)
FROM `teachers`
WHERE `phone` IS NULL

(gli insegnanti che non hanno un numero di telefono sono 50)
