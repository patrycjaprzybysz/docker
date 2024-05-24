# docker



## 1. Uruchomienie pierwszego kontenera

* Uruchomienie kontenera na podstawie ubuntu

```
docker run ubuntu ls -l

```
 Polecenie ```ls -l``` wyświetla listę plików i katalogów w bieżącym katalogu z opcją wyświetlania szczegółowych informacji.

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/6f34d0b2-420b-42e6-91fa-7c2e3606bd1f)

* Sprawdzenie wersji jądra systemu operacyjnego

```
docker run ubuntu uname -a

```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/4415522a-00f3-4ee7-bb34-3bec4d8ca5d8)

* uruchomienie nowego kontenera na podstawie debian (te same jądro systemu)

```
docker run debian uname -a

```

* uruchomienie interaktywnego kontenera na podstawie ubuntu

```
docker run --interactive --tty ubuntu bash

```
* Stworzenie pliku txt i wyświetlenie jego zawartości

```
echo "skni" > skni.txt
cat skni.txt
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/c3b91a65-bccd-42cf-b3fe-bdaad268c18a)

* wyswietlenie wszystkich stworzonych kontenerów

```
docker container ls -a
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/7ed3146b-f593-4731-8cd0-c13193630c9f)

* uruchomienie kontenera o podanym id

```
docker start <id>
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/78988809-4b7f-4122-8b9d-238b99f05eef)

* otworzenie pliku zapisanego w kontenerze o podanym id (exec umozliwia wykonywanie operacji)
```
docker exec <id> cat skni.txt
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/c740ba0f-552a-423d-a923-b96e04a992ad)


## 2. Jak działają obrazy dockerowe?

* utworzenie nowej warstwy obrazu
```
docker commit <id kontenera> skni_img

```

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/a3034ff5-cfb7-4d5e-b2f6-c373629f4b4c)

* wyswietlenie wszytskich obrazow
```
docker image ls

```

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/f4847d2b-38fe-4a15-9da2-ce3d6711e333)

* wyswietlenie wszytskich warstw składajacych się na obraz
```
docker history skni_img

```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/908245e7-bd13-41b7-9148-137b4063c4bc)

* wyswietlenie wszytskich warstw składajacych się na ubuntu (widać ze skni_img ma warstwy ubuntu i jedną nową swoją dodaną)
```
docker history ubuntu

```

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/06713ba9-d091-40c8-bbe0-36738b796390)

* stworzenie kontenera na podstawie obrazu
```
docker run -it skni_img bash

```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/4150f90e-53e9-4856-a9b9-04670b677280)

* sprawdzenie czy w naszym kontenerze skni_img mamy plik skni.txt oraz zainstalowanie vim'a
```
cat skni.txt
apt update && apt install vim
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/525a666c-7403-41b5-b084-8e77f60f443c)

* utworzenie obrazu vim_img
```
docker commit 1b40 vim_img
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/a4e3ff1b-dbf3-466e-9052-eada8632765b)

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/8c3f17ff-49cd-4dbf-bb55-6af29d9a4753)

* wyswitelenie wszystkich warstw składających się na vim_img

```
docker history vim_img
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/98f57cae-9ba1-4094-806a-70c372a1e84c)


## 3. Docker hub

Docker Hub jest hostowanym rejestrem Docker zarządzanym przez Docker. Docker Hub zawiera ponad 100 000 obrazów kontenerów, pochodzących od dostawców oprogramowania, projektów open source i społeczności.

* pobranie i zapisanie obrazu

```
docker pull postgres
```

*zmiana nazwy obrazu (stary obraz sie nie usuwa, id jest to samo)
zeby ddoac obraz na docker hub musi byc zawarta nazwa uzytkownika

```
docker tag skni_img patrycjaprzybysz/obraz
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/5c77e959-a2a9-44f1-b398-11a3edb9dded)

* wgrywanie obrazu

```
docker push patrycjaprzybysz/obraz
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/1a0e4d43-b5cc-47ed-b0f8-7f4cef780e30)

## 4. Kopiowanie plików - Polecenie docker cp

*skopiowanie pliku polega na podaniu miejsca kopiowanego pliku i miejsca do którego chcemy skopiowac ( . - bieżacy katalog)

```
 docker cp affectionate_banach:/skni.txt .

```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/547778e7-791d-41b5-9610-89097092900c)

* kopiowanie z powrotem do kontenera pliku

  ```
  docker cp skni.txt affectionate_banach:/
  ```
  
## 5. Dockerfile, czyli automatyczne budowanie obrazów

* stworzenie pliku Dockerfile i wpisanie tam komend

```
notepad Dockerfile

```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/22c114bc-7101-4546-bb6d-5e174057593e)

* zbudowanie dockerfile w biezącym katalogu

```
docker build .

```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/43ff5f8d-995a-4aef-beb9-599afa7a9288)

## 6. Nazwij obraz! | Tagowanie

* zmiana nazwy obrazu

```
docker build --tag mojvim .
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/a966f1a8-fc42-4a19-b197-04e8d96def09)

* zmiana nazwy po zbudowaniu

```
docker tag mojvim:latest mojvim:2.0

```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/062049a8-8506-4ca5-9b0a-f995fb719156)


## 7. Build Context

* budowanie obrazu używając pliku Dockerfile znajdującego się poza bieżącym katalogiem

```
docker build -f ../Dockerfile .
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/bd03d57b-531b-46f8-8fbb-72d285e841f2)

## 8. Konteneryzacja aplikacji konsolowej i webowej

* utworzenie pliku z app.py
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/02ba3210-34cd-4adc-bfd8-3678afd3e2c1)
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/3ebb2930-555c-4b48-b32a-6ac6d1eb0844)

* utworzenie pliku requirements.txt zawiera on komende "flask"
* plik Dockerfile
  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/c20ece9e-b1be-42a3-90b0-eb53a0c3e664)

  *zbudowanie
  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/6a58132c-4f0d-4af6-9b3a-8f3b79a74e14)

* uruchomienie aplikacji webowej
  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/a331fe66-c74d-4350-b887-238fcbf9a4f2)

* aplikacje konsolową tak samo sie buduje i uruchamia jest tylko inny wynik

DODAJ ZDJ

## 9. Polecenia ADD COPY i WORKDIR

#### ADD
Polecenie add ma takie same mozliwości jak copy, jednakże moze:
* kopiowac elementy z okreslonej ścieżki url
* może również rozpakowywać archiwa tar

```
# Użycie ADD do rozpakowywania archiwum tar
ADD archive.tar.gz /path/in/container/

# Użycie ADD do pobierania pliku z URL
ADD http://example.com/file.txt /path/in/container/
```

 #### COPY

Kopiuje pliki i katalogi z lokalnego systemu plików do systemu plików obrazu Docker. ma mozliwość:
* kopiowac pliki do katalogów (jesli katalog nie istnieje zostanie on stworzony)
  ```
  COPY test.txt /moj_katalog/
  ```
* kopiowac katalogi do obrazu kontenera (*-wszytskie pliki)
   ```
  COPY katalog/* /moj_katalog/*
  ```
* mozna na raz kopiowac wiele plików
   ```
  COPY test.txt test1.txt /moj_katalog/
  ```
#### Workdir

utworzy katalog jesli nie istenije, ustawia katalog roboczy dla wszystkich kolejnych instrukcji tzn. jesli ustawimy katalog /app to wszytskie polecenia np COPY test.txt będą zapisywane w tym katalogu

```
FROM ubuntu
WORKDIR /app
COPY text.txt .
CMD pwd && ls
```

## 10. Czym różni się CMD od ENTRYPOINT

#### CMD
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/2800256e-0a4c-4fca-a659-3b59cc04a214)

* można wpisywać komendy które mają się wykonać w dwóch formach
  1. powershell
     ```
     CMD ls /test
     ```
  3. exec (do uruchamiania pojedynczych programów)
     ```
     CMD ['ls', 'test']
     ```

* zbudowanie cmd
  ```
  docker build -f cmd.Dockerfile -t cmd .
  ```
  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/5d68b410-0d2d-4344-aa3e-d12b14be8861)

* odpalenie (wykona sie ls)

```
docker run cmd
```
  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/b2bf8a77-6afb-4d7f-9a2a-056ff7725b90)

* uruchomienie innego polecenia w obrazie (zamiana ls na uname -a - nadpisanie)
  
```
docker run cmd uname -a
```
  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/ad73fd9a-17da-4a45-82ac-ea9e748977ec)

* nie da się dopisac polecenia (żeby wykonało sie ls a potem /dev)
  ```
  docker run cmd /dev
  ```
  polecenie sie nadpisuje

  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/45b1a7ab-8f49-4d9f-aed7-1bc82f0030ca)

można jedynie tak wykonać to polecenie
```
docker run cmd ls/dev
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/ee4378c2-2774-4334-bdec-2ac8d3724e13)

#### ENTRYPOINT

tak samo jak CMD występuje w formie shellowej i exec tzn ``` ENTRYPOINT ls ``` lub ```ENTRYPOINT ['ls']```

* zbudowanie
  ```
  docker build entrypoint.Dockerfile -t entry .
  ```
  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/9a799ee8-7b03-4696-8a35-b3d87a41c3b9)

* uruchomienie
  ```
  docker run entry
  ```
  ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/156bf0cc-6c87-430a-b105-56887c707a6c)

* ENTRYPOINT umozliwia dopisanie polecenia przy uruchomieniu NIE nadpisuje plików, przekazuje jako parametr na końcu

  ```
  docker run entry /test
  ```

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/869ce974-8d99-438c-9fa7-5171c46dc4b3)

* można nadpisać polecenia w ENTRYPOINT ręcznie
  ```
  docker run --entrypoint pwd entry
  ```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/6372c847-1d0b-4202-931d-1caea38a8cec)

#### CMD i ENTRYPOINT

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/3ab7b567-3e35-4f74-a928-c5f85b5bf715)

CMD zostanie wykorzystane jako domyslne parametry dla ENTRYPOINTA. w tym przypadku zostanie uruchomione ```ls -al /test```. Uzycie CMD umozliwia nadpisanie poleceń. 

po wpisaniu komendy ``` docker run entry /etc``` polecenie ```/test``` zostanie zastąpione ```/etc```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/19191365-404d-4225-a955-3492781469c0)

## 11. Dane w kontenerze: VOLUMES

Docker wolumeny (volumes) to sposób zarządzania danymi tworzonymi i używanymi przez kontenery. Wolumeny umożliwiają przechowywanie danych nawet po ponownym uruchomieniu lub usunięciu kontenera i mogą być współdzielone między wieloma kontenerami

#### Wolumeny zarządzane przez dockera (VOLUME)

* utworzenie
```
docker volume create moj-volume
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/ab9bbb17-86e0-4458-a2eb-859596eb1edc)

* usunięcie
```
docker volume rm moj-volume
```
* utworzenie vol.Dockerfile
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/9774962b-9ec5-4807-afa5-94abd957839b)

* zbudowanie
```
docker build -f vol.Dockerfile -t vol_test .
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/2946b138-5538-48e8-a3c3-713646ece250)

* uruchomienie
```
docker run vol_test
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/afc3ade4-7570-44ad-b373-b539c09d65e1)

* uzycie wolumenu
```
docker run --volume moj-volume:/katalog vol_test
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/029ba6a0-31ca-4008-b72b-c9d16a275809)

dzięki temu jesteśmy w stanie zapisac na stałe jakies dane z kontenera

#### Anonimowe wolumeny

nie trzeba podawac nazwy volumenu, docker sam ją stworzy

```
docker run --volume /katalog vol_test
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/a38dbe62-7116-4ced-9507-1cc4e9f7f972)

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/c7237bf0-4924-446a-8e89-a9fc69c91fda)

#### Bind mount

umozliwia łączenie kontenerów z plikami lokalnymi

* uruchomienie z podaniem sciezki, gdzie chcemy utworzyc volume
```
docker run --volume //c/Users/patip/python2/katalog:/katalog vol_test
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/9d804d3b-1a1f-49b8-92e3-5f0038af1c1d)

* zawartosc katalogu
```
dir katalog
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/58148567-9e6f-4bfb-a3b8-768604cc1865)

 * obserwowanie zmian w katalogu
   ```
   docker run -it --volume //c/Users/patip/python2/katalog:/katalog vol_test watch ls /katalog
   ```
   ![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/6eaf3093-3296-40df-a286-01fa4f6d2e02)

zmiany lokalne pojawiaja sie w katalogu

## 12. Baza danych w kontenerze

* wypisanie wszystkich zmiennych srodowiskowych
```
docker run ubuntu env
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/fb25c5a2-29d5-4ae7-8ebb-f31b79a3055b)

* dodanie zmiennej środowiskowej
```
docker run -e MOJA_ZMIENNA=true ubuntu env
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/8b240c57-c8cc-482e-8668-e01803deb378)

* wykorzystanie obrazu postgresa do uruchomienia bazy danych w kontenerze

```
docker run --name baza --detach -e POSTGRES_PASSWORD=haslo postgres
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/177c5c88-074a-496b-bf1d-93f057d6df13)

* uruchomienie wiersza polecen postgresa do wykonywania polecen

```
docker exec -it baza psql --username postgres
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/6ff1e338-828d-4569-a662-f2dd76f7b8a6)

wyjście z wiersza poleceń wykonujemy komenda ``` \q```
zatrzymanie bazy wykonujemy komenda ```docker stop baza```

* tworzenie bazy z wolumenami aby zapisywac zmiany

```
docker run --name baza --detach -e POSTGRES_PASSWORD=haslo --volume dane_bazy:/var/lib/postgresql/data po
stgres
```

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/c1a4d17f-89f5-4cef-aa66-dd76b5fbf7c0)

* po usunieciu bazy jego volume dalej istnieje
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/0f3ea9e7-913b-4bd4-9592-ac22c881a867)

* gdy na nowo utworzymy baze z tym samym volumenem będziemy miec jej zawartosc

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/d5b8b043-3205-44f0-ab2c-9fc58999bb02)

* podpięcie z zewnatrz z bazą danych (porty)

```
docker run --name baza --detach -e POSTGRES_PASSWORD=haslo -e POSTGRES_USER=ja --volume dane_bazy:/var/lib/postgresql/data -p 5432:5432 postgres
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/bc9953e0-d786-4d99-b6cd-390898ab34b2)

## 13. Polecenie Docker Inspect

pokazuje duzo informacji o kontenerze

```
docker inspect 953cf
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/a9803567-7b12-459b-9dc2-458d286b3742)

## 14. Docker Networks: wirtualne sieci w kontenerach

służa do komunikacji pomiędzy kontenerem a internetem oraz pomiedzy kontenerami na tym samym hostcie. Docker automatycznie tworzy sieci dla kontenerów.

* wypisanie sieci
```
docker network ls
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/905982ba-4b92-4df1-bf8f-a954f470ebb0)

#### sieć bridge (domyslna, tworzona automatycznie)

* uruchomienie kilku kontenerów na podstawie obrazu busybox

```
docker run -dit --name contA busybox
```

* kontenery podłaczone automatycznie do sieci (mogą korzystac z internetu)

``` docker network inspect```

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/71819b45-efff-4a8f-bad6-f8b3af4d19fd)

* odpalenie terminala kontenera A

```
docker attach contA
```
* sprawdzenie interfejsów sieci i adresu IP kontenera

```
ip addr
```

![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/82dbbbd1-e730-470a-809b-850c7479c8ff)

* sprawdzenie połaczenia z siecią
```
ping google.com
```
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/874f8615-92e7-4502-ae4e-c0a843639759)

* połaczenie z drugim kontenerem

```
ping 172.17.05
``
![image](https://github.com/patrycjaprzybysz/docker/assets/100605325/45caf9c1-55d8-46dc-8383-ec675d9d8fd1)

#### tworzenie własnej sieci typu bridge




