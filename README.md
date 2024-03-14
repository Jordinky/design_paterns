<h1>Patrones de diseño</h1>

<h2>Singleton</h2>

## proposito

<p><b>Singleton</b> es un patrón de diseño creacional que nos permite asegurarnos de que una clase tenga una única instancia, a la vez que proporciona un punto de acceso global a dicha instancia.</p>

<h3>Problema</h3>

<p>El patrón Singleton resuelve dos problemas al mismo tiempo, vulnerando el <i>Principio de responsabilidad.</i></p>

<h4>1. Garantizar que una clase tenga una única instancia.</h4>

<p>El motivo más habitual es controlar el acceso a algún recurso compartiodo, como una base de datos o un archivo.</p>

<p>Este comportamiento es imposible de implementar con un constructor normal, ya que una llamada al constructor siempre <b>debe</b>devolver un nuevo objecto por diseño.</p>

<h4>2. Proporcionar un punto de acceso global a dicha instancia</h4>

<p>Las variables globales aunque son muy utiles también son poco seguras, ya que cualquier código podria sobrescribir el contenido de esas variables y descomponer la aplicación.</p>

<p>Al igual que una variable global, el patrón Singleton nos permite acceder a un objecto desde cualquier parte del programa. No obstante, también evita que otro código sobreescriba esa instancia.</p>

<h3>Solución</h3>
<p>Todas las implementaciones del patrón Singleton tienen estos dos pasos en común:</p>
<ul>
    <li>Hacer privado el constructor por defecto para evitar que otros objetos utilicen el operador <i>new</i> con la clase Singleton.</li>
    <li>Crear un método de creación estático que actue como constructor,este método invoca al constructor privado para crear un objeto y lo guarda en un campo estático. Las Siguiente llamadas a este método devuelve en el objeto almacenado en caché.</li>
</ul>

## Estructura

<p>La clase <b>Singleton</b> debe ocultarse en el código cliente. La llamada al método <i>obtenerInstancia</i>debe ser la única manera de obtener el objeto de Singleton.</p>
</br>
<img src = "https://refactoring.guru/images/patterns/diagrams/singleton/structure-es-indexed.png">

## Pseudocódigo

<p>En este ejemplo, la clase de conexión de la base de datos actua como <b>Singleton.</b> Esta clase no tiene un constructor público, por lo que la única manera de obtener su objeto es invocando al método <i>obtenerInstancia.</i> Este método almacena en caché el primer objeto creado y lo devuelve en todas las llamadas siguientes.</p>


    // La clase Base de datos define el método `obtenerInstancia`
    // que permite a los clientes acceder a la misma instancia de
    // una conexión de la base de datos a través del programa.
    class Database is
        // El campo para almacenar la instancia singleton debe
        // declararse estático.
        private static field instance: Database

        // El constructor del singleton siempre debe ser privado
        // para evitar llamadas de construcción directas con el
        // operador `new`.
        private constructor Database() is
            // Algún código de inicialización, como la propia
            // conexión al servidor de una base de datos.
            // ...

        // El método estático que controla el acceso a la instancia
        // singleton.
        public static method getInstance() is
            if (Database.instance == null) then
                acquireThreadLock() and then
                    // Garantiza que la instancia aún no se ha
                    // inicializado por otro hilo mientras ésta ha
                    // estado esperando el desbloqueo.
                    if (Database.instance == null) then
                        Database.instance = new Database()
            return Database.instance

        // Por último, cualquier singleton debe definir cierta
        // lógica de negocio que pueda ejecutarse en su instancia.
        public method query(sql) is
            // Por ejemplo, todas las consultas a la base de datos
            // de una aplicación pasan por este método. Por lo
            // tanto, aquí puedes colocar lógica de regularización
            // (throttling) o de envío a la memoria caché.
            // ...

    //Clase para la aplicación
    class Application is
        method main() is
            Database foo = Database.getInstance()
            foo.query("SELECT ...")
            // ...
            Database bar = Database.getInstance()
            bar.query("SELECT ...")
            // La variable `bar` contendrá el mismo objeto que la
            // variable `foo`.

## Aplicabilidad

<p><b>Utiliza el patrón Singleton cuando una clase de tu programa tan solo deba tener una instancia disponible para los clientes; por ejemplo, el único objetode base de datos compartido por distintas partes del programa.</b></p>

<p>El patrón Singleton deshabilita el resto de las maneras de crear objetos de una clase, excepto el método especial de creación. Este método crea un nuevo objeto, o bien devuelve uno existente si ya ha sido creado.</p>

<p><b>Utiliza el patrón Singleton cuando necesites un control mas estricto de las variables globales.</b></p>

<p>Al contrario que las variables globales, el patrón Singleton garantia que haya una única instancia de una clase. A excepcion de la propia clase Singleton, nada puede sustituir la instancia en caché.</p>

## Cómo implementarlo

<ol>
    <li>
        <p>Añade un campo estático privado a la clase para almacenar la instancia Singleton.</p>
    </li>
    <li>
        <p>Declara un método de creación estático público para obtener la instancia Singleton</p>
    </li>
    <li>
        <p>Implementa una inicialización diferida dentro del método estático. Debe crear un nuevo objeto en su primera llamada y colocarlo dentro del campo estático. El método debera devolver siempre esa instancia en todas las llamadas siguientes.</p>
    </li>
    <li>
        <p>Declara el constructor de clase como privado. El método estático de la clase seguirá siendo capaz de invocar al constructor, pero no a los otros objetos.</p>
    </li>
    <li>
        <p>Repasa el código cliente y sustituye todas las llamadas directas al constructor de la instancia Singleton por llamadas a su método de creación estático.</p>
    </li>
</ol>

## Pros y contras

<div align-items="center">
    <ul>
        <li>Puedes tener la certeza de que una clase tiene una única instancia.</li>
        <li>Obtienes un punto de acceso global a dicha instancia.</li>
        <li>El objeto Singleton solo se inicializa cuando se requiere por primera vez.</li>
    </ul>
    <ul>
        <li>vulnera el <i>Principio de responsabilidad única. El patrón resuelve dos problemas al mismo tiempo.</i></li>
        <li>El patrón Singleton puede enmascarar un mal diseño, por ejemplo, cuando los componentes del programa saben demasiado los unos sobre los otros.</li>
        <li>El patrón requiere de un tratamiento especial en un entorno con múltiples hilos de ejecución, para que varios hilos no creen un objeto Singleton varias veces.</li>
        <li>Puede resultar complicado realizar la prueba unitaria del código cliente del Singleton porque muchos <i>frameworks</i> de prueba dependen de la herencia a la hora de crear objetos simulados (mock objects). Debido a que la clase Singleton es privada y en la mayoria de los lenguajes resulta imposible sobreescribir métodos estaticos.</li>
    </ul>
</div>

