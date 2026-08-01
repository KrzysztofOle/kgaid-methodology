---
document_id: KGAID-CP-006
title: Change Proposal Tool-First LLM Architecture Principle

document_type: governance
status: draft
version: 0.1.0

owner: Governance

approval_status: draft
approved_by:
approved_at:
---

# CP-006 — Tool-First LLM Architecture Principle

## Status propozycji

Ten Change Proposal proponuje przekrojową zasadę architektoniczną KGAID:
powtarzalne, deterministyczne i weryfikowalne operacje mają być domyślnie
realizowane przez dedykowane narzędzia, a modele LLM mają przede wszystkim
interpretować ich wyniki, planować oraz formułować wnioski wymagające
rozumowania.

CP nie zmienia obecnego baseline'u KGAID-0.1.0 ani nie ustanawia nowej normy.
Dokument [KGAID AI Assistant Instructions](../../20-methodology/27-ai-assistant-instructions.md)
jest proponowanym, od razu używalnym profilem instrukcji lokalnych. Przyjęcie
P13 i włączenie obu zmian do przyszłego baseline'u wymaga odrębnej decyzji
Human Authority.

## Problem

W dokumentacji KGAID istnieje niezależny od dostawcy model współpracy człowiek
– AI oraz kontrakt zadania AI, ale nie ma jednej zasady, która architektonicznie
rozdzielałaby odpowiedzialność narzędzi i LLM. W szczególności nie istnieje
wyznaczone miejsce na uniwersalne instrukcje dla ChatGPT ani innych modeli.

Bez tej zasady proces może traktować LLM jako domyślne narzędzie do
wyszukiwania, porównywania, liczenia, walidacji i agregacji. Zaciera to granicę
między obserwowalnym faktem a jego interpretacją oraz niepotrzebnie wiąże
analizę z konkretnym kontekstem i możliwościami modelu.

## Oczekiwany wynik

KGAID powinno jawnie wymagać następującego podziału odpowiedzialności:

- dedykowane narzędzia zbierają i weryfikują fakty w deklarowanym zakresie;
- narzędzia tworzą zwarte, odtwarzalne raporty lub manifesty;
- LLM interpretuje wyniki w kontekście zaakceptowanej wiedzy;
- LLM przygotowuje plan, rekomendację lub pakiet decyzji, nie przejmując
  authority człowieka.

Reguła nie dotyczy oszczędzania tokenów jako celu. Jest niezależną od modelu
zasadą projektowania procesów i ma obowiązywać także wtedy, gdy LLM ma duży
kontekst, niski koszt lub szczególnie dobre zdolności analizy kodu.

## Najlepsze miejsce w metodyce

Rekomendowane są dwa poziomy zapisu:

1. **Zasada fundamentalna:** dodać P13 do
   [KGAID Principles](../../00-foundations/02-principles.md), bezpośrednio po
   P12. Tylko poziom fundamentów zapewnia, że reguła obowiązuje wszystkie
   procesy, profile i przyszłe projekty KGAID.
2. **Instrukcja operacyjna:** utrzymać nowy dokument
   [KGAID AI Assistant Instructions](../../20-methodology/27-ai-assistant-instructions.md)
   w `docs/20-methodology/`. Jest to właściwe miejsce dla przenośnego tekstu
   instrukcji dla ChatGPT oraz przyszłych modeli, ponieważ rozwija on model
   współpracy, a nie zastępuje zasad lub kontraktów.

Sam dokument instrukcji nie powinien być jedynym miejscem reguły: instrukcja
może nie zostać załadowana przez konkretny system AI, a zasada architektoniczna
powinna zachować moc niezależnie od interfejsu z modelem.

## Proponowane brzmienie P13

### P13. Tools gather facts; LLMs reason over them

**Statement:** A KGAID process MUST prefer dedicated tools for repeatable,
deterministic, and verifiable operations. LLMs SHOULD be used primarily to
interpret tool results, plan work, make bounded recommendations, and generate
content that requires reasoning.

**Rationale:** Mechanical fact collection and comparison are best made
reproducible, inspectable, and independent of a particular model. LLMs add the
most value where context, interpretation, trade-offs, and synthesis require
reasoning. Separating these responsibilities lets KGAID retain evidence and
reuse analysis while models, providers, and interfaces change.

**Consequences:**

- repository inventory, comparison, search, validation, aggregation, report
  generation, and similar operations SHOULD be delegated to appropriate tools;
- a tool result SHOULD identify its scope, inputs, configuration, version, and
  limitations sufficiently for the reported facts to be reproduced or
  challenged;
- an LLM MUST distinguish a tool-derived fact from its interpretation,
  assumption, and recommendation;
- a large raw context dump MUST NOT be the default substitute for a compact
  tool report when the task is mechanical;
- an LLM MAY perform a mechanical step when an appropriate tool is unavailable
  or disproportionate, but the result MUST disclose that limitation; and
- projects MAY choose different tools and report formats, but MUST preserve the
  separation of reproducible fact gathering from judgment.

## Reguła operacyjna

Preferowany przebieg pracy jest prosty:

```text
1. narzędzie zbiera fakty;
2. narzędzie tworzy zwarty raport lub manifest;
3. LLM interpretuje raport;
4. LLM formułuje wnioski, decyzje lub rekomendacje.
```

Raport albo manifest jest granicą przekazania pomiędzy analizą mechaniczną i
rozumowaniem. Powinien zawierać zakres, identyfikację wejść, wynik, ograniczenia
oraz odwołanie do surowych danych lub sposobu ich odtworzenia. Nie nadaje
samodzielnie authority żadnej decyzji.

## Przykłady

| Sytuacja | Preferowany podział | Niepreferowany wariant |
| --- | --- | --- |
| Ocena wpływu zmian | `git diff` lub równoważne narzędzie ustala zmienione pliki, symbole i testy; LLM ocenia wpływ na architekturę, kontrakty i delivery. | LLM sam przeszukuje pełny kod wyłącznie po to, aby mechanicznie znaleźć różnice. |
| Analiza setek plików | Narzędzie inwentaryzuje pliki, zależności, hotspoty i naruszenia; LLM formułuje rekomendację architektoniczną. | Przesłanie całego repozytorium do LLM bez uprzedniego zawężenia faktów. |
| Zmiana schematu danych | Narzędzie porównuje snapshoty SQL i raportuje dodane, usunięte i zmienione obiekty; LLM interpretuje konsekwencje migracji i kompatybilności. | Ręczne porównywanie snapshotów przez LLM bez odtwarzalnego diffu. |
| Porównanie dużych fragmentów kodu | Narzędzie wykonuje porównanie i tworzy manifest różnic; LLM wyjaśnia znaczenie wykrytych zmian. | Przekazanie tysięcy linii kodu do LLM tylko w celu mechanicznego porównania. |

## Uzasadnienie architektoniczne

Rozdzielenie odpowiedzialności przynosi korzyści niezależne od konkretnego LLM:

- ogranicza koszt obliczeniowy, ponieważ pracę deterministyczną wykonują
  mechanizmy do tego przeznaczone;
- ogranicza zużycie kontekstu, ponieważ model otrzymuje zwarty wynik zamiast
  nieuporządkowanego materiału źródłowego;
- zwiększa powtarzalność dzięki odtwarzalnemu zakresowi, konfiguracji i
  wynikowi narzędzia;
- pozwala wykonywać i przechowywać analizę niezależnie od wybranego modelu LLM;
- pozwala wielokrotnie użyć tego samego narzędzia oraz raportu przez różne
  modele, ludzi i niezależne kontrole;
- ułatwia review, ponieważ można niezależnie zakwestionować fakty z narzędzia,
  interpretację LLM albo decyzję człowieka.

## Proponowane zmiany po decyzji

Po zaakceptowaniu CP należy wykonać spójną zmianę normatywną:

1. dodać P13 w `docs/00-foundations/02-principles.md` oraz dopisać ją do
   przekrojowych zasad w sekcji „Relationship Between the Principles”;
2. uaktualnić `docs/20-methodology/22-human-ai-collaboration.md`, w
   szczególności Context Package i AI Execution Protocol, aby wymagały
   identyfikacji narzędzia, zakresu oraz raportu jako wejścia do interpretacji;
3. uaktualnić `docs/20-methodology/23-ai-execution-task-contract.md`, aby plan
   weryfikacji i format handoffu rozróżniały raport faktów od rekomendacji LLM;
4. zaakceptować, odpowiednio zrewidować i włączyć `KGAID-MTH-007` do nowego
   baseline'u jako przenośny profil instrukcji dla AI;
5. zaktualizować indeksy repozytorium, mapowanie zasad, manifest przyszłego
   baseline'u i — jeśli zasady zaakceptowane w repozytorium są prezentowane na
   stronie — oba warianty językowe strony;
6. wykonać repository controls, testy narzędzi i kontrolę linków na dokładnej
   rewizji kandydackiej.

## Compatibility i migracja

Zasada nie narzuca dostawcy LLM, frameworka agentowego, języka ani konkretnej
nazwy narzędzia. Projekty mogą zachować istniejące prompty i automatyzacje, ale
dla materialnych procesów powinny jawnie określić, które kroki zbierają fakty
narzędziowo, jaki raport przekazują do LLM i kiedy odstępstwo jest
proporcjonalne.

Przyszły rollout powinien być stopniowy:

1. zinwentaryzować powtarzalne działania wykonywane obecnie przez LLM;
2. wyodrębnić najpierw kroki o wysokiej skali, deterministyczności lub ryzyku;
3. dodać odtwarzalne narzędzia i zwarte raporty bez zmiany authority;
4. zaktualizować instrukcje i task contracts;
5. monitorować błędne interpretacje, niekompletne manifesty i przypadki, w
   których automatyzacja byłaby nieproporcjonalna.

Nie należy wymagać stworzenia dedykowanego narzędzia dla jednorazowego,
małego lub wysoce interpretacyjnego zadania. To byłoby sprzeczne z P11 o
proporcjonalności do ryzyka i niepewności.

## Wpływ normatywny i SemVer

Propozycja dodaje obowiązek przekrojowy do KGAID Principles i zmienia oczekiwany
kształt współpracy z AI. Powinna dlatego wejść do przyszłego baseline'u jako
zmiana normatywna, nie jako fakultatywna wskazówka optymalizacji. Wstępna ocena
to co najmniej **minor release** przed `1.0.0`; decyzja Human Authority może
podnieść wpływ, jeśli przyjęcie ustanowi nowy obowiązkowy warunek conformance
dla już deklarujących zgodność projektów.

## Ocena statusu fundamentalnego

**Rekomendacja: tak.** Zasada powinna zostać uznana za fundamentalną,
cross-cutting architectural principle KGAID. Nie opisuje jednego procesu,
narzędzia ani modelu, lecz trwały podział odpowiedzialności między
automatyzacją faktów i rozumowaniem. Wpływa równocześnie na projektowanie
procesów, task contracts, evidence, traceability, quality, security oraz
przenośność pomiędzy modelami.

P13 wzmacnia istniejące P8 (claims do not exceed evidence), P10 (AI assists;
humans remain accountable), P11 (rigor is proportional to risk and
uncertainty) oraz P12 (tool and implementation independence), ale nie wynika z
żadnej z nich dostatecznie jednoznacznie. Własna zasada jest uzasadniona, aby
uniknąć domyślnego używania LLM do czynności mechanicznych w przyszłych
projektach.

## Evidence, ograniczenia i wymagane review

CP opiera się na analizie architektonicznej metodyki, a nie na claimie
potwierdzonej skuteczności między projektami. Przed przyjęciem należy zebrać
evidence z co najmniej jednego reprezentatywnego procesu, pokazujące:

- zakres wejściowy i narzędzie wykonujące analizę;
- stabilny raport lub manifest oraz możliwość jego ponownego użycia przez co
  najmniej dwa konteksty interpretacyjne, gdy jest to proporcjonalne;
- oddzielenie faktów, interpretacji i decyzji;
- koszt, ograniczenia, błędy oraz przypadki uzasadnionego odstępstwa;
- wpływ na kontekst, powtarzalność i jakość review bez szerszych claimów niż
  wspierają dowody.

Review powinien objąć Architecture, Quality, Governance i co najmniej jeden
projekt adopcyjny. Human Authority rozstrzyga: brzmienie P13, minimalny zakres
conformance, wymagania dla MTH-007, wpływ SemVer oraz inclusion w baseline.
