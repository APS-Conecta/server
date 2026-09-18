<!--
 - SPDX-FileCopyrightText: 2016-2024 Nextcloud GmbH and Nextcloud contributors
 - SPDX-FileCopyrightText: 2013-2016 ownCloud, Inc.
 - SPDX-FileCopyrightText: 2026 APS Conecta contributors
 - SPDX-License-Identifier: AGPL-3.0-or-later
-->
# APS Conecta Gestión — Servidor

**Un fork-mod de Nextcloud 34, a la medida de la Atención Primaria de Salud.**

Este repositorio es el servidor de **APS Conecta Gestión**, la suite de gestión interna para la red de **Atención Primaria de Salud (APS)**. No es una copia sin cambios: es una **bifurcación modificada** — un *fork-mod* de **Nextcloud Server 34** — en la que el motor es upstream y lo propio son las **apps** y la **piel**.

> En una frase: **Nextcloud 34, trasplantado al primer nivel de atención.**

## Qué es el fork-mod, capa por capa

| Capa | Qué es | Dónde vive |
|---|---|---|
| **El motor** | Nextcloud Server 34 — la línea que despliega Gestión (imagen `nextcloud:34-apache`, fijada por digest) | este repositorio |
| **Las apps propias** | Software escrito para el trabajo diario de un establecimiento de APS | un repositorio por app en la organización |
| **La piel** | Tema CSS personalizado `apsconecta` | [`gestion/themes/apsconecta`](https://github.com/APS-Conecta/gestion/tree/main/themes/apsconecta) |

## Las apps propias

- **[epidemiologia](https://github.com/APS-Conecta/epidemiologia)** — vigilancia epidemiológica a la vista del equipo: alertas del MINSAL, informes IRAG y tablero de seguimiento.
- **[territorio](https://github.com/APS-Conecta/territorio)** — el mapa de la comunidad: mapeo territorial y asignación de sectores, sobre un basemap propio de OpenStreetMap (todo Chile, zoom 0–15, autohospedado).
- **[farmacia](https://github.com/APS-Conecta/farmacia)** — el arsenal farmacológico del establecimiento como vademécum, con importación CSV por etapas.

A ellas se suman, ya integradas a la suite, apps de terceros **parcheadas y fijadas por sha256** (Calendar, Contacts, `side_menu`, `groupfolders`, Euro-Office, Talk): una instalación limpia **no contacta la tienda de apps**.

## La piel: tema CSS `apsconecta`

El tema no es un color de acento: es identidad. **Tipografías autohospedadas** (Fraunces + Nunito Sans, sin CDN ni Google Fonts), paleta propia — violeta primario, oro de acento — con su libro de contraste documentado (**AA**), y cobertura hasta la ruta de render *legacy*: mantenimiento, instalación y páginas de error también llevan la marca.

## Por qué un fork

- **Pertinencia.** La APS necesita apps que no existen en ninguna tienda — epidemiología, territorio, vademécum — y una identidad visual propia, no prestada.
- **Determinismo.** Cada byte que un establecimiento ejecuta es verificable: imágenes por digest, apps por sha256, nada se descarga en el camino.
- **Permanencia.** La AGPL permite modificar y obliga a compartir. Lo hacemos con gusto.

## Para quién — y para quién no

Para el **sector de la Atención Primaria de Salud**: el equipo de un CESFAM, PSR, CECOSF, COSAM, SAPU o cualquiera de la red. Cada instalación sirve a **un establecimiento**, nombrado en su propia configuración — el producto no nomina ninguno.

Y el límite, escrito en el frente: **Gestión es operación interna** — documentos, coordinación, chat y oficina. **No es ficha clínica: sin datos de pacientes**, y el desarrollo trabaja solo con datos sintéticos.

## El ecosistema

| Repositorio | Rol |
|---|---|
| **server** (este) | la base: fork-mod de Nextcloud 34 |
| [gestion](https://github.com/APS-Conecta/gestion) | la suite que despliega: Docker Compose + PostgreSQL 18 + Redis 8 + Euro-Office + Talk, config-as-code |
| [epidemiologia](https://github.com/APS-Conecta/epidemiologia) · [territorio](https://github.com/APS-Conecta/territorio) · [farmacia](https://github.com/APS-Conecta/farmacia) | las apps propias |
| [calculadora-ecicep](https://github.com/APS-Conecta/calculadora-ecicep) | motor clínico del calculador de riesgo ECICEP: 52 condiciones crónicas, pesos y códigos CIE-10 |
| [aps-conecta-web](https://github.com/APS-Conecta/aps-conecta-web) | el sitio público de APS Conecta |

## Cómo se despliega

No se despliega desde aquí. Un establecimiento instala un **release** de [gestion](https://github.com/APS-Conecta/gestion) — `git clone --branch vX.Y.Z --depth 1` — y un solo comando (`make install`) levanta la pila, aprovisiona y se autoverifica. `main` es el tronco de desarrollo y no es lo que va a producción.

## Procedencia y licencia

Este repositorio es una bifurcación de trabajo de [`nextcloud/server`](https://github.com/nextcloud/server); la suite parte de su línea 34. El upstream es el autor del motor: nuestro agradecimiento a **Nextcloud GmbH** y su comunidad — y, un escalón atrás en la historia, a **ownCloud, Inc.** Todo el árbol se distribuye bajo **AGPL-3.0-or-later**: motor, apps y tema. Cada archivo conserva sus encabezados SPDX con la autoría original; lo que cambia respecto del upstream se lee en la historia de `git` de este repositorio.

## Soporte y contribución

El soporte de este fork es el de la organización **APS Conecta**, no el de Nextcloud GmbH. Para el motor upstream: [foro](https://help.nextcloud.com) y [documentación](https://docs.nextcloud.com/server). Para el desarrollo propio: empieza por [gestion](https://github.com/APS-Conecta/gestion) y su `CONTRIBUTING.md`.
