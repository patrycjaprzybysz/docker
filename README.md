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


## 2. Jak działają obrazy dockerowe







