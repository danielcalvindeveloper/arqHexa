# Arquitectura Hexagonal - Ejemplo de Artefactos para Cliente

Este documento presenta la organización de artefactos en una arquitectura hexagonal utilizando el paquete `ar.com.sabadostech`. Se asigna cada artefacto a su correspondiente capa de la aplicación de forma genérica, adaptable a distintas plataformas (por ejemplo, C#, Java, etc.), sin referir a tecnologías específicas. Se mencionan frameworks de persistencia y otros en función de la funcionalidad prestada.

---

## 1. Capa de Dominio

- **Paquete:** `ar.com.sabadostech.domain.model`
  - **Cliente:** Entidad que representa al cliente en el modelo de negocio.

- **Paquete:** `ar.com.sabadostech.domain.repository`
  - **ClienteRepository:** Interfaz (puerto) que define las operaciones de persistencia para la entidad Cliente, sin acoplarse a detalles de infraestructura.

---

## 2. Capa de Infraestructura

### 2.1 Persistencia

- **Paquete:** `ar.com.sabadostech.infrastructure.persistence.entity`
  - **ClienteEntity:** Modelo de datos adaptado para el almacenamiento, estructurado para satisfacer los requerimientos del sistema de persistencia (definido de forma genérica).

- **Paquete:** `ar.com.sabadostech.infrastructure.persistence.repository`
  - **GenericClienteRepository:** Interfaz del repositorio genérico, proporcionado por un framework de persistencia (sin referirse a uno en particular) que facilita operaciones CRUD.

### 2.2 Adaptadores y Mapeo

- **Paquete:** `ar.com.sabadostech.infrastructure.mapper`
  - **ClienteMapper:** Componente encargado de transformar entre el modelo de dominio (Cliente) y el modelo de persistencia (ClienteEntity), permitiendo que el dominio se mantenga independiente de detalles técnicos.

- **Paquete:** `ar.com.sabadostech.infrastructure.adapter`
  - **ClienteRepositoryAdapter:** Implementación del puerto `ClienteRepository` definida en el dominio, que utiliza el repositorio genérico de persistencia y el mapper para convertir entre los modelos.

---

## 3. Capa de Aplicación

- **Paquete:** `ar.com.sabadostech.application.usecase`
  - **RegistrarClienteUseCase:** Caso de uso que coordina la creación y registro de un nuevo Cliente en el sistema. Este artefacto orquesta la interacción entre el dominio y la infraestructura a través del puerto `ClienteRepository`.

---

**Opinión:**  
Esta estructura en capas favorece un fuerte desacoplamiento entre la lógica de negocio y los detalles técnicos, lo que facilita la portabilidad del sistema a distintas plataformas y mejora su mantenibilidad y testabilidad. Al definir claramente la responsabilidad de cada capa y emplear adaptadores y mappers, se logra una arquitectura robusta y adaptable a diversos entornos tecnológicos.
