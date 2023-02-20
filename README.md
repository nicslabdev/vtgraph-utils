# CCBHash (Compound Code Block Hash)

## Objetivo

El objetivo de esta herramienta es crear un ***fuzzy hash*** capaz de complementar o incluso sustituir a algunos de los ya existentes como SSDEEP o TLSH.

Con ella podemos calcular el ***fuzzy hash*** tanto de las funciones de un fichero, como del fichero completo, pudiendo comparar las funciones de varios ficheros para determinar si alguna de las funcionas es maliciosa y, a su vez, comparar varios ficheros para ver si alguno es malicioso.

Un *hash* no es más que una función matemática que resume una gran cantidad de bits (o bytes) en unos pocos. Una de las características de los *hashes* es que dos conjuntos de bytes que son exactamente iguales excepto en un bit, deben dar lugar a dos *hashes* totalmente diferentes. Por el contrario, un ***fuzzy hash*** es un *hash* en cuanto resume una gran cantidad de bits en unos pocos pero, en este caso, dos conjuntos de bytes parecidos deben dar lugar a dos ***fuzzy hashes*** muy parecidos o incluso iguales.

Nuestro *hash* llamado **CCBHash** (Compound Code Block Hash) se compone de 16 bytes y se han demostrado resultados prometedores que mejoran a ***fuzzy hashes*** consolidados como SSDEEP o TLSH. Para más información, esta propuesta fue presentada en la RECSI 2022, por lo que se pueden consultar las actas de dicho congreso.

Actas del congreso: https://recsi2022.unican.es/wp-content/uploads/2022/10/LibroActas-978-84-19024-14-5.pdf

Diapositivas de CCBHash en el congreso: https://recsi2022.unican.es/wp-content/uploads/2022/11/Pablo-Perez-CCBHash-Compound-Code-Block-Hash-para-Analisis-de-Malware.pdf

## Funcionamiento

El único fichero realmente necesario es `ccbhash.py`.
El resto de ficheros componen la interfaz gráfica que, en este caso, no es necesaria.
La versión de Python utilizada es la 3.9.0.

Para usar `ccbhash.py` lo descargamos y desde un script de Python se ejecuta: `import ccbhash`

Para utilizar la interfaz gráfica:
1. Se despliega el backend ejecutando en: `python3 index.py`
2. Se abre en el navegador la dirección por defecto: `http://localhost:8000`
3. Se interactúa con la interfaz tal y cómo se indica en el frontend


# VT Graph

## Objetivo

El objetivo de esta propuesta es complementar/mejorar la herramienta de VirusTotal llamada VT Graph. En ella se puede observar información de ficheros, direcciones IPs, dominios y URLs dispuesta en forma de grafo, mostrando como los nodos se relacionan entre sí y aportando un gran valor en cuanto a malware se refiere.

Esta herramienta incorpora la creación de grupos, de forma automática y también manual si el usuario así lo desea. Estos grupos pueden concentrar la información de varios nodos. De la misma forma, al crear grupos de nodos, estos nodos se relacionan entre sí, tal y como lo hacen los nodos, pero simplificando y resumiendo notablemente la información. Para no perder detalle, el usuario podrá ampliar los grupos para ver como están formados y observar en detalle como los nodos que lo componen se relacionan con el resto de nodos/grupos.

Otra incorporación notable es la posibilidad de seleccionar varios grupos o nodos y ver cuales son los nodos comunes en el camino que los une, es decir, los nodos con los que estos se relacionan. Esta funcionalidad se puede ejecutar junto a la operación OR o AND, es decir, se destacan todos los nodos relacionados con los nodos seleccionados, o solo los comunes a todos ellos.

Para más detalles se recomienda poner en marcha la herramienta y en ella se muestra un menú detallado con todas las funcionalidades existentes.

## Funcionamiento

El fichero `vt_graph_util.py` incluye la librería usada para el backend. 
El fichero `vt_script.py` incluye un ejemplo de su uso.

Para desplegar el backend únicamente se debe ejecutar el fichero `index.py`.
La versión de Python utilizada es la 3.9.0.

Los ficheros `index.html` y `vt-graph.js` componen el frontend.

El funcionamiento utilizando la interfaz gráfica es muy sencillo:
1. Se despliega el backend ejecutando en: `python3 index.py`
2. Se abre en el navegador la dirección por defecto: `http://localhost:8000`
3. Se interactúa con la interfaz tal y cómo se indica en el frontend

El funcionamiento utilizando `vt_graph_util.py` desde un script:
1. Se obtiene el grafo generado con el algoritmo usando: `graph = Graph(graph_id, API_KEY)`
2. Se modifica el grafo a voluntad, usando funciones como `detail`, `expand`, `custom_group`...
3. Se obtiene el JSON con los grupos y links del grafo usando: `json_data = graph.graph_to_json()`
4. Se envía el JSON al frontend para que lo visualice
