# EJERCICIO 1 - PRUEBA DE CARGA DEL SERVICIO DE LOGIN

1. OBJETIVO

---

Realizar una prueba de carga sobre un servicio HTTP de autenticación utilizando
Apache JMeter, parametrizando las credenciales desde un archivo CSV y evaluando
los siguientes criterios:

* Throughput mínimo: 20 TPS (transacciones por segundo).
* Tiempo máximo de respuesta: 1.500 ms.
* Porcentaje de errores: menor al 3%.

2. NOTA IMPORTANTE - ENDPOINT ORIGINAL NO DISPONIBLE

---

El ejercicio proporcionó originalmente el siguiente servicio:

POST https://fakestoreapi.com/auth/login

Durante las pruebas realizadas, el endpoint original respondió HTTP 522.

Para verificar que el inconveniente no correspondiera exclusivamente a la
configuración de Apache JMeter, se realizó adicionalmente una prueba directa
utilizando curl.exe, fuera de JMeter.

La solicitud directa también obtuvo HTTP 522.

Por lo anterior, se determinó que el endpoint proporcionado originalmente
presentaba un problema de disponibilidad/accesibilidad desde el entorno de
ejecución y que el comportamiento no estaba relacionado exclusivamente con
la configuración de JMeter.

Debido a esta situación, se utilizó temporalmente un endpoint público
alternativo para poder validar técnicamente la implementación de la prueba:

POST https://dummyjson.com/auth/login

IMPORTANTE:

Los resultados de rendimiento incluidos en este proyecto corresponden al
endpoint alternativo DummyJSON y NO representan resultados de rendimiento
de FakeStoreAPI.

La prueba sobre FakeStoreAPI deberá repetirse cuando el endpoint original
se encuentre disponible para obtener una medición definitiva.

3. TECNOLOGÍAS

---

Herramienta:

* Apache JMeter 5.6.3

Java:

* Java 8 o superior.

Sistema operativo:

* Windows

Protocolo:

* HTTPS

Método:

* POST

Formato:

* JSON

4. ESTRUCTURA DEL PROYECTO

---

jmeter-login/
|
+-- jmeter-login.jmx
+-- users.csv
+-- README.txt
+-- conclusiones.txt
+-- resultados.txt

5. DATOS DE ENTRADA

---

Archivo:

users.csv

Contenido:

user,passwd
donero,ewedon
kevinryan,kev02937@
johnd,m38rmF$
derek,jklg**56
mor_2314,83r5^*

Configuración utilizada en CSV Data Set Config:

* Filename: users.csv
* Variable Names: user,passwd
* Ignore first line: True
* Delimiter: ,
* Recycle on EOF: True
* Stop thread on EOF: False

6. SERVICIO ORIGINAL DEL EJERCICIO

---

Endpoint:

POST https://fakestoreapi.com/auth/login

Body:

{
"username": "${user}",
"password": "${passwd}"
}

Resultado de las pruebas:

HTTP 522

La respuesta HTTP 522 fue obtenida tanto desde Apache JMeter como mediante
una solicitud directa utilizando curl.exe.

Esto permitió diferenciar un problema de disponibilidad del servicio de un
problema específico de configuración del script de JMeter.

7. ENDPOINT ALTERNATIVO

---

Debido a la indisponibilidad del endpoint original, se utilizó temporalmente
DummyJSON:

POST https://dummyjson.com/auth/login

Body:

{
"username": "${user}",
"password": "${passwd}"
}

El endpoint alternativo permitió validar:

* Configuración del HTTP Request.
* Método POST.
* Envío del body JSON.
* Parametrización mediante CSV.
* Sustitución de las variables ${user} y ${passwd}.
* Ejecución concurrente.
* Configuración de throughput.
* Obtención de métricas mediante JMeter.

8. CONFIGURACIÓN DE JMETER

---

THREAD GROUP

Number of Threads:
50

Ramp-Up Period:
10 segundos

Loop Count:
Infinite

Scheduler:
Habilitado

Duration:
30 segundos

CONSTANT THROUGHPUT TIMER

Target Throughput:
1200 samples/minute

Calculate Throughput Based On:
All active threads

9. THROUGHPUT OBJETIVO

---

El ejercicio solicita alcanzar como mínimo 20 TPS.

TPS significa Transactions Per Second, es decir, transacciones o solicitudes
por segundo.

La configuración utilizada fue:

1200 solicitudes/minuto / 60 segundos = 20 solicitudes/segundo

Por lo tanto:

1200 samples/minute = 20 TPS

10. CONFIGURACIÓN HTTP

---

HTTP Request:

Protocol:
https

Server:
dummyjson.com

Method:
POST

Path:
/auth/login

HTTP Header Manager:

Content-Type: application/json

Body:

{
"username": "${user}",
"password": "${passwd}"
}

11. EJECUCIÓN

---

Para ejecutar la prueba:

1. Instalar Java 8 o superior.

2. Instalar Apache JMeter 5.6.3.

3. Abrir el archivo jmeter-login.jmx.

4. Verificar que users.csv se encuentre disponible.

5. Verificar la configuración del CSV Data Set Config.

6. Verificar el Thread Group.

7. Verificar el Constant Throughput Timer.

8. Ejecutar el Test Plan.

9. Revisar el Summary Report.

10. Comparar los resultados contra los criterios de aceptación.

11. RESULTADOS OBTENIDOS

---

La ejecución documentada produjo los siguientes resultados:

Samples:
799

Average:
662 ms

Min:
184 ms

Max:
21415 ms

Standard Deviation:
2767.36 ms

Error %:
34.168%

Throughput:
0.19302 TPS

Received:
0.43 KB/sec

Sent:
0.04 KB/sec

Average Bytes:
2287.1

13. EVALUACIÓN DE LOS CRITERIOS

---

CRITERIO 1 - THROUGHPUT

Objetivo:

> = 20 TPS

Resultado:
0.19302 TPS

Estado:
NO CUMPLE

CRITERIO 2 - TIEMPO MÁXIMO DE RESPUESTA

Objetivo:
<= 1500 ms

Resultado:
21415 ms

Estado:
NO CUMPLE

CRITERIO 3 - PORCENTAJE DE ERRORES

Objetivo:
< 3%

Resultado:
34.168%

Estado:
NO CUMPLE

14. OBSERVACIONES

---

Aunque el Constant Throughput Timer fue configurado para intentar alcanzar
1200 solicitudes por minuto, esta configuración no garantiza que el servidor
pueda procesar efectivamente 20 solicitudes por segundo.

El throughput real obtenido fue de 0.19302 TPS.

También se observaron respuestas con tiempos elevados, alcanzando un máximo
de 21415 ms (21.415 segundos), además de un porcentaje de errores del 34.168%.

El tiempo promedio de 662 ms se encuentra por debajo de 1500 ms, pero el
criterio del ejercicio establece un tiempo MÁXIMO de 1500 ms, por lo que el
máximo registrado es el valor utilizado para determinar el incumplimiento.

15. REPRODUCIBILIDAD

---

El archivo jmeter-login.jmx contiene la configuración de la prueba y
users.csv contiene los datos de entrada.

El proyecto puede ser abierto utilizando Apache JMeter 5.6.3.

Debe tenerse en cuenta que DummyJSON es un servicio público, por lo que
su disponibilidad, comportamiento, tiempos de respuesta y restricciones
pueden cambiar.

16. CONCLUSIÓN DEL README

---

La prueba fue implementada y ejecutada utilizando Apache JMeter.

El endpoint original FakeStoreAPI no pudo ser utilizado para la ejecución
final debido a que respondió HTTP 522 tanto desde JMeter como mediante
curl.exe.

Por este motivo se utilizó DummyJSON como alternativa técnica para validar
el escenario.

Los resultados obtenidos con DummyJSON no cumplen los criterios establecidos
de 20 TPS, máximo de 1500 ms y menos del 3% de errores.

Estos resultados no deben interpretarse como una evaluación definitiva de
FakeStoreAPI.

Para obtener una conclusión definitiva sobre el servicio originalmente
solicitado, se recomienda repetir la prueba contra FakeStoreAPI cuando
el endpoint vuelva a estar disponible.
