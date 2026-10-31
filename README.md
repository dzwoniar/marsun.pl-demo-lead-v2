# Marsun — lead magnet, wariant v2

Rozwinięty wariant statycznego landing page promującego PDF o konfiguracji falowników Deye. Projekt demonstruje formularz pozyskania kontaktu, obsługę stanów interfejsu, popup i mobilne wezwanie do działania.

Kod realizuje demonstrację frontendu. Nie wysyła zgłoszeń ani materiałów e-mailem.

## Funkcje interfejsu

- Formularz imienia, adresu e-mail, opcjonalnego NIP i wymaganej zgody.
- Natywna walidacja pól HTML, czyszczenie znaków i formatowanie NIP.
- Symulowana wysyłka z wyłączonym przyciskiem i ekranem potwierdzenia po 1,2 s.
- Popup uruchamiany przy opuszczaniu strony lub po 45 s, z flagą sesji ograniczającą powtórzenia.
- Przeniesienie adresu e-mail z popupu do głównego formularza.
- Mobilny pasek CTA, animacje sekcji i dodatkowe CTA do szkolenia na ekranie potwierdzenia.

## Podgląd lokalny

Wymagania: współczesna przeglądarka i Python 3 do prostego serwera plików.

```bash
git clone https://github.com/dzwoniar/marsun.pl-demo-lead-v2.git
cd marsun.pl-demo-lead-v2
python -m http.server 8000 --bind 127.0.0.1
```

Przejdź do [http://localhost:8000](http://localhost:8000). Na Windows można użyć `py` zamiast `python`. `Ctrl+C` zatrzymuje serwer. Projekt nie wymaga menedżera pakietów ani budowania.

## Struktura i przepływ danych

```text
.
├── index.html   # treść, style, formularz i skrypty
└── README.md
```

[index.html](index.html) łączy HTML5, CSS i JavaScript bez frameworka. Fonty DM Sans i Playfair Display pochodzą z Google Fonts i są ładowane przez sieć. Animacje korzystają z `IntersectionObserver`.

Główny formularz przechodzi walidację HTML, następnie `handleSubmit()` zatrzymuje wysyłkę przez `preventDefault()`. Po opóźnieniu przełącza widok formularza na potwierdzenie. Popup tylko kopiuje e-mail do głównego pola. `sessionStorage` przechowuje flagę `marsun_popup_shown`; dane kontaktowe nie są zapisywane przez aplikację do magazynu przeglądarki.

Warunkowe wywołania `gtag` i `fbq` mogą emitować zdarzenie leada, jeśli takie funkcje zostały dostarczone z zewnątrz. Repozytorium nie zawiera ich bibliotek ani konfiguracji.

## Ograniczenia

- Komunikat o wysłaniu materiału jest symulacją. Nie ma backendu, bazy kontaktów, integracji mailingowej ani pliku PDF.
- Formatowanie NIP nie obejmuje sprawdzenia sumy kontrolnej ani zapytania do rejestru firm.
- Link polityki prywatności i CTA do szkolenia na ekranie sukcesu mają `href="#"`.
- Opinie, liczby i obietnice handlowe są elementami treści prototypu; kod nie potwierdza ich aktualności.
- Brakuje skonfigurowanego zestawu testów automatycznych i procesu wdrożenia.

## Kontekst wersji

[Pierwszy wariant](https://github.com/dzwoniar/marsun.pl-lead) zawiera ten sam podstawowy mechanizm formularza. Wariant v2 rozszerza prezentację materiału i ekran potwierdzenia. Osobny [landing B2B v2](https://github.com/dzwoniar/marsun.pl-demo-v2) demonstruje ofertę i kalkulator kosztu awarii.
