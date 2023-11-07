CREATE TABLE IF NOT EXISTS `hotel`.`cliente` (
  `cod_cliente` INT NOT NULL AUTO_INCREMENT,
  `nome_cliente` VARCHAR(45) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  `telefone` INT NOT NULL,
  `sexo` VARCHAR(1) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  `cpf` INT NOT NULL,
  `passaporte` VARCHAR(45) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  `documento` VARCHAR(45) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  PRIMARY KEY (`cod_cliente`))
ENGINE = InnoDB
AUTO_INCREMENT = 12;

CREATE TABLE IF NOT EXISTS `hotel`.`nacionalidade` (
  `sigla` VARCHAR(3) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  `nome` VARCHAR(45) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  PRIMARY KEY (`sigla`))
ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `hotel`.`cliente_nacionalidade` (
  `FK_cod_cliente` INT NOT NULL,
  `FK_sigla` VARCHAR(2) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  INDEX `cod_cliente_idx` (`FK_cod_cliente` ASC) VISIBLE,
  INDEX `FK_idx` (`FK_cod_cliente` ASC) VISIBLE,
  INDEX `FK_idy` (`FK_sigla` ASC) VISIBLE,
  CONSTRAINT `FK_cod_cliente`
    FOREIGN KEY (`FK_cod_cliente`)
    REFERENCES `hotel`.`cliente` (`cod_cliente`),
  CONSTRAINT `FK_sigla`
    FOREIGN KEY (`FK_sigla`)
    REFERENCES `hotel`.`nacionalidade` (`sigla`))
ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `hotel`.`operadora` (
  `cod_ope` INT NOT NULL,
  `nome_ope` VARCHAR(45) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  PRIMARY KEY (`cod_ope`))
ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `hotel`.`quarto` (
  `num_quar` INT NOT NULL,
  `andar` INT NOT NULL,
  PRIMARY KEY (`num_quar`))
ENGINE = InnoDB;

CREATE TABLE IF NOT EXISTS `hotel`.`reserva` (
  `num_res` INT NOT NULL AUTO_INCREMENT,
  `num_cartao` INT NOT NULL,
  `qnt_dia` INT NOT NULL,
  `data_res` DATE NOT NULL,
  `data_ini` DATE NOT NULL,
  `status` INT NOT NULL,
  PRIMARY KEY (`num_res`))
ENGINE = InnoDB
AUTO_INCREMENT = 5;

CREATE TABLE IF NOT EXISTS `hotel`.`tipo_quar` (
  `cod_tipo_quar` INT NOT NULL,
  `desc_tipo` VARCHAR(45) COLLATE 'utf8mb3_unicode_ci' NOT NULL,
  `val_tipo_quar` INT NOT NULL,
  PRIMARY KEY (`cod_tipo_quar`))
ENGINE = InnoDB;

ALTER TABLE cliente_nacionalidade
ADD INDEX FK_idx (FK_cod_cliente ASC) VISIBLE,
ADD INDEX FK_idy (FK_sigla ASC) VISIBLE;

ALTER TABLE cliente_nacionalidade
ADD CONSTRAINT FK_cod_cliente
FOREIGN KEY (FK_cod_cliente)
REFERENCES cliente (cod_cliente),
ADD CONSTRAINT FK_sigla
FOREIGN KEY (FK_sigla)
REFERENCES nacionalidade (sigla)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE quarto
ADD INDEX FK_idz (FK_cod_tipo_quar ASC) VISIBLE;

ALTER TABLE quarto
ADD CONSTRAINT FK_cod_tipo_quar
FOREIGN KEY (FK_cod_tipo_quar)
REFERENCES tipo_quar (cod_tipo_quar)
ON DELETE NO ACTION
ON UPDATE NO ACTION;

ALTER TABLE reserva
ADD INDEX FK_ida (FK_cod_cliente ASC) VISIBLE,
ADD INDEX FK_idb (FK_cod_tipo_quar ASC) VISIBLE,
ADD INDEX FK_idc (FK_cod_ope ASC) VISIBLE;

ALTER TABLE reserva
ADD CONSTRAINT FK_cod_cliente
FOREIGN KEY (FK_cod_cliente)
REFERENCES cliente (cod_cliente),
ADD CONSTRAINT FK_cod_tipo_quar
FOREIGN KEY (FK_cod_tipo_quar)
REFERENCES tipo_quar (cod_tipo_quar),
ADD CONSTRAINT FK_cod_ope
FOREIGN KEY (FK_cod_ope)
REFERENCES operadora (cod_ope)
ON DELETE NO ACTION
ON UPDATE NO ACTION;


INSERT INTO cliente(nome_cliente, telefone, sexo, cpf, passaporte, documento)
VALUES ('Roberto', 984327241, 'm', 07966584, '98786-542', '25585-877');

INSERT INTO nacionalidade(sigla, nome)
VALUES ('BR', 'Brasil');

INSERT INTO operadora(cod_ope, nome_ope)
VALUES (321, 'mastercard');

INSERT INTO reserva(num_cartao, qnt_dia, data_res, data_ini, status)
VALUES (321654987, 7, '2023-10-31', '2023-11-06', 1);

INSERT INTO tipo_quar(cod_tipo_quar, desc_tipo, val_tipo_quar)
VALUES (01, 'suite luxo', 500);

INSERT INTO quarto(num_quar, andar)
VALUES (674, 6);


INSERT INTO cliente(nome_cliente, telefone, sexo, cpf, passaporte, documento)
VALUES ('Lucas', 987654321, 'm', 1232344124, '133442-112', '2232322-437');

INSERT INTO nacionalidade(sigla, nome)
VALUES ('JP', 'Japao');

INSERT INTO operadora(cod_ope, nome_ope)
VALUES (426, 'visa');

INSERT INTO reserva(num_cartao, qnt_dia, data_res, data_ini, status)
VALUES (233434, 3, '2023-11-05', '2023-11-8', 1);

INSERT INTO tipo_quar(cod_tipo_quar, desc_tipo, val_tipo_quar)
VALUES (03, 'quarto comum', 150);

INSERT INTO quarto(num_quar, andar)
VALUES (145, 1);


INSERT INTO cliente(nome_cliente, telefone, sexo, cpf, passaporte, documento)
VALUES ('Laura', 912345678, 'f', 534242443, '2323442-533', '23242442-232');

INSERT INTO nacionalidade(sigla, nome)
VALUES ('EUA', 'Estados Unidos');

INSERT INTO operadora(cod_ope, nome_ope)
VALUES (242, 'nubank');

INSERT INTO reserva(num_cartao, qnt_dia, data_res, data_ini, status)
VALUES (32232324, 5, '2023-06-30', '2023-07-5', 1);

INSERT INTO tipo_quar(cod_tipo_quar, desc_tipo, val_tipo_quar)
VALUES (02, 'suite', 350);

INSERT INTO quarto(num_quar, andar)
VALUES (421, 4);

SELECT cliente.nome_cliente, nacionalidade.nome
FROM cliente_nacionalidade
INNER JOIN nacionalidade ON nacionalidade.sigla = cliente_nacionalidade.FK_sigla
INNER JOIN cliente ON cliente.cod_cliente = cliente_nacionalidade.FK_cod_cliente;


UPDATE cliente
SET telefone = 987365415, cpf = 23214521
WHERE cod_cliente = 2;

DELETE FROM cliente
WHERE sexo = 'm';

SELECT nome_cliente
FROM cliente;

SELECT FK_sigla
FROM cliente_nacionalidade;

SELECT sigla
FROM nacionalidade;

SELECT nome_ope
FROM operadora;

SELECT num_quar
FROM quarto;

SELECT num_res
FROM reserva;

SELECT desc_tipo
FROM tipo_quar;
