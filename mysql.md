# MySQL

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

