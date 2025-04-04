![image](https://github.com/user-attachments/assets/031419a1-1e56-40d4-819c-9a0761b5585c)# **IBM Cloud Satellite - Configuración**

Esta guía ofrece un paso a paso para crear una ubicación de IBM Cloud Satellite, desplegar un clúster de OpenShift y configurar Satellite Config.

**Nota:** Esta guía está diseñada para un despliegue rápido e intuitivo de un clúster y una aplicación, sin requerir conocimientos técnicos profundos. Para un entendimiento más detallado de la solución IBM Cloud Satellite y su gestión, consulta el otro archivo `README.md`.


## **Contenido**

1. [Pre-requisitos](#pre-requisitos)
2. [Schematics y Terraform](#schematics-y-terraform)
   1. [Creación del workspace](#creación-del-workspace)
   2. [Generación del plan](#generación-del-plan)
   3. [Ejecución del plan](#ejecución-del-plan)
3. [Asignación de hosts al control plane](#asignación-de-hosts-al-control-plane)
4. [Instalación de OpenShift](#instalación-de-openshift)
5. [Ingreso al Bastion](#Ingreso-al-Bastion)
---

## **Pre-requisitos** :pencil:

- Contar con una cuenta en [IBM Cloud](https://cloud.ibm.com/).
- Permisos sobre **Schematics**, **Satellite**, **OpenShift** e infraestructura **VPC**. 

Se utilizará un pequeño proyecto de Terraform para levantar la infraestructura necesaria en IBM Cloud, facilitando el despliegue de los servicios de IBM Cloud Satellite de manera rápida y sencilla.

---

## **Schematics y Terraform**
### **Creación del workspace**

1. A partir del fork del repositorio, crea un **workspace** en Schematics apuntando al directorio `terraform-infraestructura`.

   ![image](https://github.com/user-attachments/assets/54abe4a3-48ef-4ac6-85dc-bffb9e778874)

2. Utiliza el grupo de recursos con los permisos necesarios. Los permisos sobre infraestructura clásica recaen en el usuario.

   ![image](https://github.com/user-attachments/assets/1b27be25-42ec-4e0e-b357-a6fcd5fa2aab)

---

### **Generación del plan**

En este proecso se analiza la infraestructura actual y compara los cambios definidos en el código de configuración. Esto genera un plan detallado que muestra las acciones que se tomarán (crear, modificar o eliminar recursos) sin aplicarlas aún.

1. Antes de generar el plan, verifica las variables que se utilizarán.
   - Los valores predeterminados funcionan correctamente en la mayoría de los casos.
   - Si necesitas realizar cambios, es preferible editarlas directamente en los archivos de Terraform con un editor de código. Las listas de hosts pueden ser especialmente propensas a errores si se editan desde la consola de IBM Cloud.

   ![image](https://github.com/user-attachments/assets/616c53f8-082e-468b-93c4-0cc962e9f71f)

2. Una vez revisadas las variables, procede a generar el plan.

   ![image](https://github.com/user-attachments/assets/008875f9-338e-472e-a0e8-f53e9c9152a9)

---

### **Ejecución del plan**

Terraform realiza las acciones especificadas para alinear la infraestructura con el estado deseado definido en el código.

1. Después de generar el plan correctamente, aplica el plan y revisa los logs generados.

   ![image](https://github.com/user-attachments/assets/2d91bc9b-e4a8-4a81-85e5-b84f30cffaf0)

2. La ejecución del plan será exitosa si todos los hosts creados son visibles en la consola de Satellite con el estado **Ready**.

   ![image](https://github.com/user-attachments/assets/15ecfaf3-16b3-4166-a968-a167e75741c4)

---

## **Asignación de hosts al control plane**

Asigna los hosts correspondientes al control plane en las zonas correspondientes. Los hosts para los workers se asignarán durante la instalación de OpenShift.

![image](https://github.com/user-attachments/assets/1434fea6-2501-479e-9402-e0d586379cb9)

---

## **Instalación de OpenShift**

1. Desde la consola de IBM Cloud, selecciona la infraestructura de Satellite.
2. Escoge la ubicación creada previamente, el grupo de recursos con los permisos necesarios y define las características de los hosts existentes en la ubicación.

   ![image](https://github.com/user-attachments/assets/6a33fc08-16a0-4314-84a7-41083b0282f6)

   **Nota:** para usar satellite config es necesario habilites el acceso de administracion de satellite al momento de desplegar el cluster.

---

## **Ingreso al Bastion**

1. Descargar conexion RDP desde la consola de ibmcloud.
   ![image](https://github.com/user-attachments/assets/b6b32f62-a4a2-4b2e-8d12-1ccd71613463)
2. Obtener contrasena utilizando la ssh key privada que se encuentra en el repositorio.(seguir esta [documentacion](#https://cloud.ibm.com/docs/vpc?topic=vpc-vsi_is_connecting_windows&locale=es))  
