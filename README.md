CREATE DATABASE dbConferenceVG
GO

USE dbConferenceVG
GO
--CREACIÓN DE TABLAS
CREATE TABLE PARTICIPANTE (
    IDPAR INT IDENTITY(1,1),
    FECREGPAR DATE DEFAULT GETDATE(),
    NOMPAR VARCHAR(50),
	APEPAR VARCHAR(50),
    DNIPAR CHAR(8),
	TIPPAR CHAR(1),
	CELPAR CHAR(9),
	EMAPAR VARCHAR(90),
	DIRPAR VARCHAR(90),
    ESTPAR CHAR(1) DEFAULT 'A',
	CODREG char(5),
    CONSTRAINT IDPAR PRIMARY KEY (IDPAR)
) 
GO

create table PONENTE (
	CODPON char(5),
	NOMPON varchar(50),
	APEPON varchar(80),
	CELPON char(9),
	DNIPON char(9),
	EMAPON varchar(90),
	DIRPON varchar(90),
	CONSTRAINT CODPON PRIMARY KEY (CODPON)
)
GO

 create table CONFERENCIA (
	CODCONF char(5),
    TEMCONF varchar(90),
    FECCONF date DEFAULT GETDATE(),
    PONCONF char(5),
    CONSTRAINT CODCONF PRIMARY KEY (CODCONF)
 )
 GO

  create table REGISTRO(
	CODREG char(5),
    CODPAR int ,
    FECREG date DEFAULT GETDATE(),
    CERTREG char(1),
	IDPAR INT,
    CONSTRAINT CODREG PRIMARY KEY (CODREG)
 )
 GO
    
 create table REGISTRODETALLE(
	IDREGDET int IDENTITY(1,1),
    CODREG char(5),
	CODCONF char(5),
	CANTPART int,
    FECREG char(5)DEFAULT GETDATE(),
    CONSTRAINT IDREGDET PRIMARY KEY (IDREGDET)
 )
 GO

--RELACIONES DE TABLAS
ALTER TABLE REGISTRO
	ADD CONSTRAINT PARTICIPANTE_REGISTRO
	FOREIGN KEY (IDPAR)
	REFERENCES PARTICIPANTE(IDPAR)


ALTER TABLE REGISTRODETALLE
	ADD CONSTRAINT REGISTRO_REGISTRODETALLE
	FOREIGN KEY (CODREG)
	REFERENCES REGISTRO(CODREG)


ALTER TABLE CONFERENCIA
	ADD CONSTRAINT _PONENTE_CONFERENCIA
	FOREIGN KEY (PONCONF)
	REFERENCES PONENTE(CODPON)


ALTER TABLE REGISTRODETALLE
	ADD CONSTRAINT REGISTRODETALLE_CONFERENCIA
	FOREIGN KEY (CODCONF)
	REFERENCES CONFERENCIA(CODCONF)

-- VER ESTRUCTURAS DE LAS TABLAS
EXEC sp_columns @table_name='PARTICIPANTE' 
GO

EXEC sp_columns @table_name='PONENTE' 
GO

EXEC sp_columns @table_name='CONFERENCIA' 
GO

EXEC sp_columns @table_name='REGISTRO' 
GO

EXEC sp_columns @table_name='REGISTRODETALLE' 
GO


--INSERTAR REGISTRO EN LA TABLA PARTICIPANTE	
SET DATEFORMAT dmy 
GO

INSERT INTO PARTICIPANTE
(NOMPAR,APEPAR,DNIPAR,TIPPAR,CELPAR,EMAPAR,DIRPAR,ESTPAR)
VALUES
('Juan','Campos Pérez','40255133','1','986512478','juan.campos@vallegrande.edu.pe','Av.Miraflores','A'),
('sofia','Solano Ávila','64978531','1','974815258','sofia.solano@vallegrande.edu.pe','Jr.Huallaga','A'),
('María','Rosales Guerra','15925874','1','986532147','maria.rosales@vallegrande.edu.pe','Calle Girasoles','A'),
('Marcos','Alarcón Hermosa','48781512','2','','marcos.alarcon@vallegrande.edu.pe','','A'),
('Martín','Samán Arata','84152631','2','','martin.saman@vallegrande.edu.pe','Jr.La Unión','A'),
('José','Quispe Luyo','48161937','2','978415321','jose.quispe@vallegrande.edu.pe','Calle Abancay','A'),
('Claudia','Barraza Carrasco','78452596','3','','cbarraza@gmail.com','Jr.Las Gardenias','A'),
('Jhohana','Bendezú Anccasi','74321564','3','','jbendezu@yahoo.com','','A'),
('Mario','Acosta Palomino','15326499','3','931764521','mario.acosta@outlook.com','Av.Miraflores','A')
GO
--Listar registros PARCTICIPANTES
SELECT * FROM PARTICIPANTE
GO
--Insertar registros en la tabla PONENTE
SET DATEFORMAT dmy 
GO

INSERT INTO PONENTE
(CODPON,NOMPON,APEPON,CELPON,DNIPON,EMAPON,DIRPON)
VALUES
('P0001','Alberto','Corrales Lozada','','15363798','alberto.corrales@yahoo.com','Calle Los Portales'),
('P0002','Juana','Sánchez Ortega','974815258','13256497','juana.sanchez@yahoo.com','Av.La Libertad'),
('P0003','Javier','Nakasone Villa','995236147','15953575','javier.nakasone@yahoo.com','Jr.San Martín'),
('P0004','Sonia','Huayta Medina','','12657814','sonia.huayta@yahoo.com','Av.Las Gardenias'),
('P0005','Fabiano','Carrión Ávila','','12233647','','Jr.Huancayo')
GO

--listar registros PONENTE
SELECT * FROM PONENTE
GO

--Insertar registros en la tabla REGISTRO
INSERT INTO REGISTRO
(CODREG,CODPAR,CERTREG)
VALUES
('R0001','1','S'),
('R0002','3','S'),
('R0003','4','S'),
('R0004','7','S'),
('R0005','2','N'),
('R0006','5','N'),
('R0007','6','N'),
('R0008','9','N')
GO
--Listar registros de la tabla REGISTRO
SELECT*FROM REGISTRO
GO
