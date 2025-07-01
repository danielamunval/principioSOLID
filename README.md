# principioSOLID

# Equipo 3 AsmaGeneration
 
Este repositorio contiene una explicación individual de cada uno de los cinco principios SOLID en la Programación Orientada a Objetos. Cada principio fue abordado por un integrante del grupo:
 
- **S – Single Responsibility Principle** → Tais
- **O – Open/Closed Principle** → Claudio
- **L – Liskov Substitution Principle** → Marcela
- **I – Interface Segregation Principle** → Rodrigo
- **D – Dependency Inversion Principle** → Daniela
 
Estos principios son fundamentales para el desarrollo de código limpio, mantenible y escalable.

S-Single Responsability Principle
Principio de Responsabilidad Única

Este principio dice que una clase debe tener una única razón para cambiar, es decir, debe tener una única responsabilidad o propósito.

O - Open/Closed Principle (OCP)
Principio de Abierto/Cerrado
Puedes extender el comportamiento de una clase sin modificar su código original (por ejemplo, usando herencia o interfaces).

L – Liskov Substitution Principle o Principio de Sustitución de Liskov.
“Subclases que encajan”

Si tienes una clase padre A y una hija B (subclase), puedes usar B donde sea y de todas maneras dará A, sin que falle.

🧩 I – Interface Segregation Principle (ISP)
Principio de Segregación de Interfaces
📜 Definición
El Principio de Segregación de Interfaces establece que:

"Los clientes no deben estar forzados a depender de interfaces que no utilizan."
– Robert C. Martin

En otras palabras, es preferible tener muchas interfaces específicas en lugar de una sola interfaz general con métodos innecesarios.

❌ Problema que resuelve
Cuando una interfaz tiene demasiados métodos, algunas clases que la implementan se ven obligadas a definir comportamientos que no les corresponden o que no necesitan. Esto acopla innecesariamente esas clases y puede causar errores si esos métodos se usan incorrectamente.

✅ Solución que propone ISP
Dividir las interfaces en partes más pequeñas y enfocadas, de forma que las clases solo implementen lo que realmente usan. Esto da mayor flexibilidad, cohesión y reduce el riesgo de errores.

🧪 Ejemplo sin ISP (violación del principio)
java
Copiar
Editar
public interface Ave {
    void volar();
    void nadar();
    void caminar();
}
java
Copiar
Editar
public class Pinguino implements Ave {
    public void volar() {
        // ❌ El pingüino no vuela. ¿Qué hacemos aquí?
        throw new UnsupportedOperationException();
    }

    public void nadar() {
        System.out.println("El pingüino nada bien");
    }

    public void caminar() {
        System.out.println("El pingüino camina torpemente");
    }
}
Este diseño obliga al pingüino a tener un método volar, aunque no puede volar. Estamos violando el ISP.

✅ Aplicando ISP (buen diseño)
java
Copiar
Editar
public interface IVolar {
    void volar();
}

public interface INadar {
    void nadar();
}

public interface ICaminar {
    void caminar();
}
java
Copiar
Editar
public class Pinguino implements INadar, ICaminar {
    public void nadar() {
        System.out.println("El pingüino nada bien");
    }

    public void caminar() {
        System.out.println("El pingüino camina torpemente");
    }
}
Ahora el pingüino solo implementa lo que realmente sabe hacer, y otras aves pueden implementar IVolar si corresponde.

🛠️ Beneficios del ISP
Mayor modularidad y reutilización.

Código más limpio, comprensible y cohesionado.

Evita la sobrecarga innecesaria de métodos en clases que no los necesitan.

Facilita los cambios sin romper otras partes del sistema.

📌 En resumen
El ISP promueve la especialización y claridad. Así como en la vida real no obligamos a un pez a saber volar, en el código no deberíamos forzar a una clase a implementar lo que no necesita. Dividir bien las interfaces es clave para un diseño limpio y mantenible.

"D" – Dependency Inversion Principle (DIP)
También llamado "Principio de Inversión de Dependencias", en español.

“Depender de ideas, no de cosas”
* Hace referencia a que las clases de alto nivel (que hacen la principal lógica) no deben depender directamente de las clases de bajo nivel (detalles). 

Ambas dependen de abstracciones (interfaces). Sin mebargo, no deberían depender de interfaces que no usa o las interfaces no deberían tener métodos que no usan.

💡 Ventaja: Facilita reemplazar detalles (como cambiar la base de datos) sin tocar la lógica principal.

Ejemplo código:
interface Motor {
    void encender();
}

class MotorGasolina implements Motor {
    public void encender() {
        System.out.println("Motor a gasolina encendido");
    }
}

class Auto {
    private Motor motor;

    public Auto(Motor motor) {
        this.motor = motor;
    }

    public void arrancar() {
        motor.encender();
    }
}