﻿# Dossier-REST-API-Contract-example
Dossier API Documentation
Descripción

La API para consultar información de dossiers proporciona un conjunto de endpoints que permiten consultar y filtrar dossiers de acuerdo con varios parámetros, incluyendo fechas, estado, proceso, contribuyente, y más. Además, soporta paginación y ordenación de los resultados.
Información General

    Versión: 1.0.0
    Base URL: https://api.miempresa.com
    Autenticación:
        API Key: X-api-key (en el header)
        Bearer Token: Authorization: Bearer <token>

Endpoints
1. Consulta de Dossiers
GET /dossier/query

Obtiene información sobre los dossiers, con filtros avanzados.
Parámetros de Consulta:
Parámetro	Tipo	Descripción	Requerido	Valores Permitidos
search	string	Cadena opcional para búsqueda.	No	-
start_date	string	Fecha de inicio (formato yyyy-mm-dd).	Sí	-
end_date	string	Fecha de fin (formato yyyy-mm-dd).	Sí	-
status_id	string	ID del estado del dossier.	No	-
process_id	string	ID del proceso relacionado.	No	-
tax_id	string	ID del contribuyente (requerido).	Sí	-
cursor	string	Cursor para paginación.	No	-
cursor_data	string	Datos del cursor para paginación.	No	-
limit	integer	Límite de resultados por página.	No	-
order_field	string	Campo para ordenar los resultados.	No	-
order	string	Ordenamiento ascendente o descendente.	No	asc, desc
Respuesta Exitosa (200 OK):

{
  "last_cursor": "string",
  "data_cursor": "string",
  "count": 10,
  "dossier_list": [
    {
      "id": "string",
      "dossier_number": "string",
      "generation_date": "2024-01-01",
      "document_number": "string",
      "taxpayer": "string",
      "status": "string",
      "process": "string",
      "stage": "string",
      "official_settlements_trds": ["string"],
      "energy_meter_code": "string",
      "total_value": "string"
    }
  ]
}

Respuestas de Error:

    400 Bad Request: Solicitud inválida

{
  "message": "Error de solicitud"
}

    401 Unauthorized: No autorizado

{
  "message": "No autorizado"
}

    403 Forbidden: Acceso denegado

{
  "message": "Acceso denegado"
}

    500 Internal Server Error: Error interno del servidor

{
  "message": "Error interno"
}

Seguridad

La API soporta dos tipos de autenticación:

    API Key: Debes incluir un encabezado X-api-key con tu clave API.
    Bearer Token: Debes incluir un encabezado Authorization con el valor Bearer <token>.

Ejemplo de Solicitud:

curl -X 'GET' \
  'https://api.miempresa.com/dossier/query?start_date=2024-01-01&end_date=2024-12-31&tax_id=1234567890&limit=10' \
  -H 'X-api-key: <tu-api-key>'
