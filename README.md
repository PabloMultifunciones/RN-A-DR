# RN-A-DR
Redes Neuronales - Adicional - Porque usar Discount Rewards
### Introduccion ###

Aunque las tasas de descuento son una parte integral de los problemas de decisión de Markov y el aprendizaje por refuerzo (RL), a menudo seleccionamos γ=0.9 o γ=0.99 sin pensarlo dos veces. Seguramente, cuando se nos pregunta, tenemos algunas intuiciones como 'las recompensas de hoy valen más que las recompensas de mañana' o 'compensar la incertidumbre'. Cuando se le presiona, ¿puede defender por qué se mantienen esas intuiciones? ¿Por qué eliges γ=0,8 en lugar de γ=0,9? ¿No está ya incorporada la incertidumbre en el valor esperado? Si no tiene una respuesta instantánea lista, este artículo puede arrojar algo de luz sobre el asunto.  

### Descuento en matemáticas ###

Desde una perspectiva estrictamente matemática, el propósito de una tasa de descuento es obvio, al menos para problemas de horizonte infinito. De la ecuación recursiva de Bellman aprendemos a resolver funciones de valor para una secuencia de estados:  

![1_WwN-sAkWsHTEh8ECNJE6KA](https://user-images.githubusercontent.com/95035101/200392463-f8449335-1520-41e6-a858-92570a27d5ec.png)  

Si esa secuencia es infinita, también lo es la serie de recompensas. Considere la siguiente secuencia de recompensas acumulativas G_t:  

G_t = R_t + R_t+1 + R_t+2 + … = 1 + 1 + 1 + … = ∞  

Como todos sabemos, sumar una serie de recompensas infinitas produce recompensas infinitas, lo que hace que el sistema de ecuaciones sea irresoluble. Afortunadamente, al sumar una tasa de descuento γ ∈ [0,1) se obtiene una serie geométrica convergente. Por ejemplo, si ponemos γ=0.8 obtenemos:  

G_t = γ⁰R_t + γ¹R_t+1 + γ²R_t+2 + … = 1 + 0,8 + 0,64 + … = 5  

Con este truco, podemos asignar valores a los estados y resolver el sistema de ecuaciones de Bellman. Por supuesto, en Aprendizaje por Refuerzo esa solución sería aproximada.  

Eso explica el caso infinito, pero ¿por qué molestarse en descontar para horizontes de tiempo finitos? Podría argumentar que compensamos la incertidumbre, pero ¿eso no se refleja ya en el valor esperado (multiplicando las recompensas futuras por sus probabilidades)? La perspectiva matemática no resuelve esto, necesitamos sumergirnos un poco en la psique humana.  

### ¿Qué define mejor la psique humana que el dinero? ###

Un componente importante de la inversión es la existencia de una tasa libre de riesgo. Este es el rendimiento que se puede obtener sin ninguna incertidumbre o riesgo de impago, y sirve como referencia para todos los demás rendimientos. Las letras del Tesoro de EE. UU. se utilizan a menudo como un proxy. Ponga un dólar en una letra del Tesoro de EE. UU. al 2% y recibirá $ 1.02 garantizados dentro de un año. En consecuencia, preferimos $1 hoy a $1 el próximo año. Sin esfuerzo, podemos aumentar nuestra riqueza en un 2 % anual y, como tal, descontaremos las recompensas futuras en un 2 % para reflejar el valor del tiempo.  

Se vuelve más interesante cuando se consideran instrumentos de riesgo como las acciones. Supongamos que una acción aumentará un 0% o un 4% dentro de un año, ambas con una probabilidad de 0,5. El pago esperado es del 2%. Sin embargo, la posibilidad de terminar con las manos vacías es sustancial. El inversionista típico preferirá el bono del 2% libre de riesgo en este caso, a pesar de que los pagos esperados sean equivalentes. De ello se deduce que los rendimientos de las acciones se descuentan a una tasa mayor que los rendimientos de los bonos.  

Este fenómeno se conoce como aversión al riesgo. Las personas esperan ser compensadas por la incertidumbre, de lo contrario elegirían la alternativa más segura. A mayor incertidumbre, mayor tasa de descuento. Tal vez seleccionaríamos la acción si rindiera un 10 % en lugar de un 4 % (aumentando el pago esperado al 5 %). La inversión debe proporcionar una cierta prima de riesgo además de compensar el valor del tiempo.  

Todavía hay muchos temas que quedan intactos, como la tendencia a utilizar el descuento exponencial (similar a RL), los costos de oportunidad o de arrepentimiento (solo puede invertir su dinero una vez), el comportamiento de búsqueda de riesgos (las loterías tienen poco sentido desde la perspectiva de un inversor racional ), y casos límite extrañamente inconsistentes. Por ahora, fijémonos en la lógica de que las tasas de descuento reflejan tanto el valor del tiempo como una prima de riesgo.  
### Rebajando en la vida ⏳ ###

El comportamiento de descuento no se limita a los dólares. En la vida diaria, equilibramos constantemente la gratificación a corto plazo y las consecuencias a largo plazo, compensamos la certeza y la incertidumbre. Acuéstate tarde y mañana estarás cansado. Coma abundantemente durante el invierno y necesitará recortar grasa para lucir un cuerpo de playa en verano. Estudie día y noche ahora y, con suerte, coseche los frutos más adelante.  

![1_Jlo_l2_0yx_EoQdgbdPihA](https://user-images.githubusercontent.com/95035101/200392790-8eeca46d-733f-4902-a597-760c6ee0553a.png)

Se han realizado innumerables estudios psicológicos sobre el tema, lo que sugiere que los humanos tienden a realizar algo cercano al descuento hiperbólico en su toma de decisiones. Las personas que lucen un tatuaje de Carpe Diem en el brazo probablemente descuentan las recompensas futuras con bastante fuerza, otros podrían darles más peso. A pesar de las discrepancias entre los individuos, todos descontamos hasta cierto punto.   

Una razón muy natural de este fenómeno es la tasa de riesgo: la probabilidad de que no estemos vivos mañana para cosechar recompensas. Aunque el riesgo de mortalidad aguda no es tan alto como el de nuestros antepasados ​​cazadores-recolectores, el impulso biológico de preferir las recompensas ahora permanece muy intacto. El peligro no necesita ser tan morboso como la muerte. Una carrera atlética puede verse truncada por una lesión en la rodilla, y ese viaje de mochilero por Asia podría no ser posible dentro de cinco años. Incluso en el nivel más banal, preferimos tener una galleta ahora que una galleta la próxima semana.  

Como humanos, simplemente tenemos una predisposición programada para valorar las recompensas ahora más que las del futuro (lejano), sean sensatas o no.   

### Descuento en Aprendizaje por Refuerzo 📖 ###

Ahora tenemos algunas ideas sobre la lógica humana para el descuento, pero ¿ese razonamiento es válido para los problemas de aprendizaje por refuerzo? A pesar de algunas conexiones sueltas entre las redes neuronales y el cerebro humano, normalmente los algoritmos de RL no están diseñados para imitar el comportamiento humano. La tasa de riesgo también es una razón susceptible, ya que podemos modelar los peligros en el medio ambiente. Por ejemplo, un juego de caminar por un acantilado termina cuando el agente se sube al acantilado; no necesitamos descontar más para reflejar ataques cardíacos o dedos golpeados. Un contraargumento sería que tales peligros podrían ocurrir en entornos para los cuales la póliza no está capacitada, utilizando la tasa de descuento como una especie de dispositivo de solidez.  

Para muchos problemas de RL, es perfectamente aceptable no descontar las recompensas futuras. Aun así, existen razones válidas para descontar en RL, incluso para horizontes finitos. Uno de ellos es el impacto real que las decisiones tienen sobre el desempeño a largo plazo. En última instancia, depende del modelador qué tasa de descuento refleje mejor las recompensas acumuladas dentro del contexto del problema.

Supongamos que tengo que elegir entre una cena ligera o pesada esta noche. La decisión podría afectar mi sesión de gimnasio después, pero probablemente no tenga ningún impacto en mi ascenso el próximo año. Aquí, vemos una razón clara para descartar recompensas futuras: algunas consecuencias difícilmente pueden vincularse a la acción de hoy. El propósito de RL es incorporar los efectos posteriores de las decisiones actuales, pero las recompensas futuras pueden no estar correlacionadas. En general, cuanto más estocástico sea el entorno, menos impacto duradero tendrán nuestras acciones en el rendimiento.

Una respuesta en StackExchange formaliza esa noción de una manera interesante, expresando un parámetro τ que refleja el intervalo de tiempo que nos interesa:

![Uploading 1_1LuXuLAZapiULzAQn2U71Q.png…]()

Como antes, suponga que la recompensa es siempre 1. Con γ=0.8, la serie converge a 5. Efectivamente, las recompensas más allá de cinco pasos de tiempo hacia adelante (observe e^(-1/5)≈0.8) tienen poco impacto. De manera similar, una serie con γ=0.9 converge a 10 y con γ=0.99 converge a 100. Eso sí: una recompensa repentina de +100 después de t+τ aún impacta sustancialmente la recompensa descontada, pero como regla general, el enfoque hace que sentido. Si cree que las recompensas dentro de cinco pasos de tiempo tienen poco que ver con las decisiones que se toman ahora, γ=0.8 podría ser una tasa de descuento adecuada.  

Con suerte, este artículo proporcionó algo de claridad sobre el tema de las tasas de descuento, pero solo rascó la superficie. Se ha sugerido que todo el concepto es defectuoso para las aproximaciones de funciones (que normalmente usamos en RL), y que las recompensas promedio son una mejor métrica que las recompensas con descuento. Otro enfoque interesante es abandonar la noción de una tasa de descuento fija y, en su lugar, trabajar con tasas dependientes del estado. Tenga en cuenta las preferencias humanas y se abre un mundo completamente nuevo.

