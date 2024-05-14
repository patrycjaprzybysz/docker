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

* wyswitelenie wszystkich warstw składających się na vim_img

```
docker history vim_img
```









