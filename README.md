1.	Cree un nuevo proyecto usando el comando rails new proyecto_inicio_sesion.
rails new proyecto_inicio_sesion

2.	Cree un nuevo modelo llamado 'Usuario' con la información anterior.
rails g model Usuario first_name:string last_name:string email_address:string age:integer

3.	Rails inmediatamente creará el campo ID como clave primaria, que se incrementa automáticamente así como las marcas de tiempo created_at  y  updated_at.
rails db:migrate

4.	Cree algunos registros en la tabla usuarios utilizando la consola de Rails.
rails c
Usuario.create(first_name:"Diego", last_name:"Hernandez", email_address:"email1@email.com", age:36)
Usuario.create(first_name:"Andres", last_name:"Ramos", email_address:"email2@email.com", age:30)
Usuario.create(first_name:"Angelica", last_name:"Martinez", email_address:"email3@email.com", age:39)
Usuario.create(first_name:"Maria", last_name:"Ramos", email_address:"email4@email.com", age:9)
Usuario.create(first_name:"", last_name:"Martinez", email_address:"email5@email.com", age:9)

5.	Ahora, agregue algunas validaciones al modelo para que:
5.1.	Requiera los cuatro campos.
validates :first_name, :last_name, :email_address, :age, presence: true

5.2.	La edad tiene que ser numérica.
validates :age, numericality: { only_integer: true }

5.3.	El nombre y el apellido deben tener una longitud mínima de 2 caracteres cada uno.
validates :first_name, :last_name, length: { minimum: 2 }

5.4.	La edad tiene que estar entre 10 y 150 (consulte http://apidock.com/rails/ActiveModel/Validations/HelperMethods/validates_numericality_of para obtener ayuda)
validates :age, numericality: { only_integer: true, greater_than: 10, less_than: 150}

5.5.	Estás familiarizado con .save  y  .valid?
irb(main):025:0> usuario.valid?
=> false

5.6.	Utilice .errors  y  .errors.full_messages para que pueda ver o mostrar los mensajes de error cuando fallen las validaciones.
["First name can't be blank",
 "Last name can't be blank",
 "Email address can't be blank",
 "Age can't be blank",
 "Age is not a number",
 "First name is too short (minimum is 2 characters)",
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