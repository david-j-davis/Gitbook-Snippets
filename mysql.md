# MySQL
---
####Create table
---
    USE `cisco_eh`;
    CREATE TABLE IF NOT EXISTS `cisco_jobs` (
      `job_title` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
      `job_location` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
      `job_department` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
      `job_link` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
      `job_date` INT(11) UNSIGNED
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

####Select columns from table
---
    SELECT job_title, job_department FROM cisco_eh.cisco_jobs;

####Select a limit of values by an offset index number starting from 0 to the max number of values
---
    SELECT * FROM cisco_eh.cisco_jobs LIMIT 10 OFFSET 20;
    
####Find values in table that are not set and equal to null. You cannot use the quals sign with null, use "is"
---
    SELECT * FROM cisco_eh.cisco_jobs WHERE job_title IS NULL;
    
    //and the opposite
    
    SELECT * FROM cisco_eh.cisco_jobs WHERE job_title IS NOT NULL ORDER BY job_date;
    
####Set Primary keys, unique keys, and foreign keys. 
---
######Primary keys are used to define each row in a table, they can't be null and can't be duplicated ie: 1, 2, 3 etc. Unique keys are used for specification, they can be null and can't be duplicated ie: email address, ssn, etc. Foreign keys reference data from another table, they can be null and can be duplicated.

    CREATE TABLE genres (id INTEGER AUTO_INCREMENT PRIMARY KEY, name VARCHAR(30) NOT NULL UNIQUE KEY);
    INSERT INTO genres (name) VALUES ("Sci Fi");
    
####Add a column with an id, and make it the first column
---
    ALTER TABLE movies ADD COLUMN id INTEGER AUTO_INCREMENT PRIMARY KEY FIRST;
####Add a column with an id, and make it the first column
---
    ALTER TABLE movies ADD COLUMN genre_id INTEGER NULL, ADD CONSTRAINT FOREIGN KEY (genre_id) REFERENCES genres(id);
    
####Join two tables (used alone also represents INNER JOIN), followed by "ON" the table column from the first table and the column from the joined table
---
    SELECT * FROM cisco_eh.cisco_jobs JOIN cisco_postmeta ON cisco_eh.cisco_jobs.job_date = cisco_postmeta.date;
    
    //or select only specific data to join
    
    SELECT cisco_eh.cisco_jobs.job_title, cisco_postmeta.title FROM cisco_eh.cisco_jobs JOIN cisco_postmeta ON cisco_eh.cisco_jobs.job_date = cisco_postmeta.date;
    
####Join tables and use alias names for returned result set and does not rename it in the table
---
    SELECT * FROM cisco_eh.cisco_jobs JOIN cisco_postmeta AS cisco_name ON cisco_eh.cisco_jobs.job_date = cisco_postmeta.date;
    
    //Optionally use a conditional (Note: You cannot query on an alias name)
    
    SELECT * FROM cisco_eh.cisco_jobs JOIN cisco_postmeta AS cisco_name ON cisco_eh.cisco_jobs.job_date = cisco_postmeta.date WHERE cisco_postmeta = 1;
    
####Count a number of items
---
    SELECT COUNT(*) FROM cisco_eh.cisco_jobs WHERE job_title = "Something";
    
####Get min value and max value
---
    SELECT MIN(job_date) as earliest_date, MAX(job_date) AS latest_date FROM cisco_eh.cisco_jobs WHERE job_title = "Something";
    
####Insert values into table, keep in mind the columns are listed first in parentheses, followed by values, which are in the same order followed by commas for separate value rows.
---
    INSERT INTO cisco_eh.cisco_jobs (job_title, job_location, job_department, job_link, job_date) VALUES ("sometitle", "somelocation", "somedepartment", "somelink", someinteger),("sometitle", "somelocation", "somedepartment", "somelink", someinteger),("sometitle", "somelocation", "somedepartment", "somelink", someinteger),("sometitle", "somelocation", "somedepartment", "somelink", someinteger);
    
####Update all rows
---
    UPDATE cisco_eh.cisco_jobs SET job_link = "something" WHERE job_title = "Engineer";
    
####Rename table
---
    RENAME TABLE cisco_eh.cisco_jobs TO cisco_job;
    
####Delete rows like this, with Data Definition Language
---
    DELETE FROM cisco_eh.cisco_jobs WHERE job_link = "something" AND job_date = "something";
    
####Alter table to add column
---
    ALTER TABLE cisco_eh.cisco_jobs ADD COLUMN job_description VARCHAR(250);
    
####Change table column like this. Use current name followd by new name and type
---
    ALTER TABLE cisco_eh.cisco_jobs CHANGE COLUMN job_link cisco_job_link VARCHAR(250);
    
####Add a column with an id, and make it the first column
---
    ALTER TABLE movies ADD COLUMN id INTEGER AUTO_INCREMENT PRIMARY KEY FIRST;
    
####Drop a table
---
    DROP DATABASE IF EXISTS cisco_eh;