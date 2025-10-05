# Practica-3-ADBD

# 📘 Práctica 3: Modelo Entidad-Relación. **Viveros**  
---

## 🏫 Información Académica

| **Universidad**        | Universidad de La Laguna |
|------------------------|--------------------------|
| **Facultad**           | Escuela Superior de Ingeniería |
| **Asignatura**         | Administración de Bases de Datos |
| **Curso académico**    | 2025 / 2026 |
| **Práctica**           | Nº 3 – Modelo Entidad-Relación/Viveros |

---

## 👥 Miembros del Grupo

| **Nombre**                 | **Correo**                    |
|---------------------------|-------------------------------|
| Alba Pérez Rodríguez      | alu0101513768@ull.edu.es      |
| Eric Bermúdez Hernández   | alu0101517476@ull.edu.es      |
---
---

## 📑 Índice

1. [Introducción](#1-introducción)  
2. [Entidades y atributos](#2-entidades-y-atributos)  
   2.1 [🌱 Vivero](#21-vivero)  
   2.2 [🗺️ Zona](#22-zona)  
   2.2.1 [⛓️ Atributos relación Zona – Producto (Asignado)](#221-atributos-relación-zona--producto-asignado)  
   2.3 [👷 Empleado](#23-empleado)  
   2.3.1 [⛓️ Atributos relación Empleado – Zona (Pertenece)](#231-atributos-relación-empleado--zona-pertenece)  
   2.4 [📦 Producto](#24-producto)  
   2.5 [🧾 Pedido](#25-pedido)  
   2.6 [👤 Cliente](#26-cliente)  
   2.7 [⭐ Tajinaste Plus](#27-tajinaste-plus)  
3. [Relaciones](#3-relaciones)  
   3.1 [Relación Vivero – Zona (Formado)](#31-relación-vivero--zona-formado)  
   3.2 [Relación Zona – Empleado (Pertenece)](#32-relación-zona--empleado-pertenece)  
   3.3 [Relación Zona – Producto (Asignado)](#33-relación-zona--producto-asignado)  
   3.4 [Relación Empleado – Pedido (Gestiona)](#34-relación-empleado--pedido-gestiona)  
   3.5 [Relación Pedido – Producto (Forma)](#35-relación-pedido--producto-forma)  
   3.6 [Relación Cliente – Pedido (Realiza)](#36-relación-cliente--pedido-realiza)  
   3.7 [Relación Cliente – Tajinaste Plus (Pertenece)](#37-relación-cliente--tajinaste-plus-pertenece)  
4. [Restricciones semánticas](#4-restricciones-semánticas)  

---

## 1. Introducción

En este documento se presenta un **modelo entidad-relación (E-R)** diseñado para gestionar la información de un **vivero** y su operativa: zonas de cultivo, empleados, productos, pedidos y clientes, incluyendo un programa de fidelización (*Tajinaste Plus*).  
El objetivo del modelo es **organizar eficientemente** la información y describir con claridad las **relaciones** entre las entidades que aparecen en el diagrama E-R proporcionado.

---

## 2. Entidades y atributos

### 2.1 🌱 Vivero
**Descripción:** Representa cada vivero físico donde se cultivan/almacenan productos.

**Atributos:**

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **Nombre vivero (PK)** | Identificador único del vivero. | `VIV-TEGU` |
| **Ubicación (UNIQUE, derivado)** | **Par (Latitud, Longitud)** que identifica **de forma única** la posición del vivero. *No puede haber dos viveros con el mismo par lat/long.* | `28.4879, -16.3154` |
| **Latitud** | Componente de *Ubicación*. | `28.4879` |
| **Longitud** | Componente de *Ubicación*. | `-16.3154` |

> **Nota de unicidad:** La **ubicación** es **única (UNIQUE)** en *Vivero*. Esta restricción evita duplicar un vivero en la misma coordenada geográfica.

---

### 2.2 🗺️ Zona
**Descripción:** Subdivisión interna de un vivero (parcelas/camas de cultivo).

**Atributos:**

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **Nombre zona (PK)** | Identificador único de la zona (dentro del sistema). | `Z-ALOE-N2` |
| **Ubicación (UNIQUE, derivado)** | **Par (Latitud, Longitud)** único por zona. *Dos zonas no pueden compartir exactamente las mismas coordenadas.* | `28.4882, -16.3150` |
| **Latitud** | Componente de *Ubicación*. | `28.4882` |
| **Longitud** | Componente de *Ubicación*. | `-16.3150` |

> **Nota de unicidad:** Igual que en *Vivero*, la **ubicación** de *Zona* es **única**. Se destaca para asegurar la localización inequívoca de cada zona.

#### 2.2.1 ⛓️ Atributos relación Zona – Producto (Asignado)
**Descripción:** Atributos propios de la relación **Asignado** entre **Zona** y **Producto**.

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **Disponibilidad** | Disponibilidad/turno asociado a la asignación de un producto en una zona. | `L–V 08:00–14:00` |

---

### 2.3 👷 Empleado
**Descripción:** Personal que trabaja en el vivero/zona y gestiona pedidos o productos.

**Atributos:**

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **DNI (PK)** | Identificador único del empleado. | `12345678A` |
| **Nombre empleado** | Nombre y apellidos. | `Irene Martín Díaz` |

#### 2.3.1 ⛓️ Atributos relación Empleado – Zona (Pertenece)
**Descripción:** Atributos que dependen de la adscripción del **Empleado** a una **Zona**.

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **Puesto trabajo** | Rol o función desempeñada en la zona. | `Jardinero`, `Encargado` |
| **Época del año** | Temporada asociada al contrato/turno. | `Primavera` |
| **Fecha inicio** | Alta en el puesto en esa zona. | `2025-02-01` |
| **Fecha final** | Fin de contrato en esa zona (si aplica). | `2025-06-30` |

---

### 2.4 📦 Producto
**Descripción:** Catálogo de productos del vivero (plantas, semillas, etc.).

**Atributos:**

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **Código producto (PK)** | Identificador único del producto. | `PRD-ALOE-01` |
| **Nombre producto** | Denominación comercial. | `Aloe Vera 20cm` |
| **Precio** | Precio unitario. | `7.95 €` |

---

### 2.5 🧾 Pedido
**Descripción:** Encargos realizados por clientes, que pueden contener varios productos.

**Atributos:**

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **ID (PK)** | Identificador único del pedido. | `PED-000245` |
| **Fecha pedido** | Fecha en la que se registra el pedido. | `2025-03-12` |

---

### 2.6 👤 Cliente
**Descripción:** Personas que realizan pedidos al vivero.

**Atributos:**

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **DNI (PK)** | Identificador único del cliente. | `78945612K` |
| **Nombre** | Nombre y apellidos. | `Marcos García` |

---

### 2.7 ⭐ Tajinaste Plus
**Descripción:** Programa de fidelización opcional al que se puede adscribir un cliente.

**Atributos:**

| **Atributo** | **Descripción** | **Ejemplo** |
|---|---|---|
| **Id cliente (PK)** | Identificador del socio (corresponde al cliente). | `78945612K` |
| **Fecha suscripción** | Alta en el programa. | `2025-04-03` |
| **Bonificaciones** | Ventajas asociadas. | `5% descuento trimestral` |

---

## 3. Relaciones
A continuación, se describe la **participación**, **cardinalidad**, **interpretación** e **importancia** de cada relación del diagrama.

### 3.1. Relación Vivero – Zona (**Formado**)
- **Participación:**  
  - Un **vivero** está **formado** por **una o varias zonas**.  
  - Cada **zona** **pertenece** a **un único vivero**.
- **Cardinalidad:** `Vivero 1 : N Zona`, `Zona 1 : 1 Vivero`.
- **Interpretación:** La estructura del vivero se compone de varias zonas físicas diferenciadas.
- **Importancia:** Permite organizar el terreno y asociar personal/operaciones por zona.

---

### 3.2. Relación Zona – Empleado (**Pertenece**)
- **Participación:**  
  - Un **empleado** **pertenece** a **una única zona**.  
  - Una **zona** puede tener **muchos empleados**.
- **Cardinalidad:** `Zona 1 : N Empleado`, `Empleado 1 : 1 Zona`.
- **Interpretación:** Ubica a cada empleado en una zona concreta de trabajo.
- **Importancia:** Facilita la gestión de recursos humanos y planificación por zonas.

---

### 3.3. Relación **Zona – Producto** (**Asignado**)
- **Participación:**  
  - Una **zona** puede tener **varios productos asignados**.  
  - Un **producto** puede estar **asignado a varias zonas**.
- **Cardinalidad:** `1 : N`.
- **Atributos de la relación:**  
  - **Disponibilidad** Indica cuándo un producto está disponible en una zona específica.
- **Interpretación:** Determina la asignación operativa de productos a zonas.
- **Importancia:** Permite planificar operaciones de cultivo, venta y logística, asegurando que los productos estén disponibles según la planificación de la zona.

---

### 3.4. Relación Empleado – Pedido (**Gestiona**)
- **Participación:**  
  - Un **empleado** puede **gestionar** **cero o varios pedidos**.  
  - **Cada pedido** es **gestionado por un único empleado**.
- **Cardinalidad:** `Empleado 0 : N Pedido`, `Pedido 1 : 1 Empleado`.
- **Interpretación:** Asigna un responsable a cada pedido.
- **Importancia:** Traza la gestión y mejora el control de tiempos y calidad del servicio.

---

### 3.5. Relación Pedido – Producto (**Forma**)
- **Participación:**  
  - Un **pedido** está **formado** por **uno o varios productos**.  
  - Un **producto** puede **aparecer** en **muchos pedidos**.
- **Cardinalidad:** `Pedido 1 : N Producto`, `Producto 0 : N Pedido`.
- **Interpretación:** Un pedido agrupa productos.  
- **Importancia:** Eje de la venta y base para inventario y facturación.

---

### 3.6. Relación Cliente – Pedido (**Realiza**)
- **Participación:**  
  - Un **cliente** puede **realizar** **cero o varios pedidos**.  
  - **Cada pedido** está **realizado por un único cliente**.
- **Cardinalidad:** `Cliente 0 : N Pedido`, `Pedido 1 : 1 Cliente`.
- **Interpretación:** Vincula el histórico de pedidos con su titular.
- **Importancia:** Fundamental para el CRM, seguimiento y estadísticas de ventas.

---

### 3.7. Relación Cliente – Tajinaste Plus (**Pertenece**)
- **Participación:**  
  - Un **cliente** puede **no pertenecer** o **pertenecer** a **Tajinaste Plus** (**0:1**).  
  - Cada **registro** de *Tajinaste Plus* **corresponde a un único cliente**.
- **Cardinalidad:** `Cliente 0 : 1 Tajinaste Plus`, `Tajinaste Plus 1 : 1 Cliente`.
- **Interpretación:** Especialización/afiliación al programa de fidelización.
- **Importancia:** Permite aplicar bonificaciones y segmentar clientes.

---

## 4. Restricciones semánticas

1. **Unicidad de Ubicación en Vivero y Zona**  
   - En **Vivero** y en **Zona**, el atributo **Ubicación** es **UNIQUE** y **derivado de (Latitud, Longitud)**.  
   - **No pueden existir dos viveros ni dos zonas con el mismo par (lat, long)**. Esta restricción garantiza la identificación geográfica inequívoca y evita duplicidades.

2. **Integridad de claves**  
   - **Nombre vivero**, **Nombre zona**, **DNI (Empleado/Cliente)**, **Código producto** e **ID de pedido** son **claves primarias** y no admiten nulos ni duplicados.

3. **Relación Vivero – Zona**  
   - Participación **total** en ambos extremos: todo vivero tiene **al menos una zona** y máximo N zonas y toda zona **pertenece a un vivero**.

4. **Relación Zona – Empleado (Pertenece)**  
   - Cada **empleado** debe estar **asignado exactamente a una zona**.  
   - Una **zona** puede tener **uno o más empleados**.

5. **Relación Cliente – Pedido**  
   - **Cada pedido** debe estar **asociado a un cliente** y un cliente puede tener **cero o varios pedidos**.

6. **Relación Pedido – Producto**  
   - Un **pedido** debe contener **al menos un producto**.  
   - Un producto puede estar en ninguno o en múltiples pedidos.

7. **Relación Zona – Producto (Asignado)**  
   - La **Disponibilidad** debe ser coherente con calendarios/turnos definidos (sin solapes imposibles).

8. **Programa Tajinaste Plus**  
   - La afiliación es **opcional**: un cliente puede **no estar suscrito**.  
   - Si existe, debe registrarse **Fecha de suscripción** y **Bonificaciones** aplicables.

9. **Restricciones de dominio**  
   - **Precio** de *Producto* debe ser **> 0**.  
   - **Fechas**: `Fecha final` (en la relación Empleado–Zona) ≥ `Fecha inicio` cuando exista; `Fecha pedido` ≤ fecha actual.

---
