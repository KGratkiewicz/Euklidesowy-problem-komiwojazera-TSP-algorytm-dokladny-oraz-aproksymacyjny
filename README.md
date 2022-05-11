# Euklidesowy problem komiwojażera


## Teoretyczny opis problemu

Problem komiwojażera jest ściśle związany z problemem cyklu Hamiltona. Komiwojażer musi odwiedzić miast. Modelując problem za pomocą grafu pełnego o wierzchołkach, można powiedzieć że komiwojażer chce znaleźć marszrutę (cykl Hamiltona) odwiedzając każde miasto dokładnie raz i kończąc w mieście w którym zaczynał wędrówkę. Koszt podróży pomiędzy miastem a miastem jest liczba całkowita , komiwojażer chce przebyć marszrutę o minimalnym łącznym koszcie, gdzie łączny koszt jest sumą kosztów poszczególnych krawędzi marszruty.

**Ograniczenia:**

Do prezentacji rozwiązania tego problemu użyte zostaną następujące ograniczenia odnośnie prezentacji grafu:

- Każdy z wierzchołków jest punktem na płaszczyźnie.
- Pomiędzy każdą parą wierzchołków istnieje krawędź, której wagą jest odległość arytmetyczna pomiędzy wierzchołkami.


## Opis algorytmu dokładnego służącego do rozwiązania zadanego problemu

Do rozwiązania dokładnego zadania wyznaczeniu optymalnego cyklu Hamiltona, zostanie wykorzystany algorytm brutalny. Jego zadaniem będzie sprawdzenie wszystkich cyklów Hamiltona w grafie i wybranie tego, w którym suma wag krawędzi jest najmniejsza.

1. Stwórz listę wszystkich permutacji wierzchołków w grafie
2. Dodaj na koniec każdej listy pierwszy element listy (każda lista jest cyklem Hamiltona)
3. Znajdź cykl Hamiltona o najmniejszej sumie wag krawędzi.

Kluczową operacją dla działania tego algorytmu jest sprawdzenie wszystkich istniejących cyklów Hamiltona dla grafu. Z własności permutacji wiemy, że istnieje n! takich cyklów, gdzie n jest ilością wierzchołków w grafie.

![](RackMultipart20220511-1-oiophh_html_6b06643872e85df7.png)

_Rysunek 1 Określanie wszystkich cykli Hamiltona za pomocą drzewa_

![](RackMultipart20220511-1-oiophh_html_df88c196a4cec6b7.png)

_Rysunek 2 Przykład dla n=4_

Proces ten można zoptymalizować i ograniczyć się do rozpatrzenie tylko jednego z n utworzonych drzew. Wynika to z tego, że powstałe cykle Hamiltona są identyczne w każdym drzewie, a różnią się jedynie punktem startowym. W ten sposób zostanie sprawdzone jedynie n!/n permutacji, jednak nie zmniejszy to skuteczności algorytmu.

![](RackMultipart20220511-1-oiophh_html_9f8bf8362eeb3b62.png)

_Rysunek 3 Redundancyjne cykle Hamiltona na podstawie Rysunku 2_


## Opis algorytmu aproksymacyjnego służącego do rozwiązania zadanego problemu

Istnieje algorytm aproksymacyjny rozwiązujący problem komiwojażera. Oparty on jest na strukturze minimalnego drzewa rozpinającego, której waga stanowi dolne ograniczenie na długość optymalnej marszruty komiwojażera. Następnie przy użyciu minimalnego drzewa rozpinającego utworzymy marszrutę o koszcie co najwyżej dwukrotnie większym niż waga tego drzewa. Lista kroków algorytmu korzystając z oznaczeń opisu teoretycznego:

1. Wybierz wierzchołek na korzeń
2. Oblicz minimalne drzewo rozpinające dla o korzeniu za pomocą algorytmu PRIMA
3. Niech będzie listą wierzchołków drzewa w kolejności preorder
4. Return cykl Hamiltona

![](RackMultipart20220511-1-oiophh_html_7f2c5a67a71adb88.png)

_Rysunek 4 Przykładowy graf_

![](RackMultipart20220511-1-oiophh_html_8e967d1b086a93b2.png)

_Rysunek 5 Minimalne drzewo rozpinające – MST (określone algorytmem prima)_

![](RackMultipart20220511-1-oiophh_html_5e8a89aab33b82a4.png)

_Rysunek 6 Odwiedzenie wierzchołków w kolejności PREORDER_

![](RackMultipart20220511-1-oiophh_html_9047551e4cbe8098.png)

_Rysunek 7 Rozwiązanie przybliżone: 173.95_

![](RackMultipart20220511-1-oiophh_html_719a67ed93a6af92.png)

_Rysunek 8 Rozwiązanie dokładne: 163.25_
