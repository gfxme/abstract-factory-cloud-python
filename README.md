# Abstract Factory: plataforma multinube (AWS / Azure)

Implementación en Python del patrón de diseño **Abstract Factory** aplicada a un caso realista: desplegar un entorno en distintos proveedores de nube (AWS o Azure) sin cambiar el código cliente.

> Proyecto académico. Los servicios de nube están **simulados** (no se conecta a AWS ni Azure reales); el objetivo es demostrar el diseño orientado a objetos y el patrón.

## Problema que resuelve

Una aplicación necesita almacenamiento, notificaciones y autenticación. Cada proveedor de nube ofrece su propia versión de estos servicios. Si el código depende directamente de AWS, cambiar a Azure obliga a reescribirlo.

Con **Abstract Factory**, el código cliente trabaja solo con interfaces. Para cambiar de proveedor basta con pasar otra fábrica.

## Estructura

| Rol del patrón | Clases |
|---|---|
| Productos abstractos | `StorageService`, `NotificationService`, `AuthValidator` |
| Fábrica abstracta | `CloudInfrastructureFactory` |
| Fábrica y productos AWS | `AWSInfrastructureFactory` → `S3StorageService`, `SNSNotificationService`, `IAMAuthValidator` |
| Fábrica y productos Azure | `AzureInfrastructureFactory` → `BlobStorageService`, `EventGridNotificationService`, `EntraAuthValidator` |
| Cliente | `CloudDeploymentManager` |

## Uso

```python
manager = CloudDeploymentManager(AWSInfrastructureFactory())
manager.deploy_environment("AWS-12345")

manager = CloudDeploymentManager(AzureInfrastructureFactory())
manager.deploy_environment("AZURE-12345")
```

Salida con AWS:

```
Validando token mediante AWS IAM...
Token válido.
Subiendo config.txt a AWS S3...
AWS SNS: Entorno desplegado correctamente.
```

## Cómo ejecutarlo

Requiere Python 3.8 o superior, sin dependencias externas.

Abre `ECO_Cloud_Platform.ipynb` en Jupyter, VS Code o Google Colab y ejecuta las celdas en orden.

## Conceptos aplicados

- Patrón creacional **Abstract Factory**
- Clases abstractas con `abc.ABC` y `@abstractmethod`
- Polimorfismo e inyección de dependencias
- Principio abierto/cerrado: agregar un proveedor nuevo (por ejemplo, Google Cloud) solo requiere una fábrica y tres productos nuevos, sin tocar el cliente.

## Autor

Marco Alarcón Crespo · Estudiante de Ingeniería en Sistemas Inteligentes
