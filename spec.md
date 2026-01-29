# PROJEKT: SOLANA PRIVACY SCORE (BACKEND ENGINE)

Jesteś Senior TypeScript Developerem. Twoim zadaniem jest napisanie kompletnego silnika analizy portfela w czystym TypeScript (Node.js).

## CEL

Chcę mieć działający skrypt, który po wpisaniu adresu portfela zwraca JSON z oceną prywatności (0-100) i rekomendacjami.

## STRUKTURA PROJEKTU (Folder `src`)

Proszę utwórz folder `src` i wewnątrz następujące pliki:

1. `src/constants.ts`
   - Tablica `KNOWN_CEX`: Dodaj prawdziwe adresy hot walletów (Binance, Coinbase, Kraken) - znajdź je lub wymyśl wiarygodne placeholdery.
   - Lista `RECOMMENDED_TOOLS`: Privacy Cash, Radr Labs, Range.

2. `src/services/helius.ts`
   - Klasa `HeliusService`.
   - Metoda `getHistory(address)`: Pobiera 100 ostatnich transakcji (parsed).
   - Obsługa błędów: Jeśli brak klucza API, zwróć puste dane (nie crashuj).

3. `src/services/range.ts` (Mock Compliance)
   - Funkcja `checkRisk(address)`: Zwraca "Clean" lub "Sanctioned".

4. `src/detectors/` (Folder z logiką)
   - `cex.ts`: Sprawdza czy w historii są transakcje z `KNOWN_CEX`.
   - `clustering.ts`: Prosta logika - czy 50%+ transakcji jest z tym samym adresem?
   - `assets.ts`: Czy posiada NFT (POAP) lub domeny .sol?

5. `src/engine.ts` (GŁÓWNY PLIK)
   - Funkcja `analyzeWallet(address)`.
   - Zbiera dane z Helius.
   - Odpala detektory.
   - Liczy punkty (Start 100 pkt -> odejmuje za błędy).
   - Zwraca raport: { score, riskLevel, warnings[], actions[] }.

6. `src/run.ts` (PLIK TESTOWY)
   - Skrypt, który importuje `analyzeWallet`.
   - Uruchamia analizę dla przykładowego adresu.
   - Wypisuje wynik w `console.log`.

## WYMAGANIA TECHNICZNE

- Użyj `dotenv` do ładowania zmiennych.
- Kod ma być gotowy do uruchomienia przez `npx ts-node src/run.ts`.
- Bądź kreatywny z rekomendacjami ("Use Privacy Cash to fix this").
