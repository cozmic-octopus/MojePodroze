# Testy mutacyjne

## Czym są
Testy mutacyjne sprawdzają jakość testów. Narzędzie automatycznie wprowadza do kodu
drobne zmiany (mutacje), np. zamienia `>` na `>=`, i uruchamia testy. Jeśli testy
wykryją zmianę (zawiodą), mutant jest „zabity”. Jeśli testy dalej przechodzą,
mutant „przeżył”, czyli testy nie sprawdzają tego fragmentu wystarczająco dokładnie.

## Narzędzie i konfiguracja
- narzędzie: mutmut 3.8.0
- mutowany kod: `backend/app/domain/`
- uruchamiane testy: `backend/tests/unit/domain`
- konfiguracja: `backend/pyproject.toml` (sekcja `[tool.mutmut]`)

## Jak uruchomić
GitHub → Actions → Backend → Run workflow → zaznaczyć „Uruchom testy mutacyjne”.
Definicja zadania: `.github/workflows/backend.yml` (job `mutation`).

## Wynik początkowy
- liczba mutantów: 463
- zabite: 435
- ocalałe: 28
- mutation score: 93,95%

#### Zrzut ekranu z wynikiem pierwszych testów:
<img width="929" height="893" alt="image" src="https://github.com/user-attachments/assets/7088099b-c2e2-4cc3-8ca6-0c7f8289782c" />

## Przeanalizowane ocalałe mutanty

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| (nazwa z `mutmut results`) | (opis zmiany) | (czego nie sprawdzał żaden test) | dodano test `test_...` w pliku `...` |

## Mutanty równoważne
Mutanty, których nie da się zabić, bo zmiana nie wpływa na działanie programu:

- (nazwa mutanta) – uzasadnienie: ...

## Wynik końcowy
- zabite: X
- ocalałe: X
- mutation score: X%

![Wynik końcowy](img/po.png)

## Wnioski
<!--(2-3 zdania: co poprawiło się po dopisaniu testów, które moduły były najsłabiej przetestowane) -->
