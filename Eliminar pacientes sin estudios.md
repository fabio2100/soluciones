RESOLUCIÓN ELIMINACIÓN DE PACIENTES SIN DATOS EN TABLA ESTUDIOS. 
Tengo una tabla de estudios médicos con una columna que corresponde al id del paciente
Tengo una tabla con los datos de los pacientes, donde lógicamente se encuentra el id del paciente. 
Tengo que eliminar todos los datos de la tabla de pacientes que no tengan estudios alguno 
CONSULTA PARA encontrar todos los PACIENTES sin ESTUDIOS
```SELECT * from pacientes FULL JOIN estudios ON estudios.idpaciente = pacientes.idpaciente WHERE estudios.idestudio IS NULL```
PARA ELIMINAR LOS PACIENTES: 
```DELETE FROM pacientes WHERE idpaciente IN (SELECT pacientes.idpaciente from pacientes FULL JOIN estudios ON estudios.idpaciente = pacientes.idpaciente WHERE estudios.idestudio IS NULL)```
