\# ALPHEX v1 – Kompaktes, vollständiges Anforderungsprofil (Cloudflare + Supabase)



> \*\*Dokumentstatus:\*\* Version 1.0 (aktuell)

> \*\*Dateiformat:\*\* Markdown (`.md`)

> \*\*Dateiname:\*\* `PROJECT\_ANFORDERUNGEN\_UND\_EMPFEHLUNGEN.md`

>

> \*\*Branding-Hinweis:\*\*

> - Trading-Marke: \*\*PrimeSession Trading\*\*

> - Dev-Marke: \*\*Codinglobe\*\*

> - Beide Marken dürfen erwähnt werden, aber \*\*nicht\*\* als App-/Projektname dienen.

>

> \*\*Namensidee:\*\* \*\*ALPHEX\*\* (jung, klar, hype-tauglich, international skalierbar, mit dezentem Schweiz-Bezug über „ALP“).



---



\## 1) Zielbild (V1.0)



ALPHEX ist eine modulare, sichere, SQL-first Web-App mit:

\- Cloudflare (Pages + Workers)

\- Supabase (Auth + Postgres + Storage)

\- Basis/Pro-Freischaltung (Journal = Pro)

\- 4 Sprachen ab Start: DE/FR/IT/EN

\- vollständiger Nutzung auf PC und Mobile

\- öffentlicher Info-Startseite vor Login

\- zentralem Fehler- und Ticketflow inkl. Log-Anhang

\- strikt getrennter Staging/Prod-Datenbasis



\*\*Grundsatz:\*\* Produktivdaten liegen in SQL, nicht primär im LocalStorage.



---



\## 2) Tech-Stack (empfohlen)



\- \*\*Frontend:\*\* TypeScript (React oder Vue)

\- \*\*API/BFF:\*\* TypeScript auf Cloudflare Workers

\- \*\*DB:\*\* PostgreSQL (Supabase, SQL-first)

\- \*\*Auth:\*\* Supabase Auth

\- \*\*Files:\*\* Supabase Storage

\- \*\*CI/CD:\*\* GitHub Actions (YAML)

\- \*\*Tests:\*\* Vitest + Playwright



---



\## 3) Rollen, Pläne, Freischaltung



\### Rollen

\- `guest`

\- `user`

\- `admin`



\### Pläne

\- `basis`

\- `pro`



\### Pflichtregeln

\- Journal ist \*\*nur Pro\*\*.

\- Rechteprüfung auf UI-, API- und DB/RLS-Ebene.

\- Admin-Impersonation ist Pflicht:

&nbsp; - Standard read-only

&nbsp; - Schreibmodus nur explizit

&nbsp; - Audit-Log immer verpflichtend



---



\## 4) Produktumfang Basis vs. Pro



\### Basis

\- Profil

\- Rechner (Basis):

&nbsp; - Entry via Checkbox

&nbsp; - Berechnung Anzahl Orders + Avg. Entry

&nbsp; - Speichern einfacher Berechnungen

\- Dashboard

\- Tickets

\- Community



\### Pro

\- Profil

\- Rechner komplett (voller Funktionsumfang)

\- Journal

\- Dashboard

\- Tickets

\- Community



---



\## 5) Seitenstruktur (klar pro Seite)



\### 5.1 Public Info (vor Login) – Pflicht

Route: `/` oder `/info`



Inhalte:

\- Produktüberblick

\- Basis/Pro Vergleich

\- FAQ

\- Sicherheit/Datenschutz

\- Kontakt/Support

\- CTA: Login / Registrierung



Unterseiten erlaubt, z. B.:

\- `/info/faq`

\- `/info/pricing`

\- `/info/security`



\*\*Wichtig:\*\* Keine sensiblen Nutzerdaten vor Login.



\### 5.2 Login/Registrierung

Route: `/login`



\- Login

\- Registrierung

\- Recovery-Flow



\### 5.3 Dashboard (nach Login)

\- KPI-Übersicht

\- PnL-Kalender

\- Tages-/Aktivitätsliste



\### 5.4 Rechner

\- Basis: Checkbox-Entries + Anzahl Orders + Avg. Entry

\- Pro: vollständige Setup-/Entry-/Exit-/TP-/SL-Logik



\### 5.5 Journal (nur Pro)

\- Trade-Erfassung

\- Filter/Auswertung

\- Review



\### 5.6 Profil

\- Kontodaten

\- Sicherheit (Passwort/E-Mail)

\- Sprache/Theme

\- Planstatus



\### 5.7 Tickets

\- Ticket erstellen

\- Verlauf + Anhänge

\- „Ticket mit Log-Anhang“ direkt aus Fehlermeldung



\### 5.8 Community

\- Posts

\- Kommentare

\- Reaktionen

\- Basis-Moderation



---



\## 6) Internationalisierung (i18n) – global \& immer verfügbar



\### Pflichtsprachen

\- Deutsch (`de`)

\- Französisch (`fr`)

\- Italienisch (`it`)

\- Englisch (`en`)



\### Regeln

\- Alle UI-Texte, Validierungen und Fehlermeldungen in 4 Sprachen.

\- Keine produktiven Hardcoded-Texte.

\- Fallback: User-Sprache -> Browser -> `en`.

\- \*\*Sprachumschalter muss immer verfügbar sein\*\*:

&nbsp; - auf Public-Seiten,

&nbsp; - im Login/Registrierung,

&nbsp; - in allen geschützten Bereichen nach Login.



\### Umsetzung

\- `locales/de`, `locales/fr`, `locales/it`, `locales/en`

\- i18n-Vollständigkeitscheck als PR-Gate



---



\## 7) Responsive \& Accessibility (PC + Mobile)



\### Responsive Pflicht

\- Desktop, Tablet, Mobile produktiv nutzbar.

\- Mobile-optimierte Tabellenansichten (Card/Accordion/Scroll).

\- Touch-freundliche Controls.



\### Accessibility (A11y) Pflicht

\- Kontraste, Fokuszustände, Tastaturbedienbarkeit, ARIA-Basics.

\- Kernflows (Login, Rechner, Ticket) barrierearm nutzbar.



\### QA

\- E2E Smoke für mindestens 1 Desktop- und 1 Mobile-Viewport.

\- Accessibility-Smoke (Keyboard/Screenreader-Basics).



---



\## 8) Security-Baseline \& Environment-Isolation



\### Security Pflicht

\- Supabase Auth + sichere Session-Regeln.

\- Re-Auth bei sensiblen Aktionen.

\- RLS auf allen userbezogenen Tabellen.

\- Entitlements serverseitig prüfen.

\- Input-Validierung (Schema-basiert).

\- Rate Limits (Auth, Tickets, Community).

\- Restriktives CORS.

\- Secrets nur in Secret Stores (nie im Frontend).

\- Upload-Prüfung (Typ/Größe; optional Malware-Scan).

\- Audit-Logs für Admin-/Impersonation-Aktionen.

\- Security Header: CSP, HSTS, X-Content-Type-Options, Frame-Ancestors.



\### Environment-Isolation (Muss)

\- \*\*Staging (`preprod`) darf niemals Produktivdaten live lesen.\*\*

\- Preprod nutzt ausschließlich eigene Supabase-Instanz (`alphex-stg`) und eigene Keys.

\- API-Guard: `APP\_ENV=stg` akzeptiert nur `SUPABASE\_URL` von `\*-stg`.

\- Frontend-Build pro Umgebung mit getrennten Variablen/Secrets.

\- Cross-Environment Requests werden geblockt und audit-logged.

\- Wenn in `preprod` getestet wird, darf die App \*\*nur stg-Daten\*\* zeigen.



\### Secret-Rotation

\- Rotationszyklus definieren.

\- Notfallrotation mit Runbook.

\- Rotation immer mit Funktionscheck + Audit-Eintrag.



---



\## 9) Zentrales Fehler-, Monitoring- \& Incident-System



\### Fehler- \& Supportsystem

\- Zentrale Fehlererfassung (Frontend/API/DB).

\- Error-ID + Correlation-ID + Severity.

\- Nutzerfreundliche Fehlermeldung.

\- Direkte Ticket-Erstellung mit Log-Anhang.

\- Keine Secrets in Logs, PII minimieren/maskieren.



\### Monitoring \& SLOs

\- Mindestmetriken:

&nbsp; - API Fehlerquote

&nbsp; - Latenz (p50/p95)

&nbsp; - Auth-Fehlerrate

&nbsp; - Ticket-Erstellungsrate aus Fehlerdialog

\- SLOs/SLIs pro Kernmodul definieren.

\- Alerting-Kanäle + Bereitschaftslogik dokumentieren.



\### Incident Response

\- Incident-Level (SEV1-3) definieren.

\- Standardablauf: Erkennung -> Eindämmung -> Kommunikation -> Wiederherstellung -> Postmortem.

\- Postmortem-Template verpflichtend.



\### Mindesttabellen

\- `error\_events`

\- `error\_event\_context`

\- `user\_visible\_errors`

\- `support\_tickets`

\- `support\_ticket\_messages`

\- `support\_ticket\_attachments`

\- `audit\_logs`



---



\## 10) SQL-Datenmodell, Datenlebenszyklus \& Reconciliation



\### Mindestumfang V1

\- `profiles`, `user\_settings`

\- `plans`, `subscriptions`, `entitlements`

\- `calculator\_sessions`, `calculator\_entries`, `calculator\_results`

\- `journal\_trades`, `journal\_trade\_exits` (Pro)

\- `tickets`, `ticket\_messages`

\- `community\_posts`, `community\_comments`, `community\_reactions`

\- `error\_events`, `audit\_logs`

\- `backup\_jobs`, `backup\_artifacts`, `restore\_jobs`



\### DB-Regeln

\- PK/FK/Indices verpflichtend.

\- Migrationen versioniert in `supabase/migrations/`.

\- API-Versionierung verpflichtend (z. B. `/v1`).



\### Datenlebenszyklus

\- Retention Policy für:

&nbsp; - Audit-Logs

&nbsp; - Error-Logs

&nbsp; - Tickets + Attachments

&nbsp; - Community-Inhalte

&nbsp; - Backup-Artefakte

\- Regeln für Archivierung, Löschung, Wiederherstellung und DSAR-Export/Löschung dokumentieren.



\### Datenqualität

\- Regelmäßige Konsistenzchecks zwischen Rechner/Journal/Dashboard.

\- Reconciliation-Jobs protokollieren (Ergebnis, Abweichung, Korrekturmaßnahme).



---



\## 11) Admin Backup \& Restore (Pflicht)



\### Ziel

Admin kann:

1\. einzelne User-Backups (Profil/Settings/Trades/Tickets) einspielen,

2\. vollständige Backups einspielen,

3\. für Tests einen Prod-Stand kontrolliert nach Stg kopieren.



\### Sicherheitsregeln

\- Nur `admin` + zusätzliche Re-Auth.

\- Pflichtkommentar (Grund) bei jedem Restore.

\- Jeder Job in `audit\_logs`.

\- Restore zuerst als Dry-Run + Diff-Vorschau.

\- Apply erst nach expliziter Bestätigung.



\### Technische Leitplanken

\- Backup-Artefakte versioniert und signiert (Checksumme).

\- Verschlüsselung at rest + in transit.

\- Kein direkter Prod-Zugriff aus preprod-UI.

\- User-scope und Full-restore als getrennte Workflows.

\- RPO/RTO definieren und Restore-Übungen regelmäßig protokollieren.



\### Job-Typen (Beispiele)

\- `backup\_full\_prod`

\- `backup\_user\_prod`

\- `restore\_full\_to\_stg`

\- `restore\_user\_to\_stg`

\- `restore\_user\_to\_prod` (nur mit zusätzlicher Freigabe)



---



\## 12) Governance, Operations-Logging \& Dokumentationspflicht



\### Rollenverantwortung

\- System Owner, Technical Owner, Security Owner benennen.

\- Eskalationswege dokumentieren.



\### Operations-Logging

\- Protokollpflicht für:

&nbsp; - Feature-Flag Änderungen

&nbsp; - Rollen-/Rechteänderungen

&nbsp; - Entitlement-/Plan-Änderungen

&nbsp; - Migrationsausführungen

&nbsp; - Backup/Restore-Operationen

\- Mindestfelder:

&nbsp; - `who`, `when`, `where`, `what`, `before`, `after`, `reason`, `correlation\_id`



\### Dokumentationsstandard

Für jede Änderung verpflichtend:

\- fachliche Beschreibung

\- technische Beschreibung

\- Security-Auswirkung

\- Tests

\- Migration (falls relevant)

\- Release Note



Code-Kommentare:

\- nur bei nicht selbsterklärender Logik

\- Entscheidungen/Workarounds kurz begründen



ADR-Pflicht:

\- relevante Architekturentscheidungen als ADR dokumentieren



---



\## 13) GitHub-Strategie, PR-Qualität \& CI/CD



\### Branch-Strategie

\- `main` = Production (stabil)

\- `preprod` = Staging/Integrationsbranch

\- optional alternativ: `beta` statt `preprod`



\### Wichtige Regel für Daten-Sicherheit bei Merges/Releases

\- \*\*Bei neuen Releases/Merges dürfen bestehende Userdaten nicht überschrieben werden.\*\*

\- Pflicht:

&nbsp; - migrationssichere DB-Änderungen (non-destructive first)

&nbsp; - Backward-Compatible Schema-Rollout

&nbsp; - keine destruktiven Default-Migrationen ohne expliziten Migrationsplan

&nbsp; - Datenmigrationsskripte mit Dry-Run und Validierungsreport



\### Pull Request Standard (Pflicht)

\- \*\*Jeder PR muss klar betitelt und klar beschrieben sein.\*\*

\- Mindestinhalt im PR:

&nbsp; - Ziel/Motivation

&nbsp; - Scope

&nbsp; - Security/Privacy-Auswirkung

&nbsp; - Migrations-/Datenauswirkung

&nbsp; - Testnachweis

&nbsp; - Rollback-Hinweis



\### CI/CD Qualitätsgates

Pflicht pro PR:

1\. Lint

2\. Typecheck

3\. Unit/Integration

4\. E2E Smoke (Desktop + Mobile)

5\. i18n Vollständigkeitscheck (DE/FR/IT/EN)

6\. SQL-Migrationscheck

7\. Environment-Isolation-Check (stg darf nicht auf prod zeigen)

8\. Data-Safety-Check (keine ungewollte Überschreibung bestehender Userdaten)



Deploy:

\- PR Preview

\- Merge auf `preprod` -> Staging Deploy

\- Merge auf `main` -> Prod Deploy



---



\## 14) Cloudflare/Supabase Naming, Verknüpfung \& Kostenkontrolle



\### Namenskonvention

Projekt: `alphex`



Cloudflare:

\- Pages Prod: `alphex-web-prod`

\- Pages Staging: `alphex-web-stg`

\- Worker Prod: `alphex-api-prod`

\- Worker Staging: `alphex-api-stg`



Supabase:

\- `alphex-prod`

\- `alphex-stg`



\### Verknüpfung (harte Trennung)

\- Staging-UI -> Staging-API -> Staging-Supabase

\- Prod-UI -> Prod-API -> Prod-Supabase

\- keine gemischten Umgebungen

\- keine gemeinsamen Service-Role-Keys zwischen stg/prod



\### Secrets pro Environment

\- `SUPABASE\_URL`

\- `SUPABASE\_ANON\_KEY`

\- `SUPABASE\_SERVICE\_ROLE\_KEY` (nur API/Worker)

\- `APP\_ENV` (`stg`/`prod`)



\### Kosten-/Kapazitätsüberwachung

\- Kosten-Monitoring für Cloudflare und Supabase.

\- Alerts bei ungewöhnlichen Kosten-/Nutzungsspitzen.



---



\## 15) Definition of Done (V1.0)



V1.0 ist nur abgeschlossen, wenn:

\- Basis/Pro korrekt getrennt,

\- Journal nur Pro,

\- Public Info-Seite vor Login live,

\- Sprachumschalter überall verfügbar,

\- DE/FR/IT/EN vollständig,

\- PC + Mobile vollständig nutzbar,

\- Security-Baseline umgesetzt,

\- zentrales Fehler-/Ticket-Logging aktiv,

\- preprod strikt von prod getrennt,

\- Admin-Backup/Restore-Flow inkl. Audit verfügbar,

\- Releases/Merges bestehende Userdaten nicht überschreiben,

\- Governance/Retention/Incident/SLO/ADR dokumentiert,

\- `main` + `preprod` inkl. CI-Gates aktiv,

\- Änderungen sauber dokumentiert.



---



\## 16) Schluss



Dieses Dokument ist die kompakte, vollständige und aktuelle \*\*V1.0-Spezifikation\*\* für ALPHEX mit globaler Skalierbarkeit, klarem Schweiz-Bezug im Naming, starker Security-Basis, harter Environment-Trennung, klarer PR-Qualität und datensicherem Release-/Merge-Prozess.



