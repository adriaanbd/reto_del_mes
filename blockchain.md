## Tema: Componentes básicos de Blockchain

El tema que se presente a continuación gira en torno a dos piezas fundamentales de un Blockchain:

* Un Bloque

* Una Cadena de Bloques

## Concepto

El Blockchain es una cadena de bloques con mucha similitud a una estructura de datos denominada Linked List o Lista Enlazada. Cada bloque esta conectado a otro bloque en la cadena y contiene información sobre una transacción en particular, una marca de tiempo, y un hash criptográfico del bloque previo.

Podemos crear un Blockchain con lo siguiente:

* Una clase denominada Bloque

* Un metodo para obtener el hash de la información del bloque

* Una clase denominada Cadena


### La idea de un bloque

![image-20191213232613423](/home/adriaanbd/.config/Typora/typora-user-images/image-20191213232613423.png)

Nuestro blockchain utilizará como mínimo, lo siguiente:

* el hash [SHA-256](https://en.wikipedia.org/wiki/SHA-2), ver: [Hashlib](https://docs.python.org/3.5/library/hashlib.html?highlight=hashlib%20sha256)
* [Greenwich Mean Time](https://en.wikipedia.org/wiki/Greenwich_Mean_Time), ver: [Datetime](https://docs.python.org/3.5/library/datetime.html)
* String como tipaje de datos para la informacion, ver: [Str](https://docs.python.org/3.5/library/stdtypes.html#text-sequence-type-str)

#### class Bloque

```python
import hashlib

class Bloque:

    def __init__(self, timestamp, data, previous_hash):
      self.timestamp = timestamp
      self.data = data
      self.previous_hash = previous_hash
      self.hash = self.calc_hash()
    
    def calc_hash(self):
      sha = hashlib.sha256()

      hash_str = "We are going to encode this string of data!".encode('utf-8')

      sha.update(hash_str)

      return sha.hexdigest()
```


#### class Cadena

```python
class Cadena:
	def __init__(self, #argumentos):
        """Variables de inicialización necesarios para por lo menos identificar el primer bloque y/o el último bloque. Otras variables también podrán ser agregadas"""
        
    def agregar_bloque(self):
        """Agrega un bloque a la cadena. Tomar en consideración que el primer bloque es especial porque no tiene previous_hash. Retorna True si la operación es exitosa, False de lo contrario. Considerar retornar con Error si se trata de algun caso especial"""
        
    def verificar_integridad(self):
        """Revisa la integridad de la cadena, bloque por bloque, asegurandose previous_hash sea igual al hash del bloque previo. Retorna False si la verificación no es exitosa, True de lo contrario"""
        
    def crear_fork(self):
    	"""Copia la cadena entera o un segmento de ella desde un punto en adelante. Retorna una Cadena. [OPCIONAL]"""

    def __str__(self):
    	"""Representación en un string de una cadena. Tambien podrá ser utilizando def __repr__(self) si prefiere [OPCIONAL]"""
```


### Casos Excepcionales

Los bloques pueden contener cualquier tipo de datos, no solamente enteros ("int") o cadenas de texto ("str")

## El reto

Crear código en Python que a partir de las clases Blockchain y Cadena permita:

* Crear y modificar cadenas
* Crear bloques con tipos de datos `str`, `int` u otros, pero que retorne un error  cuando se quiera crear un bloque con tipo "None"
* Crear bloques con un empty `str`, i.e. `""`
