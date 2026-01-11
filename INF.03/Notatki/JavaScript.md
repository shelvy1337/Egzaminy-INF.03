# JavaScript | INF.03

📘 **Notatki do egzaminu zawodowego INF.03 – JavaScript**

Plik zawiera zebrane i uporządkowane **podstawy JavaScript**, wymagane na egzaminie zawodowym **INF.03**.  
Materiał obejmuje najczęściej spotykane zagadnienia z części teoretycznej oraz praktycznej egzaminu.

Zakres notatek:
- podpinanie JavaScript do HTML,
- zmienne i stałe,
- obsługa DOM,
- instrukcje warunkowe i pętle,
- funkcje i zdarzenia,
- formularze,
- operacje matematyczne.

Materiały idealne do:
- szybkiej powtórki przed egzaminem,
- utrwalenia podstaw JavaScript,
- nauki pod INF.03 „krok po kroku”.

---

## Podpinanie JavaScript do HTML
```html
<script src="skrypt.js" defer></script>
```
**defer** - *pozwala na załadowanie skryptu dopiero po załadowaniu wyglądu strony, umieszczamy go w sekcji **<head>***

---

## Zmienne
```js
let nazwa = "tekst"; //zmienna przechowuje wartość tekstowa - typu string
let liczba = 123; //zmienna przechowuje wartość liczbowa - typu int
```

## Stałe
```js
const PI = 3.14; //pozwala na przechowanie stałej np. stałej matematycznej liczby π
```

---

## Pobierane elementów strony
- po ID elementu:
```js
document.getElementById("id") 
//dla elementu w HTMl o danym id np. <div id="id">JakisElement</div>
```

- po klasie:
```js
document.getElementsByClassName("klasa")
//dla elementu w HTMl o danej klasie np. <div class="klasa">JakisElement</div>
```

- po selektorze CSS:
```js
document.querySelector("h1")
document.querySelector("#id")
document.querySelector(".klasa")
//dla elementu w CSS np. znacznika <h1> określonego w CSS
```

---

## Odczyt / zmiana tekstu
- innerHTML:
```js
element.innerHTML = "<b>Wstawiony tekst</b>";
```

- textContent:
```js
element.textContent = "Siema";
```

Różnica jest taka, że **innerHTML** pozwala na użycie znaczników HTML do edycji tekstu, a **textContent** wstawia sam tekst (nie interpretuje znaczników)

---

## Przykład pobrania i zapisania do zmiennej
- innerHTML:
```js
let txt = document.getElementById("element").innerHTML;
```

Zapisujemy tekst z elementu o id równym **element** do zmiennej *txt*

---

## Instrukcje warunkowe if / else + operatory
- if / else:
```js
if (wiek > 18) {
  document.getElementById("element").innerHTML = "<p>Jesteś <b>pełnoletni</b></p>";
} else {
  document.getElementById("element").innerHTML = "<p>Nie jesteś <b>pełnoletni</b></p>";
}
```

- Porównania:
```js
== - (porównuje „luźniej”, czyli 1 i "1" bedzie takie samo dla niego)
=== - (porównuje typ i wartość - 1 i "1" bedą rożne od siebie)
```

---

## Edycja stylu w JavaScript
- Zmiana stylu:
```js
document.getElementById("element").style.border = "2px solid black";
document.getElementById("element").style.backgroundColor = "red";
```
Czyli element o id **element** bedzie miał *ciągłe* obramowanie o grubości *2px* w kolorze *czarnym*, a jego tło będzie *czerwone*

---

## Funkcje w JavaScript
- Tworzenie:
```js
function nazwa(parametry) {
  document.getElementById("element").innerHTML = "<p>Wykonano funkcję!</p>";
}
```

- Wywołanie:
```js
nazwa();
```

---

## Eventy / zdarzenia
W HTML można spotkać:
- onclick
- onmouseover
- onmouseout
- onkeydown
- onfocus
- onchange

Przykład w HTML:
```html
<button onclick="funkcja()">Kliknij mnie</button>
```

A bardziej "poprawną" wersją tego powyżej, ale zapisaną w JavaScript jest:
```js
document.querySelector("#btn").addEventListener("click", funkcja);
```

---

## Formularze
- Pobranie wartości z inputa:
```js
let v = document.getElementById("pole").value;
```

- Checkbox:
```js
let c = document.getElementById("check").checked;
```
Zwraca zawsze wartość **true** lub **false** (zaznaczony lub niezaznaczony)

---

## Dodawanie elementów HTML w JavaScript
- Tworzenie elementu:
```js
let sekcja = document.createElement("section");
```

- Ustawienie treści:
```js
sekcja.innerHTML = "Tekst sekcji";
```

- Dodanie do innego istniejącego elementu:
```js
document.getElementById("kontener").appendChild(sekcja);
```
Pamiętaj, że ten kod dodaje naszą sekcje do kontenera o id **kontener**, który już istnieje, a *appendChild* spowoduje dodanie sekcji na sam koniec kontenera

---

## Tekst wielolinijkowy
```js
let msg = `Linia 1
Linia 2
Linia 3`;
```

---

## Pętle for i while
- for:
```js
for (let i = 0; i < 10; i++) {
  console.log("@");
}
```
Wypisze 10 razy znak @ w konsoli  dla i = 0 ... 9

- while:
```js
let i = 0;
while (i < 10) {
  console.log("@");
  i++;
}
```
Musimy dodać **i++**, czyli zmiane licznika, inaczej pętla nieskończona

---

## Alert, prompt, confirm
- alert:
```js
alert("Treść");
```

- prompt:
```js
let x = prompt("Podaj coś:");
```
Zwraca wpisany tekst lub wartność *null*

- confirm:
```js 
let ok = confirm("Na pewno?");
```
Zwraca true lub false

---

## Zaokrąglanie liczb
- Zaokrąglenie „matematyczne”:
```js
Math.round(x);
```

- W górę:
```js
Math.ceil(x);
```

- W dół:
```js
Math.floor(x);
```

---

### ⚠️ Informacja
Notatki mają charakter **edukacyjny** i zostały przygotowane
z myślą o nauce do egzaminu zawodowego **INF.03**.

<p align="center">© 2026 <b>shelvy</b>
