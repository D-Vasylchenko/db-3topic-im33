# Реалізація інформаційного та програмного забезпечення

В рамках проекту розробляється: 
- SQL-скрипт для створення на початкового наповнення бази даних
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema omds
-- -----------------------------------------------------
DROP SCHEMA IF EXISTS `omds` ;

-- -----------------------------------------------------
-- Schema omds
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `omds` DEFAULT CHARACTER SET utf8 ;
USE `omds` ;

-- -----------------------------------------------------
-- Table `omds`.`Type`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`Type` ;

CREATE TABLE IF NOT EXISTS `omds`.`Type` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `text` VARCHAR(45) NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`User`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`User` ;

CREATE TABLE IF NOT EXISTS `omds`.`User` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `password` VARCHAR(100) NOT NULL,
  `name` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`State`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`State` ;

CREATE TABLE IF NOT EXISTS `omds`.`State` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(255) NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`Category`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`Category` ;

CREATE TABLE IF NOT EXISTS `omds`.`Category` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `Category` INT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_Category_Category1_idx` (`Category` ASC) VISIBLE,
  CONSTRAINT `fk_Category_Category1`
    FOREIGN KEY (`Category`)
    REFERENCES `omds`.`Category` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`MetaDataKey`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`MetaDataKey` ;

CREATE TABLE IF NOT EXISTS `omds`.`MetaDataKey` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `key` VARCHAR(255) NULL,
  `description` VARCHAR(511) NULL,
  `MetaDataKey` INT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_MetaDataKey_MetaDataKey1_idx` (`MetaDataKey` ASC) VISIBLE,
  CONSTRAINT `fk_MetaDataKey_MetaDataKey1`
    FOREIGN KEY (`MetaDataKey`)
    REFERENCES `omds`.`MetaDataKey` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`ActionType`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`ActionType` ;

CREATE TABLE IF NOT EXISTS `omds`.`ActionType` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(255) NULL,
  `description` VARCHAR(255) NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`AvailableFor`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`AvailableFor` ;

CREATE TABLE IF NOT EXISTS `omds`.`AvailableFor` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `Type` INT NOT NULL,
  `MetaDataKey` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_AvailableFor_Type_idx` (`Type` ASC) VISIBLE,
  INDEX `fk_AvailableFor_MetaDataKey1_idx` (`MetaDataKey` ASC) VISIBLE,
  CONSTRAINT `fk_AvailableFor_Type`
    FOREIGN KEY (`Type`)
    REFERENCES `omds`.`Type` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_AvailableFor_MetaDataKey1`
    FOREIGN KEY (`MetaDataKey`)
    REFERENCES `omds`.`MetaDataKey` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`Role`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`Role` ;

CREATE TABLE IF NOT EXISTS `omds`.`Role` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(255) NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`AvailableAction`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`AvailableAction` ;

CREATE TABLE IF NOT EXISTS `omds`.`AvailableAction` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `Role` INT NOT NULL,
  `ActionType` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_AvailableAction_Role1_idx` (`Role` ASC) VISIBLE,
  INDEX `fk_AvailableAction_ActionType1_idx` (`ActionType` ASC) VISIBLE,
  CONSTRAINT `fk_AvailableAction_Role1`
    FOREIGN KEY (`Role`)
    REFERENCES `omds`.`Role` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_AvailableAction_ActionType1`
    FOREIGN KEY (`ActionType`)
    REFERENCES `omds`.`ActionType` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`DataSet`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`DataSet` ;

CREATE TABLE IF NOT EXISTS `omds`.`DataSet` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `updatedAt` DATE NULL,
  `createdAt` DATE NULL,
  `Category` INT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_DataSet_Category1_idx` (`Category` ASC) VISIBLE,
  CONSTRAINT `fk_DataSet_Category1`
    FOREIGN KEY (`Category`)
    REFERENCES `omds`.`Category` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`Grant`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`Grant` ;

CREATE TABLE IF NOT EXISTS `omds`.`Grant` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `User` INT NOT NULL,
  `Role` INT NULL,
  `ActionType` INT NULL,
  `DataSet` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_Grant_User1_idx` (`User` ASC) VISIBLE,
  INDEX `fk_Grant_Role1_idx` (`Role` ASC) VISIBLE,
  INDEX `fk_Grant_ActionType1_idx` (`ActionType` ASC) VISIBLE,
  INDEX `fk_Grant_DataSet1_idx` (`DataSet` ASC) VISIBLE,
  CONSTRAINT `fk_Grant_User1`
    FOREIGN KEY (`User`)
    REFERENCES `omds`.`User` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Grant_Role1`
    FOREIGN KEY (`Role`)
    REFERENCES `omds`.`Role` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Grant_ActionType1`
    FOREIGN KEY (`ActionType`)
    REFERENCES `omds`.`ActionType` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Grant_DataSet1`
    FOREIGN KEY (`DataSet`)
    REFERENCES `omds`.`DataSet` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`Action`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`Action` ;

CREATE TABLE IF NOT EXISTS `omds`.`Action` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `at` DATE NULL,
  `State` INT NOT NULL,
  `ActionType` INT NOT NULL,
  `Grant` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_Action_State1_idx` (`State` ASC) VISIBLE,
  INDEX `fk_Action_ActionType1_idx` (`ActionType` ASC) VISIBLE,
  INDEX `fk_Action_Grant1_idx` (`Grant` ASC) VISIBLE,
  CONSTRAINT `fk_Action_State1`
    FOREIGN KEY (`State`)
    REFERENCES `omds`.`State` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Action_ActionType1`
    FOREIGN KEY (`ActionType`)
    REFERENCES `omds`.`ActionType` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Action_Grant1`
    FOREIGN KEY (`Grant`)
    REFERENCES `omds`.`Grant` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`DataFile`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`DataFile` ;

CREATE TABLE IF NOT EXISTS `omds`.`DataFile` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `updatedAt` DATE NULL,
  `createdAt` DATE NULL,
  `DataSet` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_DataFile_DataSet1_idx` (`DataSet` ASC) VISIBLE,
  CONSTRAINT `fk_DataFile_DataSet1`
    FOREIGN KEY (`DataSet`)
    REFERENCES `omds`.`DataSet` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `omds`.`MetaDataValue`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `omds`.`MetaDataValue` ;

CREATE TABLE IF NOT EXISTS `omds`.`MetaDataValue` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `value` VARCHAR(255) NULL,
  `MetaDataKey` INT NOT NULL,
  `DataSet` INT NULL,
  `Category` INT NULL,
  `DataFile` INT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_MetaDataValue_MetaDataKey1_idx` (`MetaDataKey` ASC) VISIBLE,
  INDEX `fk_MetaDataValue_DataSet1_idx` (`DataSet` ASC) VISIBLE,
  INDEX `fk_MetaDataValue_Category1_idx` (`Category` ASC) VISIBLE,
  INDEX `fk_MetaDataValue_DataFile1_idx` (`DataFile` ASC) VISIBLE,
  CONSTRAINT `fk_MetaDataValue_MetaDataKey1`
    FOREIGN KEY (`MetaDataKey`)
    REFERENCES `omds`.`MetaDataKey` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_MetaDataValue_DataSet1`
    FOREIGN KEY (`DataSet`)
    REFERENCES `omds`.`DataSet` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_MetaDataValue_Category1`
    FOREIGN KEY (`Category`)
    REFERENCES `omds`.`Category` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_MetaDataValue_DataFile1`
    FOREIGN KEY (`DataFile`)
    REFERENCES `omds`.`DataFile` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

-- -----------------------------------------------------
-- Data for table `omds`.`Type`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`Type` (`id`, `text`) VALUES (1, 'String');
INSERT INTO `omds`.`Type` (`id`, `text`) VALUES (2, 'Number');
INSERT INTO `omds`.`Type` (`id`, `text`) VALUES (3, 'Boolean');

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`User`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`User` (`id`, `password`, `name`) VALUES (1, 'R6fu6v4X8B', 'Qwerty');
INSERT INTO `omds`.`User` (`id`, `password`, `name`) VALUES (2, 'spKjN924T3', 'Misha3000');
INSERT INTO `omds`.`User` (`id`, `password`, `name`) VALUES (3, 'XLy5F35a6v', 'Sam');
INSERT INTO `omds`.`User` (`id`, `password`, `name`) VALUES (4, '2UXmzGz698', 'Loik');
INSERT INTO `omds`.`User` (`id`, `password`, `name`) VALUES (5, 'VG3nguN685', 'Mark');
INSERT INTO `omds`.`User` (`id`, `password`, `name`) VALUES (6, '8y8xcM9M5D', 'Antonio');
INSERT INTO `omds`.`User` (`id`, `password`, `name`) VALUES (7, 'JG6Z3rcn57', 'Tzuker');

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`State`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`State` (`id`, `name`) VALUES (1, 'Created');
INSERT INTO `omds`.`State` (`id`, `name`) VALUES (2, 'Updated');
INSERT INTO `omds`.`State` (`id`, `name`) VALUES (3, 'Deleted');
INSERT INTO `omds`.`State` (`id`, `name`) VALUES (4, 'Viewed');

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`Category`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`Category` (`id`, `Category`) VALUES (1, NULL);
INSERT INTO `omds`.`Category` (`id`, `Category`) VALUES (2, 1);
INSERT INTO `omds`.`Category` (`id`, `Category`) VALUES (3, 1);
INSERT INTO `omds`.`Category` (`id`, `Category`) VALUES (4, NULL);

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`MetaDataKey`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (1, 'Title', NULL, NULL);
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (2, 'Organization name', 'A team of contributors', NULL);
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (3, 'Author', NULL, 2);
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (4, 'Name', NULL, 3);
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (5, 'Surname', '', 3);
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (6, 'E-mail', 'Author\'s or contributor\'s email', 3);
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (7, 'Tags', 'Keywords to find information', NULL);
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (8, 'License', NULL, NULL);
INSERT INTO `omds`.`MetaDataKey` (`id`, `key`, `description`, `MetaDataKey`) VALUES (9, 'Description', NULL, NULL);

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`ActionType`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`ActionType` (`id`, `name`, `description`) VALUES (1, 'Create', 'Create dateset');
INSERT INTO `omds`.`ActionType` (`id`, `name`, `description`) VALUES (2, 'Update', 'Update dataset');
INSERT INTO `omds`.`ActionType` (`id`, `name`, `description`) VALUES (3, 'Delete', 'Delete dataset');
INSERT INTO `omds`.`ActionType` (`id`, `name`, `description`) VALUES (4, 'Read', 'Read dataset');

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`AvailableFor`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (1, 1, 1);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (2, 2, 1);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (3, 3, 1);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (4, 2, 2);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (5, 2, 3);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (6, 3, 3);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (7, 2, 4);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (8, 3, 4);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (9, 2, 5);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (10, 3, 5);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (11, 2, 6);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (12, 3, 6);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (13, 2, 7);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (14, 2, 8);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (15, 1, 9);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (16, 2, 9);
INSERT INTO `omds`.`AvailableFor` (`id`, `Type`, `MetaDataKey`) VALUES (17, 3, 9);

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`Role`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`Role` (`id`, `name`) VALUES (1, 'Author');
INSERT INTO `omds`.`Role` (`id`, `name`) VALUES (2, 'DataPublisher');
INSERT INTO `omds`.`Role` (`id`, `name`) VALUES (3, 'DataConsumer');

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`AvailableAction`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`AvailableAction` (`id`, `Role`, `ActionType`) VALUES (1, 1, 1);
INSERT INTO `omds`.`AvailableAction` (`id`, `Role`, `ActionType`) VALUES (2, 1, 2);
INSERT INTO `omds`.`AvailableAction` (`id`, `Role`, `ActionType`) VALUES (3, 1, 3);
INSERT INTO `omds`.`AvailableAction` (`id`, `Role`, `ActionType`) VALUES (4, 1, 4);
INSERT INTO `omds`.`AvailableAction` (`id`, `Role`, `ActionType`) VALUES (5, 2, 2);
INSERT INTO `omds`.`AvailableAction` (`id`, `Role`, `ActionType`) VALUES (6, 2, 4);
INSERT INTO `omds`.`AvailableAction` (`id`, `Role`, `ActionType`) VALUES (7, 3, 4);

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`DataSet`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`DataSet` (`id`, `updatedAt`, `createdAt`, `Category`) VALUES (1, '2021-11-01', '2021-10-01', 2);

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`Grant`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`Grant` (`id`, `User`, `Role`, `ActionType`, `DataSet`) VALUES (1, 2, 3, 4, 1);
INSERT INTO `omds`.`Grant` (`id`, `User`, `Role`, `ActionType`, `DataSet`) VALUES (2, 6, 1, 1, 1);
INSERT INTO `omds`.`Grant` (`id`, `User`, `Role`, `ActionType`, `DataSet`) VALUES (3, 4, 2, 2, 1);
INSERT INTO `omds`.`Grant` (`id`, `User`, `Role`, `ActionType`, `DataSet`) VALUES (4, 1, 2, 2, 1);
INSERT INTO `omds`.`Grant` (`id`, `User`, `Role`, `ActionType`, `DataSet`) VALUES (5, 3, 3, 4, 1);

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`Action`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`Action` (`id`, `at`, `State`, `ActionType`, `Grant`) VALUES (1, '2021-11-30', 4, 4, 1);
INSERT INTO `omds`.`Action` (`id`, `at`, `State`, `ActionType`, `Grant`) VALUES (2, '2021-12-01', 1, 1, 2);
INSERT INTO `omds`.`Action` (`id`, `at`, `State`, `ActionType`, `Grant`) VALUES (3, '2021-12-01', 2, 2, 3);
INSERT INTO `omds`.`Action` (`id`, `at`, `State`, `ActionType`, `Grant`) VALUES (4, '2021-12-02', 2, 2, 4);
INSERT INTO `omds`.`Action` (`id`, `at`, `State`, `ActionType`, `Grant`) VALUES (5, '2021-12-03', 4, 4, 5);

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`DataFile`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`DataFile` (`id`, `updatedAt`, `createdAt`, `DataSet`) VALUES (1, '2021-10-04', '2021-10-03', 1);
INSERT INTO `omds`.`DataFile` (`id`, `updatedAt`, `createdAt`, `DataSet`) VALUES (2, '2021-10-22', '2021-10-15', 1);
INSERT INTO `omds`.`DataFile` (`id`, `updatedAt`, `createdAt`, `DataSet`) VALUES (3, '2021-12-02', '2021-11-01', 1);

COMMIT;


-- -----------------------------------------------------
-- Data for table `omds`.`MetaDataValue`
-- -----------------------------------------------------
START TRANSACTION;
USE `omds`;
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (1, 'Finance', 1, NULL, 1, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (2, 'Prices', 1, NULL, 2, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (3, 'Prices correction coefficients in the World', 1, 1, NULL, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (4, 'International trade in services', 1, NULL, 3, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (5, 'Prices correction coefficients in the USA', 1, NULL, NULL, 1);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (6, 'Prices correction coefficients in the EU', 1, NULL, NULL, 2);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (7, 'Population', 1, NULL, 4, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (8, 'Prices correction coefficients in the Asia', 1, NULL, NULL, 3);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (9, 'QUAO_group', 2, 1, NULL, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (10, 'Alex', 4, 1, NULL, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (11, 'Swarowsky', 5, 1, NULL, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (12, 'Leo', 4, 1, NULL, NULL);
INSERT INTO `omds`.`MetaDataValue` (`id`, `value`, `MetaDataKey`, `DataSet`, `Category`, `DataFile`) VALUES (13, 'Gorrezen', 5, 1, NULL, NULL);

COMMIT;


- RESTfull сервіс для управління даними

