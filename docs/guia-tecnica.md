# Guía técnica de uso

Esta guía muestra cómo consultar el endpoint desde una aplicación. La URL documentada es:

```text
https://deperu.com/api/rest/regionesPeru.json
```

El servicio devuelve la lista de regiones del Perú con metadata útil. Ejecuta los ejemplos desde un entorno permitido y evita consultas innecesarias.

## User-Agent personalizado

Se recomienda enviar un encabezado `User-Agent` que identifique el dominio o nombre de la aplicación cliente y su versión. Ejemplo:

```http
User-Agent: dePeru.info_Regiones/1.0
```

Reemplaza este valor por tu nombre real de app o dominio.

## cURL

```bash
curl --fail --silent --show-error \
  --max-time 10 \
  --user-agent 'dePeru.info_Regiones/1.0' \
  https://deperu.com/api/rest/regionesPeru.json
```

## Python

```python
import json
from urllib.error import HTTPError, URLError
from urllib.request import Request, urlopen

URL = "https://deperu.com/api/rest/regionesPeru.json"
USER_AGENT = "dePeru.info_Regiones/1.0"

request = Request(
    URL,
    headers={
        "Accept": "application/json",
        "User-Agent": USER_AGENT,
    },
)

try:
    with urlopen(request, timeout=10) as response:
        data = json.loads(response.read().decode("utf-8"))
except HTTPError as error:
    raise SystemExit(f"El servidor respondió HTTP {error.code}") from error
except (URLError, TimeoutError) as error:
    raise SystemExit(f"No se pudo consultar el servicio: {error}") from error
except json.JSONDecodeError as error:
    raise SystemExit(f"La respuesta no contiene JSON válido: {error}") from error

print("Servicio:", data.get("servicio", "sin nombre"))
for region in data.get("regiones", []):
    print(region.get("nombre"), "-", region.get("capital"))
```

## PHP

```php
<?php
$url = 'https://deperu.com/api/rest/regionesPeru.json';
$userAgent = 'dePeru.info_Regiones/1.0';
$curl = curl_init($url);

curl_setopt_array($curl, [
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_CONNECTTIMEOUT => 5,
    CURLOPT_TIMEOUT => 10,
    CURLOPT_USERAGENT => $userAgent,
    CURLOPT_HTTPHEADER => ['Accept: application/json'],
]);

$body = curl_exec($curl);
$status = curl_getinfo($curl, CURLINFO_HTTP_CODE);
$error = curl_error($curl);
curl_close($curl);

if ($body === false) {
    throw new RuntimeException("Error de conexión: {$error}");
}
if ($status < 200 || $status >= 300) {
    throw new RuntimeException("El servidor respondió HTTP {$status}");
}

$data = json_decode($body, true);
if (!is_array($data) || json_last_error() !== JSON_ERROR_NONE) {
    throw new RuntimeException('La respuesta no contiene JSON válido.');
}

printf("Servicio: %s\n", $data['servicio'] ?? 'sin nombre');
foreach (($data['regiones'] ?? []) as $region) {
    printf("%s - %s\n", $region['nombre'] ?? '', $region['capital'] ?? '');
}
```

## Node.js

```js
const url = "https://deperu.com/api/rest/regionesPeru.json";
const userAgent = "dePeru.info_Regiones/1.0";

async function main() {
  let response;
  try {
    response = await fetch(url, {
      headers: {
        Accept: "application/json",
        "User-Agent": userAgent,
      },
      signal: AbortSignal.timeout(10_000),
    });
  } catch (error) {
    throw new Error(`No se pudo consultar el servicio: ${error.message}`);
  }

  if (!response.ok) {
    throw new Error(`El servidor respondió HTTP ${response.status}`);
  }

  let data;
  try {
    data = await response.json();
  } catch {
    throw new Error("La respuesta no contiene JSON válido.");
  }

  console.log(`Servicio: ${data.servicio ?? "sin nombre"}`);
  for (const region of data.regiones ?? []) {
    console.log(`${region.nombre ?? ""} - ${region.capital ?? ""}`);
  }
}

main().catch((error) => {
  console.error(error.message);
  process.exitCode = 1;
});
```

## Java

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.time.Duration;

public class RegionesPeru {
    public static void main(String[] args) throws Exception {
        var client = HttpClient.newBuilder()
                .connectTimeout(Duration.ofSeconds(5))
                .build();
        var request = HttpRequest.newBuilder()
                .uri(URI.create("https://deperu.com/api/rest/regionesPeru.json"))
                .timeout(Duration.ofSeconds(10))
                .header("Accept", "application/json")
                .header("User-Agent", "dePeru.info_Regiones/1.0")
                .GET()
                .build();

        var response = client.send(request, HttpResponse.BodyHandlers.ofString());
        if (response.statusCode() < 200 || response.statusCode() >= 300) {
            throw new IllegalStateException("El servidor respondió HTTP " + response.statusCode());
        }

        System.out.println(response.body());
    }
}
```

## Manejo de respuesta y errores

- Comprueba el código HTTP antes de interpretar el cuerpo.
- Usa timeout para evitar bloqueos indefinidos.
- Valida la presencia de `regiones` y que cada item tenga las propiedades esperadas.
- Usa un `User-Agent` claro y mantenlo consistente con tu app o sitio.

## Frecuencia y caché

Como es una lista relativamente estática, es recomendable consultar la respuesta y almacenarla en caché si la usas en una interfaz web o aplicativa recurrente.
