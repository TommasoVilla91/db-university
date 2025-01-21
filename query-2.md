<!-- 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia -->
SELECT `students`.`id`, `students`.`name`,`students`.`surname`, `degrees`.`name`, `degrees`.`level`
FROM `students`
INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia"
ORDER BY `students`.`surname`;

<!-- 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze -->
SELECT `degrees`.`id`, `degrees`.`name` AS `degree_name`, `degrees`.`level`, `departments`.`id`, `departments`.`name` AS `department_name`
FROM `degrees`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = "magistrale"
AND `departments`.`name` = "Dipartimento di Neuroscienze";

<!-- 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44) -->
SELECT `teachers`.`id`, `teachers`.`name`, `teachers`.`surname`, `courses`.*
FROM `courses`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id` = 44
ORDER BY `courses`.`period`;

<!-- 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome -->
SELECT `students`.`id`, `students`.`name`, `students`.`surname`, `degrees`.`name` AS `degree_name`, `degrees`.`level`, `departments`.`name` AS `department_name`
FROM `students`
INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`name`, `students`.`surname`;

<!-- 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti -->
SELECT `degrees`.`name` AS `degree_name`, `degrees`.`level`, `courses`.`name` AS `course_name`, `courses`.`period`, `courses`.`year`, `teachers`.*
FROM `degrees`
INNER JOIN `courses`
ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`;

<!-- 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54) -->
SELECT `teachers`.*, `departments`.`name` AS `department_name`
FROM `teachers`
INNER JOIN `course_teacher`
ON  `course_teacher`.`teacher_id` = `teachers`.`id`
INNER JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`;

<!-- 7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami -->
<!-- student_id / exam_id / curse_id -->
SELECT `students`.`name`,`students`.`surname`, `courses`.`name` AS `course_name`, COUNT(`exam_student`.`vote`) AS `attempt_num`, MAX(`exam_student`.`vote`) AS `max_vote`
FROM `students`
INNER JOIN `exam_student`
ON  `exam_student`.`student_id` = `students`.`id`
INNER JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
INNER JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`;