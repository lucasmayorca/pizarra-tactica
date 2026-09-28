# publicar/ — el repo de GitHub Pages

Este directorio **es un repositorio git propio**, separado del proyecto. Sirve una
sola cosa: hostear el reporte en una URL pública.

```
robots.txt                    Disallow: / — que no lo indexen los buscadores
od8adtochf39qt/index.html     el reporte de PREPARACIÓN (antes de jugar)
3s7vsnpp94j69y/index.html     el RESUMEN del partido jugado
```

**Una ruta por tipo de reporte, y no se pisan.** El previo se sigue leyendo después
de jugar —es contra lo que contrasta el resumen— y su link ya está repartido en el
plantel.

No hay `index.html` en la raíz **a propósito**: quien entre a la raíz recibe un 404.
Solo funciona la ruta completa con el token.

## Las URLs

```
preparación  https://lucasmayorca.github.io/pizarra-tactica/od8adtochf39qt/
resumen      https://lucasmayorca.github.io/pizarra-tactica/3s7vsnpp94j69y/
```

Es **pública con el link, pero no listada**: cualquiera que lo tenga entra, y no
aparece buscando en Google. No es seguridad — si alguien reenvía el link, entra.
Para el plan de partido contra un rival, alcanza.

**No cambies el nombre de los directorios `od8adtochf39qt` ni `3s7vsnpp94j69y`**
o se rompen los links que ya compartiste.

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
./publicar.sh                            # preparación (por defecto Munro vs Banade)
./publicar.sh "Munro" "CEPA"             # preparación, otro rival
./publicar.sh --resumen "Munro" "CyP"    # el resumen del partido ya jugado
```

Regenera el reporte desde la base, lo copia a **su** ruta, commitea y pushea. Si no
cambió nada, no hace commit. El YAML es opcional: sin él, el guion se deriva solo.

## Qué queda público

El repo es público (Pages gratuito lo exige), así que **se ve el HTML del reporte**:
los números del rival, los nombres de sus jugadores y el plan de partido. No se sube
la base, ni las planillas, ni los YAML: solo el archivo generado.
