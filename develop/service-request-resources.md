---
title: Zasoby żądania obsługi
description: Partnerzy mogą zgłaszać żądania obsługi w imieniu swoich partnerów w celu zgłaszania przerw w działaniu usług oferowanych przez firmę Microsoft lub żądania pomocy technicznej innej firmy, która nie jest w stanie jej zapewnić.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f919b3c34ff179a7a6cd0541f34c53737ec4148e44791419d2252fae64b0658d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993235"
---
# <a name="service-request-resources"></a>Zasoby żądania obsługi

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Partnerzy mogą zgłaszać żądania obsługi w imieniu swoich partnerów w celu zgłaszania przerw w działaniu usług oferowanych przez firmę Microsoft lub żądania pomocy technicznej innej firmy, która nie jest w stanie jej zapewnić.

## <a name="servicerequest"></a>ServiceRequest

Opisuje żądanie obsługi zgłoszone przez partnera, w tym sposób, w jaki żądanie postępuje.

| Właściwość         | Typ                                                          | Opis                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Tytuł            | ciąg                                                        | Tytuł żądania obsługi.                                                           |
| Opis      | ciąg                                                        | Opis.                                                                     |
| Ważność         | ciąg                                                        | Ważność: "nieznany", "krytyczny", "umiarkowany" lub "minimalny".                       |
| SupportTopicId   | ciąg                                                        | Identyfikator tematu pomocy technicznej.                                                         |
| SupportTopicName | ciąg                                                        | Nazwa tematu pomocy technicznej.                                                       |
| Id               | ciąg                                                        | Identyfikator żądania obsługi.                                                       |
| Stan           | ciąg                                                        | Stan żądania obsługi: "brak", "otwarte", "zamknięte" lub "potrzebna \_ uwaga". |
| Organizacja     | [ServiceRequestOrganization](#servicerequestorganization)     | Organizacja, dla której utworzono żądanie obsługi.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Podstawowa osoba kontaktowa w żądaniu obsługi.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | Kontakt "Ostatnia aktualizacja przez" w przypadku zmian w żądaniu obsługi.                        |
| ProductName      | ciąg                                                        | Nazwa produktu, która odpowiada żądaniu obsługi.                     |
| ProductId        | ciąg                                                        | Identyfikator produktu.                                                               |
| CreatedDate      | data                                                          | Data utworzenia żądania obsługi.                                          |
| LastModifiedDate | data                                                          | Data ostatniej modyfikacji żądania obsługi.                                 |
| LastClosedDate   | data                                                          | Data ostatniego zamknięcia żądania obsługi.                                   |
| Linki do plików        | tablica [zasobów FileInfo](utility-resources.md#fileinfo) | Kolekcja linków do plików odnoszących się do żądania obsługi.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Notatkę można dodać do istniejącego żądania obsługi.                                  |
| Uwagi            | tablica [elementów ServiceRequestNotes](#servicerequestnote)           | Kolekcja notatek dodanych do żądania obsługi.                                  |
| CountryCode      | ciąg                                                        | Kraj odpowiadający żądaniu obsługi.                                    |
| Atrybuty       | ResourceAttributes                                            | Atrybuty metadanych odpowiadające żądaniu obsługi.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Opisuje kontakt, który tworzy lub modyfikuje żądanie obsługi.

| Właściwość     | Typ                                                      | Opis                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organizacja | [ServiceRequestOrganization](#servicerequestorganization) | Organizacja, dla której utworzono żądanie obsługi. |
| Contactid    | ciąg                                                    | Unikatowy identyfikator kontaktu.                               |
| LastName (Nazwisko)     | ciąg                                                    | Nazwisko kontaktu.                          |
| FirstName (Imię)    | ciąg                                                    | Imię kontaktu.                         |
| E-mail        | ciąg                                                    | Adres e-mail kontaktu.                              |
| PhoneNumber  | ciąg                                                    | Numer telefonu kontaktu.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Opisuje notatkę dołączona do żądania obsługi.

| Właściwość      | Typ   | Opis                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | ciąg | Nazwa twórcy notatki.         |
| CreatedDate   | data   | Data i godzina utworzenia notatki. |
| Tekst          | ciąg | Tekst notatki.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Opisuje organizację, dla której utworzono żądanie obsługi.

| Właściwość    | Typ   | Opis                           |
|-------------|--------|---------------------------------------|
| Id          | ciąg | Unikatowy identyfikator organizacji.    |
| Nazwa        | ciąg | Nazwa organizacji.         |
| PhoneNumber | ciąg | Numer telefonu organizacji. |

## <a name="supporttopic"></a>SupportTopic

Opisuje temat pomocy technicznej. Żądania obsługi określają temat pomocy technicznej, aby upewnić się, że są przetwarzane szybko i efektywnie.

| Właściwość    | Typ               | Opis                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Nazwa        | ciąg             | Nazwa tematu pomocy technicznej.                                |
| Opis | ciąg             | Opis tematu pomocy technicznej.                         |
| Id          | ciąg             | Unikatowy identyfikator tematu pomocy technicznej.                           |
| Atrybuty  | ResourceAttributes | Atrybuty metadanych odpowiadające żądaniu obsługi. |

