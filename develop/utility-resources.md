---
title: Zasoby narzędziowe
description: Interfejs API REST Centrum partnerskiego zawiera wiele zasobów, które opisują modele danych ogólnego przeznaczenia używane w całym zestawie SDK.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 53d39e4f76684128d48eacdce75706d853c7ce74
ms.sourcegitcommit: f5178dca1d9a51059738972810235d8858e6a67a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/18/2020
ms.locfileid: "97768581"
---
# <a name="utility-resources"></a>Zasoby narzędziowe

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Interfejs API REST Centrum partnerskiego zawiera wiele zasobów, które opisują modele danych ogólnego przeznaczenia używane w całym zestawie SDK.

## <a name="address"></a>Adres

Adres używany przez profile klienta lub partnera. Aby uzyskać więcej informacji na temat obsługiwanych formatów i właściwości w różnych krajach/regionach, zobacz [pobieranie reguł formatowania adresów według rynku](get-market-specific-validation-data.md).

| Właściwość     | Typ   | Długość (min., maks.) | Opis                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | ciąg | (1, 200)          | Pierwszy wiersz adresu.                                                                   |
| AddressLine2 | ciąg | (0, 200)          | Drugi wiersz adresu. Ta właściwość jest opcjonalna.                                       |
| City (Miasto)         | ciąg | n/d               | Miasto.                                                                                        |
| Stan        | ciąg | (0, 2)            | Stan.                                                                                       |
| PostalCode   | ciąg | n/d               | Kod ZIP lub kod pocztowy.                                                                     |
| Kraj      | ciąg | (2, 2)            | Kraj/region w formacie kodu kraju ISO.                                                   |
| Region (Region)       | ciąg | n/d               | Region.                                                                                      |
| FirstName (Imię)    | ciąg | (1, 50)           | Imię kontaktu w firmie/organizacji klienta.                              |
| MiddleName   | ciąg | (1, 50)           | Drugie imię kontaktu w firmie/organizacji klienta. Ta właściwość jest opcjonalna.  |
| LastName (Nazwisko)     | ciąg | (1, 50)           | Nazwisko osoby kontaktowej w firmie/organizacji klienta.                               |
| PhoneNumber  | ciąg | n/d               | Numer telefonu kontaktu w firmie/organizacji klienta. Ta właściwość jest opcjonalna.|
|PhoneNumber|ciąg|n/d|Numer telefonu kontaktu w firmie/organizacji klienta. W profilu klienta ta właściwość jest wymagana przez firmę/organizację klienta znajdującą się w następujących krajach. Armenia (AM), Azerbejdżan (AZ), Białoruś (przez), Węgry (HU), Kazachstan (KZ), Kirgistan (KG), Mołdawia (MD), Rosja (RU), Tadżykistan (TJ), Uzbekistan (UZ), Ukraina (UA). W przeciwnym razie jest to opcjonalne.|


## <a name="contact"></a>Kontakt

Opisuje informacje kontaktowe dla konkretnej osoby.

| Właściwość    | Typ   | Opis                  |
|-------------|--------|------------------------------|
| FirstName (Imię)   | ciąg | Imię kontaktu.    |
| LastName (Nazwisko)    | ciąg | Nazwisko osoby kontaktowej.     |
| E-mail       | ciąg | Adres e-mail osoby kontaktowej. |
| PhoneNumber | ciąg | Numer telefonu kontaktu.  |

## <a name="fieldfilter"></a>FieldFilter

Opisuje filtr, który można zastosować do wyników wyszukiwania.

| Właściwość | Typ   | Opis                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operator | ciąg | Operator filtru: "Equals", "nie \_ równa się", "większe niż \_ ", "większe \_ niż \_ lub \_ równe", "mniejsze \_ niż", "mniejsze \_ niż \_ lub \_ równe", "podciąg", "i", "lub", "zaczyna się od" \_ , "nie \_ zaczyna się \_ od". |

## <a name="fileinfo"></a>FileInfo

Reprezentuje plik zewnętrzny przekazany do Centrum partnerskiego.

| Właściwość                 | Typ   | Opis                                   |
|--------------------------|--------|-----------------------------------------------|
| Komentarz                  | ciąg | Komentarz skojarzony z przekazywaniem pliku.    |
| FileExtension            | ciąg | Rozszerzenie pliku.                           |
| FileNameWithoutExtension | ciąg | Nazwa pliku, rozszerzenie nie jest uwzględnione. |
| Rozmiar pliku                 | długi   | Rozmiar pliku.                         |
| Id                       | ciąg | Unikatowy identyfikator przekazywania pliku.            |

## <a name="link"></a>Łącze

Zawiera łącze identyfikatora URI i powiązane z nim informacje.

| Właściwość | Typ                   | Opis                        |
|----------|------------------------|------------------------------------|
| URI      | ciąg                 | Identyfikator URI.                           |
| Metoda   | ciąg                 | Metoda reprezentowana przez identyfikator URI. |
| Nagłówki  | Tablica KeyValuePairs | Nagłówki dla linku.          |

## <a name="passwordprofile"></a>PasswordProfile

Opisuje określone hasło i jeśli należy zmienić to hasło.

>[!NOTE]
>Nieobsługiwane w centrum partnerskim obsługiwanym przez firmę 21Vianet.

| Właściwość            | Typ                          | Opis                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Hasło            | [SecureString](#securestring) | Hasło.                                                          |
| ForceChangePassword | boolean                       | Określa, czy należy wymusić zmianę hasła przy następnym logowaniu. |

## <a name="resourcelinks"></a>ResourceLinks

Zawiera listę linków dla zasobu.

| Właściwość   | Typ                                      | Opis                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [Łącze](#link)                             | Własny identyfikator URI.                                      |
| Następne       | [Łącze](#link)                             | Następna strona elementów.                            |
| Poprzednie   | [Łącze](#link)                             | Poprzednia strona elementów.                        |
| Atrybuty | [ResourceAttributes](#resourceattributes) | Atrybuty metadanych odpowiadające użytkownikowi. |

## <a name="resourceattributes"></a>ResourceAttributes

Zawiera metadane atrybutu dla zasobu.

| Właściwość   | Typ   | Opis                                 |
|------------|--------|---------------------------------------------|
| Element ETag       | ciąg | Element ETag, znany również jako wersja obiektu. |
| ObjectType | ciąg | Typ obiektu zasobu podstawowego.    |

## <a name="securestring"></a>SecureString

Przechowuje zabezpieczone informacje, takie jak hasło.

| Właściwość | Typ | Opis                       |
|----------|------|-----------------------------------|
| Długość   | int  | Długość bezpiecznego ciągu. |

## <a name="validationcode"></a>ValidationCode

Reprezentuje kod weryfikacyjny w chmurze dla instytucji rządowych.

| Właściwość         | Typ         | Opis                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Identyfikator partnera                                                       |
| OrganizationName | ciąg       | Nazwa organizacji podana podczas procesu weryfikacji             |
| ValidationId     | int          | Unikatowy identyfikator na potrzeby walidacji                                       |
| MaxCreates       | wartość null int | Maksymalna liczba klientów, którzy mogą być tworzeniu przy użyciu tego kodu weryfikacyjnego    |
| RemainingCreates | wartość null int | Pozostały klient tworzy w ramach tego identyfikatora weryfikacji                      |
| Element ETag             | ciąg       | Określona wersja tego zasobu. Zmiany w momencie zmiany zasobu. |
