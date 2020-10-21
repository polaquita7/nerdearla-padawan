# Creá un asistente virtual nivel Padawan - Nerdearla 2020
Tutorial introductorio a Watson Assistant. 

## Prerequisitos
Tener una cuenta en IBM Cloud. En caso de no tenerla aún, podés registrarte en https://ibm.biz/Bdqwk2

## Tiempo estimado
De 10 a 40 minutos; dependiendo del lado de la fuerza que elijas.

## ¿Qué es Watson Assistant?
Watson Assistant es un producto de inteligencia artificial de IBM que permite crear, entrenar e implementar interacciones conversacionales en cualquier aplicación, dispositivo o canal. Watson Assistant sabe cuándo buscar una respuesta de una base de conocimiento, cuándo pedir aclaraciones y cuándo transferir usuarios a un agente humano. 
Se puede implementar en cualquier entorno en la nube o local, lo que significa que la IA más inteligente finalmente está disponible en cualquier lugar donde la necesite.
Un chatbot como Watson Assistant con una implementación rápida y entrenamiento progresivo puede ayudarle a elevar la experiencia de sus usuarios y de su equipo.

## Parte 1: Watson Assistant
1. Ingresá a tu cuenta de [IBM Cloud](https://cloud.ibm.com/login)
1. En el catálogo, buscá _Assistant_ y creá una instancia. Seleccioná el plan _Lite_, poné el nombre que más te guste para el servicio y dale click a _Create_
![Assistant Catalog](/img/6Assistant.png)
1. Ingresá a la interfaz de Watson Assistant haciendo click en el botón _Launch Watson Assistant_
![Launch Watson Assistant](/img/7AssistantPage.png)
1. Ingresá al asistente que se crea por defecto (_My first assistant_)  y hacé click en el icono de _Skills_  (segundo del menú que está a la izquierda)
![Skills](/img/9MyFirstAssistant.png)
![Create skill](/img/10Skills.png)

A partir de acá tenemos dos opciones:
* Podés importar este skill que te ofrecemos y tener tu asistente armado en un solo paso 
o 
* Armar tu asistente manualmente con estas instrucciones

### ![Vader](/img/vader.jpg) Importá el skill ya terminado
Importá el archivo [skill-nerdear.la-padawan.json](/skill-nerdear.la-padawan.json)
![Importar skill](/img/11ImportSkill.gif)

### ![Leia](/img/leia.jpg)  Armá asistente de manera manual
1. Creá un nuevo skill en español.
![Crear skill](/img/12CreateSkill.gif)
2. Una vez creado, vas a ver la pantalla de _Intents_ (intenciones) 
![Intents](/img/13Intents.png)
<br>Las Intenciones son las acciones que el usuario del asistente desea realizar, por ejemplo en nuestro caso, levantar una máquina virtual. Al reconocer la intención expresada en una entrada de usuario, el servicio Watson Assistant puede elegir el flujo de diálogo correcto para responder a la misma.<br>Crea una nueva intención llamada `Crear`.

![Intents](/img/14IntentName.png)

Cargale ejemplos de cómo un usuario pediría esa información.
![Intents](/img/15IntentExamples.gif) <br>

3. Ingresá a la opción _Entities_ (entidades) <br> 
Las entidades representan a los sustantivos: el objeto o el contexto de una acción. En nuestro caso, el recurso que vamos a crear, la máquina virtual. <br> 
Por eso, vamos a crear una entidad llamada `Recurso` y le vamos a cargar la lista de recursos que podríamos dar de alta. Podés inventar las que quieras, pero si no se te ocurren, siempre podés volver a la opción de Importar el skill donde ya están todas cargadas.

![Entities](/img/16Entities.png) <br>

4. Ingresá a la opción _Dialog_ (Diálogo) Por defecto, ya vienen los nodos "Bienvenido" y "en otras cosas".
![Default dialog](/img/17DialogStart.png) <br>

Vamos a crear un nuevo nodo al que voy a llamar `crear_recurso`. <br>
   a) Como condición del nodo, agregá `#Crear` (o el nombre que hayas usado para tu intent)<br>
    ![Create node](/img/18CreateNode.gif)<br>


   b) Desde la opción _Customize_ habilitá los slots para ese nodo. Esto permite que el assistant pueda contestar con la respuesta adecuada si tiene toda la información necesaria o pedir que se defina un tipo de recurso si el usuario no lo hizo.
    
   c) Esto habilita una nueva sección en donde vas a tener que configurar que el assistant chequee por `@recurso`. Si el usuario indicó un recurso, la misma se guarda en la variable de entorno `$recurso`. Si no, el assistant va a preguntar por ella con el texto que definamos en _If not present, then ask_
   <br>
![Create node](/img/19SlotConfig.gif)
    <br>

5. Ahora vamos al menú _Options > Webhooks_. En URL vas a tener que agregar la URL pública de tu función, que guardaste en el punto 6 de la Parte 1. Al final de la URL agregá `.json`
![Create node](/img/20Webhooks.png) <br>

6. Volvé a tu nodo `Pedir_Info_Clima` y creá un child node que se llame `API_call` y en _Customize_, habilitá la opción "Webhook". Esto va a habilitar otra sección nueva en el nodo para incluir la información que le vamos a mandar a la función como parámetro. <br>
*Key* `city` *Value* `El clima en $ciudad está $webhook_result_1.clima`

![Create node](/img/21Webhookconfig.gif) <p>

Una vez que están configurados los parámetros, en la respuesta, incluí el texto que quieras responder. Por ejemplo:
* If assistant recognizes * `$webhook_result_1` * Respond with * `El clima en $ciudad está $webhook_result_1.clima`

7. Volvé al nodo `Pedir_Info_Clima` y asegurate de setear para que saltee la interacción con el usuario.
![Create node](/img/22JumpNode.png) 
<br>


## Prueba de Habilidad:
Te desafíamos a subir tu asistente a la nube de IBM y compartirlo en redes sociales con el hashtag #nerdearla2020
Si necesitás una ayudita, podés seguir este tutorial https://github.com/watson-developer-cloud/assistant-simple

## Prueba de Coraje:
¿Y si conectamos una API? Podés aprender a hacerlo acá https://developer.ibm.com/es/technologies/artificial-intelligence/tutorials/cloud-functions/

## Material de Referencia:
Iniciación a Watson Assistant: https://cloud.ibm.com/docs/services/assistant?topic=assistant-getting-started&locale=es

## Presentaron en Nerdear.la 2020:
Antonella Ovando - ovandoan@ar.ibm.com
Cecilia Bel - belcecilia@ar.ibm.com



