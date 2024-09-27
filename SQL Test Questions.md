SELECT AVG(grade)  AS avg_grade
FROM Enrollments;

SELECT Students.name, Courses.course_name
FROM Enrollments
JOIN Students ON Enrollments.student_id = Students.student_id
JOIN Courses ON Enrollments.course_id = Courses.course_id;

SELECT grade_level, COUNT(*) AS student_count
FROM Students
GROUP BY grade_level;

SELECT Courses.course_name, MAX(Enrollments.grade) AS max_grade
FROM Enrollments
JOIN Courses ON Enrollments.course_id = Courses.course_id
GROUP BY Courses.course_name;

SELECT AVG(Enrollments.grade) AS avg_grade_level_3
FROM Enrollments
JOIN Students ON Enrollments.student_id = Students.student_id
WHERE Students.grade_level = 3;

SELECT Students.name AS student_name, Courses.course_name, Courses.credits
FROM Enrollments
JOIN Students ON Enrollments.student_id = Students.student_id
JOIN Courses ON Enrollments.course_id = Courses.course_id;

SELECT Courses.course_name, AVG(Enrollments.grade) AS avg_grade
FROM Enrollments
JOIN Courses ON Enrollments.course_id = Courses.course_id
GROUP BY Courses.course_name
HAVING AVG(Enrollments.grade) > 3.0;

SELECT DISTINCT Students.name AS student_name
FROM Students
WHERE Students.student_id NOT IN (
    SELECT Enrollments.student_id
    FROM Enrollments
    WHERE Enrollments.grade = 4.0
);

SELECT s.name
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
GROUP BY s.name
HAVING AVG(e.grade) > (SELECT AVG(grade) FROM Enrollments);

SELECT s.name, 
       COUNT(e.course_id) AS total_courses, 
       AVG(e.grade) AS average_grade
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
GROUP BY s.name;
