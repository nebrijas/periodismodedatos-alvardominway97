# Actividad dirigida 2

El 'modus operandi' que hemos llevado a cabo en esta práctica ha sido el siguiente:

### IMPORTAR LIBRERÍA

-Comenzamos importando las librerías requests y el BeautifulSoup del bs4, para bajarnos la páhina web de la que queremos obtener los datos.

-Después procedimos a explicar las variables que vamos a utilizar, en este caso: países, oro, plata, bronce y total.

### DEFINIR URL

-Más tarde definimos la URL: En la web de [El País](https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/) aparece el medallero de TOKIO 2020, y cuyos datos vamos a usar para hacer web scarping.

### PETICIÓN A LA WEB

-Una vez establecida la URL, le haremos una peticióna la web: solo podrá leerla si el status code es = 200. En caso de no ser 200 la página no podrá leerse y por tanto no podrá llevarse a cabo la petición de hacer web scraping.

- Después pasaremos el contenido HTML de la página a un objeto 'Beautiful'.

### DEFINIR VARIABLES

- Ahora procedemos a definir las variables. Como se trata de los países en el medallero de los Juegos Olímpicos 2020, nuestras variables serán país (th), oro, plata, bronce y total (td).

### PREGUNTAMOS

- Una vez hayamos definido nuestras variables y las hayamos identificado con una función, preguntamos cuáles son los países que han obtenido más medallas en los juegos y establecemos una respuesta para ese input. Si la respuesta es 'sí', se imprimirá la respuesta 'vamos a ello'.

### INICIO DEL BUCLE DE DATOS 

- Cuando respondamos de forma afirmativa se impirmiran los resultados de los juegos con la premisa 'for i in range (20)' es decir, de los 20 países del medallero, para iniciar el bucle de obtención de datos. Usamos el bucle for para repetir un código de valores en una lista, en este caso de de países y medallas.

- Con el find all, buscamos por todas la etiquetas que tienen la clase país, oro, plata bronce o total, es decir, nuestras variables, dando el total de cada tipo de medallas y los paises.

-Una vez terminado el bucle, se imprimirán los resultados, en este caso los número de el ránking de los JJOO (%d) y las medallas (%s). Gracias la orden i+1 el bucle cuenta consatantemente entre el rango de sus variables.

 ` ` `
from bs4 import BeautifulSoup
import requests
#Datos sobre los Juegos Olímpicos en 2020

respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
  print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
  print ('PAÍSES')
  URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
  # Realizamos la petición a la web
  req = requests.get(URL)
  # Si el estatus code no es 200 no se puede leer la página
  if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
  # Pasamos el contenido HTML de la web a un objeto BeautifulSoup()
  html = BeautifulSoup(req.text, "html.parser")
  # Obtenemos todos los divs donde están las entradas
  paises = html.find_all("th",{"class":"pais"})
  oros = html.find_all("td",{"class":"m_oro"})
  platas = html.find_all("td",{"class":"m_plata"})
  bronces = html.find_all("td",{"class":"m_bronce"})
  totales = html.find_all("td",{"class":"m_total"})
  for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
    print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))

else:
  print('Qué lástima, y...')
