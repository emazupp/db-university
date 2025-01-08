## DB UNIVERSITY JOIN EX

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
    SELECT
	`students`.`name` AS `nome_studente`,
    `students`.`surname` AS `cognome_studente`,
    `degrees`.`name` AS `nome_corso`

    FROM `students`

    INNER JOIN `degrees`
    ON `degrees`.`id` = `students`.`degree_id`

    WHERE `degrees`.`id` = 53;
```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze

```sql
    SELECT `degrees`.*
    FROM `departments`

    INNER JOIN `degrees`
    ON `degrees`.`department_id` = `departments`.`id`

    WHERE `degrees`.`level` = "magistrale" AND `departments`.`id` = 7;
```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
    SELECT `courses`.*
    FROM `course_teacher`

    INNER JOIN `courses`
    ON `course_teacher`.`course_id` = `courses`.`id`
    WHERE `course_teacher`.`teacher_id` = 44;
```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
   nome

```sql
    SELECT
	`students`.`name`,
    `students`.`surname`,
    `departments`.`name` `nome_dipartimento`,
    `degrees`.`name` `nome_corso_di_laurea`,
    `degrees`.`level`,
    `degrees`.`address`,
    `degrees`.`email`,
    `degrees`.`website`
    FROM `students`

    INNER JOIN `degrees`
    ON `students`.`degree_id` = `degrees`.`id`

    INNER JOIN `departments`
    ON `degrees`.`department_id` = `departments`.`id`

    ORDER BY `students`.`surname`, `students`.`name`;
```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
    SELECT
	`courses`.*,
    `degrees`.`name` AS `nome_corso`,
    `teachers`.`name` AS `nome_prof`,
    `teachers`.`surname` AS `cognome_prof`,
    `teachers`.`email` AS `email_prof`

    FROM `degrees`

    INNER JOIN `courses`
    ON `courses`.`degree_id` = `degrees`.`id`

    INNER JOIN `course_teacher`
    ON `course_teacher`.`course_id` = `courses`.`id`

    INNER JOIN `teachers`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`;
```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

```sql
    SELECT
	`teachers`.`name`,
	`teachers`.`surname`,
    `departments`.`name` AS `nome_dipartimento`

    FROM `teachers`

    INNER JOIN `course_teacher`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`

    INNER JOIN `courses`
    ON `courses`.`id` = `course_teacher`.`course_id`

    INNER JOIN `degrees`
    ON `degrees`.`id` = `courses`.`degree_id`

    INNER JOIN `departments`
    ON `departments`.`id` = `degrees`.`department_id`

    WHERE `departments`.`id` = 5;
```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

```sql
    SELECT
	COUNT(`exam_student`.`student_id`) AS `numero_tentativi`,
    MAX(`exam_student`.`vote`) AS `voto_massimo`

    FROM `exam_student`

    INNER JOIN `students`
    ON `students`.`id` = `exam_student`.`student_id`

    WHERE `exam_student`.`vote` >= 18
    GROUP BY `exam_student`.`student_id`;
```
