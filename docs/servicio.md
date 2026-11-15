# Descripción del servicio

## Resumen

El servicio documentado devuelve la lista de regiones del Perú con información útil para cada una: nombre, slug, capital, código telefónico, ubigeo y enlace al detalle regional. La estructura se observa como un objeto con `servicio`, `fuente`, `enlace` y una colección `regiones`.

## Enlaces

- Infoperu: http://www.deperu.com/infoperu/
- Endpoint: https://deperu.com/api/rest/regionesPeru.json
- Contacto: https://deperu.com/contacto

## Propiedades conocidas

- Nombre: Regiones del Perú
- Fuente: DePeru.com
- Formato observado: JSON
- Estructura: `servicio` + `fuente` + `enlace` + `regiones[]`

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
    }
  ]
}
```

## Estructura observada

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `servicio` | Cadena | Nombre del servicio |
| `fuente` | Cadena | Fuente de datos |
| `enlace` | Cadena | Enlace a la sección de información |
| `regiones` | Lista | Colección de objetos regionales |
| `nombre` | Cadena | Nombre de la región |
| `slug` | Cadena | Identificador amigable |
| `capital` | Cadena | Capital regional |
| `codigo_telefonico` | Cadena | Código telefónico |
| `ubigeo` | Cadena | Código ubigeo |
| `url` | Cadena | URL del detalle regional |

## Consideraciones

- Revisa siempre la estructura antes de usarla en una app.
- La lista puede variar o actualizarse según DePeru.com.
- Para un despliegue de producción, considera usar caché y validaciones adicionales.
