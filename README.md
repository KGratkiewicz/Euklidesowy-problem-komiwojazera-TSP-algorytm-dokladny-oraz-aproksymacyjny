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

_Rysunek 1 Określanie wszystkich cykli Hamiltona za pomocą drzewa_

![TSP brutforce drawio — kopia (2)](https://user-images.githubusercontent.com/71324202/167785708-fe63a9b0-cc21-49d8-803e-9dd4b975fd0d.png)

_Rysunek 2 Przykład dla n=4_

![TSP brutforce drawio — kopia](https://user-images.githubusercontent.com/71324202/167785710-a964d154-eaa6-4774-916c-1f70c9c9df77.png)


Proces ten można zoptymalizować i ograniczyć się do rozpatrzenie tylko jednego z n utworzonych drzew. Wynika to z tego, że powstałe cykle Hamiltona są identyczne w każdym drzewie, a różnią się jedynie punktem startowym. W ten sposób zostanie sprawdzone jedynie n!/n permutacji, jednak nie zmniejszy to skuteczności algorytmu.

_Rysunek 3 Redundancyjne cykle Hamiltona na podstawie Rysunku 2_

![TSP brutforce drawio](https://user-images.githubusercontent.com/71324202/167785712-df7990f2-fb3e-46e5-9721-cd67abc45cb3.png)



## Opis algorytmu aproksymacyjnego służącego do rozwiązania zadanego problemu

Istnieje algorytm aproksymacyjny rozwiązujący problem komiwojażera. Oparty on jest na strukturze minimalnego drzewa rozpinającego, której waga stanowi dolne ograniczenie na długość optymalnej marszruty komiwojażera. Następnie przy użyciu minimalnego drzewa rozpinającego utworzymy marszrutę o koszcie co najwyżej dwukrotnie większym niż waga tego drzewa. Lista kroków algorytmu korzystając z oznaczeń opisu teoretycznego:

1. Wybierz wierzchołek na korzeń
2. Oblicz minimalne drzewo rozpinające dla o korzeniu za pomocą algorytmu PRIMA
3. Niech będzie listą wierzchołków drzewa w kolejności preorder
4. Return cykl Hamiltona

_Rysunek 4 Przykładowy graf_

![Graf](https://user-images.githubusercontent.com/71324202/167785482-c0426b96-8608-475f-92ac-acf20b336cc6.png)

_Rysunek 5 Minimalne drzewo rozpinające – MST (określone algorytmem prima)_

![MST](https://user-images.githubusercontent.com/71324202/167785489-b1c29e09-ee80-46d5-9039-87565a70e37e.png)


_Rysunek 6 Odwiedzenie wierzchołków w kolejności PREORDER_

![Preorder](https://user-images.githubusercontent.com/71324202/167785498-fef5d374-0cff-48a7-9f0a-f95b1840699d.png)


_Rysunek 7 Rozwiązanie przybliżone: 173.95_

![aprox](https://user-images.githubusercontent.com/71324202/167785472-1329666d-9eee-40e9-91e3-4cc348026056.png)


_Rysunek 8 Rozwiązanie dokładne: 163.25_

![brutal](https://user-images.githubusercontent.com/71324202/167785478-a712ca01-29ca-4d9a-adc6-4729112559d8.png)


