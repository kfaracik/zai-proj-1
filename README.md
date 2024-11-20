### Opis Projektu: **Online Store System**  

#### Projekt 1: Aplikacja eCommerce
Projekt obejmuje budowę systemu sprzedaży online złożonego z dwóch aplikacji:
1. **eCommerce-Front**: Aplikacja frontendowa skierowana do użytkowników końcowych, umożliwiająca przeglądanie produktów, zarządzanie koszykiem i dokonywanie zakupów.
2. **eCommerce-Admin**: Panel administracyjny pozwalający na zarządzanie produktami, kategoriami oraz zamówieniami.  

---

### **Cele Projektu**
- Zaimplementowanie skalowalnej platformy eCommerce, która pozwala użytkownikom na zakupy online.
- Stworzenie intuicyjnego panelu administracyjnego dla zarządzania zasobami.
- Zastosowanie nowoczesnych technologii frontendowych i backendowych, by zapewnić wysoką wydajność, estetykę i bezpieczeństwo.

---

### **Funkcjonalności**

#### **Aplikacja Frontendowa (eCommerce-Front)**
1. **Główne ekrany i widoki**:
   - Strona główna: prezentacja wybranych produktów oraz najnowszych ofert.
   - Strona produktu: szczegóły produktu, opcje dodania do koszyka.
   - Koszyk: podsumowanie wybranych produktów, możliwość zmiany ilości oraz przejścia do płatności.
   - Proces płatności: integracja z bramkami płatniczymi, weryfikacja danych.
2. **Funkcje użytkownika**: (inprogess)
   - Zakładanie konta i logowanie.
   - Przeglądanie historii zamówień.
   - Zarządzanie listą ulubionych produktów.
3. **Responsywny design**:
   - Obsługa na urządzeniach mobilnych, tabletach i komputerach.

#### **Panel Administracyjny (eCommerce-Admin)**
1. **Zarządzanie produktami**:
   - Dodawanie, edycja, usuwanie produktów.
   - Zarządzanie stanami magazynowymi.
2. **Zarządzanie kategoriami**:
   - Tworzenie kategorii oraz przypisywanie produktów.
3. **Zarządzanie zamówieniami**:
   - Przeglądanie, aktualizacja statusów, kontakt z klientem.
4. **Uwierzytelnianie i autoryzacja**:
   - Logowanie za pomogą OAuth z podziałem na role (administrator, edytor).
5. **Estetyczny i przejrzysty interfejs użytkownika**:
   - Prostota obsługi oraz intuicyjne rozmieszczenie opcji administracyjnych.

---

### **Technologie Wykorzystane**
1. **Frontend**:
   - **React**: dynamiczne komponenty oraz zaawansowane zarządzanie stanem aplikacji.
   - **TypeScript**: zapewnienie statycznego typowania i lepszej jakości kodu.
   - **CSS**: estetyczne i responsywne style aplikacji.
2. **Backend**:
   - **Node.js**: logika aplikacji oraz integracja z bazą danych.
   - **MongoDB**: relacyjna baza danych przechowująca informacje o produktach, zamówieniach i użytkownikach.
3. **Inne technologie**:
   - Zabezpieczenie przed SQL Injection.
   - Hashowanie haseł (np. za pomocą `bcrypt`).
   - Publicznie dostępny hosting.
4. **Zarządzanie**:
   - **GitHub**: kontrola wersji i współpraca zespołowa.

---

### **Dodatkowe Informacje**
- **Testowanie i optymalizacja**:
   - Przeprowadzone testy responsywności oraz wydajności aplikacji.
- **Dokumentacja**:
   - Instrukcja uruchomienia systemu. (znajduje się w każdym repozytorium)
   - Struktura bazy danych z opisem relacji.
 
     # Struktura bazy danych

## Kolekcje i pola

### 1. Users
- `_id` (ObjectId): Unikalny identyfikator użytkownika.
- `name` (String): Imię użytkownika.
- `email` (String): Adres email użytkownika.
- `image` (String): URL do zdjęcia użytkownika.
- `emailVerified` (Boolean/Null): Informacja, czy email został zweryfikowany.

### 2. Sessions
- `_id` (ObjectId): Unikalny identyfikator sesji.
- `sessionToken` (String): Token sesji użytkownika.
- `userId` (ObjectId): Klucz obcy odwołujący się do `Users._id`.
- `expires` (Date): Data wygaśnięcia sesji.

### 3. Accounts
- `_id` (ObjectId): Unikalny identyfikator konta.
- `provider` (String): Dostawca usług logowania (np. Google).
- `type` (String): Typ konta (np. `oauth`).
- `providerAccountId` (String): Identyfikator konta u dostawcy.
- `access_token` (String): Token dostępu.
- `expires_at` (Number): Data wygaśnięcia tokenu w formacie UNIX timestamp.
- `scope` (String): Zakres uprawnień tokenu.
- `token_type` (String): Typ tokenu (np. Bearer).
- `id_token` (String): Token identyfikacyjny.
- `userId` (ObjectId): Klucz obcy odwołujący się do `Users._id`.

### 4. Products
- `_id` (ObjectId): Unikalny identyfikator produktu.
- `title` (String): Tytuł produktu.
- `description` (String): Opis produktu.
- `price` (Number): Cena produktu.
- `images` (Array of String): URL-e obrazów produktu.
- `category` (ObjectId): Klucz obcy odwołujący się do `Categories._id`.
- `createdAt` (Date): Data utworzenia produktu.
- `updatedAt` (Date): Data ostatniej aktualizacji produktu.

### 5. Orders
- `_id` (ObjectId): Unikalny identyfikator zamówienia.
- `line_items` (Array of Objects): Lista produktów w zamówieniu (dane inline, brak referencji).
- `name` (String): Imię osoby zamawiającej.
- `email` (String): Email osoby zamawiającej.
- `city` (String): Miasto.
- `postalCode` (String): Kod pocztowy.
- `streetAddress` (String): Adres ulicy.
- `country` (String): Kraj.
- `paid` (Boolean): Informacja o statusie płatności.
- `createdAt` (Date): Data utworzenia zamówienia.
- `updatedAt` (Date): Data ostatniej aktualizacji zamówienia.

### 6. Categories
- `_id` (ObjectId): Unikalny identyfikator kategorii.
- `name` (String): Nazwa kategorii.
- `properties` (Array): Lista właściwości kategorii.
- `__v` (Number): Wersja dokumentu (od MongoDB).

---

## Relacje

1. **Users → Sessions**
   - Relacja: Jeden do wielu.
   - Opis: Jeden użytkownik może posiadać wiele sesji. Relacja definiowana jest przez `Sessions.userId`, który wskazuje na `Users._id`.

2. **Users → Accounts**
   - Relacja: Jeden do wielu.
   - Opis: Jeden użytkownik może mieć wiele kont (np. połączone różne dostawcy logowania). Relacja definiowana jest przez `Accounts.userId`, który wskazuje na `Users._id`.

3. **Products → Categories**
   - Relacja: Wiele do jednego.
   - Opis: Każdy produkt należy do jednej kategorii. Relacja definiowana jest przez `Products.category`, który wskazuje na `Categories._id`.

4. **Orders → Products**
   - Relacja: Dane zagnieżdżone.
   - Opis: Zamówienie przechowuje produkty jako zagnieżdżone obiekty w `Orders.line_items`. Brak jawnej referencji do `Products`.

5. **Users → Orders**
   - Relacja: Brak bezpośredniej relacji.
   - Opis: Informacje o użytkownikach są przechowywane inline w zamówieniach (`Orders.email`, `Orders.name`). Nie ma jawnej referencji do `Users._id`.

   - Zrzuty ekranów prezentujące funkcjonalności.

---

**Repozytoria**:  
- [eCommerce Frontend](https://github.com/kfaracik/ecommerce-front)  
- [eCommerce Admin](https://github.com/kfaracik/ecommerce-admin)  

Projekt ten łączy w sobie praktyczne podejście do implementacji systemu eCommerce z solidnymi podstawami technicznymi, zapewniając skalowalność, bezpieczeństwo i estetykę interfejsu.
