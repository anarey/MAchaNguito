http://mysql-python.sourceforge.net/MySQLdb.html#mysqldb

Ejemplo de acceso a una base de datos

# -*- coding: utf-8 -*-
## Obtener datos proyecto.
## Hacemos consulta a la base de datos

## importamos el modulo de mysql
import MySQLdb

servidor = "localhost"
usuario = "root"
clave = "4n4r3y!"
bd = "drupal6"

### Creamos la conexión a la base de datos 
### Parámetros: servidor, usuario, clave, bd, etc 
### Devuelve un objeto connetion

con = MySQLdb.connect(servidor, usuario, clave)
con.select_db(bd)

### Creamos un cursos

cursor = con.cursor()

## Consulta a ejecutar
sql="SELECT * from table"

## Ejecutamos la consulte
cursor.execute(sql)

## Consultamos los datos.
## obtiene todos los datos en forma de tuplas
rows = cursor.fetchall()
for x in rows:
    print "%d, %s" % (x[0],x[1])

print "El numero de lineas es ", cursor.rowcount

cursor.close()

### 


########## Devolviento los datos en diccionarios: 

cursor = con.cursor(MySQLdb.cursors.DictCursor)
### Problemas de codificación de bases de datos:

db.set_character_set('utf8')
dbc.execute('SET NAMES utf8;')
dbc.execute('SET CHARACTER SET utf8;')
dbc.execute('SET character_set_connection=utf8;')

##"db" is the result of MySQLdb.connect, and "dbc" is the result of db.cursor().
http://www.dasprids.de/blog/2007/12/17/python-mysqldb-and-utf-8


Uso de la clase:

** En el mismo archivo:

  9 class Proyecto():
 10     """ Clase proyecto  """
 11     def __init__(self, proyecto):
 12         self.proyecto = proyecto

 39     p = Proyecto(x['nombre'])
 40     print "#################"
 41     print p.proyecto


** Distinto archivo

