**Temat lekcji: Prosty zapis i odczyt danych z bazy MySQL w PHP**

---

**Cel lekcji:**

- Nauczysz się, jak w prosty sposób zapisywać dane do bazy MySQL i odczytywać je za pomocą PHP, skupiając się tylko na podstawowych operacjach.

---

**Wprowadzenie:**

W tej lekcji pokażemy, jak połączyć się z bazą danych MySQL, zapisać do niej dane oraz je odczytać, używając PHP. Skupimy się na podstawowej funkcjonalności, pomijając sprawdzanie poprawności połączenia czy zabezpieczenia.

---

### **1. Tworzenie bazy danych i tabeli**

**a) Utworzenie bazy danych "szkola"**

- Otwórz phpMyAdmin w przeglądarce (np. `http://localhost/phpmyadmin`).
- Kliknij na zakładkę **"Bazy danych"**.
- W polu **"Utwórz bazę danych"** wpisz `szkola` i kliknij **"Utwórz"**.

**b) Utworzenie tabeli "uczniowie"**

- Wybierz bazę danych **"szkola"** z listy po lewej stronie.
- Kliknij na zakładkę **"SQL"** i wprowadź następujące polecenie SQL:

```sql
CREATE TABLE uczniowie (
    id INT AUTO_INCREMENT PRIMARY KEY,
    imie VARCHAR(50),
    nazwisko VARCHAR(50)
);
```

- Kliknij **"Wykonaj"**.

---

### **2. Tworzenie formularza HTML do wprowadzania danych**

**a) Utworzenie pliku "formularz.html"**

- Otwórz edytor tekstu (np. Notepad++ lub Notatnik).
- Wklej poniższy kod:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Dodaj ucznia</title>
</head>
<body>
    <h1>Dodaj nowego ucznia</h1>
    <form action="dodaj.php" method="post">
        Imię:<br>
        <input type="text" name="imie"><br><br>
        Nazwisko:<br>
        <input type="text" name="nazwisko"><br><br>
        <input type="submit" value="Dodaj">
    </form>
</body>
</html>
```

- Zapisz plik jako **`formularz.html`** w folderze serwera WWW (np. `htdocs` w przypadku XAMPP).

---

### **3. Tworzenie skryptu PHP do zapisywania danych**

**a) Utworzenie pliku "dodaj.php"**

- W edytorze tekstu utwórz nowy plik i wklej poniższy kod:

```php
<?php
// Połączenie z bazą danych
$polaczenie = mysqli_connect("localhost", "root", "", "szkola");

// Pobranie danych z formularza
$imie = $_POST['imie'];
$nazwisko = $_POST['nazwisko'];

// Wstawienie danych do bazy
mysqli_query($polaczenie, "INSERT INTO uczniowie (imie, nazwisko) VALUES ('$imie', '$nazwisko')");

// Potwierdzenie dodania danych
echo "Dodano ucznia.<br>";
echo "<a href='lista.php'>Zobacz listę uczniów</a>";
?>
```

- Zapisz plik jako **`dodaj.php`** w folderze serwera WWW.

---

### **4. Tworzenie skryptu PHP do odczytywania danych**

**a) Utworzenie pliku "lista.php"**

- W edytorze tekstu utwórz nowy plik i wklej poniższy kod:

```php
<?php
// Połączenie z bazą danych
$polaczenie = mysqli_connect("localhost", "root", "", "szkola");

// Pobranie danych z bazy
$wynik = mysqli_query($polaczenie, "SELECT * FROM uczniowie");

// Wyświetlanie danych
echo "<h1>Lista uczniów:</h1>";
while($uczen = mysqli_fetch_assoc($wynik)) {
    echo $uczen['imie'] . " " . $uczen['nazwisko'] . "<br>";
}
?>
```

- Zapisz plik jako **`lista.php`** w folderze serwera WWW.

---

### **5. Testowanie aplikacji**

**a) Uruchomienie serwera WWW**

- Upewnij się, że serwer Apache jest uruchomiony (np. w XAMPP).

**b) Dodawanie nowego ucznia**

- Otwórz przeglądarkę internetową.
- Przejdź do adresu `http://localhost/formularz.html`.
- Wypełnij formularz danymi ucznia i kliknij **"Dodaj"**.

**c) Wyświetlanie listy uczniów**

- Po dodaniu ucznia pojawi się komunikat oraz link do wyświetlenia listy uczniów.
- Kliknij na link **"Zobacz listę uczniów"**, aby zobaczyć wprowadzone dane.

---

### **Podsumowanie:**

- Stworzyliśmy prostą bazę danych i tabelę w MySQL.
- Napisaliśmy formularz HTML do wprowadzania danych.
- Utworzyliśmy skrypty PHP do zapisywania i odczytywania danych.
- Przetestowaliśmy działanie aplikacji.

---

### **Zadania do samodzielnego wykonania:**

1. **Dodaj pole "klasa" do tabeli "uczniowie". Zaktualizuj formularz oraz skrypty PHP tak, aby móc wprowadzać i wyświetlać klasę ucznia.**

2. **Zmodyfikuj skrypt "lista.php", aby przed imieniem i nazwiskiem ucznia wyświetlał się jego numer ID.**

3. **Dodaj na stronie "lista.php" link powrotny do formularza, aby ułatwić dodawanie kolejnych uczniów.**

---

**Uwaga:**

W powyższych przykładach skupiliśmy się na podstawowej funkcjonalności, pomijając sprawdzanie poprawności połączenia i zabezpieczenia danych. W praktycznych zastosowaniach zawsze należy zabezpieczać dane wprowadzane przez użytkowników, aby uniknąć potencjalnych zagrożeń, takich jak ataki SQL injection.

---

**Powodzenia w dalszej nauce!**
