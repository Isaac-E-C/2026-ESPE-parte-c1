Eres un experto en construir programas de software, necesito que en base a estas instrucciones: "1.          Realice un fork del repositorio https://github.com/GRISE-UPM/2026-ESPE-parte-c1

2.          Clone el repositorio forkeado localmente.

3.          Añada un fichero README.md con su nombre y apellidos.

4.          Realice un commit. El mensaje debe ser significativo.

5.          Implemente el código indicado en la especificación adjunta.

·      Para ello, puede utilizar el LLM indicado por el profesor.

Utilice el interfaz web, ya que deberá aportar una copia de la conversación que

ha mantenido con el LLM.

·      Si desea hacer algún comentario, realícelo en el espacio siguiente:

 

 

 

 

6.          Añada al directorio del proyecto un fichero denominado conv_programacion.<ext> con la conversación mantenida

con el LLM. Asegúrese de que pone este fichero bajo el control de git. Realice

un commit. El mensaje debe ser significativo.

7.          Confeccione las pruebas de unidad usando jUnit.

·      Para ello, debe utilizar el LLM indicado por el profesor.

Utilice el interfaz web, ya que deberá aportar una copia de la conversación que

ha mantenido con el LLM.

·      Si desea hacer algún comentario, realícelo en el espacio siguiente:

 

 

 

 

8.          Añada al directorio del proyecto un fichero denominado conv_prueba.<ext> con la conversación mantenida

con el LLM. Asegúrese de que pone este fichero bajo el control de git.

Realice un commit. El mensaje debe ser significativo.

9.          Realice un push del proyecto al repositorio forkeado.

10.       Realice un pull request al repositorio original. Incluya su

nombre y apellidos en el comentario del pull request. " Y el pdf adjunto, haz una guía completa y detallada para realizar correctamente el programa y la comunicación con github, si tienes preguntas hazmelas.

¡Hola! Como experto en ingeniería de software, te guiaré paso a paso para que completes esta tarea con éxito, cumpliendo tanto con los requisitos técnicos de la clase File como con el flujo de trabajo en GitHub.

A continuación, presento la guía detallada dividida en fases.

Fase 1: Configuración de GitHub y Entorno Local
Fork y Clonación:

Ve a https://github.com/GRISE-UPM/2026-ESPE-parte-c1.

Haz clic en el botón Fork (arriba a la derecha) para copiarlo a tu cuenta.

En tu terminal local, ejecuta: git clone https://github.com/TU_USUARIO/2026-ESPE-parte-c1.git

Identificación:

Crea un archivo README.md en la raíz.

Escribe tu Nombre y Apellidos.

Commit: git add README.md y git commit -m "Add README with student identification"

Fase 2: Implementación de la Clase File
Basándome en la especificación, aquí tienes la implementación que debes seguir.

Estructura de la Clase

Tipo de archivo: Debe ser un enum o constante (PROPERTY o IMAGE).


Atributo content: Debe ser un ArrayList<Character> inicializado vacío.

Métodos a implementar:
1. addProperty(char[] newcontent)
Lógica:

Si newcontent es null, lanza InvalidContentException.

Si el tipo es IMAGE, lanza WrongFileTypeException.

Si es válido, recorre el array y añade cada char al ArrayList.

2. getCRC32()
Lógica:

Si content está vacío, retorna 0L.

Si no, convierte el ArrayList<Character> a un byte[]. Para ello, toma solo el byte menos significativo de cada carácter.

Llama a FileUtils.calculateCRC32(byteArray) y devuelve el resultado.

Instrucción Git: Una vez implementado, guarda esta conversación en un archivo conv_programacion.pdf (o .txt), añádelo a Git y haz un commit: git commit -m "Implement File class and add LLM conversation log".

Fase 3: Pruebas de Unidad con JUnit
Para cumplir con el punto 7 de tus instrucciones, debes crear una clase de prueba (ej. FileTest.java). Deberías probar, al menos:

Excepciones: Verificar que addProperty lanza InvalidContentException con nulos y WrongFileTypeException si el archivo es de tipo IMAGE.

Cálculo CRC32:

Verificar que un archivo nuevo (vacío) devuelve 0.

Verificar que un archivo con contenido devuelve un valor coherente al llamar a FileUtils.

Integridad de datos: Que addProperty realmente concatena el contenido al ArrayList.

Instrucción Git: Guarda la conversación de la fase de pruebas como conv_prueba.pdf, añádela y haz commit: git commit -m "Add unit tests and testing conversation log".

Fase 4: Entrega Final
Push: Sube tus cambios a tu repositorio en GitHub: git push origin main

Pull Request (PR):

En GitHub, ve a tu repositorio y haz clic en "New Pull Request".

Asegúrate de que el "base repository" sea el de GRISE-UPM.

Importante: En el comentario del PR, escribe de nuevo tu Nombre y Apellidos [punto 10].

Preguntas para Clarificar
Para ayudarte mejor, ¿podrías confirmarme lo siguiente?

¿Ya tienes las excepciones (InvalidContentException, etc.) creadas en el proyecto base o debo darte el código para definirlas?

¿Tienes acceso a la clase FileUtils o necesitas que simulemos su comportamiento para las pruebas?

¿Te gustaría que te genere el código Java completo de la clase File ahora mismo basándome en estas reglas?

Necesito que la guía incluya los códigos de cada archivo

Entendido. Aquí tienes la guía técnica completa con el código fuente necesario para cumplir con la especificación.

Estructura de Clases y Lógica de Negocio
El sistema se basa en una clase File que gestiona recursos de software. El contenido se almacena internamente en un ArrayList<Character> para manejar tanto texto (UTF-16) como datos binarios de imágenes (UTF-8, usando solo el byte menos significativo).

1. Implementación de la Clase File
Este código sigue estrictamente las reglas de instanciación y gestión de tipos definidos.

Java
import java.util.ArrayList;

public class File {
    private FileType type;
    private ArrayList<Character> content;

    public File(FileType type) {
        this.type = type;
        // El contenido debe estar vacío, pero no ser null [cite: 14]
        this.content = new ArrayList<>();
    }

    /**
     * Añade un par clave=valor al contenido[cite: 17].
     */
    public void addProperty(char[] newcontent) throws InvalidContentException, WrongFileTypeException {
        // Si newcontent es null, se lanza InvalidContentException [cite: 19]
        if (newcontent == null) {
            throw new InvalidContentException();
        }

        // Si el tipo es IMAGE, se lanza WrongFileTypeException [cite: 20]
        if (this.type == FileType.IMAGE) {
            throw new WrongFileTypeException();
        }

        // newcontent se añade al content existente [cite: 18]
        for (char c : newcontent) {
            content.add(c);
        }
    }

    /**
     * Calcula el CRC32 del contenido[cite: 22].
     */
    public long getCRC32() {
        // Si el contenido está vacío, devuelve 0 [cite: 26]
        if (content.isEmpty()) {
            return 0L;
        }

        // El contenido debe transformarse en un byte[] antes de calcular el CRC32 [cite: 25]
        byte[] byteArray = new byte[content.size()];
        for (int i = 0; i < content.size(); i++) {
            // Se usa solo el byte menos significativo (intervalo [0, 255]) [cite: 11]
            byteArray[i] = (byte) (content.get(i) & 0xFF);
        }

        // Se utiliza el método proporcionado por FileUtils [cite: 23]
        return FileUtils.calculateCRC32(byteArray);
    }
}
2. Definiciones de Apoyo (Enums y Excepciones)
Para que el código anterior compile, necesitas definir los tipos y las excepciones mencionadas en la especificación.

Java
// Tipos de archivo permitidos [cite: 5]
enum FileType {
    PROPERTY, IMAGE
}

// Excepciones requeridas [cite: 19, 20]
class InvalidContentException extends Exception {}
class WrongFileTypeException extends Exception {}

// Clase de utilidad externa (Simulada según especificación) [cite: 23]
class FileUtils {
    public static long calculateCRC32(byte[] data) {
        // Implementación interna de la librería
        return 0L; // Valor de ejemplo
    }
}
3. Pruebas de Unidad (JUnit 5)
Siguiendo el paso 7 de tus instrucciones, aquí tienes las pruebas esenciales para validar el comportamiento:

Java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class FileTest {

    @Test
    public void testAddPropertyToImageThrowsException() {
        File file = new File(FileType.IMAGE);
        char[] data = "DATE=2025".toCharArray();
        assertThrows(WrongFileTypeException.class, () -> file.addProperty(data));
    }

    @Test
    public void testAddNullPropertyThrowsException() {
        File file = new File(FileType.PROPERTY);
        assertThrows(InvalidContentException.class, () -> file.addProperty(null));
    }

    @Test
    public void testEmptyFileReturnsZeroCRC() {
        File file = new File(FileType.PROPERTY);
        assertEquals(0L, file.getCRC32(), "Un archivo vacío debe devolver CRC 0");
    }
}
Próximos Pasos en GitHub
Ahora que tienes el código, sigue este orden para cumplir con los puntos 6 y 8 de tu guía:

Crea conv_programacion.md: Copia el texto de nuestra conversación sobre la implementación de la clase File y súbelo.

Crea conv_prueba.md: Copia la parte de la conversación donde definimos las pruebas JUnit.

Commits finales: Asegúrate de que cada archivo esté bajo control de versiones antes de hacer el push final y el Pull Request.

¿Te gustaría que redacte los mensajes de commit significativos para cada uno de estos pasos?

te envio las estructuras de cada file:package es.upm.grise.profundizacion.file;



import java.util.List;



public class File {



    private FileType type;

    private List<Character> content;



    /*

     * Constructor

     */

    public File() {

       

    }



    /*

     * Method to code / test

     */

    public void addProperty(char[] content) {



    }



    /*

     * Method to code / test

     */

    public long getCRC32() {

       

        return 0L;

       

    }

   

   

    /*

     * Setters/getters

     */

    public void setType(FileType type) {

       

        this.type = type;

       

    }

   

    public List<Character> getContent() {

       

        return content;

       

    }

   

}

package es.upm.grise.profundizacion.file;



public enum FileType {



    PROPERTY, IMAGE

   

}package es.upm.grise.profundizacion.file;



public class FileUtils {

   

    // Please notice the difference between the class diagram and this implementation

    // The reason is to facilitate unit testing

   

    long CRC32;

   

    void setCRC(long CRC32) {

       

        this.CRC32 = CRC32;

       

    }

   

    long calculateCRC32(byte[] bytes) {

       

        return this.CRC32;

       

    }



}package es.upm.grise.profundizacion.file;



import org.junit.jupiter.api.Test;



public class FileTest {

   

    @Test

    public void smokeTest() {}



}

// Source code is decompiled from a .class file using FernFlower decompiler (from Intellij IDEA).

package es.upm.grise.profundizacion.file;



import java.util.List;



public class File {

   private FileType type;

   private List<Character> content;



   public File() {

   }



   public void addProperty(char[] content) {

   }



   public long getCRC32() {

      return 0L;

   }



   public void setType(FileType type) {

      this.type = type;

   }



   public List<Character> getContent() {

      return this.content;

   }

}

// Source code is decompiled from a .class file using FernFlower decompiler (from Intellij IDEA).

package es.upm.grise.profundizacion.file;



public enum FileType {

   PROPERTY,

   IMAGE;



   private FileType() {

   }

}

// Source code is decompiled from a .class file using FernFlower decompiler (from Intellij IDEA).

package es.upm.grise.profundizacion.file;



public class FileUtils {

   long CRC32;



   public FileUtils() {

   }



   void setCRC(long CRC32) {

      this.CRC32 = CRC32;

   }



   long calculateCRC32(byte[] bytes) {

      return this.CRC32;

   }

}

// Source code is decompiled from a .class file using FernFlower decompiler (from Intellij IDEA).

package es.upm.grise.profundizacion.file;



import org.junit.jupiter.api.Test;



public class FileTest {

   public FileTest() {

   }



   @Test

   public void smokeTest() {

   }

}

Y toma en cuenta el archivo adjunto en el chat para su implementación, y enviame nuevamente la guía después de el README.md

Perfecto. He adaptado la implementación a las estructuras exactas de los archivos que has proporcionado y a las reglas de la especificación técnica. Aquí tienes la guía completa, empezando desde la implementación del código (Punto 5 de tus instrucciones).

1. Implementación del Código (Punto 5)
Debes modificar los archivos existentes en tu repositorio local con el siguiente código.

File.java
Este archivo gestiona la lógica principal. He incluido la inicialización obligatoria del ArrayList y las validaciones de tipo y contenido.

Java
package es.upm.grise.profundizacion.file;

import java.util.ArrayList;
import java.util.List;

public class File {

    private FileType type;
    private List<Character> content;
    // Necesitamos una referencia a FileUtils para calcular el CRC32
    private FileUtils fileUtils = new FileUtils();

    /*
     * Constructor: El content debe estar vacío, pero no ser null [cite: 14]
     */
    public File() {
        this.content = new ArrayList<>(); [cite: 8, 14]
    }

    /*
     * Añade un par clave=valor al content [cite: 16, 17]
     */
    public void addProperty(char[] newContent) throws InvalidContentException, WrongFileTypeException {
        // Si newcontent es null, se lanza InvalidContentException [cite: 19]
        if (newContent == null) {
            throw new InvalidContentException();
        }

        // Si el type del file es IMAGE, se lanza WrongFileTypeException [cite: 20]
        if (this.type == FileType.IMAGE) {
            throw new WrongFileTypeException();
        }

        // newcontent se añade al content existente [cite: 18]
        for (char c : newContent) {
            this.content.add(c);
        }
    }

    /*
     * Calcula el CRC32 del content [cite: 21, 22]
     */
    public long getCRC32() {
        // Si content está vacío, devuelve 0 [cite: 26]
        if (content.isEmpty()) {
            return 0L;
        }

        // Transformar content en un byte[] [cite: 25]
        byte[] byteArray = new byte[content.size()];
        for (int i = 0; i < content.size(); i++) {
            // Se usa solo el byte menos significativo [cite: 11]
            byteArray[i] = (byte) (content.get(i) & 0xFF);
        }

        // Se devuelve el valor calculado por FileUtils [cite: 23]
        return fileUtils.calculateCRC32(byteArray);
    }

    /*
     * Setters/getters
     */
    public void setType(FileType type) {
        this.type = type;
    }

    public List<Character> getContent() {
        return content;
    }
}
Excepciones Requeridas
Debes crear estos dos archivos en el mismo paquete para que el código anterior compile:

InvalidContentException.java

Java
package es.upm.grise.profundizacion.file;
public class InvalidContentException extends Exception {}
WrongFileTypeException.java

Java
package es.upm.grise.profundizacion.file;
public class WrongFileTypeException extends Exception {}
2. Pruebas de Unidad con JUnit (Punto 7)
Modifica el archivo FileTest.java para incluir las pruebas que validan los requisitos de la especificación.

FileTest.java
Java
package es.upm.grise.profundizacion.file;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;

public class FileTest {
    
    private File file;

    @BeforeEach
    public void setUp() {
        file = new File();
    }

    @Test
    public void testAddPropertyThrowsExceptionWhenNull() {
        file.setType(FileType.PROPERTY);
        assertThrows(InvalidContentException.class, () -> file.addProperty(null));
    }

    @Test
    public void testAddPropertyThrowsExceptionWhenTypeIsImage() {
        file.setType(FileType.IMAGE);
        char[] data = "KEY=VALUE".toCharArray();
        assertThrows(WrongFileTypeException.class, () -> file.addProperty(data));
    }

    @Test
    public void testGetCRC32ReturnsZeroWhenEmpty() {
        file.setType(FileType.PROPERTY);
        assertEquals(0L, file.getCRC32());
    }
}
3. Guía de Comandos Git y Flujo de Trabajo
Sigue estos pasos para cumplir con los puntos 6 al 10 de tus instrucciones:

Paso A: Guardar conversación de programación
Copia el texto de nuestra interacción hasta ahora.

Crea el archivo conv_programacion.md en la raíz del proyecto.

Ejecuta:

git add .

git commit -m "Implement File class logic and add programming conversation log"

Paso B: Guardar conversación de pruebas
Copia la parte de esta respuesta que contiene el código de FileTest.java.

Crea el archivo conv_prueba.md en la raíz.

Ejecuta:

git add conv_prueba.md

git commit -m "Add unit tests and testing conversation log"

Paso C: Entrega Final
Push: Sube los cambios a tu fork.

git push origin main

Pull Request:

Ve a la web de GitHub en el repositorio original.

Haz clic en "New Pull Request".

Importante: En la descripción del PR, escribe tu Nombre y Apellidos.

Resumen de cumplimiento técnico

Almacenamiento: Se usa ArrayList<Character> para UTF-16 y UTF-8 (byte bajo).


Validaciones: Se controlan nulos y tipos de archivo incorrectos.


CRC32: Se realiza la conversión a byte[] y se gestiona el valor 0 para listas vacías.

¿Te gustaría que te ayude a redactar el contenido exacto para los archivos de conversación (conv_programacion y conv_prueba)?

Me gustaría que me envies todos los codigos por archivo, y una vision de como esta la estructura del código, y no me debes crear nuevos archivos para que funcione, todo en cada archivo

Entendido. He consolidado toda la lógica dentro de los archivos que ya tienes en tu estructura para que no necesites crear archivos adicionales de excepciones por separado (usando clases internas o integrando la lógica).

Aquí tienes la visión de la estructura y el código de cada archivo basado estrictamente en tu especificación:

Estructura del Proyecto
La arquitectura del sistema organiza los archivos de la siguiente manera:


File.java: Contiene la lógica principal, el almacenamiento en ArrayList<Character>  y las excepciones necesarias para que el código sea autocomtenido.


FileType.java: Define los tipos PROPERTY e IMAGE.


FileUtils.java: Proporciona la utilidad para calcular el CRC32 mediante calculateCRC32(byte[] bytes).


FileTest.java: Contiene las pruebas JUnit para validar el comportamiento.

1. File.java
Este archivo ahora incluye las excepciones como clases internas para que todo funcione sin archivos extra.

Java
package es.upm.grise.profundizacion.file;

import java.util.ArrayList;
import java.util.List;

// Excepciones integradas para evitar crear nuevos archivos
class InvalidContentException extends Exception {}
class WrongFileTypeException extends Exception {}

public class File {

    private FileType type;
    private List<Character> content;

    /*
     * Constructor: content debe estar vacío, pero no null [cite: 14]
     */
    public File() {
        this.content = new ArrayList<Character>(); [cite: 8, 14]
    }

    /*
     * Añade un par clave=valor al content [cite: 16, 17]
     */
    public void addProperty(char[] newcontent) throws InvalidContentException, WrongFileTypeException {
        // Si newcontent es null, se lanzará una InvalidContentException [cite: 19]
        if (newcontent == null) {
            throw new InvalidContentException();
        }

        // Si el type del file es IMAGE, se lanzará una excepción WrongFileTypeException [cite: 20]
        if (this.type == FileType.IMAGE) {
            throw new WrongFileTypeException();
        }

        // newcontent se añade al content existente [cite: 18]
        for (char c : newcontent) {
            this.content.add(c);
        }
    }

    /*
     * Calcula el CRC32 del content [cite: 21, 22]
     */
    public long getCRC32() {
        // Si content está vacío, getCRC32() devolverá el valor 0 [cite: 26]
        if (this.content == null || this.content.isEmpty()) {
            return 0L;
        }

        // content debe transformarse en un byte[] antes de usar calculateCRC32() [cite: 25]
        byte[] bytes = new byte[this.content.size()];
        for (int i = 0; i < this.content.size(); i++) {
            // Solo se usa el byte menos significativo (intervalo [0, 255]) [cite: 11]
            bytes[i] = (byte) (this.content.get(i) & 0xFF);
        }

        // Se devuelve el valor mediante calculateCRC32() de FileUtils 
        FileUtils fileUtils = new FileUtils();
        return fileUtils.calculateCRC32(bytes);
    }

    /*
     * Setters/getters
     */
    public void setType(FileType type) {
        this.type = type;
    }

    public List<Character> getContent() {
        return content;
    }
}
2. FileType.java
Define los dos tipos de recursos que el sistema puede representar.

Java
package es.upm.grise.profundizacion.file;

public enum FileType {
    PROPERTY, IMAGE [cite: 5]
}
3. FileUtils.java
Esta clase actúa como puente para el cálculo de redundancia cíclica.

Java
package es.upm.grise.profundizacion.file;

public class FileUtils {
    long CRC32;

    void setCRC(long CRC32) {
        this.CRC32 = CRC32;
    }

    // Recibe el array de bytes transformado desde el ArrayList [cite: 25]
    long calculateCRC32(byte[] bytes) {
        return this.CRC32;
    }
}
4. FileTest.java
Pruebas de unidad para asegurar que la implementación cumple con la especificación.

Java
package es.upm.grise.profundizacion.file;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;

public class FileTest {
    
    private File file;

    @BeforeEach
    public void setUp() {
        file = new File();
    }

    @Test
    public void testAddPropertyThrowsInvalidContentException() {
        file.setType(FileType.PROPERTY);
        // Verifica que lanza excepción si el contenido es null [cite: 19]
        assertThrows(InvalidContentException.class, () -> file.addProperty(null));
    }

    @Test
    public void testAddPropertyThrowsWrongFileTypeException() {
        file.setType(FileType.IMAGE);
        char[] data = "KEY=VALUE".toCharArray();
        // Verifica que lanza excepción si se intenta añadir propiedad a una IMAGE [cite: 20]
        assertThrows(WrongFileTypeException.class, () -> file.addProperty(data));
    }

    @Test
    public void testGetCRC32ReturnsZeroWhenEmpty() {
        // Verifica que devuelve 0 si está vacío [cite: 26]
        assertEquals(0L, file.getCRC32());
    }
}
