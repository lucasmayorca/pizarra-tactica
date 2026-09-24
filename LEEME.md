# publicar/ — el repo de GitHub Pages

Este directorio **es un repositorio git propio**, separado del proyecto. Sirve una
sola cosa: hostear el reporte en una URL pública.

```
robots.txt                    Disallow: / — que no lo indexen los buscadores
od8adtochf39qt/index.html     el reporte
```

No hay `index.html` en la raíz **a propósito**: quien entre a la raíz recibe un 404.
Solo funciona la ruta completa con el token.

## La URL

```
https://lucasmayorca.github.io/pizarra-tactica/od8adtochf39qt/
```

Es **pública con el link, pero no listada**: cualquiera que lo tenga entra, y no
aparece buscando en Google. No es seguridad — si alguien reenvía el link, entra.
Para el plan de partido contra un rival, alcanza.

**No cambies el nombre del directorio `od8adtochf39qt`** o se rompe el link que ya
compartiste.

## Alta, una sola vez

```bash
cd "$(git rev-parse --show-toplevel 2>/dev/null || pwd)"
gh repo create pizarra-tactica --public --source=. --push
gh api -X POST repos/lucasmayorca/pizarra-tactica/pages \
  -f build_type=legacy -F 'source[branch]=main' -F 'source[path]=/'
```

Tarda uno o dos minutos en estar arriba la primera vez.

## Después, cada vez que haya datos nuevos

Desde `reportes/`:

```bash
./publicar.sh
```

Regenera el reporte desde la base, lo copia acá, commitea y pushea. Si no cambió
nada, no hace commit.

Para otro rival: `./publicar.sh "Munro" "CEPA"` — necesita su YAML en `partidos/`.

## Qué queda público

El repo es público (Pages gratuito lo exige), así que **se ve el HTML del reporte**:
los números del rival, los nombres de sus jugadores y el plan de partido. No se sube
la base, ni las planillas, ni los YAML: solo el archivo generado.
