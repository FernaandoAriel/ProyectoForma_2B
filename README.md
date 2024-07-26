CREATE TABLE Enfermero (
    id_Enfermero INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    correo VARCHAR2(100) UNIQUE NOT NULL,
    contrasena_Enfermero VARCHAR2(50) NOT NULL
);

INSERT ALL INTO Enfermero (
    correo,
    contrasena_Enfermero
) VALUES (
    'fernando@gmail.com',
    'Ariel1312DD'
) 
SELECT * FROM dual;

SELECT * FROM Enfermero;

drop table Enfermero
SELECT * FROM Enfermero WHERE correo = 'fernando@gmail.com' AND contrasena_Enfermero = 'Ariel1312DD';

CREATE TABLE Pacientes (
    id_Pacientes INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    paciente_Nombre VARCHAR2(100) NOT NULL,
    paciente_Apellido VARCHAR2(100) NOT NULL,
    paciente_Edad INT NOT NULL,
    paciente_Enfermedad VARCHAR2(200) NOT NULL,
    numero_Habitacion INT NOT NULL,
    cama INT NOT NULL,
    fecha_Ingreso DATE NOT NULL
);

drop table Pacientes

select *from pacientes
COMMIT;

insert into pacientes ( paciente_Nombre,
    paciente_Apellido,
    paciente_Edad,
    paciente_Enfermedad,
    numero_Habitacion,
    cama,
    fecha_Ingreso
) VALUES (
    'Katherine',
    'Sofía',
    18,
    'Diabetes',
    220,
    1,
    '22/08/2023'
);
 
insert into Pacientes (
    paciente_Nombre,
    paciente_Apellido,
    paciente_Edad,
    paciente_Enfermedad,
    numero_Habitacion,
    cama,
    fecha_Ingreso
) VALUES (
    'Katherine',
    'Sofía',
    18,
    'Diabetes',
    220,
    1,
    '22/08/2023'
);

insert into Pacientes (
    paciente_Nombre,
    paciente_Apellido,
    paciente_Edad,
    paciente_Enfermedad,
    numero_Habitacion,
    cama,
    fecha_Ingreso
) VALUES (
    'Kevin',
    'Fernando',
    17,
    'Ansiedad Cronica',
    133,
    1,
    '13/03/2007'
);

SELECT * FROM dual;

SELECT * FROM Pacientes;

CREATE TABLE Medicamentos_Paciente (
    id_Medicamento INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    nombre_Medicamento VARCHAR2(100) NOT NULL,
    descripcion_Medicamento VARCHAR2(500) NOT NULL
);


INSERT INTO Medicamentos_Paciente (
    nombre_Medicamento,
    descripcion_Medicamento
) VALUES (
    'Penicilina',
    'Medicamento utilizado para el tratamiento de enfermedades respiratorias'
);

INSERT INTO Medicamentos_Paciente (
    nombre_medicamento,
    descripcion_Medicamento
) VALUES (
    'Acetaminofen',
    'Controlador de dolores fuertes, que ayuda a la relajacion de sintomas de dolor'
);

SELECT * FROM Medicamentos_Paciente;
SELECT * FROM Pacientes;

CREATE TABLE aplicacion_Medicamentos (
    id_Aplicacion INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    tiempo_Aplicacion VARCHAR2(10) NOT NULL,
    id_Paciente INT,
    id_Medicamento INT,
    CONSTRAINT fk_paciente FOREIGN KEY ( id_Paciente )
    REFERENCES Pacientes ( id_Pacientes ),
    CONSTRAINT fk_medicamento FOREIGN KEY ( id_Medicamento )
    REFERENCES Medicamentos_Paciente ( id_Medicamento)
);

SELECT id_Pacientes FROM Pacientes WHERE (paciente_Nombre || ' ' || paciente_Apellido ) = 'Fernando Morales';

SELECT id_Medicamento FROM Medicamentos_Paciente WHERE nombre_Medicamento = 'Penicilina';

SELECT * FROM Pacientes;

INSERT INTO aplicacion_Medicamentos (
    tiempo_Aplicacion,
    id_Paciente,
    id_Medicamento
) VALUES (
    '3:00 AM',
    6,
    5
); 

INSERT INTO aplicacion_Medicamentos (
    tiempo_Aplicacion,
    id_Paciente,
    id_Medicamento
) VALUES (
    '10:00 PM',
    7,
    4
);



SELECT * FROM aplicacion_Medicamentos;

SELECT
    p.paciente_Nombre AS nombre,
    p.paciente_Apellido AS apellido,
    p.paciente_Edad AS edad,
    p.paciente_Enfermedad AS enfermedad,
    p.numero_Habitacion AS habitacion,
    p.cama AS cama,
    p.fecha_Ingreso AS fecha_ingreso,
    m.nombre_Medicamento AS nombre_medicamento,
    am.tiempo_Aplicacion
FROM
         aplicacion_Medicamentos am
    INNER JOIN Pacientes p ON am.id_Paciente = p.id_Pacientes
    INNER JOIN Medicamentos_Paciente m ON am.id_Medicamento = m.id_Medicamento;
    
drop table aplicacion_Medicamentos
drop table Medicamentos_Paciente
drop table Pacientes
drop table Enfermero
