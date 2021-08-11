---
title: Zasoby narzędziowe
description: Interfejs API REST Partner Center zawiera wiele zasobów opisujących modele danych ogólnego przeznaczenia używane w zestawie SDK.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: de97feed13a4d0bae9743939a03f8cb8470f5f960bec0507cd9c5adfad287120
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115998046"
---
# <a name="utility-resources"></a>Zasoby narzędziowe

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Interfejs API REST Partner Center zawiera wiele zasobów opisujących modele danych ogólnego przeznaczenia używane w zestawie SDK.

## <a name="address"></a>Adres

Adres do użycia dla profilów klientów lub partnerów. Aby uzyskać więcej informacji o obsługiwanych formatach i właściwościach w różnych krajach/regionach, zobacz [Get address formatting rules by market](get-market-specific-validation-data.md).

| Właściwość     | Typ   | Długość (minimalna, maksymalna) | Opis                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | ciąg | (1, 200)          | Pierwszy wiersz adresu.                                                                   |
| Addressline2 | ciąg | (0, 200)          | Drugi wiersz adresu. Ta właściwość jest opcjonalna.                                       |
| City (Miasto)         | ciąg | n/d               | Miasto.                                                                                        |
| Stan        | ciąg | (0, 2)            | Stan.                                                                                       |
| PostalCode   | ciąg | n/d               | Kod POCZTOWY lub kod pocztowy.                                                                     |
| Kraj      | ciąg | (2, 2)            | Kraj/region w formacie kodu kraju ISO.                                                   |
| Region (Region)       | ciąg | n/d               | Region.                                                                                      |
| FirstName (Imię)    | ciąg | (1, 50)           | Imię kontaktu w firmie/organizacji klienta.                              |
| Middlename   | ciąg | (1, 50)           | Drugie imię i nazwisko kontaktu w firmie/organizacji klienta. Ta właściwość jest opcjonalna.  |
| LastName (Nazwisko)     | ciąg | (1, 50)           | Nazwisko kontaktu w firmie/organizacji klienta.                               |
| PhoneNumber  | ciąg | n/d               | Numer telefonu kontaktu w firmie/organizacji klienta. Ta właściwość jest opcjonalna.|
|PhoneNumber|ciąg|n/d|Numer telefonu kontaktu w firmie/organizacji klienta. W profilu klienta ta właściwość jest obowiązkowa w przypadku firmy/organizacji klienta znajdującej się w następujących krajach: Isa (AM), Gdynia (AZ), Przemysl (BY), Kolumbia (HU), KZ), Kyrgyzstan (KG), Kolumbia (MD), Tadżykistan (RU), Tadżykistan (TJ), Przemowa (UZ), Indie, Brazylia, Republika Południowej Afryki, Dynamo, Stany Zjednoczone Stanów Zjednoczonych, Arabia, Kolumbia, Argentyna, Hania, Hania, Hanii, Stanów Zjednoczonych, Stanów Zjednoczonych i Azji. W przeciwnym razie jest to opcjonalne.|


## <a name="contact"></a>Kontakt

Opisuje informacje kontaktowe określonej osoby.

| Właściwość    | Typ   | Opis                  |
|-------------|--------|------------------------------|
| FirstName (Imię)   | ciąg | Imię kontaktu.    |
| LastName (Nazwisko)    | ciąg | Nazwisko kontaktu.     |
| E-mail       | ciąg | Adres e-mail kontaktu. |
| PhoneNumber | ciąg | Numer telefonu osoby kontaktowej.  |

## <a name="fieldfilter"></a>Filtr pola

Opisuje filtr, który można zastosować do wyników wyszukiwania.

| Właściwość | Typ   | Opis                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operator | ciąg | Operator filtru: "equals", "not \_ equals", "greater \_ than", "greater \_ than or \_ \_ equals", "less \_ than", "less \_ than or \_ \_ equals", "substring", "and", "or", "starts \_ with", "not \_ starts \_ with". |

## <a name="fileinfo"></a>Fileinfo

Reprezentuje plik zewnętrzny przekazany do Partner Center.

| Właściwość                 | Typ   | Opis                                   |
|--------------------------|--------|-----------------------------------------------|
| Komentarz                  | ciąg | Komentarz skojarzony z przekazywaniem pliku.    |
| Rozszerzenie pliku            | ciąg | Rozszerzenie pliku.                           |
| Nazwa plikuWithoutExtension | ciąg | Nazwa pliku, rozszerzenie nie jest uwzględnione. |
| Rozmiar pliku                 | długi   | Rozmiar pliku.                         |
| Id                       | ciąg | Unikatowy identyfikator przekazywania pliku.            |

## <a name="link"></a>Link

Zawiera link URI i skojarzone informacje.

| Właściwość | Typ                   | Opis                        |
|----------|------------------------|------------------------------------|
| URI      | ciąg                 | The URI.                           |
| Metoda   | ciąg                 | Metoda reprezentowana przez URI. |
| Nagłówki  | Tablica parametrów KeyValuePairs | Nagłówki linku.          |

## <a name="passwordprofile"></a>PasswordProfile

Opisuje określone hasło i informacje o tym, czy należy je zmienić.

>[!NOTE]
>Nieobsługiwane na Partner Center obsługiwanych przez firmę 21Vianet.

| Właściwość            | Typ                          | Opis                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Hasło            | [Securestring](#securestring) | Hasło.                                                          |
| Forcechangepassword | boolean                       | Określa, czy należy fortywnie zmienić hasło podczas następnego logowania. |

## <a name="resourcelinks"></a>ResourceLinks

Zawiera listę linków dla zasobu.

| Właściwość   | Typ                                      | Opis                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Link](#link)                             | Własny URI.                                      |
| Następne       | [Link](#link)                             | Następna strona elementów.                            |
| Poprzednie   | [Link](#link)                             | Poprzednia strona elementów.                        |
| Atrybuty | [ResourceAttributes](#resourceattributes) | Atrybuty metadanych odpowiadające użytkownikowi. |

## <a name="resourceattributes"></a>ResourceAttributes

Zawiera metadane atrybutów dla zasobu.

| Właściwość   | Typ   | Opis                                 |
|------------|--------|---------------------------------------------|
| Etag       | ciąg | Etag, znany również jako wersja obiektu. |
| ObjectType | ciąg | Typ obiektu zasobu podstawowego.    |

## <a name="securestring"></a>Securestring

Przechowuje zabezpieczone informacje, takie jak hasło.

| Właściwość | Typ | Opis                       |
|----------|------|-----------------------------------|
| Długość   | int  | Długość zabezpieczonego ciągu. |

## <a name="validationcode"></a>ValidationCode

Reprezentuje kod weryfikacji Government Community Cloud partnera.

| Właściwość         | Typ         | Opis                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Identyfikator partnera                                                       |
| OrganizationName | ciąg       | Nazwa organizacji podana podczas procesu walidacji             |
| ValidationId     | int          | Unikatowy identyfikator weryfikacji                                       |
| MaxCreates       | dopuszczanie wartości null int | Maksymalna liczba klientów, którzy mogą zostać utworzeni za pomocą tego kodu weryfikacji    |
| RemainingCreates | dopuszczanie wartości null int | Pozostały klient tworzy pod tym identyfikatorem walidacji                      |
| Etag             | ciąg       | Konkna wersja tego zasobu. Zmienia się, gdy zasób jest zmieniany. |
