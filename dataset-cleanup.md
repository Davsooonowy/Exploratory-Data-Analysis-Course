# Wstępna Analiza Datasetu i Plan Projektu: Credit Risk Modeling

**Dotyczy:** Temat nr 4  
**Zbiór danych:** Lending Club (Kaggle)

---

## 1. Zarys Problemu i Zdefiniowanie Zmiennej Docelowej (Problem Framing)

**Cel główny:** Przewidywanie, czy pożyczka zakończy się niespłaceniem (default) lub odpisaniem w straty (charged-off).

**Zamysł analityczny (Definicja Targetu):**

Zbiór Lending Club nie posiada wprost zdefiniowanej, binarnej zmiennej docelowej gotowej do modelowania. Pierwszym krokiem analitycznym będzie odfiltrowanie pożyczek w toku (np. status "Current", "In Grace Period"), ponieważ ich ostateczny wynik jest nieznany. Następnie utworzony zostanie target na podstawie historycznych, zamkniętych statusów:

* **Klasa 0 (Brak ryzyka):** Statusy oznaczające pełną spłatę (np. "Fully Paid").
* **Klasa 1 (Ryzyko/Default):** Statusy "Charged Off" oraz "Default".

---

## 2. Wstępna Analiza Danych i Czyszczenie (Data Understanding & Cleaning)

Głównym wyzwaniem na wczesnym etapie pracy z tym zbiorem jest zjawisko **wycieku danych (data leakage)**. Model oceniający ryzyko kredytowe przed przyznaniem pożyczki absolutnie nie może opierać się na informacjach pozyskanych w trakcie jej trwania.

* **Wyciek danych (Leakage checks):** Konieczna jest rygorystyczna identyfikacja i eliminacja zmiennych, które aktualizują się po udzieleniu finansowania (np. całkowita spłacona kwota, zebrane opłaty z tytułu opóźnień, kwoty z windykacji, daty ostatnich płatności). 
* **Brakujące wartości i szum (Missing values & label noise):** Analiza zbioru wykazuje zazwyczaj znaczne braki w kolumnach takich jak staż pracy (`emp_length`). Wymagane jest ustalenie logiki imputacji tych braków oraz weryfikacja spójności etykiet.
* **Podstawowa eksploracja (EDA):** Analiza rozkładu kluczowych zmiennych z momentu aplikacji (kwota pożyczki, stopa procentowa, cel finansowania, wskaźnik DTI - Debt-to-Income) w relacji do utworzonej zmiennej docelowej.

---

## 3. Inżynieria Cech i Modelowanie (Wstępny Zarys)

Zgodnie z metodyką end-to-end Data Science pipeline, po przygotowaniu spójnego zbioru danych planowane jest następujące podejście:

* **Pre-processing:** Odpowiednie kodowanie zmiennych kategorialnych (np. status mieszkaniowy, cel pożyczki) oraz skalowanie danych numerycznych.
* **Wybór modeli:** Zbudowanie modelu bazowego opartego na Regresji Logistycznej, a następnie przetestowanie modeli z rodziny gradient boosting (CatBoost, LightGBM), które natywnie radzą sobie ze strukturą danych tabelarycznych.
* **Kalibracja prawdopodobieństwa:** Zastosowanie metod kalibracji (Platt lub izotoniczna), aby zwracane przez model wartości odzwierciedlały faktyczne prawdopodobieństwo wystąpienia zdarzenia.

---

## 4. Ewaluacja, Sprawiedliwość i Interpretowalność (Evaluation & Explanations)
TODO
