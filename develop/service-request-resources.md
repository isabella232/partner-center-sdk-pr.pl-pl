---
title: Zasoby żądania obsługi
description: Partnerzy mogą zgłosić żądania usługi plików w imieniu swoich partnerów w celu zgłaszania przez firmę Microsoft nieprzerwanych usług lub zażądać innych pomocy technicznej, których nie mogą zapewnić.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 072f9eddaf9d854f1dcc8cc65f7928b6c95700fa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767825"
---
# <a name="service-request-resources"></a>Zasoby żądania obsługi

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Partnerzy mogą zgłosić żądania usługi plików w imieniu swoich partnerów w celu zgłaszania przez firmę Microsoft nieprzerwanych usług lub zażądać innych pomocy technicznej, których nie mogą zapewnić.

## <a name="servicerequest"></a>Przepływy

Opisuje żądanie obsługi zgłoszone przez partnera, w tym informacje o postępie tego żądania.

| Właściwość         | Typ                                                          | Opis                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Tytuł            | ciąg                                                        | Tytuł żądania obsługi.                                                           |
| Opis      | ciąg                                                        | Opis.                                                                     |
| Ważność         | ciąg                                                        | Ważność: "nieznany", "krytyczny", "umiarkowany" lub "minimalny".                       |
| SupportTopicId   | ciąg                                                        | Identyfikator tematu pomocy technicznej.                                                         |
| SupportTopicName | ciąg                                                        | Nazwa tematu pomocy technicznej.                                                       |
| Id               | ciąg                                                        | Identyfikator żądania obsługi.                                                       |
| Stan           | ciąg                                                        | Stan żądania obsługi: "Brak", "otwarte", "zamknięte" lub " \_ wymagana Uwaga". |
| Organizacja     | [ServiceRequestOrganization](#servicerequestorganization)     | Organizacja, dla której jest tworzone żądanie obsługi.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Podstawowy kontakt z żądaniem obsługi.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Ostatni zaktualizowany przez" kontakt dotyczący zmian w żądaniu obsługi.                        |
| ProductName      | ciąg                                                        | Nazwa produktu odpowiadającego żądaniu usługi.                     |
| ProductId        | ciąg                                                        | Identyfikator produktu.                                                               |
| CreatedDate      | date                                                          | Data utworzenia żądania obsługi.                                          |
| LastModifiedDate | date                                                          | Data ostatniej modyfikacji żądania obsługi.                                 |
| LastClosedDate   | date                                                          | Data ostatniego zamknięcia żądania obsługi.                                   |
| FileLinks        | Tablica zasobów [FileInfo](utility-resources.md#fileinfo) | Kolekcja linków do plików odnoszących się do żądania obsługi.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | Notatkę można dodać do istniejącego żądania obsługi.                                  |
| Uwagi            | Tablica [ServiceRequestNotes](#servicerequestnote)           | Kolekcja uwag dodanych do żądania obsługi.                                  |
| CountryCode      | ciąg                                                        | Kraj odpowiadający żądaniu obsługi.                                    |
| Atrybuty       | ResourceAttributes                                            | Atrybuty metadanych odpowiadające żądaniu usługi.                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

Opisuje osobę kontaktową, która tworzy lub modyfikuje żądanie obsługi.

| Właściwość     | Typ                                                      | Opis                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organizacja | [ServiceRequestOrganization](#servicerequestorganization) | Organizacja, dla której jest tworzone żądanie obsługi. |
| ContactId    | ciąg                                                    | Unikatowy identyfikator kontaktu.                               |
| LastName (Nazwisko)     | ciąg                                                    | Nazwisko osoby kontaktowej.                          |
| FirstName (Imię)    | ciąg                                                    | Imię kontaktu.                         |
| E-mail        | ciąg                                                    | Adres e-mail osoby kontaktowej.                              |
| PhoneNumber  | ciąg                                                    | Numer telefonu kontaktu.                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

Zawiera opis notatki dołączonej do żądania obsługi.

| Właściwość      | Typ   | Opis                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | ciąg | Nazwa twórcy notatki.         |
| CreatedDate   | date   | Data i godzina utworzenia notatki. |
| Tekst          | ciąg | Tekst notatki.                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

Opisuje organizację, dla której jest tworzone żądanie obsługi.

| Właściwość    | Typ   | Opis                           |
|-------------|--------|---------------------------------------|
| Id          | ciąg | Unikatowy identyfikator organizacji.    |
| Nazwa        | ciąg | Nazwa organizacji.         |
| PhoneNumber | ciąg | Numer telefonu organizacji. |

## <a name="supporttopic"></a>SupportTopic

Opisuje temat pomocy technicznej. Żądania obsługi określają temat pomocy technicznej, aby upewnić się, że są one przetwarzane szybko i efektywnie.

| Właściwość    | Typ               | Opis                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Nazwa        | ciąg             | Nazwa tematu pomocy technicznej.                                |
| Opis | ciąg             | Opis tematu pomocy technicznej.                         |
| Id          | ciąg             | Unikatowy identyfikator tematu pomocy technicznej.                           |
| Atrybuty  | ResourceAttributes | Atrybuty metadanych odpowiadające żądaniu usługi. |

