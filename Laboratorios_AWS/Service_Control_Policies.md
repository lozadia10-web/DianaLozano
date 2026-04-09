# 🏛️ Laboratorio AWS: Gobierno Corporativo con Service Control Policies (SCP)

Este repositorio documenta mi práctica sobre el control centralizado de permisos en una organización de AWS, utilizando **Service Control Policies (SCP)** para establecer barreras de seguridad.

* **Servicio:** AWS Organizations

---

## 1. Diseño de la Estructura Organizacional
El primer paso de mi laboratorio consistió en organizar la jerarquía de la cuenta. Creé **Unidades Organizacionales (OU)** para segmentar los entornos de trabajo, lo que permite aplicar políticas de forma selectiva según el propósito de cada cuenta.

La estructura que definí fue:
* **Root**
    * **OU-Workloads** (Contiene las sub-unidades **DEV** y **PROD**)
    * **OU-Security** (Contiene la unidad **SECURITY**)

> **Evidencia:** > ![Estructura Organizacional](./img/Estructura_Organizacional.png)

---

## 2. Implementación de Service Control Policies (SCP)
Las SCP son políticas que permiten limitar los permisos máximos que los usuarios y roles pueden tener en las cuentas de la organización. 

### 2.1. Creación de la Política
En la cuenta principal (*Management*), procedí a crear una política en formato JSON. Esta política tiene como objetivo restringir acciones críticas, asegurando que se cumplan los estándares de seguridad sin importar los permisos individuales que tenga un usuario IAM.

> **Evidencia:** > ![Creacion SCP](./img/Creacion_SCP.png)



### 2.2. Asociación y Herencia
Asocié la política creada a la **Unidad Organizacional (OU)** correspondiente. Pude validar cómo la política se hereda a todas las cuentas que se encuentren bajo esa unidad, permitiendo un control administrativo eficiente y centralizado.

---

## 3. Conclusiones

* **Control Centralizado:** Aprendí que las SCP son la herramienta más potente para evitar que se realicen acciones prohibidas (como borrar logs de CloudTrail o crear recursos costosos) en toda la empresa.
* **Jerarquía:** La importancia de organizar las cuentas en OUs para aplicar seguridad de manera escalable.
* **Seguridad Preventiva:** A diferencia de IAM (que otorga permisos), las SCP funcionan como un filtro que prohíbe acciones, proporcionando una capa de seguridad superior.
