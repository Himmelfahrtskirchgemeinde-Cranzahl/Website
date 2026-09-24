# Himmelfahrtskirche Cranzahl — Website

Neue Website der Ev.-Luth. Himmelfahrtskirchgemeinde Cranzahl.

- **Framework:** Next.js (App Router, TypeScript), Node.js 22
- **Hosting:** Hostinger (Node.js Web App)
- **Datenbank:** MySQL/MariaDB bei Strato
- **Verwaltung:** ChurchTools-Extension
- **Design:** Figma-Datei „Neues Webdesign KGCranzahl", Seite „🎨 Design"

## Entwicklung

```bash
npm install
npm run dev        # http://localhost:3000
npm run typecheck
npm run build
```

## Arbeitsweise

- `main` ist immer lauffähig. Änderungen entstehen auf Feature-Branches (`feature/…`)
  und kommen per Pull Request nach `main`.
- Welche Seiten und Daten es gibt, steht in [`docs/datenplan.md`](docs/datenplan.md).
  Inhalte werden erst eingebaut, wenn sie dort freigegeben sind.
