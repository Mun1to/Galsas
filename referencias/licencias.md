# Licencias: qué te has metido dentro del producto

> **Última verificación de este documento: 14 de agosto de 2026.**
> Las licencias envejecen mejor que las leyes, pero **un paquete puede cambiar de licencia entre dos
> versiones** (ha pasado con proyectos grandes). Se escanea la versión instalada, no la recordada.

La pregunta que responde este módulo es una sola: **¿puedo distribuir y cobrar por esto tal como
está?** Y la respuesta no está en el `LICENSE` de la raíz, está en el árbol de dependencias.

## Escanear, por ecosistema

Lo primero es la lista real de licencias de lo instalado. Con `--prod` cuando el objetivo es lo que
se distribuye: las dependencias de desarrollo no viajan dentro del binario, y meterlas en el informe
solo genera ruido.

| Ecosistema | Comando | Nota |
|---|---|---|
| pnpm | `pnpm licenses list --prod --json` | Integrado, no hay que instalar nada |
| npm | `npx license-checker --production --summary` | Descarga la herramienta al vuelo |
| Rust / Cargo | `cargo install cargo-license && cargo license` | Alternativa sin instalar: `cargo metadata --format-version 1` y leer el campo `license` de cada paquete |
| Rust, auditoría seria | `cargo install cargo-deny && cargo deny check licenses` | Permite una política escrita en `deny.toml`, que es lo que se quiere a largo plazo |
| Python | `pip install pip-licenses && pip-licenses --format=markdown` | Sin instalar nada: `pip show <paquete>` uno a uno |
| Go | `go install github.com/google/go-licenses@latest && go-licenses report ./...` | |

**Comprueba que el comando existe antes de prometerlo en el informe.** Si la herramienta no está
instalada, dilo y ofrece el fallback; no des por hecho un resultado que no has ejecutado.

Lo que hay que mirar en el resultado, por este orden:

1. Todo lo que sea **GPL, AGPL, SSPL, BUSL, Elastic, CC-BY-NC** o "custom".
2. Todo lo que salga **`UNKNOWN`, `UNLICENSED`, vacío o "SEE LICENSE IN..."**. Esto es tan grave como
   una GPL y se ignora mucho más.
3. Los paquetes con **licencia dual** (`MIT OR Apache-2.0`): eliges tú, y conviene dejar escrito cuál.

## Las familias, y qué te dejan hacer

| Familia | Licencias típicas | En un producto comercial cerrado |
|---|---|---|
| **Permisiva** | MIT, ISC, BSD-2, BSD-3, Apache-2.0, 0BSD, Unlicense | ✅ Sí. Obliga a **conservar el aviso de copyright y la licencia**, cosa que casi nadie hace |
| **Copyleft débil** | MPL-2.0, LGPL-2.1, LGPL-3.0, EPL-2.0 | ⚠️ Sí, con condiciones. Lo modificado **de esos archivos** se libera; el resto de tu producto no |
| **Copyleft fuerte** | GPL-2.0, GPL-3.0 | ⛔ Si **distribuyes** el binario, el conjunto se distribuye bajo GPL. Uso interno sin distribuir, no dispara la obligación |
| **Copyleft de red** | AGPL-3.0 | ⛔ Además, ofrecerlo **como servicio por red** ya cuenta: hay que dar el fuente a los usuarios del servicio |
| **Fuente disponible, no libre** | SSPL, BUSL-1.1, Elastic 2.0, PolyForm | ⚠️ No son open source. Suelen prohibir ofrecer el producto como servicio competidor. **Se leen enteras**, son cortas |
| **No comercial** | CC-BY-NC, CC-BY-NC-SA | ⛔ En un producto que cobra, no |
| **Sin licencia** | ausencia de `LICENSE`, `UNLICENSED` | ⛔ Sin licencia no hay permiso: por defecto son **todos los derechos reservados** |

### Apache-2.0, dos detalles que se saltan siempre
Trae **concesión expresa de patentes** (bueno para ti) con cláusula de represalia, y su sección 4
obliga a **propagar el archivo `NOTICE`** si el paquete lo trae. Y una incompatibilidad clásica:
Apache-2.0 **no es compatible con GPL-2.0** en el mismo binario (sí con GPL-3.0).

## Las cinco trampas de verdad

**1. Rust y el enlazado estático.** Cargo enlaza **estáticamente** por defecto. La LGPL se apoya en
que el usuario pueda sustituir la biblioteca, algo que el enlazado dinámico da gratis y el estático
no. Una LGPL enlazada estáticamente dentro de un binario cerrado es un problema real, no teórico.
Aplica igual a cualquier binario compilado, Go incluido.

**2. AGPL y el producto en la nube.** Es la que pilla a los productos SaaS: no hace falta distribuir
nada, basta con que la gente lo use por la red. Si el modelo de negocio es "lo mismo pero cómodo y en
la nube", una AGPL dentro obliga a publicar el fuente del servicio.

**3. Pegar código, no solo instalar paquetes.** Copiar treinta líneas de un repositorio GPL a tu
producto lo contamina exactamente igual que añadir la dependencia, y no aparece en ningún escaneo.
La norma sana: se guarda **el patrón y el enlace**, no el código. Vale también para el código que
sugiere un asistente de IA cuando reproduce un fragmento reconocible de un proyecto con licencia.

**4. Los assets no son código, y tienen su propio régimen.** Fuentes tipográficas (OFL suele exigir
que la fuente derivada no se venda suelta), iconos, ilustraciones, **música de fondo de un vídeo**,
fotografías de banco. Una pista musical mal licenciada en un vídeo de lanzamiento da más disgustos
que cualquier dependencia, porque la reclamación llega automática desde la plataforma.

**5. Los pesos de un modelo de IA no son software libre por defecto.** Muchos modelos "abiertos" se
publican bajo licencias propias (comunitarias, con límites de usuarios, con restricciones de uso o
prohibiendo entrenar otros modelos con sus salidas). Si el producto **empaqueta o descarga** un
modelo, su licencia va en el informe igual que una dependencia.

## Lo que el escaneo no ve, y hay que preguntar

- **Una licencia permisiva en el core no protege la edición de pago.** Si el código público es MIT,
  cualquiera puede compilarlo y montar su propia versión cómoda. Es un modelo perfectamente válido
  (se vende la comodidad y el servicio, no el código), pero tiene que ser una decisión tomada a
  sabiendas, no un descubrimiento.
- **Si hay una edición cerrada encima del núcleo abierto**, cualquier auditoría pública audita el
  repositorio, no el binario que ejecuta el cliente. No se puede insinuar lo contrario.
- **Marca y nombre no son licencia.** Que el código sea libre no autoriza a usar el nombre ni el
  logotipo del proyecto original para vender el tuyo.

## Qué se entrega

1. La sección de licencias del `LEGAL.md`: **solo lo que está mal o pide decisión**, no el listado
   completo de 900 paquetes.
2. Un `THIRD-PARTY.md` (o `NOTICE`) con las atribuciones, generado del escaneo. Es la parte de MIT y
   BSD que todo el mundo incumple sin enterarse, y arreglarla es un comando.
3. Si el proyecto es en Rust o va a durar: un `deny.toml` con la política escrita, para que el
   siguiente paquete problemático lo pare la máquina y no una auditoría dentro de un año.
