# Marcado de IA: el artículo 50 del AI Act

> **Última verificación de este documento: 14 de agosto de 2026.** Si hoy han pasado más de seis
> meses, reverifica las fechas antes de afirmarlas. Fuentes en `fuentes.md`.

El Reglamento (UE) 2024/1689 tiene más de cien artículos y **casi todos son para otros**: para quien
entrena modelos grandes o para quien construye sistemas que deciden sobre la vida de la gente. Si el
producto conversa o genera contenido, **el artículo que aplica es el 50**, y son dos páginas.

**Está en vigor desde el 2 de agosto de 2026.** Hay periodo de gracia hasta el **2 de diciembre de
2026**, y solo para una cosa: la obligación de marcado del art. 50.2 en sistemas que ya estaban en
el mercado antes del 2 de agosto. Todo lo demás es exigible ya.

⚠️ **Dato que hay que comprobar en cada auditoría:** el *Digital Omnibus* sobre IA entró en vigor el
27 de julio de 2026 y **modificó el artículo 50**. El AI Act Service Desk de la Comisión avisa en su
propia página de que el texto que muestra todavía no refleja esas enmiendas. Lee la **versión
consolidada en EUR-Lex** antes de dar por buena cualquier redacción, incluida esta.

## Primero: ¿proveedor o responsable del despliegue?

Cambia lo que toca hacer, así que se decide antes de nada.

| | Quién es | Qué le obliga |
|---|---|---|
| **Proveedor** | Desarrolla el sistema y lo pone en el mercado bajo su nombre o marca | Párrafos **1 y 2**: avisar de que es una IA, y marcar la salida generada |
| **Responsable del despliegue** | Usa el sistema bajo su propia autoridad, en su producto o negocio | Párrafos **3 y 4**: informar en biometría, y revelar ultrafalsos y textos de interés público |

Construir sobre la API de otro **no te convierte automáticamente en proveedor**, pero tampoco te
libra: puedes ser las dos cosas según el caso. La Comisión publicó directrices sobre transparencia
que explican quién es quién; se miran antes de concluir.

## Las reglas rápidas

| Si el producto... | Entonces... | Base |
|---|---|---|
| Conversa con personas | Avisa de que es una IA, **salvo que sea evidente** | Art. 50.1 |
| Genera imagen, audio, vídeo o texto | Marca la salida **en formato legible por máquina** | Art. 50.2 |
| Solo asiste a editar, o no cambia el fondo de lo que le das | **No hay que marcar nada** | Art. 50.2 |
| Genera ultrafalsos (personas, lugares o hechos realistas) | Revela que es generado o manipulado | Art. 50.4 |
| Publica textos de interés público sin revisión humana | Revela que es generado por IA | Art. 50.4 |
| Publica esos textos **con** revisión humana que firma | **No hay que revelar nada** | Art. 50.4 |
| Detecta emociones o clasifica biometría | Informa a las personas expuestas | Art. 50.3 |
| Decide sobre personas (crédito, empleo, sanidad) | Alto riesgo, otro capítulo entero, **abogado** | Cap. III |

**Cuándo se informa:** de forma clara y distinguible, **a más tardar en la primera interacción o
exposición**, y de forma **accesible**. Ese último detalle casi nadie lo menciona: el aviso de IA
también tiene que cumplir requisitos de accesibilidad.

## Las exenciones, que es la parte que más ahorra

Están en el propio artículo 50 y ningún resumen las cuenta bien, porque no venden tanto como el
titular de la multa.

**1. Cuando es evidente que es una IA.** El aviso del chatbot no aplica si resulta obvio para una
persona razonablemente informada, observadora y prudente, según el contexto de uso.
→ *En la práctica:* aun así, ponlo. Es una línea de texto y te quita la discusión sobre si era
"evidente".

**2. Cuando solo asistes a editar, o no alteras el fondo.** No hay obligación de marcar si el sistema
hace una **función asistencial de edición estándar** o **no altera sustancialmente los datos de
entrada del usuario ni su semántica**.
→ *Esta es la exención grande para las herramientas.* Un corrector, un autocompletado, un ajuste de
formato o una **transcripción fiel** de lo que alguien dictó no generan contenido sintético: ayudan
a editar lo que ya había. En cuanto la herramienta **redacta, resume o reescribe cambiando el
significado**, sale de la exención y vuelve la obligación de marcar.

**3. Cuando es obra artística, creativa, satírica o de ficción.** La obligación se limita a revelar
que ese contenido existe, de forma que no estropee la exhibición ni el disfrute de la obra. No te
obligan a estampar una marca encima de un plano de tu cortometraje: basta con decirlo en los
créditos o en la descripción.

**4. Cuando un humano revisa y firma.** En textos de interés público, no hay que revelar nada si ha
habido revisión humana o control editorial y alguien asume la responsabilidad editorial.
→ *Además de eximir, es el mejor flujo de trabajo: la IA propone, la persona revisa y firma.*

Hay una quinta transversal, para sistemas autorizados por ley para detectar o perseguir delitos.
Salvo que trabajes con fuerzas de seguridad, no es tu caso.

## Qué se escribe en el código

Esto no interpreta ninguna ley: es ingeniería, y es lo que hace que cumplir salga barato.

1. **Un solo punto de salida.** Todo el contenido generado sale por una única función. Ahí se
   enchufa después la firma, la marca de agua o el registro sin tocar el resto del producto.
2. **El aviso de IA, dentro del componente**, no en los términos ni en el pie de página.
3. **Dos capas de marcado cuando se genere contenido publicable:** una etiqueta que ve una persona y
   una marca que lee una máquina. Los metadatos solos no bastan, y no por interpretación legal sino
   por un hecho técnico: **las redes sociales los borran al subir el archivo**. El propio Código de
   Buenas Prácticas de la UE ya lo dice.
4. **Registro de qué modelo generó qué y cuándo.** Modelo, versión, marca de tiempo.
5. **Si el producto despliega agentes que actúan solos:** identidad propia por agente en vez de una
   credencial compartida, y registro de quién autorizó qué. Hoy no lo obliga nadie en la UE, pero un
   agente que mueve dinero o toca sistemas ajenos se acerca al alto riesgo, y montarlo así desde el
   principio cuesta cero frente a reescribirlo después.

## Firmar con C2PA, en la práctica

- La herramienta es **`c2patool`**, de línea de comandos. Photoshop y Lightroom lo llevan de serie.
- **Hay capa gratuita**: SSL.com anuncia un certificado de firma de nivel 1 válido un año y 10.000
  sellos de tiempo anuales, exigiendo un ID de registro de conformidad C2PA. El precio del nivel de
  pago no lo publican, así que **cualquier cifra concreta que leas por ahí es un bulo hasta que la
  veas en su web**.
- La lista de confianza provisional **se congeló el 1 de enero de 2026**: lo firmado con la vieja
  puede no validar.
- ⚠️ Los validadores, `c2patool` incluido, **no comprueban revocación por defecto**.

Un manifiesto C2PA útil lleva: acción `c2pa.ai.generated`, modelo y versión, certificado de la
organización, sello de tiempo RFC-3161 y hash del contenido.

**Lo caro se puede aparcar con criterio.** El marcado invisible en la señal (píxeles, ondas, patrones
en el texto) y la batería de pruebas de robustez son proyecto de meses. La regla razonable: la firma
y la etiqueta visible se hacen ya porque son baratas; el *watermarking* invisible se abre cuando haya
usuarios europeos reales.

## Si el producto vende a Estados Unidos

El marco de referencia es el **NIST AI RMF** (26 de enero de 2023), voluntario, con cuatro funciones:
Govern, Map, Measure, Manage. Varias leyes estatales lo toman como referencia, pero **cuidado con la
idea de que "cumplir el NIST te da puerto seguro"**: donde existe algo así, el mecanismo real es más
estrecho y nombra un perfil concreto del marco.

## Bulos frecuentes, para no repetirlos

1. "La Ley de Accesibilidad obliga a que cualquier web sea accesible." Cubre una lista cerrada.
2. "Cualquier chatbot cae bajo la SB 243 de California." Su texto excluye expresamente los bots de
   atención al cliente, las funciones de videojuego y los asistentes de voz independientes.
3. "Un certificado C2PA cuesta 289 dólares." El proveedor no publica ese precio.
4. "El Digital Omnibus retrasó el artículo 50." Retrasó el **alto riesgo**; el 50 aplica desde el 2
   de agosto de 2026, aunque sí lo modificó (ver el aviso de arriba).

**De los bulos que circulan, la inmensa mayoría hacen la ley MÁS amplia de lo que es.** Ese es el
sesgo del sector: los resúmenes exageran para asustar. Por eso aquí se prefiere quedarse corto y
enlazar.
