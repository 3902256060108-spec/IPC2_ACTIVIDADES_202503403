# Actividad Corta de Laboratorio: De ADO.NET Tradicional a la Automatización con EF Core

## Parte 1: Diagnóstico Técnico y Brecha de Impedancia

### Serie 1

La brecha de impedancia representa la diferencia entre el modelo orientado a objetos utilizado en C# y el modelo relacional empleado por las bases de datos. Entity Framework Core permite relacionar ambos modelos de forma automática.

* **Clase Clásica (POCO)** → **Tabla**
* **Propiedad/Atributo** → **Columna**
* **Instancia de Objeto** → **Fila (Registro)**

### Serie 2

Una de las ventajas de Entity Framework Core es que construye las consultas SQL utilizando parámetros de manera automática, lo que evita que la información ingresada por el usuario sea interpretada como parte del código SQL. En ADO.NET esta protección se conseguía agregando parámetros al objeto `SqlCommand`, por ejemplo mediante `AddWithValue()`.

### Serie 3

El método `.AsNoTracking()` se utiliza cuando los datos solo serán consultados y no modificados. Al no mantener un seguimiento de las entidades obtenidas, Entity Framework Core consume menos memoria y procesa las consultas con mayor eficiencia, lo que beneficia el rendimiento de la aplicación.

---

# Parte 2: Desafío de Refactorización de Código

## Serie 1

```csharp
using Microsoft.EntityFrameworkCore;

public class UnidadAcademicaContext : DbContext
{
    public UnidadAcademicaContext(DbContextOptions<UnidadAcademicaContext> configuracion)
        : base(configuracion)
    {
    }

    public DbSet<Catedratico> TblCatedraticos { get; set; }
}
```

## Serie 2

```csharp
using Microsoft.EntityFrameworkCore;

public class ServicioCatedraticos
{
    private readonly UnidadAcademicaContext contexto;

    public ServicioCatedraticos(UnidadAcademicaContext contexto)
    {
        this.contexto = contexto;
    }

    public IEnumerable<Catedratico> ListarIngenieros()
    {
        return contexto.TblCatedraticos
                       .AsNoTracking()
                       .Where(c => c.Nombre.StartsWith("Ing."))
                       .OrderBy(c => c.Nombre)
                       .ToList();
    }
}
```

---

# Parte 3: Referencias Bibliográficas

* Facultad de Ingeniería, USAC. (2026). *Sesión 17: Conectividad con SQL Server. Acceso Estructurado a Datos mediante C# y ADO.NET.* Laboratorio de Introducción a la Programación y Computación 2. Guatemala.

* Facultad de Ingeniería, USAC. (2026). *Sesión 18: Mapeo de Objetos Relacionales. Persistencia Automatizada con Entity Framework Core.* Laboratorio de Introducción a la Programación y Computación 2. Guatemala.
