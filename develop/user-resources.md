---
title: Zasoby użytkownika
description: Opisuje użytkownika Partner Center, informacje o jego osobistych i kontach oraz uprawnienia, które ma w Partner Center.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 26bb202db3eefd9be8fe57ed2cc4dc220c8807d4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529685"
---
# <a name="user-resources"></a>Zasoby użytkownika

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Opisuje użytkownika Partner Center, informacje o jego osobistych i kontach oraz uprawnienia, które ma w Partner Center.

## <a name="user"></a>Użytkownik

Opisuje pojedynczego użytkownika.

| Właściwość              | Typ                                                           | Opis                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg                                                         | Identyfikator użytkownika.                                                                                                                                                                                                       |
| userPrincipalName     | ciąg                                                         | Identyfikator podmiotu zabezpieczeń użytkownika.                                                                                                                                                                                             |
| firstName             | ciąg                                                         | Imię użytkownika.                                                                                                                                                                                                |
| lastName              | ciąg                                                         | Nazwisko użytkownika.                                                                                                                                                                                                 |
| displayName           | ciąg                                                         | Wyświetlana nazwa użytkownika.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Profil hasła użytkownika.                                                                                                                                                                                               |
| phoneNumber           | ciąg                                                         | Numer telefonu użytkownika.                                                                                                                                                                                                   |
| lastDirectorySyncTime | ciąg w formacie daty i godzin UTC                                 | Czas ostatniej synchronizacji informacji dla tego użytkownika między Azure Active Directory lokalna usługa Active Directory. Wartość daty i czasu jest wyświetlana tylko wtedy, gdy Połączenie synchronizacji usługi Azure AD jest włączona. W przeciwnym razie wartość jest null. |
| userDomainType        | ciąg                                                         | Typ domeny użytkownika: "brak", "zarządzany" lub "federowany".                                                                                                                                                                   |
| stan                 | ciąg                                                         | Stan użytkownika: "aktywny", "nieaktywny" (dla usuniętego użytkownika).                                                                                                                                                          |
| softDeletionTime      | ciąg w formacie daty i godzin UTC                                 | Reprezentuje początek 30-dniowego okresu, po którym dane skojarzone z usuniętym użytkownikiem są trwale usuwane i w związku z tym nienadajne do przejęcia.                                                                          |
| Linki                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Link do zasobu.                                                                                                                                                                                                        |
| atrybuty            | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                                                                                                                                                                   |

## <a name="customeruser"></a>Użytkownik_klienta

Opisuje użytkownika klienta.

| Właściwość              | Typ                                                           | Opis                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | ciąg                                                         | Lokalizacja, w której użytkownik zamierza korzystać z licencji.                                                                                                                                                                    |
| identyfikator                    | ciąg                                                         | Identyfikator użytkownika.                                                                                                                                                                                                       |
| userPrincipalName     | ciąg                                                         | Identyfikator podmiotu zabezpieczeń użytkownika.                                                                                                                                                                                             |
| firstName             | ciąg                                                         | Imię użytkownika.                                                                                                                                                                                                |
| lastName              | ciąg                                                         | Nazwisko użytkownika.                                                                                                                                                                                                 |
| displayName           | ciąg                                                         | Wyświetlana nazwa użytkownika.                                                                                                                                                                                            |
| immutableId           | ciąg                                                         | Niezmienny identyfikator użytkownika.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Profil hasła użytkownika.                                                                                                                                                                                               |
| phoneNumber           | ciąg                                                         | Numer telefonu użytkownika.                                                                                                                                                                                                   |
| lastDirectorySyncTime | ciąg w formacie daty i godzin UTC                                 | Czas ostatniej synchronizacji informacji dla tego użytkownika między Azure Active Directory lokalna usługa Active Directory. Wartość daty i czasu jest wyświetlana tylko wtedy, gdy Połączenie synchronizacji usługi Azure AD jest włączona. W przeciwnym razie wartość jest null. |
| userDomainType        | ciąg                                                         | Typ domeny użytkownika: "brak", "zarządzany" lub "federowany".                                                                                                                                                                   |
| stan                 | ciąg                                                         | Stan użytkownika: "aktywny", "nieaktywny" (dla usuniętego użytkownika).                                                                                                                                                          |
| softDeletionTime      | ciąg w formacie daty i godzin UTC                                 | Reprezentuje początek 30-dniowego okresu, po którym dane skojarzone z usuniętym użytkownikiem są trwale usuwane i w związku z tym nienadajne do przejęcia.                                                                          |
| Linki                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Link do zasobu.                                                                                                                                                                                                        |
| atrybuty            | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

Opisuje poświadczenia logowania użytkownika.

| Właściwość | Typ                                               | Opis                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | ciąg                                             | Nazwa użytkownika.                |
| hasło | [Securestring](utility-resources.md#securestring) | Bezpiecznie przechowywane hasło użytkownika. |

## <a name="usermember"></a>UserMember (Użytkownik jest użytkownikiem)

Opisuje informacje o członkach użytkownika.

| Właściwość          | Typ                                                           | Opis                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | ciąg                                                         | Wyświetlana nazwa użytkownika.   |
| userPrincipalName | ciąg                                                         | Nazwa podmiotu zabezpieczeń użytkownika.    |
| roleId            | ciąg                                                         | Identyfikator roli użytkownika. |
| identyfikator                | ciąg                                                         | Identyfikator członka.      |
| atrybuty        | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.           |

