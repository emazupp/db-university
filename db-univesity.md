## DB UNIVERSITY QUERY

1. Selezionare tutti gli studenti nati nel 1990 (160)

```sql
    SELECT *
    FROM `students`
    WHERE YEAR(date_of_birth) = 1990;
```

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
    SELECT *
    FROM `courses`
    WHERE `cfu`>10;
```

3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql
    SELECT *
    FROM `students`
    WHERE (YEAR(curdate()) - YEAR(`date_of_birth`)) > 30;
```

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
   laurea (286)

```sql
    SELECT *
    FROM `courses`
    WHERE `period` LIKE "I semestre" AND `year` = 1;
```

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
   20/06/2020 (21)

```sql
    SELECT *
    FROM `exams`
    WHERE DATE(`date`) = "2020-06-20" AND HOUR(`hour`) > 14;
```

6. Selezionare tutti i corsi di laurea magistrale (38)

```sql
    SELECT *
    FROM `degrees`
    WHERE `level` = "magistrale";
```

7. Da quanti dipartimenti è composta l'università? (12)

```sql
    SELECT COUNT(*)
    FROM `departments`;
```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql
    SELECT COUNT(*)
    FROM `teachers`
    WHERE `phone` IS NULL;
```

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
   degree_id, inserire un valore casuale)

   ```sql
    INSERT INTO `students` (degree_id, name, surname, date_of_birth, fiscal_code, enrolment_date, registration_number, email)
    VALUES (44, "Emanuele", "Zuppardo", "2001-12-04", "QPXGBC51Z02T871B", "2025-01-07", 041201, "emanuele@gmail.com");
   ```

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

```sql
    UPDATE `teachers`
    SET `office_numbers` = 126
    WHERE `name` LIKE "Pietro" AND `surname` LIKE "Rizzo";
```

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

```sql
    DELETE FROM `students` WHERE `name` LIKE "Emanuele";
```

## BONUS

1. Contare quanti iscritti ci sono stati ogni anno

```sql
    SELECT COUNT(*),  YEAR(`enrolment_date`)
    FROM `students`
    GROUP BY YEAR(`enrolment_date`);
```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
    SELECT COUNT(*) AS numero, `office_address`
    FROM `teachers`
    GROUP BY `office_address`;
```

3. Calcolare la media dei voti di ogni appello d'esame

```sql
    SELECT `exam_id` ,AVG(`vote`) AS media
    FROM `exam_student`
    GROUP BY `exam_id`;
```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
    SELECT `department_id`, COUNT(*) AS numero_corsi
    FROM `degrees`
    GROUP BY `department_id`;
```
