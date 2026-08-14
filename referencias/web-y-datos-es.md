# Web pública y datos personales (España / UE)

> **Última verificación de este documento: 14 de agosto de 2026**, sobre texto consolidado del BOE,
> EUR-Lex y la sede de la AEPD. Enlaces en `fuentes.md`.

Aplica en cuanto hay **una web publicada** o **se recogen datos de personas**. Una landing con un
formulario de correo ya entra; un binario que corre en local y no se comunica con nadie, no.

## 1. Aviso legal: art. 10 LSSI (Ley 34/2002)

Obliga a dar acceso "por medios electrónicos, de forma permanente, fácil, directa y gratuita" a:

| Letra | Contenido |
|---|---|
| a) | Nombre o razón social, domicilio, correo electrónico y medio de contacto directo y efectivo |
| b) | Datos registrales, si procede |
| c) | Autorización administrativa y órgano supervisor, si la actividad lo exige |
| d) | Colegio profesional y número de colegiado, si es profesión regulada |
| e) | **NIF / CIF** |
| f) | Si se mencionan precios: información clara sobre el precio, si incluye impuestos y los gastos de envío |
| g) | Códigos de conducta a los que esté adherido |

**Sanciones reales:** incumplir de forma significativa las letras a) y f) es infracción **grave**
(art. 38.3.b), de 30.001 a 150.000 €. El resto son **leves** (art. 38.4.b), hasta 30.000 €.

> ⚠️ **Corrección de un bulo muy extendido:** las cifras de 300.000 y 3.000.000 € que citan
> muchísimas guías vienen del **Real Decreto-ley 9/2024, que fue derogado** por acuerdo del Congreso
> publicado el 23 de enero de 2025. Las cuantías vigentes son las del art. 39.1 LSSI: hasta 30.000
> (leves), de 30.001 a 150.000 (graves) y de 150.001 a 600.000 € (muy graves). Si un informe repite las cifras
> viejas, está copiado de internet, no leído.

**Hallazgo típico:** un aviso legal con el nombre comercial de la marca pero sin la persona física o
sociedad que factura, sin NIF y sin domicilio. Eso no cumple.

## 2. Política de privacidad: arts. 13 y 14 RGPD

Contenido mínimo del art. 13, y se comprueba punto por punto:

- Identidad y contacto del responsable (y del DPD si existe).
- **Fines del tratamiento y base jurídica de cada uno.** Si se invoca interés legítimo (art. 6.1.f),
  hay que decir cuál es.
- Destinatarios o categorías: aquí entran el hosting, la pasarela de pago, la herramienta de correo,
  la analítica, el proveedor de IA al que se envían los prompts.
- Transferencias a terceros países, con la garantía aplicable (decisión de adecuación, cláusulas
  contractuales tipo) y cómo obtener copia.
- Plazo de conservación, o criterios para determinarlo.
- Derechos: acceso, rectificación, supresión, limitación, oposición, portabilidad.
- Derecho a retirar el consentimiento y a reclamar ante la AEPD.
- Si dar los datos es requisito legal o contractual y qué pasa si no se dan.
- **Existencia de decisiones automatizadas o elaboración de perfiles**, con la lógica aplicada y sus
  consecuencias. Este punto es el que activan las funciones "inteligentes" que personalizan la
  interfaz o el precio.

**Método de auditoría:** lista los destinos reales de datos leyendo el código (`fetch`, SDKs,
variables de entorno con claves de terceros) y compáralos con los que declara la política. Los que
falten son el hallazgo.

## 3. Cookies y almacenamiento: art. 22.2 LSSI + guía de la AEPD

**Versión vigente de la guía: mayo de 2024**, en `https://www.aepd.es/guias/guia-cookies.pdf`. La de
julio de 2023 sigue colgada en una URL antigua y está superada.

Reglas que se comprueban **en el navegador**, nunca en la documentación de la librería:

- **Rechazar tan fácil como aceptar.** Si hay botón de aceptar, hay botón de rechazar, en la misma
  capa, al mismo nivel y con la misma visibilidad. Nada de mandar a rechazar a una segunda pantalla.
  (La fórmula "el mismo número de clics" que circula por ahí **no** está en la guía; lo que sí está
  es lo de la misma capa.)
- **Seguir navegando no es consentimiento.** Tampoco lo es abrir la segunda capa informativa.
- **Nada premarcado** a favor de aceptar, ni contraste engañoso, ni dar a entender que hay que
  aceptar para poder navegar.
- **Granularidad por finalidades**, no cookie a cookie.
- **Renovar el consentimiento cada 24 meses** es buena práctica recomendada por la AEPD, no plazo
  legal.
- **La política de cookies lista cada cookie concreta**: nombre, titular, finalidad y duración. Una
  lista genérica no cumple, y cada integración nueva obliga a actualizarla.

**Exentas** (Dictamen 4/2012 recogido por la guía): entrada del usuario, autenticación **solo de
sesión**, seguridad, sesión de reproductor multimedia, equilibrado de carga, personalización de
interfaz elegida por el usuario (idioma, moneda, contraste) y ciertos complementos sociales.

> **La analítica NO está exenta con carácter general.** Hay una vía estrecha en la guía de medición
> de audiencia (enero de 2024) con condiciones muy duras: solo para medir la audiencia de ese sitio,
> en nombre exclusivo del editor, estadísticas anónimas, sin cruzar con otros tratamientos, sin
> ceder a terceros y **sin seguimiento entre sitios**. Google Analytics tal como se implanta
> habitualmente **no cabe ahí y necesita consentimiento previo**.

**Verificación obligatoria, y es la que descubre casi todos los incumplimientos:**

1. Abrir la web en ventana de incógnito.
2. Herramientas de desarrollador → Aplicación → borrar todo el almacenamiento.
3. Recargar y, **sin tocar el banner**, mirar qué cookies y qué entradas de `localStorage` se han
   escrito. Todo lo que aparezca y no esté en la lista de exentas es un incumplimiento.
4. Repetir tras pulsar "Rechazar": no debe quedar ninguna cookie no exenta.
5. Repetir cada vez que se añada o actualice una integración de terceros.

Sanción: infracción **leve** del art. 38.4.g) LSSI, hasta 30.000 €.

## 4. Registro de actividades de tratamiento: art. 30 RGPD

La excepción de "menos de 250 empleados" **casi nunca sirve**, porque decae si el tratamiento no es
ocasional. La propia AEPD lo dice en su FAQ 0249: en la práctica la mayoría de responsables con menos
de 250 trabajadores **sí están obligados**. Gestionar clientes o una newsletter es continuado, no
ocasional.

Contenido (art. 30.1): responsable y contacto, DPD si lo hay, fines, categorías de interesados y de
datos, categorías de destinatarios, transferencias internacionales y sus garantías, plazos de
supresión y descripción general de las medidas de seguridad. Por escrito, vale electrónico.

> El *Digital Omnibus* propone subir ese umbral a 750 empleados, pero **es una propuesta, no está en
> vigor**. Hoy rige el 250.

## 5. Encargados de tratamiento: art. 28 RGPD

Cada proveedor que toca datos por cuenta del producto (hosting, correo, analítica, pasarela, API de
IA) necesita **contrato de encargado (DPA)**. Muchos lo incorporan automáticamente a sus condiciones
y no hay que firmar nada aparte; otros exigen aceptarlo expresamente. Se comprueba y se guarda copia.

El art. 28.3 exige, como mínimo: tratar solo con instrucciones documentadas, confidencialidad del
personal, medidas del art. 32, condiciones para subencargados, asistencia en derechos y en los arts.
32 a 36, supresión o devolución al terminar, y permitir auditorías.

**Y una pregunta que casi nadie se hace:** ¿los prompts que el producto manda al proveedor de IA
llevan datos personales de los usuarios? Si la respuesta es sí, ese proveedor es un encargado, va en
la política de privacidad y necesita su DPA.

## 6. Transferencias internacionales

El **Marco de Privacidad de Datos UE-EEUU** (Decisión (UE) 2023/1795) sigue vigente, pero está bajo
presión: el Tribunal General desestimó el recurso *Latombe* (T-553/23) el 3 de septiembre de 2025 y
hay casación pendiente que **no suspende** la decisión. Práctica sana: documentar que las
transferencias se amparan **tanto** en la decisión de adecuación **como** en las cláusulas
contractuales tipo del DPA del proveedor, y comprobar la certificación de cada proveedor
estadounidense en `https://www.dataprivacyframework.gov/list`.

## 7. Correo comercial y menores

**Art. 21 LSSI:** prohibido enviar comunicaciones comerciales no solicitadas. Excepción: si hay
relación contractual previa y los datos se obtuvieron lícitamente, se pueden enviar comunicaciones de
**productos similares propios**, ofreciendo siempre oponerse. En cada correo, **baja sencilla y
gratuita con una dirección electrónica válida**; "responde a este correo" como único mecanismo no
vale. Envío masivo o insistente incumpliendo esto es infracción **grave**: 30.001 a 150.000 €.

- Casilla de la newsletter **sin premarcar**, siempre.
- El **doble opt-in no es obligatorio** por ninguna norma ni guía oficial, pero el art. 7.1 RGPD
  obliga a **poder demostrar** que la persona consintió, y el doble opt-in es la forma práctica de
  hacerlo. Recomendado, no exigido.

**Menores: en España la edad son 14 años** (art. 7 LOPDGDD). Por debajo hace falta consentimiento de
quien tenga la patria potestad. Si el producto tiene público joven, esto no es teórico: incumplirlo
es infracción **grave** del art. 73.a) LOPDGDD.

## 8. Brechas de seguridad: arts. 33 y 34 RGPD

Notificación a la autoridad **sin dilación indebida y como máximo en 72 horas** desde que se tiene
constancia, salvo que sea improbable que suponga riesgo. Si hay alto riesgo, además hay que
comunicárselo a los afectados. **Todas las brechas se documentan internamente**, se notifiquen o no.

Sanciones del art. 83: hasta 10.000.000 € o el 2% del volumen de negocio anual global en el
apartado 4, y hasta 20.000.000 € o el 4% en los apartados 5 y 6.

**Hallazgo de producto, no de papeleo:** si no hay registro de accesos ni forma de saber qué datos
se vieron, esas 72 horas son imposibles de cumplir aunque exista el protocolo escrito.

## 9. Lo que hay que dejar claro en el informe

- **DPD (delegado de protección de datos):** un producto pequeño normalmente **no** lo necesita
  (art. 37.1 RGPD y art. 34.1 LOPDGDD). Y designarlo "por si acaso" somete voluntariamente a todo el
  régimen: no se recomienda a la ligera.
- **Evaluación de impacto:** solo si se cruzan perfilado, geolocalización o identificadores únicos a
  escala. Las listas de la AEPD dicen cuándo.
- Lo que dependa de la forma jurídica, de la facturación o de un caso concreto, va a la sección
  **"necesita abogado"**, no se resuelve por analogía.
