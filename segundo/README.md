# Segundo ASIR
Este apartado contiene los apuntes correspondientes a los módulos profesionales del segundo curso del Ciclo Formativo de Grado Superior en Administración de Sistemas Informáticos en Red. El contenido sigue el plan de estudios oficial regulado por la [Orden EDU/1287/2024](https://www.educa.jcyl.es/es/resumenbocyl/orden-edu-1287-2024-26-noviembre-concretan-aspectos-especif) y el [Decreto 24/2024](https://www.educa.jcyl.es/es/resumenbocyl/decreto-24-2024-21-noviembre-establece-curriculo-ciclos-for) de la Junta de Castilla y León.

## Asignaturas

| Código | Siglas | Nombre de la Asignatura | Enlace |
| :--- | :--- | :--- | :--- |
| 1665 | DASP | Digitalización aplicada a los sectores productivos (GS) | [Ver Apuntes](asir-apuntes/segundo/dasp) |
| 0374 | ASO | Administración de sistemas operativos | [Ver Apuntes](asir-apuntes/segundo/aso) |
| 0375 | SRI | Servicios de red e internet | [Ver Apuntes](asir-apuntes/segundo/sri) |
| 0376 | IAW | Implantación de aplicaciones web | [Ver Apuntes](asir-apuntes/segundo/iaw) |
| 0377 | ASGBD | Administración de sistemas gestores de bases de datos | [Ver Apuntes](asir-apuntes/segundo/asgbd) |
| 0378 | SAD | Seguridad y alta disponibilidad | [Ver Apuntes](asir-apuntes/segundo/sad) |
| 1708 | SASP | Sostenibilidad aplicada al sistema productivo | [Ver Apuntes](asir-apuntes/segundo/sasp) |
| 1710 | IPE II | Itinerario personal para la empleabilidad II | [Ver Apuntes](asir-apuntes/segundo/ipe-ii) |
| 0379 | PIASIR | Proyecto intermodular de administración de sistemas informáticos en red | [Ver Apuntes](asir-apuntes/segundo/piasir) |

### Optativas

| Código | Elegida | Siglas | Nombre | Enlace |
| :--- | :--- | :--- | :--- | :--- |
| CL2002 | [X] | CN | Computación en la nube (GS) | [Ver Apuntes](asir-apuntes/segundo/cn) |
| CL2003 | [ ] | FC | Fundamentos de ciberseguridad (GS) | [Ver Apuntes](asir-apuntes/segundo/fc) |

## Enlaces y Recursos de Interés

* **Currículo Base y Título (ASIR):** Consulta la distribución horaria de segundo en la [Ficha Técnica de ASIR en el Portal de Educación de la Junta de Castilla y León](https://www.educa.jcyl.es/fp/es/catalogo-titulos-modalidad-presencial/titulos-grado-superior/administracion-sistemas-informaticos-red).
* **Módulos Optativos de Segundo:** Revisa la regulación de los contenidos específicos del curso en el [Catálogo de Módulos Optativos de Oferta Común](https://www.educa.jcyl.es/fp/es/normativa-castilla-leon/catalogo-modulos-optativos/modulos-optativos-ciclos-formativos-grado-superior) de la Junta de Castilla y León para la materia TSP.

## Estructura de Directorios

La organización de las carpetas dentro de este directorio se corresponde con las siglas oficiales de cada módulo:

```text
segundo/
├── asgbd/      # Administración de Sistemas Gestores de Bases de Datos
├── aso/        # Administración de Sistemas Operativos
├── cn/         # Computación en la nube
├── iaw/        # Implantación de Aplicaciones Web
├── ipe2/       # Itinerario Personal para la Empleabilidad II
├── pi/         # Proyecto Intermodular
├── sad/        # Seguridad y Alta Disponibilidad
├── sasp/       # Sostenibilidad Aplicada al Sistema Productivo
└── sri/        # Servicios de Red e Internet
```

## Entorno Tecnológico y Herramientas

Para el seguimiento de las prácticas, despliegues y laboratorios de este segundo año se utilizan las siguientes herramientas:

* **Sistemas e Infraestructura:** Oracle VM VirtualBox / VMware Workstation y clientes SSH como PuTTY (para la administración remota de servidores Linux y Windows Server).
* **Gestión de Bases de Datos:** MongoDB Compass y phpMyAdmin / DBeaver (para la administración de bases de datos relacionales y no relacionales).
* **Servicios y Despliegue Web:** Docker, servidores Apache/Nginx y plataformas CMS (para el módulo de Implantación de Aplicaciones Web).
* **Editor y Control de Versiones:** Git y Visual Studio Code (utilizado para scripts de automatización, configuraciones de red y seguridad).

### Extensiones de Visual Studio Code Recomendadas:
* **Remote - SSH:** Para conectarte y editar archivos directamente en tus servidores virtuales desde el editor.
* **Docker:** Para gestionar contenedores, imágenes y archivos Dockerfile de forma visual.
* **YAML / Jinja:** Para el formateo de archivos de configuración de servicios y automatizaciones.
* **Prettier - Code formatter:** Para mantener un estilo de código limpio y consistente.

## Uso del Repositorio

Para clonar de forma parcial únicamente el contenido de este segundo curso sin descargar el resto de archivos del repositorio, ejecuta los siguientes comandos en tu terminal:

```bash
git clone --filter=blob:none --sparse https://github.com/N0EV/asir-apuntes.git
cd asir-apuntes
git sparse-checkout set segundo
```
