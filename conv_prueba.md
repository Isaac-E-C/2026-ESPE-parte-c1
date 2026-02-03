Para validar que la implementación de la clase File cumple con todos los requisitos de la especificación técnica, se ha diseñado la siguiente batería de pruebas en el archivo FileTest.java. Estas pruebas aseguran el manejo correcto de excepciones y los valores por defecto del CRC32.

Código de Pruebas Propuesto (FileTest.java):
Java
package es.upm.grise.profundizacion.file;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;

public class FileTest {
    
    private File file;

    @BeforeEach
    public void setUp() {
        // Se instancia un nuevo objeto File antes de cada test
        file = new File();
    }

    @Test
    public void testAddPropertyThrowsInvalidContentException() {
        // Requisito: Si newcontent es null, se debe lanzar InvalidContentException
        file.setType(FileType.PROPERTY);
        assertThrows(InvalidContentException.class, () -> file.addProperty(null));
    }

    @Test
    public void testAddPropertyThrowsWrongFileTypeException() {
        // Requisito: Si el tipo es IMAGE, addProperty debe lanzar WrongFileTypeException
        file.setType(FileType.IMAGE);
        char[] data = "KEY=VALUE".toCharArray();
        assertThrows(WrongFileTypeException.class, () -> file.addProperty(data));
    }

    @Test
    public void testGetCRC32ReturnsZeroWhenEmpty() {
        // Requisito: Si el contenido está vacío, getCRC32() debe devolver 0
        assertEquals(0L, file.getCRC32(), "El CRC32 debe ser 0 para archivos sin contenido");
    }
}
Explicación de la Cobertura de Pruebas:

testAddPropertyThrowsInvalidContentException: Verifica la robustez del método addProperty ante entradas nulas, asegurando que se dispare la excepción personalizada definida en la especificación.


testAddPropertyThrowsWrongFileTypeException: Valida la restricción de diseño que impide añadir propiedades de texto a archivos que han sido marcados como tipo IMAGE.


testGetCRC32ReturnsZeroWhenEmpty: Comprueba que el sistema maneja correctamente el estado inicial (vacío) del ArrayList<Character>, devolviendo el valor long 0 como se requiere específicamente.