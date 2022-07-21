# Euklidesowy problem komiwojażera 

Autor: Jakub Grątkiewicz

## Teoretyczny opis problemu

Problem komiwojażera jest ściśle związany z problemem cyklu Hamiltona. Komiwojażer musi odwiedzić n miast. Modelując problem za pomocą grafu pełnego o n wierzchołkach, można powiedzieć że komiwojażer chce znaleźć marszrutę (cykl Hamiltona) odwiedzając każde miasto dokładnie raz i kończąc w mieście w którym zaczynał wędrówkę. Koszt podróży pomiędzy miastem i a miastem j jest liczba całkowita c(i,j), komiwojażer chce przebyć marszrutę o minimalnym łącznym koszcie, gdzie łączny koszt jest sumą kosztów poszczególnych krawędzi marszruty.

![image](https://user-images.githubusercontent.com/71324202/180169489-d66ebc62-e449-4317-9f56-0f3832bbf688.png)


**Ograniczenia:**

Do prezentacji rozwiązania tego problemu użyte zostaną następujące ograniczenia odnośnie prezentacji grafu:

- Każdy z wierzchołków jest punktem na płaszczyźnie.
- Pomiędzy każdą parą wierzchołków istnieje krawędź, której wagą jest odległość euklidesowa pomiędzy wierzchołkami.

## Opis algorytmu dokładnego służącego do rozwiązania zadanego problemu

Do rozwiązania dokładnego zadania wyznaczeniu optymalnego cyklu Hamiltona, zostanie wykorzystany algorytm brutalny. Jego zadaniem będzie sprawdzenie wszystkich cyklów Hamiltona w grafie i wybranie tego, w którym suma wag krawędzi jest najmniejsza.

1. Stwórz listę wszystkich permutacji wierzchołków w grafie
1. Dodaj na koniec każdej listy pierwszy element listy (każda lista jest cyklem Hamiltona)
1. Znajdź cykl Hamiltona o najmniejszej sumie wag krawędzi.

Kluczową operacją dla działania tego algorytmu jest sprawdzenie wszystkich istniejących cyklów Hamiltona dla grafu. Z własności permutacji wiemy, że istnieje n! takich cyklów, gdzie n jest ilością wierzchołków w grafie. 

![image](https://user-images.githubusercontent.com/71324202/180170225-70e3d5e7-a475-404c-ab3d-dde8ecb9fceb.png)

*Rysunek 1 Określanie wszystkich cykli Hamiltona za pomocą drzewa*

![image](https://user-images.githubusercontent.com/71324202/180170288-fa289bdd-1c4a-4938-8f6c-f9d5285a099b.png)

*Rysunek 2 Przykład dla n=4*

Proces ten można zoptymalizować i ograniczyć się do rozpatrzenie tylko jednego z n utworzonych drzew. Wynika to z tego, że powstałe cykle Hamiltona są identyczne w każdym drzewie, a różnią się jedynie punktem startowym. W ten sposób zostanie sprawdzone jedynie n!/n permutacji, jednak nie zmniejszy to skuteczności algorytmu.

![image](https://user-images.githubusercontent.com/71324202/180170502-5ae7069e-32ca-4b24-bb3e-c617eb65c773.png)

*Rysunek 3 Redundancyjne cykle Hamiltona na podstawie Rysunku 2*

## Opis algorytmu aproksymacyjnego służącego do rozwiązania zadanego problemu
Istnieje algorytm dwu-aproksymacyjny rozwiązujący problem komiwojażera. Oparty on jest na strukturze minimalnego drzewa rozpinającego, której waga stanowi dolne ograniczenie na długość optymalnej marszruty komiwojażera. Następnie przy użyciu minimalnego drzewa rozpinającego utworzymy marszrutę o koszcie co najwyżej dwukrotnie większym niż waga tego drzewa. Lista kroków algorytmu korzystając z oznaczeń opisu teoretycznego: 

1. Wybierz wierzchołek r∈G.V na korzeń
1. Oblicz minimalne drzewo rozpinające T dla G o korzeniu r  za pomocą algorytmu PRIMA
1. Niech H będzie listą wierzchołków drzewa T w kolejności preorder
1. Return cykl Hamiltona H

![image](https://user-images.githubusercontent.com/71324202/180170623-772a454c-ab34-41ee-9a87-51859294c84f.png)

*Rysunek 4 Przykładowy graf*

![image](https://user-images.githubusercontent.com/71324202/180170682-f23def27-7278-4923-aa6d-541f74089fd7.png)

*Rysunek 5 Minimalne drzewo rozpinające – MST (określone algorytmem prima)*

![image](https://user-images.githubusercontent.com/71324202/180170728-a3af1acb-c722-4366-974d-fb858ba2418f.png)

*Rysunek 6 Odwiedzenie wierzchołków w kolejności PREORDER*

![image](https://user-images.githubusercontent.com/71324202/180170791-c67bd3c9-47a1-46fd-9d9d-71f919106939.png)

*Rysunek 7 Rozwiązanie przybliżone: 173.95* 

![image](https://user-images.githubusercontent.com/71324202/180170867-66cd1e0d-a7a8-4f52-a30f-23cdbe1160a1.png)

*Rysunek 8 Rozwiązanie dokładne: 163.25*

## Implementacja algorytmów przy użyciu Notebook Colaboratory i języka Python

Rozwiązanie implementacyjne zostało załączone w postaci pliku TSP.ipynb

*Program 1 Implementacja algorytmów*

Algorytm dokładny: brutForceTSP.

Algorytm aproksymacyjny: approxTSP.

Generator egzemplarzy: generateGraph

Zmierzona złożoność czasowa: timBrutal, timApprox

## Szacowanie złożoności teoretycznej.

Na potrzeby rozważań teoretycznych przyjmuję:

![image](https://user-images.githubusercontent.com/71324202/180172518-4b694fec-8eca-469d-8de2-a8dde265a0ce.png)


### Teoretyczna złożoność obliczeniowa algorytmów.

Dla obu algorytmów nie istnieje pesymistyczna wartość złożoności, ponieważ złożoność algorytmów zależy jedynie od rozmiaru danych i nie zależą od zawartości danych. Dlatego w tym punkcie zostanie oszacowana złożoność oczekiwana, która jest równa złożoności pesymistycznej. 

#### Algorytm dokładny – algorytm brutalny.

Ideą algorytmu brutalnego jest sprawdzenie wszystkich możliwych rozwiązań. Za operację podstawową tego problemu weźmiemy pod uwagę sprawdzenie cyklu Hamiltona. Oszacowaniem naszego algorytmu będzie więc ilość przypadków. Wszystkie przypadki tego algorytmu są określane za pomocą permutacji wierzchołków. Z własności permutacji wynika, że istnieje n! permutacji zbioru o liczności n zatem n! jest złożonością naszego algorytmu. Jak było to opisane we wstępie teoretycznym, istnieje możliwość optymalizacji tego procesu poprzez sprawdzenie tylko permutacji zaczynających się od jednego wierzchołka. Nasza złożoność czasowa tego algorytmu wynosić będzie zatem n!/n. Aproksymacyjne otrzymamy jednak złożoność:

![image](https://user-images.githubusercontent.com/71324202/180172630-4b7bb917-fde7-4bfc-9f77-5a63c6aa3938.png)

#### Algorytm aproksymacyjny.

Określenie złożoności dla użytego algorytmu aproksymacyjnego jest tak naprawdę określeniem złożoności dla algorytmu PRIMA określającego minimalne drzewo rozpinające. Dzieje się tak, ponieważ po otrzymaniu minimalnego drzewa rozpinającego naszym rozwiązaniem jest odczytanie go metodą preorder – co możemy potraktować jako pojedynczą operację. Algorytm PRIMA zaimplementowany został w oparciu o macierz sąsiedztwa. W przypadku tego algorytmu kluczowym elementem jest wyszukiwanie kolejnego wierzchołka położonego w najmniejszej odległości od już dodanych. Czas wyszukania takiego wierzchołka wynosi lgn. Łączny czas wyszukania wszystkich wierzchołków wyniesie zatem  w∙lgn. Przyjmując założenia, że mamy do czynienia z grafem pełnym nieskierowanym wartość w możemy uzależnić od n.

![image](https://user-images.githubusercontent.com/71324202/180172684-d00f2b2d-412a-4dd1-8942-947b57f29006.png)


Z powyższych wyliczeń otrzymujemy zatem, że złożoność algorytmu PRIMA wynosi:

![image](https://user-images.githubusercontent.com/71324202/180172759-79297255-d678-459a-acab-3e2eac70f68a.png)

Algorytm ten jak już było to wspomniane we wstępie teoretycznym jest algorytmem dwu-aproksymacyjnym. Własnością takiego algorytmu jest więc fakt, że znalezione rozwiązanie jest maksymalnie dwa razy gorsze, niż rozwiązanie dokładne.

### Teoretyczna złożoność pamięciowa algorytmów.

#### Algorytm dokładny – algorytm brutalny.

W przypadku algorytmu dokładnego, wykonane zostanie n! list n elementowych, co jest kluczowym elementem określenia złożoności pamięciowej tego algorytmu. Wynika to z faktu, że na początku działania algorytmu tworzone zostają wszystkie permutacje zbioru wierzchołków o liczności n każdy. Podobnie jak w przypadku złożoności obliczeniowej, własność permutacji mówi nam o n! takich przypadków. Złożonością pamięciową przedstawionego algorytmu dokładnego będzie zatem:

![image](https://user-images.githubusercontent.com/71324202/180172839-467c1c3f-75b7-4112-8f68-c3d97e863e62.png)

Rozwiązanie to można jednak zmienić wprowadzając do algorytmu prostą modyfikację, polegającą na generowaniu kolejnych permutacji po czym przejścia do jej sprawdzenia. Modyfikacja  ta pozwoliłaby przechowywać jedynie jedną tablicę o rozmiarze n, zatem złożoność pamięciowa takiego algorytmu wyniosłaby: 

![image](https://user-images.githubusercontent.com/71324202/180172931-9686eab5-b4e9-4f81-85d1-878595fcea7e.png)

#### Algorytm aproksymacyjny.

W przypadku algorytmu aproksymacyjnego utworzone zostanie drzewo o n wierzchołkach. Inne używane mają stały rozmiar więc nie należy brać ich pod uwagę w kontekście liczenia złożoności pamięciowej. Z tego wynika, że pamięciowa złożoność algorytmu aproksymacyjnego wynosi:
\*

![image](https://user-images.githubusercontent.com/71324202/180172992-c43f685a-50c0-4fc3-be88-1e04167cb4fa.png)


## Sprawdzenie poprawności rozważań teoretycznych metodą eksperymentalną

### Porównanie złożoności czasowej – algorytm dokładny.

Do sprawdzenia poprawności przeprowadzonej analizy odnośnie złożoności obliczeniowej algorytmu dokładnego został przeprowadzony eksperyment porównujący obliczoną wartość oczekiwaną z rzeczywistym czasem działania algorytmu. W teście wygenerowano grafy o ilości wierzchołków od 2-9 oraz zmierzono rzeczywisty czas działania algorytmu oraz policzono wartość oczekiwaną obliczoną w punkcie 5.1.1. sprawozdania. Wyniki eksperymentu zostały zestawione na wykresie 1.

![image](https://user-images.githubusercontent.com/71324202/180173092-71a9c412-f0a8-4450-9e02-ab23d2d5e638.png)

*Wykres 1 Wykres złożoności oszacowanej i zmierzonej dla algorytmu dokładnego*

### Porównanie złożoności czasowej – algorytm aproksymacyjny.

Do sprawdzenia poprawności przeprowadzonej analizy odnośnie złożoności obliczeniowej algorytmu aproksymacyjnego został przeprowadzony eksperyment porównujący obliczoną wartość oczekiwaną z rzeczywistym czasem działania algorytmu. W teście wygenerowano po 500 egzemplarzy grafów o rozmiarach od 2 do 50 wierzchołków. Dla każdego z wierzchołków obliczono średni czas działania algorytmu i takie wyniki porównano z wartością określoną w rozważaniach teoretycznych w punkcie 5.1.2. sprawozdania. Wyniki eksperymentu zostały zestawione na wykresie 2.

![image](https://user-images.githubusercontent.com/71324202/180173218-f071757d-377d-4787-8b24-18f788dadc93.png)

*Wykres 2 Wykres złożoności oszacowanej i zmierzonej dla algorytmu aproksymacyjnego*

### Porównanie złożoności rzeczywistej algorytmu dokładnego i aproksymacyjnego

Do porównania złożoności obliczeniowej zastosowanych algorytmów obliczono średnie czasy wykonania algorytmów dla grafów o rozmiarze 2-7 wierzchołków (dla algorytmu dokładnego) oraz 2-10 wierzchołków (dla algorytmu aproksymacyjnego). Każdą średnią policzono z próby 5 grafów każdego rozmiaru. Wyniki zestawiono na wykresie 3.

![image](https://user-images.githubusercontent.com/71324202/180173301-0a9ca4db-135d-4a7e-8ac9-dace1c911427.png)

*Wykres 3 Porównanie złożoności czasowej algorytmu aproksymacyjnego i dokładnego*

### Porównanie odległości rozwiązania dokładnego oraz rozwiązania aproksymacyjnego

Przeprowadzono serię testów grafów o rozmiarze 3-8 wierzchołków gdzie w stu próbach określana była średnia odległość pomiędzy rozwiązaniami oraz ilość znalezionych rozwiązań dokładnych przez algorytm aproksymacyjny. Wyniki zestawiono na wykresach 4 i 5.

![image](https://user-images.githubusercontent.com/71324202/180173367-edeeea14-c3d8-4aca-9e3e-f18b7e3e7039.png)

*Wykres 4 Średnia odległość od rozwiązania dokładnego w zależności od ilości wierzchołków*

![image](https://user-images.githubusercontent.com/71324202/180173399-372ab219-24cd-4611-8ade-46af8ed8c424.png)

*Wykres 5 Liczba znalezionych rozwiązań dokładnych przez algorytm aproksymacyjny*

Dokonano serię 100 pomiarów grafów o rozmiarze 7 wierzchołków i zbadano ich odległości względne (wyrażone w %). Wyniki przedstawiono na wykresie 6.

![image](https://user-images.githubusercontent.com/71324202/180173430-e904b8ff-0e17-4aa5-8c16-41c6b6b673d2.png)

*Wykres 6 Seria 100 pomiarów odległości względnej dla grafów o rozmiarze 7 wierzchołków*

Dokonano serię 100 pomiarów grafów o rozmiarze 5 wierzchołków i zbadano ich odległości względne (wyrażone w %). Wyniki przedstawiono na wykresie 7.

![image](https://user-images.githubusercontent.com/71324202/180173493-34266593-108c-49ad-a13b-1f0ec50ffdf8.png)

*Wykres 7  Seria 100 pomiarów odległości względnej dla grafów o rozmiarze 5 wierzchołków*

## Wnioski

### Porównanie złożoności czasowej

Na podstawie eksperymentów 6.1 oraz 6.2 można stwierdzić, że oszacowana przez nas złożoność czasowa zbiega się ze zmierzoną wartością złożoności. W wyniku eksperymentu 6.3 można zauważyć różnicę w złożoności algorytmu dokładnego oraz aproksymacyjnego.

### Badanie dokładności algorytmu aproksymacyjnego

W eksperymencie 6.4 zostały zmierzone odległości rozwiązań przybliżonych od rozwiązań dokładnych. Na wykresie 4 można zauważyć, że średnia odległość rozwiązania przybliżonego w stosunku do rozwiązania dokładnego rośnie wraz z liczbą wierzchołków grafu. Drugą wartością zmierzoną w badaniu był procent rozwiązań algorytmu aproksymacyjnego, które wskazały wartość dokładną (wykres 5). 

### Podsumowanie

Wyniki eksperymentów pokrywają się z przewidywaniami. Niestety nie udało się zbliżyć do granicy dwuaproksymacyjności algorytmu aproksymacyjnego. Wynika to ze zbyt szybko rosnącego czasu wymaganego do obliczania kolejnych rozwiązań dokładnych. Jednak na podstawie wyników badań (wykresów 4-7) można przypuszczać, że dla dużych problemów rozwiązanie takie jest zbliżone do tej granicy.

Podczas pracy nad projektem zapoznaliśmy się z narzędziem Colaboratory w którym mogliśmy pisać kod w języku Python. Uważamy, że narzędzie to idealnie spełnia rolę narzędzia do implementacji i analizy algorytmów. Dodatkowo mogliśmy dokładnie zapoznać się z problemem komiwojażera, oraz zapoznać się z istniejącymi algorytmami rozwiązującymi ten problem. 

# Bibliografia

[1] Cormen T. H, Leiserson C. E, Rivest R. L, Stein C. (2020) Wprowadzenie do algorytmów, Wydawnictwo Naukowe PWN SA, (23) s. 646-649, (34.5) s. 1121-1122, (35.2) s. 1137-1140.
14 | Strona

