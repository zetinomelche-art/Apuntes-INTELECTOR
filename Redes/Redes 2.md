# Phisical Layer Technologies


En la capa fisica hay 3 formas de mover los datos
    - Cableado de cobre
    - Fibra Optica
    - Wireles

# Cableado de cobre

Este a su ves se subdivide en 2 categorias

## De par trenzado (Twisted Pair)
Se usa por que podemos tranportar gran cantidad de datos.

La razon de por que son trenzado es para evitar interferencias de campos magneticos, conocido como diafonia.

- Se hay cables con blindaje para evitar interferencias externas

### Categorias

Cat 1       -> Dorbell
Cat 3       -> Telefono /10Mbps
Cat 5       -> 100Mb
Cat 6       -> Gb Ethernet, se aumentarion las specs y se le agrego al una cruz de plastico al centro.
Cat 6a/7    -> 10Gb
Cat 8       -> 10 Gb

### RJ-11
Conector utilizado para telfono, cat-3. Un conector de solo 4 hilos, pa

### RJ-45
Tiene 8 pines

Orientacion ->

1   -> Transmit +
2   -> Transmit -
3   ->  Recieve +
4   ->
5   ->
6   ->  Recieve -
7   ->
8   -> 

- Cable cruzado
    Conectar router con ruoutwr
    Conectar Switchs con switch
    Conectar pc con pc

- Auto-MFI-X (Auto mediun dependent interface crossover)
Casi todos los disposivios usan esta tecnologia, significa que si el dispositivo tiene esta tecnologia no tienes que precuparte por el cable 

## Coaxial
- El cable fisico se llama RG-6
- El conectar el F-Type Connector

Twinaxial Cable
En centros de datos, para tranmitir datos 10Gb o hasta 40 Gb


## Fibra Optica

### Fibra Mono-modo
Se utlizan materiales muy estrictos encuanto a calidad, para que el pulso de luz recorra el tubo lo mas recto posibles, haciendo que la atenuacion sea menor, perfecto para grandes distancias.

### Fibra Multimodo
Tiene una un poco menos de calidad que la anterior, el tubo es mas grueso, pero es mas economica y perfecta para distancias no tan prolongadas. La luz tiende a rebotar mas en el tubo.

### Comprativa

Laser Type  | Wavelength    | Fiber         | Dsitance
LX          | 1270 - 1610nm | Single Mode   | 70 k 
SX          | 770 - 860 nm  | Multi mode    | 1/2 - 1 km

### OPtical Netwotk Interface Card

- GBIC
- SFT
- SFP+
- QSFP
- QSFP+

### Tipos de conectores

- ST Connector
- SC Connector
- LC Connector
Comun en redes modernas, se conecta a SFT

- MTRJ Connector
- FC Connector

### Angled Physical Contact (APC)
Es el angulo en que tiene que estar cortada la fibra para poder hacer un buen contacto y permitir el paso de la luz de manera correcta

### Ultra Phisical Contact (UPC)


### Simplex Pair
Es una de las maneras en que se conectan 2 dispositivos, ejemplo un switc, se usan una fbra para ir de A -> B y otra para ir de A -> A

### Bidireccional

Funciona con un solo cable, por lo que para lograr la comunicaion usa 2 hondas de luz diferentes. Para eso se usa algo llamado:

- Wave Division Multiplexing (WDM) - Multiplexación por división de ondas


