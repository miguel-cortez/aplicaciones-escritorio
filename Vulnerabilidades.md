# Vulnerabilidades

## Detalles de la vulnerabilidad
![alt text](./img/capturavulnerabilidad.png)  

```bash
  Determinando los proyectos que se van a restaurar...
C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.BLL\InventarioAC.BLL.csproj : warning NU1902: El paquete "System.Security.Cryptography.Pkcs" 9.0.18 tiene una vulnerabilidad de gravedad moderada conocida, https://github.com/advisories/GHSA-2fmv-rv2c-59x7 [C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.slnx]
C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.DAL\InventarioAC.DAL.csproj : warning NU1902: El paquete "System.Security.Cryptography.Pkcs" 9.0.18 tiene una vulnerabilidad de gravedad moderada conocida, https://github.com/advisories/GHSA-2fmv-rv2c-59x7 [C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.slnx]
C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.BLL\InventarioAC.BLL.csproj : warning NU1903: El paquete "System.Security.Cryptography.Pkcs" 9.0.18 tiene una vulnerabilidad de gravedad alta conocida, https://github.com/advisories/GHSA-846f-f764-76mx [C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.slnx]
C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.DAL\InventarioAC.DAL.csproj : warning NU1903: El paquete "System.Security.Cryptography.Pkcs" 9.0.18 tiene una vulnerabilidad de gravedad alta conocida, https://github.com/advisories/GHSA-846f-f764-76mx [C:\Users\Miguel Cortez\source\repos\InventarioAC\InventarioAC.slnx]
  Todos los proyectos est├ín actualizados para la restauraci├│n.

✂️ CÓDIGO OMITIDO

```

## Recomendación

Instalar el paquete con vulnerabilidad a la versión más reciente `9.0.21`. Se puede hacer gráficamente con NuGet o mediante la `Consola del Administrador de paquetes`.

### En entorno gráfico

1. Clic derecho en el nombre del proyecto que tiene la vulnerabilidad.  

2. Clic en Administrador de paquetes NuGet.

3. Busque el paquete reciente e instale

En la siguiente imagen se muestra la versión reciente (11.0.0) del paquete `System.Security.Cryptography.Pkcs`

![alt text](./img/paquete11.0.0.png)  

### En la consola de Administrador de paquetes

1. Clic en Herramientas.  

2. Administrador de paquetes NuGet.  

3. Consola del Administrador de paquetes.  

```bash
Install-Package System.Security.Cryptography.Pkcs -Version 11.0.0
```

![alt text](./img/consolaadministradorpaquetes.png)  

## Problema de bloqueo

### Consultar el registro de eventos

1. Abre el Visor de eventos.

2. Ve a Registros de aplicaciones y servicios.

3. Microsoft → Windows → CodeIntegrity → Operational.

4. Busca eventos 3076 o 3077.

![alt text](./img/problemabloqueo.png)  

:books: El bloqueo se produce durante el proceso de compilación, cuando MSBuild intenta cargar tu biblioteca de acceso a datos.  

### Posibles causas del error  

- App Control for Business (WDAC): Windows tiene una política que exige que determinados archivos estén firmados por un editor autorizado.

- Política de integridad de código: una regla de seguridad impide ejecutar o cargar DLL que no cumplen determinados requisitos.

- DLL generada localmente: tu biblioteca InventarioAC.DAL.dll no tiene una firma reconocida por la política de seguridad del equipo.

https://support.microsoft.com/es-es/windows/security/threat-malware-protection/smart-app-control-has-blocked-part-of-this-app
