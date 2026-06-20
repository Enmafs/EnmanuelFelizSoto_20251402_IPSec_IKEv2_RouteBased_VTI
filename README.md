# 🔐 Lab 03 — IPSec IKEv2 — Route-Based (VTI)

**Estudiante:** Enmanuel Feliz Soto | **Matrícula:** 2025-1402  
**Institución:** Instituto Tecnológico de Las Américas (ITLA)  
**Curso:** Seguridad en Redes | **Sección:** 5  
**Docente:** Jonathan Esteban Rondón Corniel

---

## 📋 Descripción

VPN basada en rutas usando VTI. Más flexible que Policy-Based, permite routing dinámico sobre el túnel.

| Campo | Valor |
|-------|-------|
| **Tipo de VPN** | Site-to-Site |
| **Protocolo** | IKEv2 + IPSec ESP-AES256-SHA256 |
| **Mecanismo** | Static VTI (Virtual Tunnel Interface) + Rutas Estáticas |
| **Routing** | Rutas estáticas apuntando a Tunnel0 |
| **Pre-shared Key** | `Cisco2025-1402-VTI!` |

---

## 🗺️ Topología

> 📸 **[INSERTAR CAPTURA DE TOPOLOGÍA AQUÍ]**

<!-- Coloca aquí el screenshot de PNetLab con la topología del Lab 02 -->

**Entorno:** PNetLab — Cisco IOL  
**Peers:** R1-S1 (20.25.2.2) ↔ R4-S2 (20.25.2.6)

### Tabla de Direccionamiento

| **Router** | **Rol** | **IP WAN** | **Interfaz WAN** | **IP LAN** | **Interfaz LAN** | **IP VPN** | **Interfaz VPN** |
|------------|---------|------------|------------------|------------|------------------|------------|------------------|
| R2    | Peer 1   / Iniciador | 20.25.2.6 | Ethernet0/0 | 30.30.30.1/24 | Ethernet0/1 | 14.2.10.1 | Tunnel0 |
| R5    | Peer 2 / Respondedor | 20.25.1.10| Ethernet0/0 | -- | Ethernet0/1 | 14.2.10.2 | Tunnel0 |
| R5    | -- | -- | -- | 10.10.10.1/24 | Ethernet0/1.10 | -- | -- |
| R5    | -- | -- | -- | 20.20.20.1/24 | Ethernet0/1.20 | -- | -- |


### ISP

| Interfaz ISP | IP | Descripción |
|-------------|-----|-------------|
| Ethernet0/0 | 20.25.1.1/30 | Link to R1-S1 |
| Ethernet0/1 | 20.25.1.5/30 | Link to R4-S2 |
| Ethernet0/2 | 20.25.1.9/30 | Link to R5    |

### Dirección Túnel
| Endpoint | IP Tunnel |
|----------|-----------|
| R1-S1 Tunnel0 | 14.2.10.1/30 |
| R4-S2 Tunnel0 | 14.2.10.2/30 |

---

## ⚙️ Configuración

El script completo de configuración se encuentra en:  
📄 [`EnmanuelFelizSoto_2025-1402_IPSec_IKEv2_RouteBased_VTI_P3.txt`](./EnmanuelFelizSoto_2025-1402_IPSec_IKEv2_RouteBased_VTI_P3.txt)

### Parámetros IKE/IPSec

| Parámetro | Valor |
|-----------|-------|
| Encryption | AES-256 |
| Hash/Integrity | SHA-256 |
| DH Group | 14 (2048-bit) |
| SA Lifetime (IKE) | 86400 s (24h) |
| SA Lifetime (IPSec) | 3600 s (1h) |
| PFS | Group 14 |
| Auth Method | Pre-Shared Key |

---

## ▶️ Procedimiento de Ejecución

### 1. Cargar configuración en PNetLab
```
# Aplicar configuración en cada dispositivo en el orden:
# 1. ISP → 2. R1-S1 → 3. R2 → 4. R5
```

### 2. Verificar la VPN

```
show crypto isakmp sa
```
```
show crypto ipsec sa
```
```
show interface Tunnel0
```

### 3. Prueba de conectividad
```
ping 14.2.10.2 source 14.2.10.1
```

---

## 📸 Capturas de Verificación

> 📸 **[INSERTAR CAPTURA: show crypto isakmp sa]**

<!-- Captura mostrando el estado QM_IDLE / ESTABLISHED -->

> 📸 **[INSERTAR CAPTURA: show crypto ipsec sa]**

<!-- Captura mostrando pkts encaps/decaps incrementando -->

> 📸 **[INSERTAR CAPTURA: ping exitoso]**

<!-- Captura del ping source 10.14.11.0/24 -->

---

## 🔍 Análisis y Comparativa

### Ventajas de este tipo de VPN
- Ver documentación técnica en el informe PDF

### Diferencias con otros labs
- Ver tabla comparativa en el README principal

---

## 📎 Recursos

| Recurso | Enlace |
|---------|--------|
| Repositorio Principal | [Enmafs/NetSec](https://github.com/Enmafs/NetSec) |
| Script de configuración | [`EnmanuelFelizSoto_2025-1402_IPSec_IKEv2_RouteBased_VTI_P3.txt`](./EnmanuelFelizSoto_2025-1402_IPSec_IKEv2_RouteBased_VTI_P3.txt) |
| Video demostración | 🎬 **Pendiente** |

---

> ⚠️ *Laboratorio realizado en entorno controlado (PNetLab). Fines exclusivamente académicos.*
