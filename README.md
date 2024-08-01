# decisiones para crear la historia de usuario
Motivos para crear los casos de pruebas

Cobertura Completa: Asegurar que todas las funcionalidades principales sean testeadas para detectar posibles fallos.
Usabilidad: Verificar que la interfaz de usuario sea intuiriva y facil de usar.
Rendimiento: Evaluar como se comporta la aplicacion bajo diferentes condiciones de carga.
Seguridad: identificar y corregir posibles vulnerabilidades de seguridad.
Compatibilidad: Garantizar que la aplicacion funcione correctamente en diversos dispositivos y navegadores.

 Documentación de Casos de Prueba en Gherkin


Inclui todos los casos en un solo Feature. 
 Feature: Registro de Curso

(Prueba de Exito)

  Scenario: Registro de Curso Completo (Presencial)
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
    
  Scenario: No se puede registrar un curso con campos obligatorios vacíos
    Given El formulario de registro de curso está accesible
    When El usuario deja todos los campos vacíos
    And El usuario hace clic en el botón "Registrar"
    Then El sistema muestra mensajes de error indicando que los campos obligatorios deben ser completados


  Scenario: Registro de Curso Completo (Online)
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

    Scenario: Crear un curso presencial dejando el campo de imagen vacio.
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
    Then ESe muestra el mensaje de que el campo "Imagen esta vacion."

    Scenario: Crear un curso presencial dejando uno de los campos de fecha y el campo numerico vacio.
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
    Then ESe muestra el mensaje de que algunos campos estan vacions

    Scenario: Crear un curso dejando el campo descripcion vacion
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
    Then Se muestra el mensaje de que el campo "Descripcione sta vacion"

    (Casos de prueba Fallido que en este caso son Bug)
    
    Scenario: Realizar el registro del curso con los campos requeridos vacios
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

    Scenario: Crear un curso con fechano disponible
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

    Scenario: Crear un curso con numero de estudiante en cantidades negativas
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

    Scenario: Crear un curso sin seleccionar el tipo de curso
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
    Then "Se deberia de mostrar un error ya que no se puede registrar con campos requeridosvacios"

     Scenario: Crear un curso scon datos numericos en los campos
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

     Scenario: Realizar la eliminacion de uno de los cursos en el listao de cursos
    Given El formulario de registro de curso está accesible
    When Se meustra que existen cursos creado en la lita de cursos
    And El usuario hace clic en el botón "Eliminar Curso"
    Then "Se deberia de mostrar un mensaje indicando que se elimino pero no lo permite porque esta dando error."

Problemas de la plataforma que se tienen que tomar en consideracion

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














    


    



