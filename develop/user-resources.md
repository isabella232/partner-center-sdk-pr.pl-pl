---
title: Zasoby użytkownika
description: Opisuje indywidualnego użytkownika Centrum partnerskiego, informacje osobiste i dotyczące konta oraz uprawnienia, które mają w centrum partnerskim.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c88b9b65dfb925712ff85fb42d34251cca6e0b5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767681"
---
# <a name="user-resources"></a>Zasoby użytkownika

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Opisuje indywidualnego użytkownika Centrum partnerskiego, informacje osobiste i dotyczące konta oraz uprawnienia, które mają w centrum partnerskim.

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
| lastDirectorySyncTime | ciąg w formacie daty i godziny czasu UTC                                 | Czas ostatniej synchronizacji informacji dla tego użytkownika między Azure Active Directory i Active Directory lokalnymi. Wartość daty i godziny jest wyświetlana tylko wtedy, gdy synchronizacja Azure AD Connect jest włączona. W przeciwnym razie wartość jest równa null. |
| userDomainType        | ciąg                                                         | Typ domeny użytkownika: "none", "Managed" lub "federacyjna".                                                                                                                                                                   |
| stan                 | ciąg                                                         | Stan użytkownika: "aktywny", "nieaktywny" (dla usuniętego użytkownika).                                                                                                                                                          |
| softDeletionTime      | ciąg w formacie daty i godziny czasu UTC                                 | Przedstawia Początek 30-dniowego okresu, po którym dane skojarzone z usuniętym użytkownikiem są trwale usuwane i w związku z tym nieodwracalne.                                                                          |
| linki                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów.                                                                                                                                                                                                        |
| atrybuty            | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

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
| lastDirectorySyncTime | ciąg w formacie daty i godziny czasu UTC                                 | Czas ostatniej synchronizacji informacji dla tego użytkownika między Azure Active Directory i Active Directory lokalnymi. Wartość daty i godziny jest wyświetlana tylko wtedy, gdy synchronizacja Azure AD Connect jest włączona. W przeciwnym razie wartość jest równa null. |
| userDomainType        | ciąg                                                         | Typ domeny użytkownika: "none", "Managed" lub "federacyjna".                                                                                                                                                                   |
| stan                 | ciąg                                                         | Stan użytkownika: "aktywny", "nieaktywny" (dla usuniętego użytkownika).                                                                                                                                                          |
| softDeletionTime      | ciąg w formacie daty i godziny czasu UTC                                 | Przedstawia Początek 30-dniowego okresu, po którym dane skojarzone z usuniętym użytkownikiem są trwale usuwane i w związku z tym nieodwracalne.                                                                          |
| linki                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów.                                                                                                                                                                                                        |
| atrybuty            | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

Opisuje poświadczenia logowania użytkownika.

| Właściwość | Typ                                               | Opis                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | ciąg                                             | Nazwa użytkownika.                |
| hasło | [SecureString](utility-resources.md#securestring) | Bezpieczne przechowywane hasło użytkownika. |

## <a name="usermember"></a>UserMember

Opisuje informacje o członkach użytkownika.

| Właściwość          | Typ                                                           | Opis                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | ciąg                                                         | Wyświetlana nazwa użytkownika.   |
| userPrincipalName | ciąg                                                         | Nazwa podmiotu zabezpieczeń użytkownika.    |
| roleId            | ciąg                                                         | Identyfikator roli użytkownika. |
| identyfikator                | ciąg                                                         | Identyfikator elementu członkowskiego.      |
| atrybuty        | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.           |

