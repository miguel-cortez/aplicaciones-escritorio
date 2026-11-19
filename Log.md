## Clase Log

:books: La clase `Log` registrará información de los errores ocurridos en la aplicación. Esto será útil para depurar la aplicación.

En mi caso, los errores se registran en el directorio `C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.UI\bin\Debug\net10.0-windows` 

:books: La clase `Log` se ha creado en la capa `InventarioAC.EL` 

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
                using (StreamWriter sw = File.AppendText("log.txt"))
                {
                    Log.Entrada(mensaje, sw);
                }
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
        public static void Entrada(string logMessage, TextWriter w)
        {
            w.Write("\r\nEntrada de registro : ");
            w.WriteLine($"{DateTime.Now.ToLongTimeString()} {DateTime.Now.ToLongDateString()}");
            w.WriteLine($"{logMessage}");
            w.WriteLine("-------------------------------");
            w.Close();
        }
    }
}

```