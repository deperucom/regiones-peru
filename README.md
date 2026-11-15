# Regiones del Perú — API de DePeru.com

Repositorio informativo sobre la información de regiones del Perú publicada por [DePeru.com](https://www.deperu.com) y su endpoint JSON. Reúne la URL del servicio, la estructura observada en la respuesta, las restricciones conocidas y ejemplos sencillos para consultar la información de cada región.

> **Este repositorio no es una API oficial del Estado peruano ni un servicio oficial del gobierno.** Los datos se basan en la información publicada por DePeru.com. La fuente original debe verificarse antes de ser usada en producción o en procesos oficiales.

## Enlaces

- **Infoperu / regiones:** http://www.deperu.com/infoperu/
- **Endpoint JSON:** https://deperu.com/api/rest/regionesPeru.json
- **Contacto DePeru.com:** https://deperu.com/contacto

## ¿Qué ofrece el servicio?

El endpoint devuelve la lista de regiones del Perú con su nombre, slug, capital, código telefónico, ubigeo y enlace a la página de la región. Es útil para crear listados, filtros, mapas y menús de navegación con datos geográficos del país.

### Características conocidas

| Propiedad | Detalle |
| --- | --- |
| Servicio | Regiones del Perú |
| Fuente | DePeru.com |
| Formato observado | JSON |
| Estructura | Lista de regiones |
| Restricción geográfica | Verificar si aplica según el proveedor |
| Límite de solicitudes | No especificado en la información disponible |

## Ejemplo de respuesta

```json
{
  "servicio": "Regiones del Perú",
  "fuente": "DePeru.com",
  "enlace": "http://www.deperu.com/infoperu/",
  "regiones": [
    {
      "nombre": "Amazonas",
      "slug": "amazonas",
      "capital": "Chachapoyas",
      "codigo_telefonico": "041",
      "ubigeo": "01",
      "url": "https://www.deperu.com/infoperu/amazonas/"
    },
    {
      "nombre": "Ancash",
      "slug": "ancash",
      "capital": "Huaraz",
      "codigo_telefonico": "043",
      "ubigeo": "02",
      "url": "https://www.deperu.com/infoperu/ancash/"
    }
  ]
}
```

La respuesta incluye un objeto principal con `servicio`, `fuente`, `enlace` y una lista de regiones en `regiones`. Cada elemento regional tiene nombre, slug, capital, código telefónico, ubigeo y enlace al detalle de la región.

## Identifica tu aplicación con User-Agent

Se recomienda enviar un encabezado `User-Agent` personalizado en las solicitudes. Ejemplo:

```http
User-Agent: dePeru.info_Regiones/1.0
```

Sustituye este valor por tu dominio o nombre de app real. La clave es que el identificador sea claro y oficial para tu proyecto.

## Consulta rápida

Puedes probar el endpoint con `curl`:

```bash
curl --fail --silent --show-error \
  --max-time 10 \
  --user-agent 'dePeru.info_Regiones/1.0' \
  https://deperu.com/api/rest/regionesPeru.json
```

## Recomendaciones de consumo

- Envía un `User-Agent` claro y identificable.
- Valida que la lista `regiones` exista antes de recorrerla.
- Comprueba los campos `ubigeo`, `codigo_telefonico` y `url` antes de mostrarlos o procesarlos.
- Guarda en caché la respuesta si se consulta repetidamente.
- Maneja errores de red, JSON inválido y respuestas HTTP no exitosas.

## Uso responsable y atribución

Al mostrar los datos, conserva una atribución visible a **DePeru.com**. Este repositorio documenta el servicio, pero no concede derechos ni garantiza permanencia o disponibilidad.

## Documentación

- [Guía técnica de uso: cURL, PHP, Python, Node.js y Java](docs/guia-tecnica.md)
- [Descripción del servicio y estructura de la respuesta](docs/servicio.md)
- [Restricciones y buenas prácticas](docs/limitaciones.md)

## Aviso

Este proyecto es informativo y se basa en la estructura observada del endpoint. La API puede cambiar sin previo aviso; confirma siempre con la fuente original antes de depender de ella en producción.
