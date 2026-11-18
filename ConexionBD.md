## Clase ConexionBD

:books: Esta clase se crea en la capa InventarioAC.DAL

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