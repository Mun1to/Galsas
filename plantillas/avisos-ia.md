# Avisos de IA listos para pegar

Textos y patrones para cumplir el art. 50 del AI Act sin que parezcan letra pequeña. Dos principios
antes de copiar nada:

1. **El aviso va donde ocurre la interacción**, no en los términos ni en el pie.
2. **El aviso también tiene que ser accesible** (lo exige el propio art. 50.5): contraste real, texto
   seleccionable, y si es un icono, con etiqueta accesible. Nunca una imagen con texto dentro.

## 1. Chat o asistente conversacional

Va **antes o en el mismo momento** de la primera interacción, dentro del componente de chat.

- ES: **Hablas con una IA.** Puede equivocarse; comprueba lo importante.
- EN: **You're talking to an AI.** It can be wrong; double-check anything important.

Variante para asistente de voz, dicha en la primera frase:
- ES: Soy un asistente de inteligencia artificial.

```html
<p class="ai-notice" role="note">
  <strong>Hablas con una IA.</strong> Puede equivocarse; comprueba lo importante.
</p>
```

```jsx
// El aviso vive DENTRO del componente reutilizable, no en cada pantalla.
export function Chat({ children }) {
  return (
    <section className="chat">
      <p className="ai-notice" role="note">
        <strong>Hablas con una IA.</strong> Puede equivocarse; comprueba lo importante.
      </p>
      {children}
    </section>
  )
}
```

## 2. Contenido generado que se publica

Etiqueta **visible**, junto al contenido, no en el pie de la página.

- Imagen o vídeo: **Imagen generada con IA** · *AI-generated image*
- Voz clonada o sintética: **Voz generada con IA** · *AI-generated voice*
- Texto publicado sin revisión humana: **Texto generado con IA** · *AI-generated text*

Para una obra artística, satírica o de ficción basta con reconocerlo donde corresponda (créditos,
descripción) sin estropear la obra.

```html
<figure>
  <img src="..." alt="...">
  <figcaption>Imagen generada con IA</figcaption>
</figure>
```

## 3. Cuando NO hace falta etiquetar

Escribirlo también es trabajo del informe, porque evita poner avisos donde no tocan y perder
credibilidad:

- Corrección, autocompletado, formato o **transcripción fiel** de lo que dictó la persona: es
  edición asistida, no contenido sintético.
- Texto que **revisa y firma una persona** que asume la responsabilidad editorial.
- Chat donde es **evidente** que es una IA. (Aun así conviene ponerlo: es una línea.)

## 4. El punto único de salida

El patrón que hace barato todo lo demás. Hoy solo registra; mañana firma con C2PA sin tocar el resto
del producto.

```ts
type Salida = { archivo: Uint8Array; modelo: string; version: string }

export async function exportarGenerado({ archivo, modelo, version }: Salida) {
  registrar({ modelo, version, cuando: new Date().toISOString() })  // hoy: trazabilidad
  // mañana: firmar C2PA aquí, y solo aquí
  return archivo
}
```

Tres reglas para que siga sirviendo:
- **Nada sale del producto sin pasar por esta función.** Si hay dos caminos de exportación, el patrón
  ya no vale.
- El registro guarda **modelo, versión y marca de tiempo**. Reconstruir eso después es imposible.
- El aviso visible es una capa distinta: los metadatos se borran al subir un archivo a cualquier red
  social, así que la etiqueta que ve la persona no se sustituye por la firma.
