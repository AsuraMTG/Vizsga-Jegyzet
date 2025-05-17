# DATABASE JEGYZETEK

```SQL
SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";

CREATE DATABASE IF NOT EXISTS `jegyzet` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE `jegyzet`;

CREATE TABLE `proba` (
  `id` int(20) NOT NULL,
  `nev` varchar(54) NOT NULL,
  `kor` int(3) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

INSERT INTO `proba` (`id`, `nev`, `kor`) VALUES
(1, 'Istvan', 16),
(2, 'Erik', 38),
(3, 'Hanna', 41);

ALTER TABLE `proba`
  ADD PRIMARY KEY (`id`);

ALTER TABLE `proba`
  MODIFY `id` int(20) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=7;
COMMIT;
```
