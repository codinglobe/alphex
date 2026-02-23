# ALPHEX

ALPHEX ist eine modulare, sichere, SQL-first Web-App mit Fokus auf Trading-Workflows (Basis/Pro), Mehrsprachigkeit und klarer Trennung von Staging/Production.

## Projektstatus

- Aktuell liegt der Schwerpunkt auf der Spezifikation und Projektvorbereitung.
- Die vollständigen Anforderungen sind in folgendem Dokument beschrieben:
  - [`PROJECT_ANFORDERUNGEN_UND_EMPFEHLUNGEN.md`](./PROJECT_ANFORDERUNGEN_UND_EMPFEHLUNGEN.md)

## Zielbild (V1.0)

- Cloudflare (Pages + Workers)
- Supabase (Auth + Postgres + Storage)
- Rollen- und Planmodell (Basis/Pro)
- 4 Sprachen ab Start: DE/FR/IT/EN
- Responsive Nutzung auf Desktop und Mobile
- Security-Baseline mit RLS, Audit-Logs und Environment-Isolation

## Geplante Kernbereiche

- Public Info-Seite (vor Login)
- Login/Registrierung
- Dashboard
- Rechner (Basis/Pro)
- Journal (nur Pro)
- Profil
- Tickets
- Community

## Hinweise für Mitwirkende

1. Änderungen immer nachvollziehbar dokumentieren.
2. Auf nicht-destruktive Migrationen achten.
3. Staging und Production strikt getrennt halten.
4. Sicherheits- und Datenschutzanforderungen aus der Spezifikation einhalten.

## Lizenz

Dieses Projekt steht unter der **MIT License**.

- Volltext: [`LICENSE`](./LICENSE)
