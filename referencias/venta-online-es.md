# Vender a consumidores (España / UE)

> **Última verificación de este documento: 14 de agosto de 2026**, sobre texto consolidado del BOE y
> EUR-Lex. Enlaces en `fuentes.md`.

Aplica cuando el producto **cobra a personas físicas** (consumidores). Vender solo a empresas cambia
casi todo lo de aquí: el derecho de consumo no aplica igual, y eso también es un hallazgo que hay que
escribir en el informe.

Una decisión previa que ordena el resto: **¿se cobra directamente o a través de un *merchant of
record*?** Plataformas tipo Paddle o Lemon Squeezy venden en su nombre y asumen el IVA por país; con
Stripe u otra pasarela pura, **el vendedor eres tú** y todas las obligaciones fiscales y de consumo
son tuyas.

## 1. Información precontractual: art. 97.1 TRLGDCU

Antes de que el consumidor quede vinculado hay que dar, de forma clara y comprensible, una lista
larga. Las que más se incumplen en software:

| Letra | Contenido | Fallo típico |
|---|---|---|
| b) | Identidad del empresario, **incluido nombre comercial** | Solo aparece la marca, no quién factura |
| c) | Dirección completa, teléfono y correo | Solo un formulario de contacto |
| e) | **Precio total con impuestos** y cualquier gasto añadido | Precio sin IVA en la página de precios |
| f) | Si el precio se ha **personalizado con decisiones automatizadas**, y con qué parámetros | Descuentos por segmento sin decirlo |
| h) | Procedimientos de pago y ejecución, y **cuándo se entrega** | |
| j) k) l) m) | **Desistimiento**: condiciones, plazo, procedimiento, formulario y cuándo no lo hay | Ver punto 3 |
| n) | **Recordatorio de la garantía legal de conformidad** | Casi nunca está |
| p) | Duración y resolución del contrato; en contratos con **renovación automática**, avisar **15 días antes** de que venza el plazo para no renovar | Suscripción que se renueva sin aviso |

Esa información **forma parte del contrato** (art. 97.5) y **la carga de la prueba de haberla dado es
del empresario** (art. 97.8). Traducción técnica: guarda versionado el texto legal que había
publicado en cada momento.

## 2. El botón de pago: art. 98.2 TRLGDCU

El botón que cierra el pedido debe estar etiquetado de forma fácilmente legible **únicamente** con
"pedido con obligación de pago" o una fórmula análoga inequívoca.

**La sanción no es una multa: es que el pedido no vincula al consumidor.** Es la consecuencia más
dura de todo este bloque y se arregla cambiando una cadena de texto.

- Etiquetas que cumplen: "Pagar ahora", "Pagar pedido", "Realizar el pedido con obligación de pago".
- Etiquetas de riesgo: "Continuar", "Finalizar", "Confirmar", "Empezar".
- **Se comprueba en producción y en cada idioma**, no en el código fuente.

## 3. Derecho de desistimiento: arts. 102 a 108 TRLGDCU

**14 días naturales**, sin motivo. En venta de bienes cuentan desde que se recibe el producto.

**Si no se informa del desistimiento, el plazo se alarga 12 meses más** (art. 105.1) y el consumidor
no responde de la disminución de valor (art. 108.2). Si no se informa de que el coste de devolución
lo paga él, **lo paga el vendedor** (arts. 108.1 y 97.6). Reembolso en **14 días naturales** desde
que se comunica el desistimiento, por el mismo medio de pago (art. 107.1).

**El formulario de desistimiento hay que publicarlo**, descargable, y adjuntarlo o enlazarlo en el
correo de confirmación. Ojo con la numeración, que casi todas las plantillas tienen mal: hoy es el
**Anexo I, letras A y B** del TRLGDCU, no "Anexo A / Anexo B".

### El botón de desistimiento online: art. 11 bis de la Directiva 2011/83/UE

Lo añadió la [Directiva (UE) 2023/2673](https://www.boe.es/buscar/doc.php?id=DOUE-L-2023-81696) y es
aplicable desde el **19 de junio de 2026**. En los contratos celebrados por una interfaz en línea pide:

- Una **función de desistimiento** etiquetada "desistir del contrato aquí" o con una fórmula
  inequívoca equivalente, disponible durante todo el plazo de desistimiento.
- Una **función de confirmación** etiquetada "confirmar desistimiento" o equivalente.
- Un **acuse de recibo en soporte duradero**, sin demora indebida, con el contenido del desistimiento
  y la fecha y hora en que se presentó.

> ⚠️ **España todavía no lo ha transpuesto.** A 18 de noviembre de 2026, el TRLGDCU consolidado no
> recoge esta función. **Qué efecto tiene hoy frente a un vendedor español es pregunta para un
> abogado:** en el informe va como VIGILA, con "Abogado: sí".

### El caso del software y el contenido digital

El art. 103 recoge las excepciones, y hay que separar dos casos:

- **Software descargable (contenido digital sin soporte material), art. 103.m):** el derecho se pierde
  cuando la ejecución ha comenzado y, si hay obligación de pago, se cumplen tres condiciones:
  consentimiento previo para empezar durante el plazo, conocimiento de que con ello se pierde el
  derecho, y confirmación conforme al art. 98.7 o al 99.2.
- **Servicio digital, art. 103.a):** es un contrato de servicios (art. 59 bis.1.g). El derecho solo se
  pierde cuando el servicio se ha **ejecutado por completo**, con consentimiento previo expreso y
  sabiendo que se pierde.

> ⚠️ **No cites esa letra de memoria ni la des por buena tal cual: el RDL 24/2021 modificó varias
> letras del art. 103 y añadió requisitos.** Lee el texto consolidado del artículo antes de escribir
> nada en un informe: <https://www.boe.es/buscar/act.php?id=BOE-A-2007-20555#a103>

Lo que **sí** se puede afirmar con seguridad: la excepción del contenido digital no funciona sola. La
ley no habla de casillas, pero el empresario tiene que poder probar el consentimiento y el
conocimiento, y la forma práctica es **una casilla específica, sin premarcar, en el momento de la
compra**, donde el comprador consiente empezar ya y reconoce que pierde el desistimiento. Además hay
que **enviarle la confirmación en soporte duradero** (art. 98.7.b). Si falta alguna de las tres
condiciones, la descarga inmediata no elimina el derecho, y el producto tiene que devolver el dinero
durante 14 días.

**Hallazgo habitual:** una página de precios con "descarga inmediata, sin reembolsos". Eso, sin la
casilla y sin la información previa, no se sostiene.

## 4. Garantía legal de conformidad: arts. 114 a 127 bis TRLGDCU

| Concepto | Plazo | Artículo |
|---|---|---|
| Responsabilidad del vendedor | **3 años** bienes, **2 años** contenidos o servicios digitales en acto único o actos individuales; en **suministro continuo** (suscripciones), todo el periodo de suministro | 120.1 y 120.2 |
| Presunción de que el defecto ya existía | 2 años bienes, 1 año digital en acto único o actos individuales; en **suministro continuo**, la carga de la prueba es del empresario durante todo el periodo | 121.1 y 121.2 |
| Prescripción de la acción | **5 años** desde que se manifiesta | 124 |
| Plazo para que el consumidor avise | **Ya no existe** (el antiguo de 2 meses se suprimió) | suprimido |

La puesta en conformidad es **gratuita** (art. 118). Y hay que **mencionar la garantía** en la
información precontractual (art. 97.1.n), no basta con cumplirla en silencio.

Para software y servicios digitales hay además obligaciones de **actualizaciones** durante el periodo
correspondiente: si se vende una aplicación, dejar de darle mantenimiento no es solo mala imagen.

## 5. Precios

- **Siempre precio total con impuestos incluidos** en toda información dirigida a consumidores,
  publicidad incluida (arts. 60.2.c y 20.1.c TRLGDCU). Mostrar el precio sin IVA a un consumidor
  final es práctica desleal por engañosa (art. 20.6, remitiendo al art. 7 de la Ley 3/1991).
- **Precio anterior tachado:** el "antes" debe ser **el precio más bajo aplicado en los 30 días
  anteriores** (art. 20 de la Ley 7/1996). Subir el precio antes de una promoción para tachar más es
  ilegal, y en cualquier plataforma queda registrado.
- **Precios personalizados por decisión automatizada:** hay que informar de los parámetros usados
  (art. 97.1.f TRLGDCU y art. 27.9 LCD). Si el producto ajusta precios por segmento, esto se activa.

## 6. Reseñas y testimonios

- **Art. 20.4 TRLGDCU:** si se muestran reseñas, hay que informar de **si se garantiza o no** que
  provienen de quien realmente usó o compró el producto, y explicar **cómo se procesan**.
- **Art. 27.7 LCD:** decir "reseñas verificadas" sin tomar medidas razonables para comprobarlo está
  en la lista negra de prácticas desleales.
- **Art. 27.8 LCD:** escribir reseñas propias, encargarlas, o **borrar solo las negativas** es
  distorsión y está prohibido en todo caso.

Consecuencia técnica: el sistema de reseñas tiene que **poder demostrar** la compra o el uso. Poner
un widget de testimonios de amigos en una landing de producto no es marketing agresivo, es una
práctica desleal tipificada.

## 7. Accesibilidad: Directiva (UE) 2019/882

Aplica desde el **28 de junio de 2025** a una **lista cerrada** de productos y servicios. El que
alcanza a casi cualquier producto digital que cobre es el **comercio electrónico**. Listón práctico:
**WCAG 2.1 nivel AA**. En España la traspone la Ley 11/2023.

**Exención de microempresa (art. 4.5 de la Directiva):** las microempresas que prestan **servicios**
quedan exentas. Microempresa = menos de 10 personas y volumen de negocio o balance anual que no
supera los 2 millones de euros.

Tres avisos que van en el informe:
1. La exención es **por tamaño y reversible**. El día que se pase de ahí, la obligación aparece de
   golpe y rehacer una interfaz entera después es carísimo.
2. La exención de esta directiva **no anula** el resto del marco de no discriminación por
   discapacidad.
3. El aviso de IA del art. 50 del AI Act también tiene que ser accesible, así que ambas cosas se
   diseñan juntas.

## 8. Fiscalidad, lo justo para saber qué preguntar

> La configuración fiscal concreta (forma jurídica, epígrafe, régimen) la cierra un asesor **antes de
> la primera venta**, no después. Este apartado solo sirve para llegar con las preguntas hechas.

- **IVA general en España: 21%.** El software y los servicios digitales al consumidor final se
  muestran siempre con IVA incluido.
- **Ventas a consumidores de otros países de la UE:** umbral de **10.000 € anuales conjunto para
  toda la UE** (no por país). Por debajo, IVA español; al superarlo, IVA del país de destino, con
  registro en la **ventanilla única (OSS)**: modelo **035** para registrarse y **369** para declarar.
  Un *merchant of record* asume esto por ti, y esa es la razón principal para usarlo.
- **VERI*FACTU:** sistemas de facturación verificable. Fechas vigentes tras las prórrogas:
  contribuyentes del Impuesto sobre Sociedades antes del **1 de enero de 2027**; el resto (autónomos
  en IRPF) antes del **1 de julio de 2027**. Cualquier fecha anterior que se lea por internet (julio
  de 2025, enero de 2026) está **desfasada**.

## 9. Dos cosas que ya NO hay que poner, y una que sí

- ⛔ **La plataforma europea de resolución de litigios en línea dejó de existir el 20 de julio de
  2025**, derogada por el Reglamento (UE) 2024/3228. El enlace `ec.europa.eu/consumers/odr` que
  llevan casi todas las plantillas **solo redirige ya a un aviso de cierre de la Comisión** y ponerlo
  hoy es informar mal al consumidor. Si aparece en el pie de una web o en unas condiciones, es un
  hallazgo.
- ⛔ Las cifras de multas de la LSSI de 300.000 / 3.000.000 € (ver `web-y-datos-es.md`).
- ✅ **Sigue vivo el deber de informar sobre resolución alternativa de litigios** (Ley 7/2017, art.
  40) si se está adherido a una entidad, o si por ley o código de conducta hay que aceptarla. Y en el
  caso concreto: cuando un consumidor reclama y no se le resuelve, hay que informarle de al menos una
  entidad competente.
