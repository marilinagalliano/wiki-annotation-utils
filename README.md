# annotation-utils

Librería utilitaria para el desarrollo de anotaciones personalizadas en APIs RESTful. Este proyecto incluye dos anotaciones principales, `@Sensitive` y `@RequiredTest`, junto con sus correspondientes `Annotation Processors`. Su objetivo es facilitar el cumplimiento de políticas de seguridad y calidad de código en aplicaciones Java.
Fácilmente integrable a APIs RESTful. 

---

## Anotaciones Incluidas

### 1. `@Sensitive`

#### Descripción

Marca un campo como sensible, impidiendo que se muestre en logs o serializaciones públicas. Es útil para proteger datos como contraseñas, tokens, emails, etc.

#### Ejemplo de uso

```java
public class Usuario {
    @Sensitive
    private String password; // Esto lanzará advertencia por comentario

    public void imprimir() {
        System.out.println(password); // Esto también lanzará advertencia por log
    }
}
```

### 2. `@RequiredTest` y `@CoversMethod`

#### Descripción

Anotación de clase o método que obliga a que exista una clase de test correspondiente. El Processor analiza durante la compilación que haya un test presente para el método anotado, caso contrario el processor lanza una advertencia. Asegura la cobertura mínima de componentes críticos del sistema.

#### Ejemplo de uso

```java
// Clase Service con método que requiere test
public class UsuarioService {
    @RequiredTest
    public void guardarUsuario() {
        ...
    }
}

// Clase Test del Service con método que cubre el método requerido.
public class UsuarioServiceTest {
    @CoversMethod("guardarUsuario")
    @Test
    public void testGuardarUsuario() {
        ...
    }
}
```

## Integración a APIs RESTful

Si estás usando Maven, primero instalá el artefacto localmente, agregás en el pom.xml de la API RESTful como plugin y ejecutás el comando

```bash
mvn verify
```

## Autor

Si te interesa, podés escribirme y pedirme el repo con el código de la librería para clonar.

[@marilinagalliano](https://github.com/marilinagalliano)
