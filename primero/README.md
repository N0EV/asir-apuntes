# Primero ASIR
Este apartado contiene los apuntes correspondientes a los módulos profesionales del primer curso del Ciclo Formativo de Grado Superior en Administración de Sistemas Informáticos en Red. El contenido sigue el plan de estudios oficial regulado por la [Orden EDU/1287/2024](https://www.educa.jcyl.es/es/resumenbocyl/orden-edu-1287-2024-26-noviembre-concretan-aspectos-especif) y el [Decreto 24/2024](https://www.educa.jcyl.es/es/resumenbocyl/decreto-24-2024-21-noviembre-establece-curriculo-ciclos-for) de la Junta de Castilla y León.

## Asignaturas

| Código | Siglas | Nombre | Apuntes / Repositorio |
| :--- | :--- | :--- | :--- |
| **0369** | ISO | Implantación de sistemas operativos | [Ver apuntes](asir-apuntes/primero/iso) |
| **0370** | PAR | Planificación y administración de redes | [Ver apuntes](asir-apuntes/primero/par) |
| **0371** | FH | Fundamentos de hardware | [Ver apuntes](asir-apuntes/primero/fh) |
| **0372** | GBD | Gestión de bases de datos | [Ver apuntes](asir-apuntes/primero/gbd) |
| **0373** | LM-SGI | Lenguajes de marcas y sistemas de gestión de información | [Ver apuntes](asir-apuntes/primero/lm-sgi) |
| **0179** | ING | Inglés profesional (GS) | [Ver apuntes](asir-apuntes/primero/ing) |
| **1709** | IPE I | Itinerario personal para la empleabilidad I | [Ver apuntes](asir-apuntes/primero/ipe1) |
| **CL0036** | TSP | Transformación del Sistema Productivo | [Ver apuntes](asir-apuntes/primero/tsp) |

## Normativas

Las normativas y leyes que regulan estas asignaturas se pueden consultar en los siguientes enlaces oficiales:

* **Currículo Base y Título (ASIR):** Consulta la normativa oficial del ciclo en la [Página Título ASIR de la Junta de Castilla y León](https://jcyl.es).
* **Asignaturas Optativas:** Revisa la regulación de los módulos transversales en la [Página Optativas Transversales](https://jcyl.es) para la materia TSP.

## Estructura de Directorios

La organización de las carpetas dentro de este directorio se corresponde con las siglas oficiales de cada módulo:

```text
.
├── iso/      # Implantación de sistemas operativos
├── par/      # Planificación y administración de redes
├── fh/       # Fundamentos de hardware
├── gbd/      # Gestión de bases de datos
├── lm-sgi/    # Lenguajes de marcas y sistemas de gestión de información
├── ip/      # Inglés profesional (GS)
├── ipe1/    # Itinerario personal para la empleabilidad I
└── tsp/      # Transformación del Sistema Productivo
```

## Entorno Tecnológico y Herramientas

Para el seguimiento de las prácticas y laboratorios de este primer año se utilizan las siguientes herramientas:

* **Sistemas e Infraestructura:** Oracle VM VirtualBox (para el despliegue de máquinas virtuales).
* **Gestión de Bases de Datos:** MySQL Workbench (para el diseño y ejecución de sentencias SQL).
* **Editor y Control de Versiones:** Git y Visual Studio Code (utilizado principalmente para el módulo de Lenguajes de Marcas).

### Extensiones de Visual Studio Code Recomendadas:
* **Live Server:** Para la previsualización en tiempo real de archivos HTML/CSS.
* **XML Tools:** Para el formateo y validación de archivos XML/XSD.
* **Prettier - Code formatter:** Para mantener un estilo de código limpio y consistente.

## Uso del Repositorio

Para clonar de forma parcial únicamente el contenido de este primer curso sin descargar el resto de archivos del repositorio, ejecuta los siguientes comandos en tu terminal:

```bash
git clone --filter=blob:none --sparse https://github.com/N0EV/asir-apuntes.git
cd asir-apuntes
git sparse-checkout set primero
```