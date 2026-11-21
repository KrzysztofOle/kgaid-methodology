# Audyt gałęzi — 2026-11-21

Zdalne gałęzie GitHub porównane z `main` przed commitem raportu.

| Gałąź | Ostatni commit (UTC) | Ahead / behind | Zawartość techniczna | Rekomendacja |
|---|---|---:|---|---|
| `agent/prepare-kgaid-0.1.0` | 2026-07-21 | 0 / 24 | Przygotowanie wcześniejszej wersji metodologii, brak unikalnych commitów względem `main`. | **[USUNĄĆ]** |
| `feat/github-pages-site` | 2026-07-20 | 7 / 41 | Strona dwujęzyczna w `site/`, CSS, workflow GitHub Pages i zmiany README. Zestaw dawnych commitów nie jest osiągalny z obecnego `main`. | **[DO PRZEGLĄDU]** — porównać stronę i workflow z już opublikowanym serwisem; nie dublować konfiguracji |
| `feat/google-analytics-consent` | 2026-07-20 | 2 / 39 | `site/assets/analytics.js` i zmiany `.github/workflows/pages.yml`, obejmujące analitykę/zgodę. | **[DO PRZEGLĄDU]** — zweryfikować zgodę użytkownika i wpływ na prywatność przed ewentualnym merge |

Nie uruchamiano Pages ani analityki. Brak merge i usuwania gałęzi.
