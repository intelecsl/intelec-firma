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

### Outlook clásico
- Outlook Web → ⚙ Configuración → Ver toda la configuración → Correo → Personalizar acciones → Obtener complementos → **Mis complementos** → Agregar complemento personalizado → **Agregar desde URL**
- URL: `https://intelecsl.github.io/intelec-firma/manifest.xml`

### Nuevo Outlook / Teams
- Subir `manifest.json` empaquetado en ZIP junto con `icon-128.png` e `icon-32.png` desde la raíz
- Centro de administración Microsoft 365 → Aplicaciones integradas → Cargar aplicación personalizada

## Actualizar la app

Cada vez que se modifique el código:

1. **Subir versión** en TRES sitios (todos deben coincidir):
   - `index.html` → badge `<span class="vbadge">vX.YZ</span>`
   - `index.html` → `pdfDoc.setProducer('Firma Digital Intelec vX.YZ')`
   - `manifest.xml` → `<Version>X.Y.Z.0</Version>`
   - `manifest.json` → `"version": "X.Y.Z"`

2. **Push al repo** — GitHub Pages refresca en 1-2 minutos
3. Outlook detectará el cambio automáticamente la próxima vez que el usuario abra el add-in (compara el `Version` del manifest con el local)

> **Nota:** si se cambia el `<Id>` del manifest, Outlook lo trata como una app nueva. Mantenerlo siempre igual: `9b5a0e2f-3c7a-4d8e-9b1f-firma3digital04`

## Versión actual

**v3.04** — Estética IBM Plex (estilo Rellena Formularios) + click-to-place en vista previa + manifest configurado para auto-actualización.
