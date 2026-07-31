# Estructura de un sistema informático
Un **sistema informático** es el conjunto de elementos físicos o también llamado hardware, lógicos o software y humanos, los cuales trabajan conjuntamente para **capurar**, **procesar**, **almacenar**, **transmitir** y **presentar** información de una forma automática y eficiente.

```mermaid
flowchart LR
    H[🔌 HARDWARE] --> S[💻 SOFTWARE]
    S --> P[👤 PERSONAS]
    P --> D[📊 DATOS]
    D --> H
```

## Hardware
## Software
## Datos
## Personas

## Arquitectura de Von Neuman

```mermaid
graph TB
    %% Dispositivos de Entrada y Salida
    IN[📥 Dispositivos de Entrada<br>Teclado, Ratón, Red...] --> CPU
    CPU --> OUT[📤 Dispositivos de Salida<br>Monitor, Disco, Red...]

    %% Bloque Principal de la CPU
    subgraph CPU [🧠 CPU / Unidad Central de Procesamiento]
        direction TB
        
        subgraph UC [⚙️ Unidad de Control]
            PC[Contador de Programa / PC]
            IR[Registro de Instrucción / IR]
        end

        subgraph ALU [🧮 Unidad Aritmético-Lógica]
            Op[Circuitos Operacionales]
            AC[Acumulador]
        end
        
        %% Conexiones internas de control y datos
        UC <--> ALU
    end

    %% Memoria Principal (Datos e Instrucciones unificados)
    subgraph MEM [💾 Memoria Principal / RAM]
        direction LR
        Instrucciones[📝 Instrucciones del Programa]
        Datos[📊 Datos de Trabajo]
    end

    %% Buses del Sistema (Conexiones Bidireccionales)
    CPU <-->|Bus de Datos y Control| MEM

```

## Arquitectura de Harvard

```mermaid
graph TB
    %% Dispositivos de Entrada y Salida
    IN[📥 Dispositivos de Entrada] --> CPU
    CPU --> OUT[📤 Dispositivos de Salida]

    %% Bloque Principal de la CPU
    subgraph CPU [🧠 CPU / Unidad Central de Procesamiento]
        UC[⚙️ Unidad de Control] <--> ALU[🧮 Unidad Aritmético-Lógica]
    end

    %% Memoria de Instrucciones (Separada)
    subgraph MEM_I [📝 Memoria de Instrucciones]
        I_Code[Código del Programa]
    end

    %% Memoria de Datos (Separada)
    subgraph MEM_D [📊 Memoria de Datos]
        D_Var[Variables y Datos]
    end

    %% Buses del Sistema TOTALMENTE INDEPENDIENTES
    UC <-->|🚌 Bus de Instrucciones Dedicado| MEM_I
    ALU <-->|🚌 Bus de Datos Dedicado| MEM_D
```

### Comparación