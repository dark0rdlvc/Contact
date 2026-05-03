# ContactBook 📖

**ContactBook** je ASP.NET Core MVC web aplikacija za upravljanje kontaktima i grupama kontakata. Podaci se čuvaju u XML fajlovima (Grupa A — XML Data Engine).

## Opis aplikacije

ContactBook omogućava korisnicima da:
- Registruju se i prijave na nalog
- Dodaju, pregledaju, menjaju i brišu kontakte (sve CRUD operacije)
- Organizuju kontakte u grupe (sa bojama i ikonicama)
- Pretražuju, filtriraju i sortiraju kontakte po svim relevantnim poljima
- Paginacija rezultata (9 kontakata po stranici)
- Pregledaju statistiku na dashboard-u (Chart.js doughnut grafikon po grupama)
- Izvezu kontakte u XML, JSON ili **PDF** format
- Pregledaju i menjaju sopstveni profil

## Stranice (11 stranica)

1. **Landing** (`/Home/Landing`) — Naslovna stranica za neregistrovane korisnike
2. **Login** (`/Account/Login`) — Prijava korisnika
3. **Register** (`/Account/Register`) — Registracija korisnika
4. **Dashboard** (`/Home/Index`) — Pregled statistike, Chart.js grafikona i poslednjih kontakata
5. **Contacts/Index** — Lista kontakata sa pretragom, filtriranjem, sortiranjem i paginacijom
6. **Contacts/Details** — Detalji jednog kontakta
7. **Contacts/Create** — Forma za dodavanje kontakta
8. **Contacts/Edit** — Forma za izmenu kontakta
9. **Groups/Index** — Lista svih grupa
10. **Groups/Create** — Kreiranje grupe
11. **Groups/Edit** — Izmena grupe
12. **Profile/Index** — Korisnički profil (pregled)
13. **Profile/Edit** — Izmena profila

## Napredne funkcionalnosti (2 izabrane + bonus)

- ✅ **Korisnički profil** — Stranica za pregled i izmenu sopstvenih podataka
- ✅ **Statistika i grafikoni** — Chart.js doughnut grafikon kontakata po grupama na dashboard-u
- ✅ **Generisanje PDF izveštaja** — Export kontakata u formatiran PDF fajl (iText7)

## Tehnologije

- ASP.NET Core 8.0 MVC
- C# 12
- XML / System.Xml.Linq za čuvanje podataka (bez baze!)
- Cookie Authentication (bez Identity frameworka)
- Data Annotations + jQuery Unobtrusive Validation (client + server side)
- Bootstrap 5.3 + Bootstrap Icons
- Chart.js 4.4 (statistički grafikon)
- iText7 (PDF generisanje)
- Google Fonts (Syne + DM Sans)

## Struktura projekta

```
ContactBook/
├── App_Data/
│   ├── contacts.xml         # Kontakti (XML Data Engine)
│   ├── groups.xml           # Grupe
│   └── users.xml            # Korisnici
├── Controllers/
│   ├── AccountController.cs # Login, Register, Logout
│   ├── ContactsController.cs# CRUD + Export (XML/JSON/PDF)
│   ├── GroupsController.cs  # CRUD za grupe
│   ├── HomeController.cs    # Dashboard + Landing
│   └── ProfileController.cs # Pregled i izmena profila
├── Models/
│   ├── Contact.cs           # Entitet kontakta sa Data Annotations
│   ├── Group.cs             # Entitet grupe
│   ├── AppUser.cs           # Entitet korisnika
│   └── ViewModels.cs        # ViewModeli (Login, Register, Profile, ContactList, Dashboard)
├── Services/
│   ├── ContactService.cs    # XML čitanje/pisanje kontakata
│   ├── GroupService.cs      # XML čitanje/pisanje grupa
│   └── UserService.cs       # XML čitanje/pisanje korisnika + autentifikacija
├── Views/
│   ├── Account/             # Login.cshtml, Register.cshtml
│   ├── Contacts/            # Index, Create, Edit, Details
│   ├── Groups/              # Index, Create, Edit
│   ├── Home/                # Index (Dashboard), Landing
│   ├── Profile/             # Index, Edit
│   └── Shared/              # _Layout.cshtml (zajednički izgled)
└── wwwroot/
    ├── css/site.css         # Svi stilovi (dark theme)
    └── js/site.js           # Toast, chart animacije, active nav
```

## MVC Struktura

- **Model**: Data Annotations validacija na svim entitetima i ViewModelima
- **View**: Razor views sa `_Layout.cshtml`, jQuery Unobtrusive Validation na klijentskoj strani
- **Controller**: Odvojeni kontroleri za svaki domen, koriste servise
- **Servisi**: Servisne klase (`IContactService`, `IGroupService`, `IUserService`) komuniciraju sa XML fajlovima

## XML Data Engine

Svi podaci se čuvaju u tri XML fajla u `App_Data` folderu. Servisne klase koriste `System.Xml.Linq` za:
- Čitanje: `XDocument.Load()` → mapiranje u listu modela
- Pisanje: Kreiranje `XDocument` od liste modela → `doc.Save()`
- Thread-safety: `lock` objekt sprečava konkurentni pristup

Export akcija vraća podatke u XML, JSON ili PDF formatu.

## Pokretanje projekta

### Preduslovi
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

### Koraci

1. Klonirajte repozitorijum:
   ```bash
   git clone https://github.com/YOUR_USERNAME/ContactBook.git
   cd ContactBook/ContactBook
   ```

2. Vratite NuGet pakete i pokrenite:
   ```bash
   dotnet restore
   dotnet run
   ```

3. Otvorite browser:
   ```
   https://localhost:5001
   ```
   ili
   ```
   http://localhost:5000
   ```

4. Registrujte novi nalog i počnite!

> **Napomena**: XML fajlovi se automatski kreiraju pri prvom pokretanju. Nema podešavanja baze podataka.

## Autor

[Vaše ime] — Projekat za predmet Web Programiranje
