## University db

## Description:
Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d'Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;
per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## Table name: Department

**Columns:**
- id - BIGINT - primary key - auto increment
- name - VARCHAR(255) - not null - unique
- description - TEXT - null
- location - VARCHAR(255) - null

## Table name: Courses

**Columns:**
- id - BIGINT - primary key - auto increment
- department_id - BIGINT - not null - foreign key references Department(id)
- teacher_id - BIGINT - not null - foreign key references teacher(id)
- name - VARCHAR(255) - not null - unique
- description - TEXT - not null
- credits - INT - not null

## Table name: teacher

**Columns:**
- id - BIGINT - primary key - auto increment
- Course_id - BIGINT - not null - foreign key references Courses(id)
- name - VARCHAR(255) - not null
- surname - VARCHAR(255) - not null
- email - VARCHAR(255) - null - unique
- phone - VARCHAR(255) - null - unique

## Table name: Coures_teacher

**Columns:**
- id - BIGINT - primary key - auto increment
- course_id - BIGINT - not null - foreign key references Courses(id)
- teacher_id - BIGINT - not null - foreign key references teacher(id)

## Table name: Exam

**Columns:**
- id - BIGINT - primary key - auto increment
- course_id - BIGINT - not null - foreign key references Courses(id)
- name - VARCHAR(255) - not null
- description - TEXT - null
- date - DATE - not null
- time - TIME - not null

## Table name: Student

**Columns:**
- id - BIGINT - primary key - auto increment
- course_id - BIGINT - not null - foreign key references Courses(id)
- exam_id - BIGINT - not null - foreign key references Exam(id)
- name - VARCHAR(255) - not null
- surname - VARCHAR(255) - not null
- email - VARCHAR(255) - null - unique
- phone - VARCHAR(255) - null - unique
- date_of_birth - DATE - null

## Table name: Student_Exam

**Columns:**
- id - BIGINT - primary key - auto increment
- student_id - BIGINT - not null - foreign key references Student(id)
- exam_id - BIGINT - not null - foreign key references Exam(id)
