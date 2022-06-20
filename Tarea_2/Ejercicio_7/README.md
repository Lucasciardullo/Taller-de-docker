Se estan corriendo dos imagenes, la de postgres y la de nicopaez/jobvacancy-ruby:1.3.0
Se pueden ver ya que en la imagen esta la especificacion link a db que es el otro contenedor 


version: '2'
services:
  web: #Nombre del contenedor
    image: nicopaez/jobvacancy-ruby:1.3.0 #de donde obtener la imagen
    links: #Le  indicamos que tenga un link con el contenedor db
      - db
    ports: # Declaramos los puertos a usar
      - "3001:3000"
    environment: # Aca declaramos variables del ambiente
      PORT: "3000"
      RACK_ENV: "production"
      DATABASE_URL: "postgres://postgres:Passw0rd!@db:5432/postgres"
    depends_on: #marcamos las dependencias de el contenedor web a db
      - db
  db: #declaramos el otro contenedor
    image: postgres # la imagen la toma de postgres
    environment: #Variables
      POSTGRES_PASSWORD: Passw0rd!

