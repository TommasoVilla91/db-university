<!-- 1. Selezionare tutti gli studenti nati nel 1990 (160) -->
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990;

SELECT COUNT(*)
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990

<!-- 2. Selezionare tutti i corsi che valgono più di 10 crediti (479) -->
SELECT *
FROM `courses`
WHERE `cfu` > 10;

SELECT COUNT(*)
FROM `courses`
WHERE `cfu` > 10;

<!-- 3. Selezionare tutti gli studenti che hanno più di 30 anni -->
SELECT *, timestampdiff(YEAR, `date_of_birth`, CURDATE()) AS `age`
FROM `students`
WHERE timestampdiff(YEAR, `date_of_birth`, CURDATE()) > 30;

<!-- 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286) -->
SELECT *
FROM `courses`
WHERE `period` = "I semestre"
AND `year` = 1;

SELECT COUNT(*)
FROM `courses`
WHERE `period` = "I semestre"
AND `year` = 1;

<!-- 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21) -->
SELECT *
FROM `exams`
WHERE `hour` >= "14:00:00"
AND `date` = "2020-06-20";

SELECT COUNT(*)
FROM `exams`
WHERE `hour` > "14:00:00"
AND `date` = "2020-06-20";

<!-- 6. Selezionare tutti i corsi di laurea magistrale (38) -->
SELECT *
FROM `degrees`
WHERE `level` = "magistrale";

SELECT COUNT(*)
FROM `degrees`
WHERE `level` = "magistrale";

<!-- 7. Da quanti dipartimenti è composta l'università? (12) -->
SELECT COUNT(*)
FROM `departments`;

<!-- 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50) -->
SELECT COUNT(*)
FROM `teachers`
WHERE `phone`IS NULL;

<!--/////////// BONUS ///////////-->
<!-- 1. Contare quanti iscritti ci sono stati ogni anno -->
SELECT YEAR(`enrolment_date`) AS years, COUNT(*) AS all_students
FROM `students`
GROUP BY years
ORDER BY years;

<!-- 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio -->
SELECT `office_address` AS offices, COUNT(*) AS teachers
FROM `teachers`
GROUP BY offices
ORDER BY offices;

<!-- 3. Calcolare la media dei voti di ogni appello d'esame -->
SELECT `exam_id` AS exam, AVG(`vote`)
FROM `exam_student`
GROUP BY exam;

<!-- 4. Contare quanti corsi di laurea ci sono per ogni dipartimento -->
SELECT `department_id` AS department, COUNT(`name`) AS course
FROM `degrees`
GROUP BY department;