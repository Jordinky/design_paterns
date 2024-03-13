# Patrones de diseño

<h1>Singleton</h1>

## proposito

<p><b>Singleton</b> es un patrón de diseño creacional que nos permite asegurarnos de que una clase tenga una única instancia, a la vez que proporciona un punto de acceso global a dicha instancia.</p>

<h3>Problema</h3>

<p>El patrón Singleton resuelve dos problemas al mismo tiempo, vulnerando el <i>Principio de responsabilidad.</i></p>

<h4>1. Garantizar que una clase tenga una única instancia.</h4>

<p>El motivo más habitual es controlar el acceso a algún recurso compartiodo, como una base de datos o un archivo.</p>

<p>Este comportamiento es imposible de implementar con un constructor normal, ya que una llamada al constructor siempre <b>debe</b>devolver un nuevo objecto por diseño.</p>

<h4>Proporcionar un punto de acceso global a dicha instancia</h4>

<p>Las variables globales aunque son muy utiles también son poco seguras, ya que cualquier código podria sobrescribir el contenido de esas variables y descomponer la aplicación.</p>

<p>Al igual que una variable global, el patrón Singleton nos permite acceder a un objecto desde cualquier parte del programa. No obstante, también evita que otro código sobreescriba esa instancia.</p>

<h3>Solución</h3>
<p>Todas las implementaciones del patrón Singleton tienen estos dos pasos en común:</p>
<ul>
    <li>Hacer privado el constructor por defecto para evitar que otros objetos utilicen el operador <i>new</i> con la clase Singleton.</li>
    <li>Crear un método de creación estático que actue como constructor,este método invoca al constructor privado para crear un objeto y lo guarda en un campo estático. Las Siguiente llamadas a este método devuelve en el objeto almacenado en caché.</li>
</ul>

## motivacion

## estructura

## ejemplo de codigo

