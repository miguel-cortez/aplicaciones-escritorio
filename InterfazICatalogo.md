# Implementación de interfaces

Las interfaces definen los métodos que serán implementados en las clase que utilicen dicha interfaz, por ejemplo: ProductoDAL, CategoriaDAL, EmpleadoDAL, etc.  

## Interfaz `ICatalogo`

:books: Esta interfaz se ha creado en la capa `InventarioAC.EL` 

```csharp
using System;
using System.Collections.Generic;
using System.Text;

namespace InventarioAC.EL
{
    public interface ICatalogo<T>
    {
        static abstract bool Actualizar(T param1);
        static abstract int Agregar(T param1);
        static abstract bool Eliminar(T param1);
        static abstract T Buscar(T param1);
        static abstract List<T> ObtenerTodos();
    }
}
```

## Ejemplos de implementación de la interfaz `ICatalogo`

### En la clase ProductoDAL

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using InventarioAC.EL;
namespace InventarioAC.DAL
{
    public class ProductoDAL : ICatalogo<Producto>
    {
        public static bool Actualizar(Producto param1)
        {
            throw new NotImplementedException();
        }

        public static int Agregar(Producto param1)
        {
            throw new NotImplementedException();
        }

        public static Producto Buscar(Producto param1)
        {
            throw new NotImplementedException();
        }

        public static bool Eliminar(Producto param1)
        {
            throw new NotImplementedException();
        }

        public static List<Producto> ObtenerTodos()
        {
            throw new NotImplementedException();
        }
    }
}
```

### En la clase ProductoBLL

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using InventarioAC.DAL;
using InventarioAC.EL;
namespace InventarioAC.BLL
{
    public class ProductoBLL : ICatalogo<Producto>
    {
        public static bool Actualizar(Producto param1)
        {
            throw new NotImplementedException();
        }

        public static int Agregar(Producto param1)
        {
            throw new NotImplementedException();
        }

        public static Producto Buscar(Producto param1)
        {
            throw new NotImplementedException();
        }

        public static bool Eliminar(Producto param1)
        {
            throw new NotImplementedException();
        }

        public static List<Producto> ObtenerTodos()
        {
            throw new NotImplementedException();
        }
    }
}
```

:warning: Arriba, solo se han implementado los métodos de la interfaz pero no se han programado aún.

