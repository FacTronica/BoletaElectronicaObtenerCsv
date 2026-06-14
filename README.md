# 🚀 API Obtener Listado de Boletas Electrónicas Emitidas

![Factronica API](https://img.shields.io/badge/API-Factronica-blue)
![JSON](https://img.shields.io/badge/Formato-JSON-success)
![CSV](https://img.shields.io/badge/Exportación-CSV-orange)
![SII Chile](https://img.shields.io/badge/SII-Chile-red)

## 📖 Descripción

La API **Obtener Listado de Boletas Electrónicas Emitidas** permite consultar desde SII Chile el listado de boletas electrónicas emitidas por una empresa para un período determinado.

La consulta requiere:

- Token de acceso API
- RUT empresa
- Clave SII empresa
- Período (AñoMes)
- Tipo de documento

### Características

- ✅ Consulta automática al SII
- ✅ No requiere certificado digital
- ✅ Retorna resultados en JSON
- ✅ Genera archivo CSV descargable
- ✅ Compatible con integraciones ERP, Contabilidad y Auditoría
- ✅ Ideal para conciliación de información entre sistemas internos y SII

---

# 📑 Documentos Soportados

| Tipo DTE | Documento |
|-----------|------------|
| 39 | Boleta Electrónica Afecta |
| 41 | Boleta Electrónica Exenta |

---

# 🔄 Flujo de Integración

```text
1. Crear petición JSON
        ↓
2. Enviar solicitud al Endpoint
        ↓
3. Recibir respuesta JSON
        ↓
4. (Opcional) Descargar CSV generado
```

---

# 🌐 Endpoint

```http
POST https://dev.factronica.cl/api/sii_herramientas_boletaobtenerlistado/index.php
```

---

# 📥 Petición

## JSON de Entrada

```json
{
    "TOKEN": "-token-acceso-api-",
    "RUT": "-rut-empresa-",
    "Clave": "-aqui-clave-sii-empresa",
    "Periodo": "202602",
    "CodTipoDoc": "3941"
}
```

### Parámetros

| Campo | Tipo | Descripción |
|---------|---------|-------------|
| TOKEN | String | Token de acceso API |
| RUT | String | RUT empresa |
| Clave | String | Clave SII empresa |
| Periodo | String | AñoMes (YYYYMM) |
| CodTipoDoc | String | Tipo documento a consultar |

---

# 💻 Ejemplo CURL

```bash
curl -X POST "https://dev.factronica.cl/api/sii_herramientas_boletaobtenerlistado/index.php" \
-H "Content-Type: application/json" \
-d '{
    "TOKEN":"-token-acceso-api-",
    "RUT":"-rut-empresa-",
    "Clave":"-aqui-clave-sii-empresa",
    "Periodo":"202602",
    "CodTipoDoc":"3941"
}'
```

---

# 📂 Envío desde Archivo TXT

Guardar el JSON en un archivo:

```txt
datos_json.txt
```

Luego ejecutar:

```bash
curl -X POST "https://dev.factronica.cl/api/sii_herramientas_boletaobtenerlistado/index.php" \
-H "Content-Type: application/json" \
-d @datos_json.txt
```

---

# 📤 Respuesta Exitosa

```json
{
  "codigo": "200",
  "estado": "OK",
  "total_boletas": 4,
  "boletas": [
    {
      "item": 1,
      "tipo_doc": "39",
      "rut_receptor": "66666666-6",
      "fecha_documento": "02/02/2026",
      "folio": "535",
      "monto_neto": 28000,
      "monto_iva": 5320,
      "monto_exento": 0,
      "monto_total": 33320
    }
  ],
  "totales": {
    "monto_neto": 728997,
    "monto_iva": 138510,
    "monto_exento": 0,
    "monto_total": 867507
  },
  "csv_temp": {
    "generado": true,
    "nombre_archivo": "boletas_400507138.csv",
    "url_public": "https://dev.factronica.cl/temp/boletas_400507138.csv"
  }
}
```

---

# 📊 Estructura de Respuesta

## Datos Generales

| Campo | Descripción |
|---------|-------------|
| codigo | Código de resultado |
| estado | Estado de la operación |
| total_boletas | Cantidad de registros encontrados |

## Totales

| Campo | Descripción |
|---------|-------------|
| monto_neto | Total neto período |
| monto_iva | Total IVA período |
| monto_exento | Total exento período |
| monto_total | Total general período |

---

# 📥 Descarga de CSV

Si la respuesta contiene:

```json
"url_public":"https://dev.factronica.cl/temp/boletas_400507138.csv"
```

Puede descargar el archivo utilizando:

```bash
curl -L "https://dev.factronica.cl/temp/boletas_400507138.csv" \
-o boletas_400507138.csv
```

---

# 📄 Formato CSV

```csv
Tipo Doc;RUT Receptor;Fecha Docto;Fecha Venc.;Indicador Servicio;Folio;Monto Neto;Monto IVA;Monto Exento;Monto Total
39;66666666-6;02/02/2026;;3;535;28000;5320;0;33320
39;66666666-6;12/02/2026;;3;536;57198;10868;0;68066
39;66666666-6;16/02/2026;;3;537;313590;59582;0;373172
39;66666666-6;18/02/2026;;3;538;330209;62740;0;392949
```

---

# 🎯 Casos de Uso

- Validación de información entre ERP y SII.
- Auditorías tributarias.
- Integración con sistemas contables.
- Carga masiva de boletas.
- Procesos automáticos de conciliación.
- Control y revisión de documentos electrónicos.

---

# 👥 Público Objetivo

- Integradores de Sistemas
- Desarrolladores de Software
- Contadores
- Auditores
- Empresas PyME
- Plataformas ERP

---

# ⚡ Ventajas

- Sin certificado digital.
- Integración simple mediante JSON.
- Respuesta estructurada.
- Descarga CSV incluida.
- Automatización completa del proceso.
- Ideal para soluciones SaaS y ERP.

---

## © Factronica API

Documentación técnica generada a partir del endpoint **Obtener Listado de Boletas Electrónicas Emitidas**.
