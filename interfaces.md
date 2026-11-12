# Implementación de interfaces

## Interfaz `ICatalogo`

:books: La interfaz `ICatalogo` se ha creado en la capa `EL`.

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

## Implementación de la interfaz `ICatalogo` en la capa `DAL`.

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

## Implementación de la interfaz `ICatalogo` en la capa `BLL`.

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