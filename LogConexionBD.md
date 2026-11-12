## Clase Log
```csharp
using System;
using System.Collections.Generic;
using System.Text;

namespace InventarioAC.EL
{
    public class Log
    {
        public Log(string mensaje)
        {
            try
            {
                StreamWriter sw = new StreamWriter("log.txt");
                sw.WriteLine(mensaje);
                sw.Close();
            }
            catch (Exception e)
            {
                Console.WriteLine("Exception: " + e.Message);
            }
            finally
            {
                Console.WriteLine("Executing finally block.");
            }
        }
    }
}

```

## Clase ConexionBD

```csharp
using System;
using System.Collections.Generic;
using System.Text;
using Microsoft.Data.SqlClient;
using InventarioAC.EL;
namespace InventarioAC.DAL
{
    public class ConexionBD
    {
        public static SqlConnection Conectar()
        {
            string cs = "Data Source=ITCHAD32;Initial Catalog=Inventa;User Id=sa;Password=adminsql;Encrypt=True;TrustServerCertificate=True;";

            SqlConnection conn = null;
            try
            {
                conn = new SqlConnection(cs);
                conn.Open();
            }
            catch (Exception ex)
            {
                new Log(ex.Message);
                try
                {
                    if (conn != null && conn.State != System.Data.ConnectionState.Closed)
                    {
                        conn.Close();
                    }
                }
                catch (Exception ex2)
                {
                    new Log(ex2.Message);
                }
            }
            return conn;
        }
    }
}
```

## Producto

```csharp
using System;
using System.Collections.Generic;
using System.Text;

namespace InventarioAC.EL
{
    public class Producto
    {
        public int Id { get; set; }
        public string Nombre { get; set; }
        public Producto() { }
        public Producto(int id) {  Id = id; }
        public Producto(int id, string nombre) {
            Id = id;
            Nombre = nombre;
        }
    }
}
```