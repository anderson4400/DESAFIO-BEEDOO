# Decisiones para crear la historia de usuario
Motivos para crear los casos de pruebas

Cobertura Completa: Asegurar que todas las funcionalidades principales sean testeadas para detectar posibles fallos.
Usabilidad: Verificar que la interfaz de usuario sea intuiriva y facil de usar.
Rendimiento: Evaluar como se comporta la aplicacion bajo diferentes condiciones de carga.
Seguridad: identificar y corregir posibles vulnerabilidades de seguridad.
Compatibilidad: Garantizar que la aplicacion funcione correctamente en diversos dispositivos y navegadores.

# Documentación de Casos de Prueba en Gherkin


Inclui todos los casos en un solo Feature. 
 Feature: Registro de Curso

(Prueba de Exito)

  Scenario: TC-01 Registro de Curso Completo (Presencial)
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos
      | Nombre del Curso        | "Curso de Matemáticas"         |
      | Descripción del Curso   | "Curso avanzado de matemáticas."|
      | Instructor              | "Dr. Pérez"                    |
      | Imagen                  | "https://example.com/imagen.jpg"|
      | Fecha de Inicio         | "2024-08-01"                   |
      | Fecha de Fin            | "2024-12-01"                   |
      | Número de Estudiantes   | 30                             |
      | Tipo de Curso           | "Presencial"                   |
      | Otro                    | "Aula 101"                     |
    And El usuario hace clic en el botón "Registrar"
    Then El curso se registra correctamente y aparece en la lista de cursos
    
  Scenario: TC-02 No se puede registrar un curso con campos obligatorios vacíos
    Given El formulario de registro de curso está accesible
    When El usuario deja todos los campos vacíos
    And El usuario hace clic en el botón "Registrar"
    Then El sistema muestra mensajes de error indicando que los campos obligatorios deben ser completados


  Scenario: TC-03 Registro de Curso Completo (Online)
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos
      | Nombre del Curso        | "Curso de Programación"         |
      | Descripción del Curso   | "Curso básico de programación." |
      | Instructor              | "Ing. Rodríguez"                |
      | Imagen                  | ""                              |
      | Fecha de Inicio         | "2024-09-01"                    |
      | Fecha de Fin            | "2024-12-15"                    |
      | Número de Estudiantes   | 50                              |
      | Tipo de Curso           | "Online"                        |
      | Link Descripción        | "https://example.com/curso-online" |
    And El usuario hace clic en el botón "Registrar"
    Then El curso se registra correctamente y aparece en la lista de cursos

    Scenario:TC-04 Crear un curso presencial dejando el campo de imagen vacio.
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos
      | Nombre del Curso        | "Curso de Programación"         |
      | Descripción del Curso   | "Curso básico de programación." |
      | Instructor              | "Ing. Rodríguez"                |
      | Imagen                  | ""                              |
      | Fecha de Inicio         | "2024-09-01"                    |
      | Fecha de Fin            | "2024-12-15"                    |
      | Número de Estudiantes   | 50                              |
      | Tipo de Curso           | "Online"                        |
      | Link Descripción        | "https://example.com/curso-online" |
    And El usuario hace clic en el botón "Registrar"
    Then Se muestra el mensaje de que el campo "Imagen esta vacion."

    Scenario: TC-05 Crear un curso presencial dejando uno de los campos de fecha y el campo numerico vacio.
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos
      | Nombre del Curso        | "Curso de Programación"         |
      | Descripción del Curso   | "Curso básico de programación." |
      | Instructor              | "Ing. Rodríguez"                |
      | Imagen                  | ""                              |
      | Fecha de Inicio         |                                 |
      | Fecha de Fin            | "2024-12-15"                    |
      | Número de Estudiantes   |                                 |
      | Tipo de Curso           | "Online"                        |
      | Link Descripción        | "https://example.com/curso-online" |
    And El usuario hace clic en el botón "Registrar"
    Then Se muestra el mensaje de que algunos campos estan vacions

    Scenario: TC-06 Crear un curso dejando el campo descripcion vacion
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos
      | Nombre del Curso        | "Curso de Programación"         |
      | Descripción del Curso   | ""                              |
      | Instructor              | "Ing. Rodríguez"                |
      | Imagen                  | "https://example.com/curso-onlin"  |
      | Fecha de Inicio         | "2024-12-15"                      |
      | Fecha de Fin            | "2024-12-15"                    |
      | Número de Estudiantes   |                                 |
      | Tipo de Curso           | "Online"                        |
      | Link Descripción        | "https://example.com/curso-online" |
    And El usuario hace clic en el botón "Registrar"
    Then Se muestra el mensaje de que el campo "Descripcione esta vacion"

    (Casos de prueba Fallido que en este caso son Bug)
    
    Scenario: TC-07 Realizar el registro del curso con los campos requeridos vacios
    Given El formulario de registro de curso está accesible
    When El usuario No completa todos los campos con datos válidos
      | Nombre del Curso        | "" |
      | Descripción del Curso   | "" |
      | Instructor              | "" |
      | Imagen                  | "" |
      | Fecha de Inicio         | "" |
      | Fecha de Fin            | "" |
      | Número de Estudiantes   |    |
      | Tipo de Curso           | "" |
      | Link Descripción        | "" |
    And El usuario hace clic en el botón "Registrar"
    Then Se visualizar en la lista de cursos (Esta accion esta incorrecta.)

    Scenario: TC-08 Crear un curso con fechano no disponible
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos menos en el campo "Fecha inicion" y en "Fecha fin"
      | Nombre del Curso        | "Curso de Programación"         |
      | Descripción del Curso   | "Prueba de fecha"               |
      | Instructor              | "Ing. Rodríguez"                |
      | Imagen                  | "https://example.com/curso-onlin"  |
      | Fecha de Inicio         | "2021-12-15"                    |
      | Fecha de Fin            | "2020-04-15"                    |
      | Número de Estudiantes   |  45                             |
      | Tipo de Curso           | "Online"                        |
      | Link Descripción        | "https://example.com/curso-online" |
    And El usuario hace clic en el botón "Registrar"
    Then "Se deberia de mostrar un error ya que no se puede registrar con una fecha que ya paso"

    Scenario: TC-09 Crear un curso con numero de estudiante en cantidades negativas
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos menos en el campo numero de cantidad de estudiante con numero dnegativos
      | Nombre del Curso        | "Curso de Programación"         |
      | Descripción del Curso   | "Prueba de fecha"               |
      | Instructor              | "Ing. Rodríguez"                |
      | Imagen                  | "https://example.com/curso-onlin"  |
      | Fecha de Inicio         | "2024-08-15"                    |
      | Fecha de Fin            | "2024-09-15"                    |
      | Número de Estudiantes   |  -5                             |
      | Tipo de Curso           | "Online"                        |
      | Link Descripción        | "https://example.com/curso-online" |
    And El usuario hace clic en el botón "Registrar"
    Then "Se deberia de mostrar un error ya que no se puede registrar con numeros negativos"

    Scenario: TC-1O Crear un curso sin seleccionar el tipo de curso
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos menos en la lista de valores del tipo de curso
      | Nombre del Curso        | "Curso de Programación"         |
      | Descripción del Curso   | "Prueba de fecha"               |
      | Instructor              | "Ing. Rodríguez"                |
      | Imagen                  | "https://example.com/curso-onlin"  |
      | Fecha de Inicio         | "2024-08-15"                    |
      | Fecha de Fin            | "2024-09-15"                    |
      | Número de Estudiantes   |  4                              |
      | Tipo de Curso           |                                 |
      | Link Descripción        | "https://example.com/curso-online" |
    And El usuario hace clic en el botón "Registrar"
    Then "Se deberia de mostrar un error ya que no se puede registrar con campos requeridos vacios"

     Scenario: TC-11 Crear un curso con datos numericos en los campos
    Given El formulario de registro de curso está accesible
    When El usuario completa todos los campos con datos válidos menos en la lista de valores del tipo de curso
      | Nombre del Curso        |  4341241234|
      | Descripción del Curso   |  412341234123|
      | Instructor              |  123412341234|
      | Imagen                  |  123412341234|
      | Fecha de Inicio         |  412341234123|
      | Fecha de Fin            | 412341234123|
      | Número de Estudiantes   |  4 |
      | Tipo de Curso           |    |
      | Link Descripción        | "412412341234" |
    And El usuario hace clic en el botón "Registrar"
    Then "Se deberia de mostrar un error ya que no se puede registrar un cursos con datos numericos en campos que no deberia permitirlos"

    Scenario: TC-12 Realizar la eliminacion de uno de los cursos en el listao de cursos
    Given El formulario de registro de curso está accesible
    When Se meustra que existen cursos creado en la lita de cursos
    And El usuario hace clic en el botón "Eliminar Curso"
    Then "Se deberia de mostrar un mensaje indicando que se elimino pero no lo permite porque esta dando error."

# Problemas de la plataforma que se tienen que tomar en consideracion

Los campos del formulario tienen que ser requeridos para evitar que se registren datos vacio se tiene que mostrar un mensaje al momento de que se intente enviar el formulario vacio
![image](https://github.com/user-attachments/assets/f7cbe14b-5067-4cb3-a4d0-988065d89cf7)

los campos permiten datos numericos lo que esta muy mal solo el algunos campos tienen que recibir numero como los esto hace que se registre datos basura
![image](https://github.com/user-attachments/assets/2e111477-7153-45b8-ae41-851401838876)
![image](https://github.com/user-attachments/assets/c9eaacd9-af24-4835-af04-2473a93859bf)

El campo fecha no esta haciendo una validacion para comprobar la fecha y puede recibir fechas del paso de mucho tiempo esto se tiene que mejorar
![image](https://github.com/user-attachments/assets/62032a86-bfd5-4eea-a3d0-1b61f0164717)
![image](https://github.com/user-attachments/assets/86371afa-a077-43f8-ac05-12854db8e95a)

Campo Tipo de curso: esa lista no esta funcionando permite realizar registro sin tomar un valor de la lista otro valor que tiene que ser requerido
![image](https://github.com/user-attachments/assets/4cfc5898-b7c6-4f63-b82a-0c40527cc6af)

Campo Numero de estudiante: este recibe numero degativos lo cual esta muy mal esos datos no pueden recibir negativos porque entonces que persona tomara los cursos
![image](https://github.com/user-attachments/assets/06b2fd79-40be-402a-8a37-dee0563f8051)
![image](https://github.com/user-attachments/assets/dccf1dee-edd0-4839-926f-9b22161e39d4)

Los campos estan recibiendo cualquier tipo de caracteres eso se tiene que arreglar o aplicar una mascara para que solo reciba ciertos datos esto esta muy mal
![image](https://github.com/user-attachments/assets/7d8437de-00ed-4af1-8677-ec6286fe8757)
![image](https://github.com/user-attachments/assets/4c82284f-aee7-409f-a2db-a2e3ad6bbc2f)


La paltaforma da un 405 al momento de intentar eliminar uno de los cursos de la lista esto se tiene que resolver
![image](https://github.com/user-attachments/assets/9ca5f08b-a68b-4292-8a20-7897c1a9c6d2)


# Listado de los casos de prueba en el excel 
https://docs.google.com/spreadsheets/d/1ZFc3xUtU4UTZinGqBK4HQ64veQZGyYkqq_J3AGab6pY/edit?usp=sharing

# Link del Driver con las evidencias de las Ejecuciones
https://drive.google.com/drive/folders/1E8mRB6XzfV8a8I_KfZ_okPGV5je4CGfD?usp=sharing

# Errores descubiertos en la plataforma de https://creative-sherbet-a51eac.netlify.app/
405
![image](https://github.com/user-attachments/assets/d0284a55-5314-4d04-8f01-3e63dc4d92bb)
 Al momento de realizar la prueba de la eliminacion de los cursos se esta presentando  el error de 405 que es mas bien cuando el servidor rechada la solicitud en este caso
la de la eliminacion

-Pasos para replicarlos

Precondicion: Tener en la lista de cursos cursos ya registrados

Paso 1 - Dar click al boton de eliminar
![image](https://github.com/user-attachments/assets/2c920afa-1c80-4ae6-b7d3-e503ff0b7eab)

Paso 2 - Se mostrar un mensaje de "Curso Excluido con sucesso"
![image](https://github.com/user-attachments/assets/b8de54c0-b68e-4b61-b716-2548a2dadb9d)

- como se dio con el error 405
Utilice el inspector y luego me dirigi a "NetWork" en donde puedo ver las peticiones realizadas en el cual pude notar el errorc  405
![image](https://github.com/user-attachments/assets/500e2f2c-d31d-4f1b-ad60-ff677f2ec733)

- Gravedad del problema
esta es sumamente peligroso y arriesgado ya que el servidor esta rechanzado la peticion de eliminacion lo que quiere decir que existe un error de parte de los desarrolladores o con
el ambiente esto ocaciona que la base de datos se llene de informacion basura lo que consume espacion inecesario y que si se quiere eliminar no se podra lo cual indica una mala funcion
o comunicacion

# Vulnerabilidades
1- la plataforma no esta enmascarado la data permite cualquier tipo de datos en los campos
2- No esa realiando una validacion esta recibiendo valores vacios y lo pasa como datos correcto se necesita una validadcion de datos o de campos
3- la validacion de fecha esta permitiendo que se cree con fecha que esta muy atrasada no se puede registrar una clase para el pasado
4- La lista de valores de "Presencial" y "Online" no funciona se puede seguir el proceso sin necesidad de completarlo esta incorrecto esto
5- La eliminacion de curso no esta funcionando lo cual consumirar espacio el no poder borrar los cursos que no se necesita
6- Los campos puede recibir cualquier caracter esto es un peligro ya que pueden inyectar datos en la base de datos que puede darle informacion valiosa
7 - es muy vulnerable y carece de un codigo bien echo el simple echo de poder mandar cualquier datos lo confirma
8- el manejo de datos negativos en la ahora de las estudiante esto esta muy mal porque puede hacer un cuello de botella

Tecnica utilizada para dar con las vulnerabilidades:
Pruebas de componente y de integracion realice pruebas a cada campo uno por uno para saber cuales datos recibia y cuales no luego realice pruebas de integracion ta integrado otro campos
y probando la funcionalidad de registrar ya con esto pode encontrar esas vulnerabilidades 

# ¿Cuál sería el siguiente paso y cómo se realizaría para garantizar que la funcionalidad se entregue con calidad?

Lo primero es que si se me entrego las especificacion del modulo a trabajar digase  (Historia de HU) el modulo y los criterios de aceptacion se tienen que cumplir si o si en el modulo
si no se cumple se le hace saber al scrum master y al desarrollador que no esta cumpliendoy se devuelve hasta que el desarrollador realice los ajuste necesarios

3 puntos que puedo mencionar seria
1- La validacion de la informacion antes de ser registrar esto si o si se tiene que cumplir porque tiene que haber un filtro de datos.
2- Se tiene que realizar una demo del producto para dectetar posible cuello de botella y que si este cumpliendo los requisitos.
3- Apoyo y comuinicacion del los desarrolladores y el equipo de QA para que el producto cumplar con los estandares de calidad.


 # ¿Cómo evalúas y determinas si el error fue causado por esta funcionalidad?
 Revisar la Funcionalidad: Verificar si el error esta relacionado directamente con la funcionalidad que se esta probando. Revisar el diseño y los requisitos de la funcionalidad.

 Pruebas Aislada: Intentar replicar el error con diferentes escenarios de prueba para determinar si es espesifico de la funcionalidad o si puede ser causado por otra parte del sistema.

 Si el erro es causado por la funcionalidad
 -Documentar el problema: Detallo como la funcionalidad esta causando el error y proporsiciono reconmendaciones para su correcion.
 -Informar al equipo de desarrollo: comunicar el error al equipo de desarrollo para que puedan investigar y corregir el problema.

 # En caso de que no sea causado por ella, ¿qué harías?
 Si el error no es causado por la funcionalidad

 -Investigar Otras Areas: Examinar otras parte del sistema que podrian estar relacionados con el error. Realizar purbeas adicionales si es necesario
 -Informar el Problema: Comunicar el error al equipo responsable de la parte del sistema donde parece originarse el problema, proporcionanando toda la informacion recopilada.



    


    



