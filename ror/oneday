# One day:

* Creamos el proyecto.

rails new oneday
sudo rvm 1.9.3 do rails new pingupal

* Instalamos gemas necesarias.
sudo rvm 1.9.3 do bundle install

* Creamos paginas estáticas:
    rails generate controller Pages home contact
    
    
* Crear el modelo de datos del usuario.
 El campo `id` se genera automáticamente
    sudo rvm 1.9.3 do rails generate scaffold User name:string email:string


* Actuliazar la base de datos con los nuevos cambios incluido en el modelo de datos.
anarey@tuxiba:~/git/rail/oneday$ sudo rvm 1.9.3 do bundle exec rake db:migrate
==  CreateUsers: migrating ====================================================
-- create_table(:users)
   -> 0.0028s
==  CreateUsers: migrated (0.0030s) ===========================================

* Rutas activas para el objeto recien creado:
`config/routes.r`

    Oneday::Application.routes.draw do
        resources :users
    end
    
* Modelo de datos creado:
`app/models/user.rb`
 class User < ActiveRecord::Base
   attr_accessible :email, :name
 end
 
* Vistas creadas: 
`app/views/users/index.html.erb`
<h1>Listing users</h1>

<table>
  <tr>
    <th>Name</th>
    <th>Email</th>
    <th></th>
    <th></th>
    <th></th>
  </tr>

<% @users.each do |user| %>
  <tr>
    <td><%= user.name %></td>
    <td><%= user.email %></td>
    <td><%= link_to 'Show', user %></td>
    <td><%= link_to 'Edit', edit_user_path(user) %></td>
    <td><%= link_to 'Destroy', user, method: :delete, data: { confirm: 'Are you sure?' } %></td>
  </tr>
<% end %>
</table>

<br />

<%= link_to 'New User', new_user_path %>

      
* Controladores de los modelos de datos: app/controllers/users_controller.rb 
Definen las acciones que tendrás cada uno de los objetos. Automaticamente se crean las acciones correspondientes a view, edit, list, delete       

class UsersController < ApplicationController
  # GET /users
  # GET /users.json
  def index
    @users = User.all

    respond_to do |format|
      format.html # index.html.erb
      format.json { render json: @users }
    end 
  end 

  # GET /users/1
  # GET /users/1.json
  def show
    @user = User.find(params[:id])

    respond_to do |format|
      format.html # show.html.erb
      format.json { render json: @user }
    end 
  end 

  # GET /users/new
  # GET /users/new.json
  def new 
    @user = User.new

    respond_to do |format|
      format.html # new.html.erb
      format.json { render json: @user }
    end 
  end 

  # GET /users/1/edit
  def edit
    @user = User.find(params[:id])
  end 

  # POST /users
  # POST /users.json
  def create
    @user = User.new(params[:user])

    respond_to do |format|
      if @user.save
        format.html { redirect_to @user, notice: 'User was successfully created.' }
        format.json { render json: @user, status: :created, location: @user }
      else
        format.html { render action: "new" }
        format.json { render json: @user.errors, status: :unprocessable_entity }
      end 
    end 
  end 

  # PUT /users/1
  # PUT /users/1.json
  def update
    @user = User.find(params[:id])

    respond_to do |format|
      if @user.update_attributes(params[:user])
        format.html { redirect_to @user, notice: 'User was successfully updated.' }
        format.json { head :no_content }
      else


* Añadimos contenido general para las vistas: app/views/layouts/application.html.erb

* Integración del proyecto con bootstraps
@import bootstraps

* Contenido estático de la web (img/scc/javascript/ ...)
app/assets/stypeshees

* Creación de un helper ## crear codigo reuitlizable entre vistas
"app/helpers/application_helper.rb
  1 module ApplicationHelper
  2 
  3     def full_title(page_title)
  4         base_title = "Pagina de ejemplo de tuxpal"
  5 
  6         if page_title.empty?
  7             base_title
  8         else
  9             "#{base_title} | #{page_title}"
 10 
 11         end
 12     end
 13 end

* Partials => codigo que se saca a un fichero de forma que se facilite la lectura y pueda ser generico
app/views/layouts/_shim.html.erb

## Modelo de datos:
* Users es el Controller
* User es el Model

### Crear el modelo de datos:
rails generate model User name :string email :string

### Migraciones: 
Se crea el fichero db/development.sqlite3

* Iniciar la creación de las tables en la bd en función del modelo definido:
bundle exec rake db:migrate

* Deshacer una migración:
db: rollback

## Uso de Active Record:
user.find(1)
user.find_by_email("ana@ana@.org")  ## Método que se crea automágicamente por Active Record.
user.all ## devuelve todos los objetos.

## Actualizando datos:
* 1 forma:  user.email = "ana@baa.net"
            user.save ## Actualiza los datos en la base de datos.
* 2 forma: user.update_attributes(name: "", email: "" ) ## Sólo se pueden actualizar de esta forma los atributos incluidos en attr_access

* Obtener errores de la consola, cuando al crear un usuario hubo un error: user.errors.full_messages

## Añadir restricciones a los modelos de datos:
 12 class User < ActiveRecord::Base
 13   attr_accessible :email, :name
 14 
 15   validates :name,  presence: true, length: { maximum: 50 }
 16 
 17   VALID_EMAIL_REGEX = /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i
 18   validates :email, presence: true, format: { with: VALID_EMAIL_REGEX }, uniqueness: true
 19 
 20   has_many :microposts
 21 
 22 end

## Gemas de interes:

* annotate: crea comentarios en los ficheros del modelo de datos con las estructuras de base de datos que corresponden.




Usamos: 
app/views/layouts/application.html.erb
Mi proyecto en Ruby | <%= full_title(yield(:title)) %>


