# PHP | INF.03

📘 **Notatki do egzaminu zawodowego INF.03 – PHP**

Plik zawiera zebrane i uporządkowane **podstawy PHP**, wymagane na egzaminie zawodowym **INF.03**.  
Materiał obejmuje najczęściej spotykane zagadnienia z części praktycznej: składnia PHP, instrukcje, formularze, baza danych, cookies/sesje oraz praca z plikami.

Zakres notatek:
- wyświetlanie tekstu (`echo`),
- zmienne (`$`) + cudzysłów/apostrof,
- instrukcje warunkowe i operatory,
- pętle (`for`, `while`),
- baza danych (`mysqli_connect`, `mysqli_query`, `mysqli_fetch_assoc`),
- formularze (`$_POST`, `isset`, checkbox 1/0, INSERT),
- cookies i sesje (`setcookie`, `session_start`, `$_SESSION`),
- praca z plikami (`fopen`, `fgets`, `feof`, `fwrite`).

Materiały idealne do:
- szybkiej powtórki przed egzaminem,
- utrwalenia praktycznych schematów INF.03,
- nauki „pod zadania” (formularz + baza + pętla).

---

## Wyświetlanie tekstu
```php
echo "Witaj";
```

Polecenie **echo** służy do wypisywania tekstu na stronę.

---

## Zmienne
- Zmienna zawsze zaczyna się od znaku **$**:
```php
$zmienna = "tekst";
$liczba = 123;
```

- Wypisanie zmiennej:
```php
echo $zmienna;
```

---

## Cudzysłów vs apostrof
- **" "** (cudzysłów) - PHP „wstawia” zmienne do tekstu:
```php
$zmienna = "Kamil"
echo "Witaj $zmienna";
```
Wypisze tekst: *Witaj Kamil*

- **' '** (apostrof) - traktuje wszystko jako zwykły tekst:
```php
echo 'Witaj $zmienna';
```
Wypisze tekst: *Witaj $zmienna*

- Jeśli w środku masz cudzysłów, a na zewnątrz też cudzysłów - użyj apostrofu na zewnątrz albo escape:
```php
echo '<h1>Tekst</h1>';
echo "<h1>Tekst</h1>";
echo "<h1>\"Tekst\"</h1>";
```

---

## Instrukcje warunkowe IF / ELSE + operatory
- if / else:
```php
if ($zmienna == "tak") {
  echo "Zmienna jest równa słowu tak";
} else {
  echo "Zmienna nie jest równa słowu tak";
}
```

- Operatory:
```php
==   // równe
!=   // różne
&&   // AND (oba warunki prawdziwe)
||   // OR (jeden z warunków prawdziwy)
```

---

## Pętle for i while
- while:
```php
$i = 0;
while ($i < 10) {
  echo $i;
  $i++;
}
```

- for:
```php
for ($i = 0; $i < 10; $i++) {
  echo $i;
}
```

---

## Baza danych (mysqli)
- Schemat:
```php
$polaczenie = mysqli_connect("localhost", "login", "haslo", "nazwabazy");
```

- Dobrze zrobić *(czasem dodatkowe punkty)*: sprawdzenie czy połączenie działa
```php
if (!$polaczenie) {
  die("Błąd połączenia: " . mysqli_connect_error());
}
```

- Zamknięcie połączenia:
```php
mysqli_close($polaczenie);
```

---

## Wysyłanie zapytania SQL
```php
$zapytanie = mysqli_query($polaczenie, "SELECT * FROM tabela");
```
**mysqli_query** zwraca wynik (result) albo true/false (zależnie od typu zapytania)

---

## Pobieranie danych z SELECT
- Jeden rekord (tablica asocjacyjna):
```php
$wiersz = mysqli_fetch_assoc($zapytanie);
```

- Wypisanie kolumny:
```php
echo $wiersz["kolumna"];
```

- Wypisanie wielu rekordów (najczęściej na egzaminie):
```php
while ($wiersz = mysqli_fetch_assoc($zapytanie)) {
  echo $wiersz["kolumna"];
}
```
❗ Dlaczego **while** działa? 
Bo **mysqli_fetch_assoc** zwraca kolejny wiersz, a gdy się skończą - zwraca false i **pętla się kończy**.

---

## Formularze
Formularze ogólnie tworzymy w kodzie HTMl, a w PHP jedynie nimi manipulujemy.
Przykładowy kod formularza w HTML:
```html
<form method="post">
  <input type="text" name="imie">
  <input type="checkbox" name="zgoda">
  <button type="submit" name="send">Wyślij</button>
</form>
```

Wysyła on dane w formie **bezpiecznej**, czyli metoda POST, natomiast metoda GET jest określana jako metoda **niebezpieczna**.

---

## Odczyt danych z formularza w PHP
Dane wysłane metoda POST zapisywane są w zmiennej globalnej **$_POST**

- Zapisanie danych do zmiennej:
```php
$imie = $_POST["imie"];
```

- Żeby wykonać kod dopiero po wysłaniu formularza (ważne, aby unkinąć błędów):
```php
if (isset($_POST["send"])) {
  // kod po wysłaniu
}
```

---

## Checkbox - ON/OFF → 1/0
- Jeśli checkbox jest zaznaczony, zwykle przychodzi **"on"**
- Jak nie zaznaczony - często nie ma go w **$_POST** (czyli trzeba **isset**)

Przykład:
```php
if (isset($_POST["zgoda"])) {
  $zgoda = 1;
} else {
  $zgoda = 0;
}
```

---

## INSERT do bazy
```php
$sql = "INSERT INTO tabela (imie, zgoda) VALUES ('$imie', $zgoda)";
mysqli_query($polaczenie, $sql);
```

---

## Cookies
- Ustawienie ciastka:
```php
setcookie("rodzaj", "wartosc", time() + 3600); // 1h
```

- Odczyt ciastka:
```php
$ciastko = $_COOKIE["rodzaj"];
```

❗ Uwaga: **setcookie** działa „przy wysyłaniu nagłówków”, więc najlepiej dawać je na górze pliku (zanim echo / HTML).

---

## Sesje
- Start sesji na początku pliku:
```php
session_start();
```

- Ustawienie sesji:
```php
$_SESSION["rodzaj"] = "wartosc";
```

- Odczyt sesji:
```php
echo $_SESSION["rodzaj"];
```

**Różnica:** cookie jest w przeglądarce, a sesja po stronie serwera (zwykle wygasa po zamknięciu przeglądarki / czasie)

---

## Praca z plikami
- Otwarcie pliku:
```php
$plik = fopen("plik.txt", "r");
```

- Odczyt jednej linii:
```php
echo fgets($plik);
```

- Odczyt wszystkich linii:
```php
while (!feof($plik)) {
  echo fgets($plik);
}
```

- Zamknięcie pliku:
```php
fclose($plik);
```

**Pamiętaj, że wskazana tu kolejnośc jest ważna!**

Tryby **fopen**:
- "r" read (odczyt)
- "w" write (nadpisuje plik od zera!)
- "a" append (dopisywanie na końcu)

- Nadpisywanie pliku:
```php
$plik = fopen("plik.txt", "w");
fwrite($plik, "Tekst");
fclose($plik);
```

- Dopisywanie do pliku:
```php
$plik = fopen("plik.txt", "a");
fwrite($plik, "Tekst");
fclose($plik);
```

---

### ⚠️ Informacja
Notatki mają charakter **edukacyjny** i zostały przygotowane
z myślą o nauce do egzaminu zawodowego **INF.03**.

---

<p align="center">
  Copyright © 2026 <b>shelvy</b><br>
  PHP - INF.03<br>
  Materiały edukacyjne
</p>
