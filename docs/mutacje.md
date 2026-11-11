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

<!--
## Przeanalizowane ocalałe mutanty

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| (nazwa z `mutmut results`) | (opis zmiany) | (czego nie sprawdzał żaden test) | dodano test `test_...` w pliku `...` |
-->
# Analiza mutantów, które przeżyły

Poniższa tabela przedstawia mutanty, które przeżyły pierwsze uruchomienie testów mutacyjnych (`mutmut`). Celem dalszych prac jest uzupełnienie testów jednostkowych tak, aby wykrywały istotne zmiany w zachowaniu aplikacji.

Status początkowy: `survived`.

## 1. Moduł currency

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `convert_to_pln__mutmut_3` | Dodano `XX` na początku i końcu komunikatu o ujemnej kwocie. | Test sprawdza wystąpienie `ValueError`, ale nie weryfikuje dokładnej treści komunikatu. | Do zrobienia: dodać test `test_convert_to_pln_negative_amount_error_message`. |
| `convert_to_pln__mutmut_4` | Zmieniono pierwszą literę komunikatu z wielkiej na małą. | Brak asercji sprawdzającej dokładną treść komunikatu. | Do zrobienia: uwzględnić dokładny komunikat w teście dla ujemnej kwoty. |
| `convert_to_pln__mutmut_8` | Dodano `XX` do komunikatu o niedodatnim kursie. | Brak asercji sprawdzającej dokładną treść komunikatu. | Do zrobienia: dodać test `test_convert_to_pln_non_positive_rate_error_message`. |
| `convert_to_pln__mutmut_9` | Zmieniono pierwszą literę komunikatu o kursie z wielkiej na małą. | Brak asercji sprawdzającej dokładną treść komunikatu. | Do zrobienia: uwzględnić dokładny komunikat w teście dla niedodatniego kursu. |

## 2. Moduł common

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `trip_length_days__mutmut_3` | Dodano `XX` do komunikatu o nieprawidłowym zakresie dat. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: dodać test `test_trip_length_days_invalid_dates_error_message`. |
| `trip_length_days__mutmut_4` | Zmieniono pierwszą literę komunikatu z wielkiej na małą. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: uwzględnić dokładny komunikat w teście nieprawidłowego zakresu dat. |

## 3. Moduł trip_types

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `ensure_type_change_allowed__mutmut_17` | Separator `", "` w nazwach zablokowanych sekcji zastąpiono tekstem `"XX, XX"`. | Prawdopodobnie brakuje testu sprawdzającego komunikat przy więcej niż jednej zablokowanej sekcji. | Do zrobienia: dodać test `test_ensure_type_change_allowed_multiple_blocked_sections_message`. |

## 4. Moduł costs – porównywanie budżetu

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `compare_with_budget__mutmut_17` | Dodano `XX` do komunikatu o nieprawidłowym budżecie. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: dodać test `test_compare_with_budget_invalid_budget_error_message`. |
| `compare_with_budget__mutmut_18` | Zmieniono pierwszą literę komunikatu z wielkiej na małą. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: uwzględnić dokładny komunikat w teście nieprawidłowego budżetu. |
| `compare_with_budget__mutmut_36` | Zmieniono warunek `difference > ZERO` na `difference >= ZERO`. | Brakuje testu sprawdzającego sytuację, w której wydatki są dokładnie równe budżetowi. | Do zrobienia: dodać test `test_compare_with_budget_spent_equals_budget`. |
| `compare_with_budget__mutmut_40` | Zmieniono warunek `difference < ZERO` na `difference <= ZERO`. | Brakuje testu sprawdzającego sytuację, w której wydatki są dokładnie równe budżetowi. | Do zrobienia: dodać test `test_compare_with_budget_spent_equals_budget`. |

## 5. Moduł costs – podsumowanie kosztów

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `summarize_costs__mutmut_4` | Dodano `XX` do komunikatu o podróży trwającej mniej niż jeden dzień. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: dodać test `test_summarize_costs_invalid_trip_days_error_message`. |
| `summarize_costs__mutmut_5` | Zmieniono pierwszą literę komunikatu z wielkiej na małą. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: uwzględnić dokładny komunikat w teście nieprawidłowej liczby dni. |
| `summarize_costs__mutmut_17` | Zmieniono argument `trip_type` na `None` w wywołaniu `is_section_allowed`. | Prawdopodobnie brakuje testu weryfikującego filtrowanie sekcji niedostępnych dla konkretnego typu podróży. | Do zrobienia: dodać test `test_summarize_costs_excludes_sections_not_allowed_for_trip_type`. |

## 6. Moduł stays

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `overlaps__mutmut_3` | Zmieniono operator `<` na `<=` przy porównywaniu dat granicznych noclegów. | Brakuje testu sprawdzającego dwa noclegi, z których jeden kończy się dokładnie w dniu rozpoczęcia drugiego. | Do zrobienia: dodać test `test_stays_with_adjacent_dates_do_not_overlap`. |
| `ensure_no_overlapping_stays__mutmut_4` | Zmieniono `continue` na `break` przy pomijaniu noclegu o tym samym identyfikatorze. | Prawdopodobnie brakuje testu, w którym edytowany nocleg znajduje się przed innym noclegiem kolidującym na liście. | Do zrobienia: dodać test `test_ensure_no_overlapping_stays_checks_items_after_same_id`. |
| `ensure_check_out_within_trip__mutmut_4` | Usunięto treść komunikatu wyjątku i zastąpiono ją `None`. | Test prawdopodobnie sprawdza tylko typ wyjątku, a nie jego komunikat. | Do zrobienia: dodać test `test_ensure_check_out_within_trip_error_message`. |

## 7. Moduł errors

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `DomainError__init____mutmut_1` | Zmieniono wywołanie `super().__init__(message)` na `super().__init__(None)`. | Testy mogą sprawdzać atrybut `message`, ale nie sprawdzają wyniku `str(exception)`. | Do zrobienia: dodać test `test_domain_error_string_representation`. |

## 8. Moduł items

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `TripItem__post_init____mutmut_3` | Dodano `XX` do komunikatu o ujemnym koszcie. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: dodać test `test_trip_item_negative_cost_error_message`. |
| `TripItem__post_init____mutmut_4` | Zmieniono pierwszą literę komunikatu z wielkiej na małą. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: uwzględnić dokładny komunikat w teście ujemnego kosztu. |

## 9. Moduł album

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `group_by_day__mutmut_6` | Zmieniono `sorted(..., key=lambda pair: pair[0])` na `sorted(..., key=None)`. | Mutacja prawdopodobnie nie zmienia zachowania: domyślne sortowanie krotek również porządkuje je według pierwszego elementu, czyli daty. | Do oceny jako mutant równoważny. |
| `group_by_day__mutmut_8` | Usunięto argument `key` z wywołania `sorted`. | Mutacja jest równoważna oryginałowi: domyślne sortowanie daje ten sam rezultat. | Do oceny jako mutant równoważny. |

## 10. Moduł recommendations

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `rank_recommendations__mutmut_3` | Zmieniono `continue` na `break` dla wizyty bez oceny. | Prawdopodobnie brakuje testu, w którym wizyta bez oceny występuje przed kolejnymi ocenionymi wizytami. | Do zrobienia: dodać test `test_rank_recommendations_skips_unrated_visits`. |
| `rank_recommendations__mutmut_16` | Zmieniono `continue` na `break` przy pomijaniu grup o zbyt niskiej średniej ocenie. | Prawdopodobnie brakuje testu, w którym grupa niespełniająca progu występuje przed grupą spełniającą próg. | Do zrobienia: dodać test `test_rank_recommendations_continues_after_low_rating_group`. |
| `rank_recommendations__mutmut_36` | Zmieniono warunek wyboru wyników z `limit is None` na `limit is None and False`. | Mutacja jest równoważna: gdy `limit is None`, wyrażenie `ranked[:limit]` zwraca całą listę, tak samo jak oryginalna funkcja. | Do oceny jako mutant równoważny. |

## 11. Moduł status

| Mutant | Co zmieniono | Dlaczego przeżył | Co zrobiono |
|---|---|---|---|
| `ensure_transition_allowed__mutmut_7` | Dodano `XX` do drugiej części komunikatu o niedozwolonej zmianie statusu. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: dodać test `test_ensure_transition_allowed_error_message`. |
| `ensure_transition_allowed__mutmut_8` | Zmieniono pierwszą literę drugiej części komunikatu z wielkiej na małą. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: uwzględnić dokładny komunikat w teście niedozwolonej zmiany statusu. |
| `ensure_transition_allowed__mutmut_9` | Zmieniono drugą część komunikatu na tekst zapisany wielkimi literami. | Test nie sprawdza dokładnej treści komunikatu wyjątku. | Do zrobienia: uwzględnić dokładny komunikat w teście niedozwolonej zmiany statusu. |

<!--
## Uwagi do dalszych prac

1. W pierwszej kolejności należy uzupełnić testy komunikatów błędów, ponieważ komunikaty są wyświetlane użytkownikowi aplikacji.
2. Następnie należy uzupełnić testy przypadków brzegowych i warunków granicznych.
3. Mutanty równoważne należy udokumentować i wyłączyć z oceny mutation score, jeśli konfiguracja narzędzia na to pozwala.
4. Po każdej zmianie należy ponownie uruchomić testy i sprawdzić wynik mutacji.

Ważne: proponowane przyczyny przeżycia mutantów wymagają potwierdzenia przez analizę istniejących testów. Nazwy nowych testów mają charakter propozycji.
-->
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
