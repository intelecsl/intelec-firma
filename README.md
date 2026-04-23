# Firma Digital Intelec

App web para firmar PDFs con certificado digital (.p12/.pfx). Se integra en Outlook como add-in.

## Configuración GitHub Pages

1. Settings → Pages
2. Source: Deploy from a branch
3. Branch: `main` / Folder: `/ (root)`
4. Save

URL resultante: `https://intelecsl.github.io/intelec-firma/`

## Verificación

Abre `https://intelecsl.github.io/intelec-firma/test.html` — deben salir 6 ficheros en verde.

## Instalación del add-in

- **Outlook clásico:** sideload `manifest.xml` desde https://aka.ms/olksideload
- **Teams / Outlook nuevo:** sube el zip con `manifest.json` + iconos desde Teams → Apps → Cargar app personalizada
- **Admin Center M365:** Aplicaciones integradas → Cargar app personalizada (requiere admin)
