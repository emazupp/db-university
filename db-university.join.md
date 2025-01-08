## DB UNIVERSITY JOIN EX

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

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
    ON `degrees`.`department_id` = `departments`.`id`;
```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.
