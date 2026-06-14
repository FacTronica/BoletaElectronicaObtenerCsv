# 🚀 ERP Factronica API

![Version](https://img.shields.io/badge/version-2026-blue.svg)
![PHP](https://img.shields.io/badge/PHP-5.6%2B-777BB4.svg)
![REST API](https://img.shields.io/badge/API-REST-success.svg)
![License](https://img.shields.io/badge/license-Commercial-red.svg)

## 📌 Descripción

**ERP Factronica API** es una plataforma de integración empresarial diseñada para automatizar procesos administrativos, tributarios, comerciales y operacionales en Chile.

La API permite conectar sistemas ERP, CRM, Ecommerce, aplicaciones móviles, sistemas contables y plataformas externas mediante servicios REST JSON.

Fue desarrollada para integrarse con:

* Servicio de Impuestos Internos (SII Chile)
* Poder Judicial de Chile
* WhatsApp Business
* PrestaShop
* Sistemas Contables
* Sistemas de Remuneraciones
* Aplicaciones Móviles
* Sistemas de Gestión Empresarial

---

# 🎯 Características Principales

### ✅ Arquitectura Multiempresa

Una sola instalación permite operar múltiples empresas de forma independiente.

```text
Cliente
   │
   ▼
API Factronica
   │
   ├── Empresa A
   ├── Empresa B
   ├── Empresa C
   └── Empresa N
```

---

### ✅ Arquitectura de 3 Capas

```text
┌─────────────────────┐
│ Frontend / APP      │
└──────────┬──────────┘
           │ JSON
           ▼
┌─────────────────────┐
│ API REST Factronica │
└──────────┬──────────┘
           │ SQL
           ▼
┌─────────────────────┐
│ Base de Datos       │
└─────────────────────┘
```

---

# 🏗 Estructura del Proyecto

```text
project/
│
├── public/
│   └── index.php
│
├── src/
│   ├── Core/
│   │   ├── Database.php
│   │   ├── Router.php
│   │   └── Config.php
│   │
│   ├── Modules/
│   │   ├── Usuarios/
│   │   ├── Clientes/
│   │   ├── Productos/
│   │   ├── Ventas/
│   │   ├── Compras/
│   │   ├── Tesoreria/
│   │   ├── CRM/
│   │   ├── DTE/
│   │   ├── SII/
│   │   ├── Whatsapp/
│   │   └── Prestashop/
│
├── temp/
├── logs/
├── vendor/
└── autoload.php
```

---

# 🔐 Autenticación

Todas las peticiones requieren Token de Acceso.

```http
Authorization: Bearer TOKEN_API
```

Ejemplo:

```bash
curl -X GET \
https://api.factronica.cl/clientes \
-H "Authorization: Bearer TOKEN_API"
```

---

# 📡 Formato de Peticiones

## Request

```json
{
  "TOKEN":"xxxxxxxx",
  "RUT":"76479984-4"
}
```

## Response

```json
{
  "codigo":"200",
  "estado":"OK",
  "mensaje":"Proceso ejecutado correctamente"
}
```

---

# 📦 Módulos Disponibles

## 👥 Clientes

* Crear Cliente
* Modificar Cliente
* Eliminar Cliente
* Listar Clientes

---

## 📦 Productos

* Crear Producto
* Actualizar Producto
* Inventario
* Stock
* Categorías
* Marcas

---

## 🛒 Ventas

* Cotizaciones
* Pedidos
* Facturas
* Boletas
* Notas de Crédito

---

## 🚚 Compras

* Órdenes de Compra
* Recepción Mercadería
* Facturas de Compra

---

## 💰 Tesorería

* Ingresos
* Egresos
* Recaudaciones
* Conciliación

---

## 👨‍💼 CRM

* Prospectos
* Clientes
* Oportunidades
* Actividades

---

# 🇨🇱 Integración SII Chile

## Funcionalidades

### DTE

* Factura Electrónica
* Factura Exenta
* Nota Crédito
* Nota Débito
* Guía Despacho

### Consulta Tributaria

* F29
* Boletas Electrónicas
* Contribuyentes
* Correo Intercambio

### Autenticación

```json
{
  "RutEmpresa":"76618820-6",
  "Clave":"********"
}
```

Retorna:

```json
{
  "codigo":"200",
  "estado":"OK",
  "token":"TOKEN_SII"
}
```

---

# 🧾 API Boletas Electrónicas

Consulta masiva de boletas emitidas registradas en SII.

## Endpoint

```http
POST /api/sii_herramientas_boletaobtenerlistado
```

## Request

```json
{
  "TOKEN":"TOKEN_API",
  "RUT":"76479984-4",
  "Clave":"CLAVE_SII",
  "Periodo":"202602",
  "CodTipoDoc":"3941"
}
```

## Response

```json
{
  "codigo":"200",
  "estado":"OK",
  "total_boletas":125
}
```

---

# ⚖️ Integración Poder Judicial Chile

Consultas automatizadas.

### Penal

```json
{
  "nombre":"JUAN",
  "paterno":"PEREZ",
  "materno":"SOTO",
  "anio":2025,
  "competencia":"penal"
}
```

### Civil

```json
{
  "nombre":"JUAN",
  "paterno":"PEREZ",
  "materno":"SOTO",
  "anio":2025,
  "competencia":"civil"
}
```

### Ambas

```json
{
  "nombre":"JUAN",
  "paterno":"PEREZ",
  "materno":"SOTO",
  "anio":2025,
  "competencia":"ambas"
}
```

---

# 💬 Integración WhatsApp

Basado en:

* Baileys
* Node.js
* PM2

## Enviar Texto

```json
{
  "fono":"56911111111",
  "mensaje":"Hola Mundo"
}
```

## Enviar Archivo

```json
{
  "fono":"56911111111",
  "archivo":"documento.pdf"
}
```

---

# 🛍 Integración PrestaShop

Funciones soportadas:

* Sincronización Productos
* Categorías
* Marcas
* Stock
* Pedidos
* Clientes

ERP Factronica actúa como:

```text
MAESTRO DE DATOS
```

PrestaShop consume información desde el ERP.

---

# 🌐 Ejemplo PHP

```php
$payload = array(
    "TOKEN" => "TOKEN_API",
    "RUT" => "76479984-4"
);

$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($payload));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    "Content-Type: application/json"
));

$response = curl_exec($ch);
curl_close($ch);

echo $response;
```

---

# ⚙️ Requisitos

## Servidor

* Debian 12+
* Apache 2.4+
* PHP 5.6+
* MariaDB 10+
* OpenSSL
* CURL
* JSON

---

# 🔒 Seguridad

* Bearer Token
* Validación de IP
* HTTPS obligatorio
* Logs de Auditoría
* Control de Sesiones

---

# 📈 Casos de Uso

### ERP

* Ventas
* Compras
* Inventario

### Contabilidad

* Registro automático de documentos

### Ecommerce

* Sincronización PrestaShop

### Integradores

* Consumo REST JSON

### Auditoría

* Validación ERP vs SII

---

# 👨‍💻 Soporte

**Factronica ERP**

📧 [contacto@factronica.cl](mailto:contacto@factronica.cl)

🌐 https://www.factronica.cl

📱 +56 9 2621 3032

---

# 📄 Licencia

Software Comercial.

Todos los derechos reservados.

© Factronica ERP 2014 - 2026
