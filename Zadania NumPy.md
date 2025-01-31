# Test z NumPy – Zaawansowane Zadania

## **Zadanie 1: Tworzenie tablic**  
Utwórz tablicę NumPy o wymiarach 3x3 wypełnioną liczbami losowymi z zakresu od 0 do 10.

- [ ] Stwórz tablicę 3x3 z losowymi liczbami  
- [ ] Zapisz wynik

---

## **Zadanie 2: Podstawowe operacje matematyczne**  
Stwórz tablicę NumPy `a = np.array([2, 4, 6, 8])` i oblicz:
- Pierwiastek kwadratowy z każdego elementu.
- Wartości bezwzględne z każdego elementu.
- Kwadrat każdego elementu.

- [x] Stwórz tablicę `a`  
- [x] Oblicz pierwiastek kwadratowy  
- [x] Oblicz wartości bezwzględne  
- [x] Oblicz kwadrat każdego elementu

---

## **Zadanie 3: Indeksowanie i cięcie tablic**  
Masz tablicę `arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])`. Wybierz:
- Element w drugim wierszu, pierwszej kolumnie.
- Cały drugi wiersz.
- Całą trzecią kolumnę.

- [x] Wybierz element w drugim wierszu, pierwszej kolumnie  
- [x] Wybierz cały drugi wiersz  
- [x] Wybierz całą trzecią kolumnę

---

## **Zadanie 4: Przekształcanie tablic**  
Stwórz tablicę `arr = np.array([1, 2, 3, 4, 5])` i przekształć ją w macierz o wymiarach 5x1.

- [x] Stwórz tablicę `arr`  
- [x] Przekształć ją w macierz 5x1

---

## **Zadanie 5: Operacje na macierzach**  
Stwórz dwie macierze `A = np.array([[1, 2], [3, 4]])` i `B = np.array([[5, 6], [7, 8]])`. Oblicz:
- Sumę tych macierzy.
- Iloczyn macierzy (mnożenie).

- [x] Stwórz macierze `A` i `B`  
- [x] Oblicz sumę macierzy  
- [x] Oblicz iloczyn macierzy

---

## **Zadanie 6: Generowanie liczb losowych**  
Użyj funkcji `np.random.randn()` do wygenerowania 10 liczb losowych z rozkładu normalnego o średniej 0 i odchyleniu standardowym 1.

- [x] Użyj `np.random.randn()`  
- [x] Wygeneruj 10 liczb losowych  
- [x] Zapisz wynik

---

## **Zadanie 7: Statystyki opisowe**  
Stwórz tablicę `arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])`. Oblicz:
- Średnią.
- Mediane.
- Odchylenie standardowe.

- [x] Stwórz tablicę `arr`  
- [x] Oblicz średnią  
- [x] Oblicz medianę  
- [x] Oblicz odchylenie standardowe

---

## **Zadanie 8: Maskowanie tablic**  
Stwórz tablicę `arr = np.array([2, 4, 6, 8, 10])` i wybierz wszystkie elementy większe niż 5.

- [x] Stwórz tablicę `arr`  
- [x] Wybierz elementy większe niż 5

---

## **Zadanie 9: Zmiana kształtu tablicy**  
Stwórz tablicę NumPy o rozmiarze 12 i zmień jej kształt na 3x4.

- [x] Stwórz tablicę o rozmiarze 12  
- [x] Zmień kształt na 3x4

---

## **Zadanie 10: Macierz odwrotna**  
Stwórz macierz `A = np.array([[4, 7], [2, 6]])` i oblicz jej macierz odwrotną.

- [x] Stwórz macierz `A`  
- [x] Oblicz macierz odwrotną

---

## **Zadanie 11: Iloczyn skalarny i wektorowy**  
Masz dwa wektory:  
`v1 = np.array([1, 2, 3])`  
`v2 = np.array([4, 5, 6])`  

- [x] Oblicz **iloczyn skalarny** (dot product).  
- [x] Oblicz **iloczyn wektorowy** (cross product).  

---

## **Zadanie 12: Rozwiązywanie układów równań**  
Rozwiąż układ równań:  

$2x + 3y = 8$  
$5x + 7y = 19$
  
- [x] Zapisz układ w postaci macierzowej `Ax = b`.  
- [x] Oblicz rozwiązanie.  

---

## **Zadanie 13: Znajdowanie wartości własnych i wektorów własnych**  
Masz macierz:  
```python
A = np.array([[2, -1],  
              [-1, 2]])
```
- [ ] Oblicz wartości własne
- [ ] Oblicz wektory własne

---
## **Zadanie 14: Normalizacja danych**  
Masz tablicę `data = np.array([12, 15, 20, 25, 30])`.  
- [x] Znajdź **minimalną i maksymalną wartość**.  
- [x] Przeprowadź **normalizację Min-Max** do zakresu `[0,1]`.  

---

## **Zadanie 15: Średnia ruchoma**  
Masz tablicę `arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])`.  
- [x] Oblicz **średnią ruchomą** dla okna wielkości `3`.  

---

## **Zadanie 16: Monte Carlo – liczba π**  
Wygeneruj `100000` punktów losowych w kwadracie o boku `[-1,1]`.  
- [ ] Policz, ile znajduje się wewnątrz koła o promieniu `1`.  
- [ ] Oszacuj liczbę `π` na podstawie proporcji punktów.  

---
