# Tour war

---

**Laura Mambrilla Moreno**  
lauramambrilla@gmail.com

---

## Índice

- [Definición del prototipo](#definición-del-prototipo)  
- [Proceso de creación de las nuevas mecánicas](#proceso-de-creación-de-las-nuevas-mecánicas)  
- [Memoria de iteraciones](#memoria-de-iteraciones)


---

## Definición del prototipo

*"Tour war”* es un videojuego third person de acción aventura. El jugador se pondrá en la piel de la asesina a sueldo Eve, quien se ha encontrado envuelta en una guerra de bandas: la banda Anetit y la banda Bapef. Por motivos económicos, se encuentra en el bando de Anetit, el Team A. Su misión es colaborar con los miembros de Anetit para acabar con todos y cada uno de los integrantes de Bapef, el Team B. Primero se enfrentará con ellos en China y, tras un nuevo reclutamiento de Bapef, se enfrentarán en Egipto. Solo se puede ir a Egipto si has ganado la guerra en China.

Eve va equipada con una pistola que, con *sphere trace*, quita porcentaje de vida al resto de personajes, haciendo click izquierdo. Debe tener cuidado de no disparar a los de su equipo, pues también se pueden dañar entre integrantes del mismo grupo al recibir un balazo, como en la vida real. Para apuntar, el jugador podrá hacer click derecho: aparecerá el dibujo de una mirilla en el medio de la pantalla, y será donde irán los disparos.

Los soldados con y contra los que peleará Eve son personajes de inteligencia artificial, diseñados para acabar con los enemigos. Hay 3 tipos de soldados: Alex, Brute y Ninja; todos ellos son blueprints que heredan de la clase padre `BP_AI`:

- **BP_AI:** el padre. Es la clase padre de las 3 siguientes. Cada hijo de ella buscará, perseguirá y dañará al enemigo, siempre asegurándose primero de que no pertenezcan a la misma banda. A cada personaje se le asignará aleatoriamente a qué banda pertenecerá. En la parte superior izquierda de la pantalla se verá el recuento de los integrantes vivos de cada banda.

- **BP_AI_Alex:** el cazador. Alex porta una escopeta con la que destruirá a los enemigos con cada disparo. Se ha implementado con *sphere traces* para producir daño al enemigo. Produce el mayor daño por iteración.

- **BP_AI_Brute:** el bruto. Brute, con su super hacha en mano, machacará con devastadores golpes a sus enemigos. De los del combate cuerpo a cuerpo, es el más dañino.

- **BP_AI_Ninja:** el sigiloso. Ninja es el más rápido de los tres. Cuando se acerca al enemigo le daña a base de puñetazos, hasta la muerte. Un experto en combate cuerpo a cuerpo.

Los distintos menús son: el principal (primera pantalla), el de pausa (al pulsar la tecla P), el de ganador y el de game over.

---

## Proceso de creación de las nuevas mecánicas

Se ha implementado un sistema de equipos, en el que habrá dos grupos diferenciables: “Team A” y “Team B”. En esta guerra hay dos tipos de ataques: ataques de largo y de corto alcance. Los ataques de largo alcance los ejecutan Eve y Alex, disparando *sphere traces*. Los ataques de cuerpo a cuerpo los realizan Ninja y Brute con un *box collider* a sus pies: cuando algo entra en contacto con este *box collider* (Box), primero se comprueba si está vivo o muerto y luego si es o no enemigo y, si es enemigo, le ejerce el daño correspondiente. Distintos tipos de ataques dentro de un sistema de equipos hace el juego más interesante, ya que el jugador deberá planear una mínima estrategia.

Los equipos son asignados al azar. El jugador podrá ver quién pertenece a cada equipo, ya que los personajes de inteligencia artificial llevan una barra de vida (`HealthBarWidget`), indicando su porcentaje, y un texto (`TeamWidget`): si son de Anetit, el texto será rojo y se leerá “Team A”; por otro lado, si son de Bapef, el texto será azul y se leerá “Team B”. Esto les hace más identificativos a simple vista a los integrantes de cada equipo.

El jugador tiene la ayuda de un minimapa, al pulsar la tecla M, con el que podrá observar una parte del escenario del juego, lo que le concede cierta ventaja. Aparecerá en la parte superior derecha de la pantalla. Eve se verá como una flecha negra, los miembros de “Team A” serán círculos rojos y los miembros de “Team B” serán cuadrados azules (`IAIndicatorSprite`). Cuando ya no necesite el minimapa, pulsará otra vez a la tecla M y se deshabilitará.

Se dispone un cronómetro que nos muestra cuánto tiempo estamos tardando en completar la misión. Esto hace que el jugador tenga un reto por mejorar su propio récord. Se encuentra implementado dentro del widget `W_HUD`.

---

## Memoria de iteraciones

Los playtests del videojuego *“Tour war”* han sido realizados por un público de un rango de edad 18-25, femenino y masculino, pues sería el público objetivo real.

- **Primera iteración:** Se probó al personaje Eve: esqueleto, animaciones, disparos y efectos especiales.

- **Segunda iteración:** Se centró en la inteligencia artificial, realizando solamente el blueprint padre `BP_AI`: movimiento, detección de personajes y disparos. En el playtest se analizaron las características de `BP_AI` y Eve. Como punto de mejora se decidió crear clases hijas de `BP_AI` para contar con distintos tipos de personajes, y que cada uno aportase algo especial al juego.

- **Tercera iteración:** Se implementaron `BP_AI_Alex`, `BP_AI_Ninja` y `BP_AI_Brute`. Se analizó la sintonía de los componentes y se empezó a plantear el sistema de equipos.

- **Cuarta iteración:** Desarrollo del sistema de equipos y la UI que ayudase al jugador: barras de vida, nombres de los equipos y número de miembros vivos de cada equipo. Este punto fue un éxito en el playtest, pues el jugador ya podía luchar por cumplir su objetivo.

- **Quinta iteración:** Creación de los dos niveles: China y Egipto. Se establecieron las posiciones iniciales de los personajes.

- **Última iteración:** Desarrollo de menús, incorporación de música, implementación del cronómetro y refinamiento de aspectos de mejora. El último playtest fue exitoso, destacando el diseño del nivel, la tensión y la UI para una excelente experiencia de usuario.

---
