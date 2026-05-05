# Firma Digital Intelec — Outlook Add-in

Add-in de Outlook para aplicar firma criptográfica PKCS#7 SHA-256 a PDFs adjuntos en correos.

## Funcionalidades

- **Firma criptográfica real** (no solo sello visible) con PKCS#7 detached SHA-256
- **Detección automática** de campos AcroForm `/Sig` y texto "firma" con scoring
- **Vista previa interactiva** con click-to-place para colocar la firma con el cursor
- **Persistencia** del certificado .p12 en IndexedDB + PIN en localStorage (codificación leve)
- **Multi-documento**: firmar varios PDFs en un solo paso, descarga como ZIP o PDFs individuales
- **Detección de adjuntos en Outlook** automática

## Estructura

```
/
├── index.html          ← App principal
├── manifest.xml        ← Manifest Outlook clásico (Office 1.1)
├── manifest.json       ← Manifest unificado para nuevo Outlook / Teams
├── icons/
│   ├── icon-16.png
│   ├── icon-32.png
│   ├── icon-64.png
│   ├── icon-80.png
│   └── icon-128.png
└── README.md
```

## Despliegue

1. Subir todos los archivos al repositorio `intelecsl/intelec-firma` en GitHub
2. Activar GitHub Pages en `Settings → Pages → Branch: main / root`
3. Esperar 2-3 minutos a que la URL `https://intelecsl.github.io/intelec-firma/` esté disponible
4. Verificar acceso a `https://intelecsl.github.io/intelec-firma/index.html`

## Instalación en Outlook

### Vía Centro de Administración Microsoft 365 (recomendado)

⚠ **Subir el archivo `manifest.xml` directamente, NO un ZIP** (el ZIP solo se usa con manifest unificado JSON, que aún tiene soporte limitado).

1. https://admin.microsoft.com → Configuración → **Aplicaciones integradas**
2. Click en **Cargar aplicaciones personalizadas** → seleccionar **Office Add-in**
3. **Cargar archivo de manifiesto (.xml)** → elegir `manifest.xml`
4. Asignar a usuarios y desplegar

### Vía URL del manifest

Mismo procedimiento pero seleccionar **Proporcionar URL del manifiesto** y pegar:

`https://intelecsl.github.io/intelec-firma/manifest.xml`

### Side-load para test individual

- Outlook Web → ⚙ → Personalizar acciones → Obtener complementos → Mis complementos → Agregar desde URL
- URL: `https://intelecsl.github.io/intelec-firma/manifest.xml`

## Actualizar la app

Cada vez que se modifique el código:

1. **Subir versión** en CUATRO sitios (todos deben coincidir):
   - `index.html` → badge `<span class="vbadge">vX.YZ</span>`
   - `index.html` → `pdfDoc.setProducer('Firma Digital Intelec vX.YZ')`
   - `manifest.xml` → `<Version>X.Y.Z.0</Version>` (formato estricto x.y.z.w)
   - `manifest.json` → `"version": "X.Y.Z"`

2. **Push al repo** — GitHub Pages refresca en 1-2 minutos

3. **Re-subir el manifest.xml en Centro Admin M365**:
   - Ir a Aplicaciones integradas → "Firma Digital" → **Editar app** → Actualizar archivo
   - Subir el `manifest.xml` actualizado (Centro detecta el nuevo `<Version>` y propaga el cambio)
   - El cliente de Outlook detecta el cambio en 1-24h (la web es más rápida)

> **Nota:** si se cambia el `<Id>` del manifest, Outlook lo trata como una app nueva. Mantenerlo siempre igual: `45296c6e-05b2-45fe-b01d-9173d54288a7`

## Versión actual

**v3.05** — Estética IBM Plex (estilo Rellena Formularios) + click-to-place en vista previa + manifest configurado para auto-actualización con GUID válido.
