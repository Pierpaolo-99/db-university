1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia:


SELECT * 
FROM students
JOIN degrees ON students.degree_id = degrees.id
WHERE degrees.name = 'Corso di Laurea in Economia'


2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT courses.id AS courses_id, courses.name, degrees.level, departments.name
FROM courses
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
WHERE degrees.level = 'magistrale'
AND departments.name = 'Dipartimento di Neuroscienze'


3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT teachers.id AS teacher_id, teachers.name, teachers.surname, courses.id AS courses_id, courses.name, courses.period, courses.year, courses.cfu
FROM teachers
JOIN course_teacher ON course_teacher.teacher_id = teachers.id
JOIN courses ON course_teacher.course_id = courses.id
WHERE teachers.id = 44

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT students.id AS students_id, students.name, students.surname, degrees.id AS degrees_id, degrees.name, degrees.level, departments.name
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
ORDER BY students.surname ASC, students.name ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT degrees.id AS degrees_id, degrees.name, courses.id AS courses_id, courses.name, teachers.id AS teachers_id, teachers.name, teachers.surname
FROM degrees
JOIN courses ON courses.degree_id = degrees.id
JOIN course_teacher ON course_teacher.course_id = courses.id
JOIN teachers ON course_teacher.teacher_id = teachers.id

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (64)

SELECT teachers.id AS teachers_id, teachers.name, teachers.surname, degrees.id AS degrees_id, degrees.name, departments.id AS departments_id, departments.name
FROM teachers
JOIN course_teacher ON course_teacher.teacher_id = teachers.id
JOIN courses ON course_teacher.course_id = courses.id
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
WHERE departments.name = 'Dipartimento di Matematica'

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

SELECT 
    students.id AS student_id,
    students.name AS student_name,
    students.surname AS student_surname,
    exam_student.exam_id,
    COUNT(exam_student.student_id) AS total_attempts,
    MAX(exam_student.vote) AS max_vote
FROM 
    students
JOIN 
    exam_student ON students.id = exam_student.student_id
WHERE 
    exam_student.vote >= 18
GROUP BY 
    students.id, 
    students.name, 
    students.surname, 
    exam_student.exam_id
ORDER BY 
    students.surname ASC, 
    students.name ASC, 
    exam_student.exam_id ASC;