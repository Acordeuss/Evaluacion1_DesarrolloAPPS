# ⚓ AquaCheck - Buceo Seguro Acuícola

Aplicación móvil Android (*offline-first*) para digitalizar listas de chequeo (DPR-24), evaluar la salud preventiva de buzos y controlar riesgos (AST) en faenas marítimas.

---

## 🎨 Identidad Visual

* **Modo Oscuro:** `#121212` (Fondo general)
* **Color Principal:** `#6B21A8` (Morado Neón)
* **Color Secundario:** `#1E40AF` (Azul Tech)
* **Texto:** `#FFFFFF` (Alto contraste)

---

## 🔄 Flujo de Usuario (UML)

```mermaid
stateDiagram-v2
    [*] --> Login
    Login --> Dashboard: Credenciales Válidas
    
    state Dashboard {
        [*] --> Opciones
        Opciones --> Historial: Consultar
        Opciones --> PreChequeo: Iniciar
    }
    
    Historial --> Dashboard: Volver
    PreChequeo --> AST --> ChecklistDPR24 --> RegistroSalud --> Evidencias --> Dictamen
    
    state Dictamen {
        [*] --> Algoritmo
        state Validacion <<choice>>
        Algoritmo --> Validacion
        Validacion --> Apto: Sin desvíos
        Validacion --> NoApto: Con hallazgos/alteraciones
    }
    
    Dictamen --> GuardarBD: Almacenar Local
    GuardarBD --> Dashboard
