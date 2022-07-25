# README Usuarios

 "Last name is too short (minimum is 2 characters)"]

6.	Usando la consola de Rails...
6.1.	Verifique si le permite ingresar algunos registro que no cumplan con las reglas de validación que establecimos (ej. trate de crear un registro don la edad sea 5 ó mayor a 150 ó donde el nombre sea solo 1 caracter, etc.).
irb(main):025:0> usuario.valid?
=> false

6.2.	Asegúrate que tu consola devuelva los mensaje de error apropiados cuando intentas guardar un registro que no cumple con las reglas de validación.
"First name can't be blank"

6.3.	Consultar todos los usuarios.
Usuario.all
Usuario Load (0.3ms)  SELECT "usuarios".* FROM "usuarios"
=>
[#<Usuario:0x00000172ca947da0
  id: 1,
  first_name: "Diego",
...

6.4.	Consultar el primer usuario.
Usuario.first
Usuario Load (0.3ms)  SELECT "usuarios".* FROM "usuarios" ORDER BY "usuarios"."id" ASC LIMIT ?  [["LIMIT", 1]]
=>
#<Usuario:0x00000172cb24fe70
 id: 1,
 first_name: "Diego",
...

6.5.	Consultar el último usuario.
Usuario.last
Usuario Load (0.3ms)  SELECT "usuarios".* FROM "usuarios" ORDER BY "usuarios"."id" DESC LIMIT ?  [["LIMIT", 1]]
=>
#<Usuario:0x00000172cbec5d80
 id: 4,
 first_name: "Maria",
...

6.6.	Consultar todos los usuarios ordenados por el primer nombre (consulte las reglas para ordenar y más en  http://guides.rubyonrails.org/active_record_querying.html#ordering)
Usuario.order(first_name: :asc)

6.7.	Consultar el registro de usuario cuyo id es 3 y cambiar el apellido por otro valor. Haz esto directamente en la consola utilizando .find  y  .save.
Usuario.find(id= 3).update(last_name: "Martinezzz")

6.8.	Elimine el registro de usuario cuyo id es 4 (utilice algo como Usuario.find(2).destroy...).
Usuario.find(id= 4).destroy