use studentmanagement;

#creating student Table
CREATE TABLE student (
   Student_id INT PRIMARY KEY,
   Name VARCHAR(70),
   Math_score INT,
   Science_score INT,
   English_Score INT
   );
   
#Inserting Values into Students Table 
INSERT INTO Student VALUES (1, "sasi", 85, 96, 92); 
INSERT INTO Student VALUES (2, "kiran", 92, 98 , 91);
INSERT INTO Student VALUES (3, "Manoj", 88, 79 , 81);
INSERT INTO Student VALUES (4, "Rahul", 94, 95 , 96);
INSERT INTO Student VALUES (5, "Dawn", 76, 70 , 75);
INSERT INTO Student VALUES (6, "Nikhil", 83, 87 , 81);
INSERT INTO Student VALUES (7, "Nitish", 76, 87 , 82);
INSERT INTO Student VALUES (8, "Rana", 98, 81 , 64);
INSERT INTO Student VALUES (9, "Nitya", 81, 77 , 85);
INSERT INTO Student VALUES (10, "Mounika", 88, 94 , 96);

# 1)  Identify Top Students by Total Scores

SELECT student_id, name, total_score
FROM (
    SELECT student_id, name, 
           (Math_score + Science_score + English_score) AS total_score
    FROM student
) AS subquery
ORDER BY total_score DESC
LIMIT 7;


# 2)  Use subqueries to filter and group data for average calculations
#Example-1 : Calculate the average score of students who scored above 70 in Math

SELECT AVG(Math_score) AS average_Math_score
FROM student
WHERE Math_score > 90;

#Example-2 : Calculate the average total score of students grouped by a specific condition

SELECT COUNT(student_id) AS student_count, 
       AVG(total_score) AS average_total_score
FROM (
    SELECT student_id, 
           (math_score + science_score + english_score) AS total_score
    FROM student
) AS subquery
WHERE total_score BETWEEN 100 AND 150;

# 3) Find Second-Highest Math Scores

SELECT MAX(math_score) AS second_highest_math_score
FROM student
WHERE math_score < (
    SELECT MAX(math_score) FROM student
);


   
