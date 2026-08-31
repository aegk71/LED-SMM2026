# LED-SMM2026 — Messe-Downloadseite

Temporäre Download-Seite für die Messe. Eine einzelne `index.html` ohne Build-Schritt,
ohne Framework, ohne externe Abhängigkeiten und ohne Tracking.

**Live-URL:** https://aegk71.github.io/LED-SMM2026/

## Aufbau

```
index.html          Die komplette Seite (HTML + CSS in einer Datei)
assets/             Logo und Favicon
files/              Alle Download-Dokumente (PDF, DWG, XLSM)
files/media/        Fotos und Videos
```

## Was noch ausgefüllt werden muss

In `index.html` sind die anzupassenden Stellen mit `PLATZHALTER` kommentiert:

| Stelle | Was |
|---|---|
| Kopfleiste | Messename / Standnummer im Badge (aktuell „SMM 2026") |
| Begrüßung | Überschrift und Begrüßungstext |
| Fußbereich | Impressum: Telefon, E-Mail, Geschäftsführung, HRB, USt-IdNr. |

Suche in der Datei einfach nach `PLATZHALTER`.

> **Hinweis:** Das Impressum ist nach § 5 DDG für eine gewerbliche Seite Pflicht.
> Die Pflichtangaben sollten vor dem Verteilen des QR-Codes vollständig sein.

## Neue Datei hinzufügen

### Variante A — direkt auf github.com (ohne Git)

1. Repository öffnen: https://github.com/aegk71/LED-SMM2026
2. In den Ordner `files` wechseln
3. **Add file → Upload files**, Datei per Drag & Drop ablegen, **Commit changes**
4. Zurück im Repo-Root auf `index.html` klicken, Stift-Symbol (**Edit**)
5. Einen vorhandenen `<li class="item">…</li>`-Block kopieren und anpassen:
   Dateiname, Beschreibung, Größe und den `href` auf `files/DEINE-DATEI.pdf`
6. **Commit changes**

Nach ca. 1 Minute ist die Änderung live.

### Variante B — lokal mit Git

```bash
git pull
# Datei nach files/ kopieren, index.html anpassen
git add .
git commit -m "Neues Datenblatt ergänzt"
git push
```

### Vorlage für einen neuen Eintrag

```html
<li class="item">
  <span class="type">PDF</span>
  <div class="body">
    <div>
      <p class="name">DATEINAME.pdf</p>
      <p class="desc">Kurze Beschreibung, was drin steht.</p>
      <p class="meta">PDF &middot; 12 Seiten &middot; 800 KB</p>
    </div>
    <a class="dl" href="files/DATEINAME.pdf" download>
      <svg width="15" height="15" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M8 1.5v9"/><path d="M4.5 7.5 8 11l3.5-3.5"/><path d="M2 13.5h12"/></svg>
      Download
    </a>
  </div>
</li>
```

Für die farbigen Typ-Kacheln: `<span class="type">` (blau, PDF),
`<span class="type dwg">` (magenta, CAD), `<span class="type xlsm">` (grün, Excel).

### Vorlage für ein neues Foto

Im Block `<ul class="grid">` ergänzen:

```html
<li><a href="files/media/DATEINAME.jpg" target="_blank" rel="noopener"><img src="files/media/DATEINAME.jpg" alt="Kurze Bildbeschreibung" loading="lazy"></a></li>
```

### Vorlage für ein neues Video

Im Block `<ul class="videos">` ergänzen. Der `<div class="frame">` ist wichtig —
er begrenzt die Höhe, sonst füllt ein Hochformat-Clip den ganzen Handybildschirm:

```html
<li><figure>
  <div class="frame"><video controls preload="metadata" playsinline src="files/media/DATEINAME.mp4"></video></div>
  <figcaption>Video 4 &middot; 2,5 MB</figcaption>
</figure></li>
```

### Dateinamen

Keine Leerzeichen, keine Klammern und keine Umlaute — die stehen später in der URL.
Punkte und Bindestriche sind unproblematisch (`LED.STS.A60.UseMan.06.pdf` ist in Ordnung).

Grenzen von GitHub Pages: max. 100 MB pro Datei, ca. 1 GB pro Repository,
100 GB Traffic pro Monat. Für eine Messe reicht das mit großem Abstand.

## Seite wieder offline nehmen

### Nur Pages abschalten, Repo behalten

1. https://github.com/aegk71/LED-SMM2026/settings/pages
2. Unter **Build and deployment → Source** auf **None** stellen

Oder per CLI:

```bash
gh api -X DELETE repos/aegk71/LED-SMM2026/pages
```

Die URL liefert danach 404, die Dateien bleiben im Repo erhalten.

### Repo auf privat stellen (Pages wird dadurch inaktiv)

```bash
gh repo edit aegk71/LED-SMM2026 --visibility private --accept-visibility-change-consequences
```

### Alles löschen

```bash
gh repo delete aegk71/LED-SMM2026 --yes
```

Das ist endgültig. Vorher sicherstellen, dass die Originaldateien noch lokal liegen
(hier: `C:\Users\a.kruse\Desktop\CLAUDE.WORKFILE\Messedownload`).

## QR-Code

Der QR-Code zeigt auf https://aegk71.github.io/LED-SMM2026/ — die URL ändert sich nicht,
solange Repo-Name und Konto gleich bleiben. Inhalte lassen sich also beliebig nachpflegen,
ohne den gedruckten QR-Code zu entwerten.

## Hinweis zur Sichtbarkeit

Das Repository ist öffentlich: alle Dateien sind ohne Login abrufbar. Die Seite trägt
`noindex, nofollow`, was seriöse Suchmaschinen von der Indexierung abhält — ein
Zugriffsschutz ist das jedoch nicht.
