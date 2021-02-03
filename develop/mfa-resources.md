---
title: Zasoby dotyczące wymagań dotyczących zabezpieczeń partnerów
description: Informacje na temat wdrażania usługi MFA w celu spełnienia wymagań dotyczących zabezpieczeń partnerów.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 5eb77c3c10e95c9dc835cfe05e014b9256531b51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767777"
---
# <a name="partner-security-requirements-resources"></a>Zasoby dotyczące wymagań dotyczących zabezpieczeń partnerów

**Dotyczy:**

- Centrum partnerskie

Ten artykuł ułatwia zapoznanie się ze szczegółami wdrażania uwierzytelniania wieloskładnikowego (MFA), aby pomóc organizacji w spełnieniu stanu wymagań dotyczących zabezpieczeń partnerów. 

## <a name="portal-request-without-mfa"></a>Żądanie portalu bez usługi MFA

Wskaż użytkownika, który uzyskuje dostęp do portalu Centrum partnerskiego bez uwierzytelniania MFA.

| Właściwość                            | Typ            | Opis                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | ciąg          | Identyfikator obiektu użytkownika                        |
| TenantId                            | ciąg          | Identyfikator dzierżawy CSP                         |
| Głównej                                 | ciąg          | Główna nazwa użytkownika                   |
| LastNonMfaCompliantLoginDateTime    | datetime        | Godzina ostatniego logowania użytkownika bez usługi MFA |


## <a name="api-request-summarized-by-application"></a>Żądanie interfejsu API podsumowane przez aplikację

Podsumowanie żądania interfejsu API wykonane przez aplikację i poświadczenia użytkownika, zagregowane według daty i identyfikatora aplikacji.

| Właściwość                            | Typ            | Opis               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | Data żądania interfejsu API          |
| MfaCompliantRequestCount            | długi            | Liczba żądań z uwierzytelnianiem MFA    |
| TotalRequestCount                   | długi            | Łączna liczba żądań       |
| ApplicationId                       | ciąg          | Identyfikator aplikacji        |
| ApplicationName                     | ciąg          | Nazwa aplikacji      |


## <a name="api-request-details"></a>Szczegóły żądania interfejsu API

Żądanie interfejsu API wykonane przez aplikację i poświadczenia użytkownika. 

| Właściwość                            | Typ            | Opis                              |
|-------------------------------------|-----------------|------------------------------------------|
| IdentyfikatorŻądania                           | ciąg          | MS-RequestId                             |
| CorrelationId                       | ciąg          | MS-CorrelationId                         |
| OperationName                       | ciąg          | Ścieżka interfejsu API z metodą żądania         |
| RequestDateTime                     | DateTime        | Czas żądania interfejsu API                     |
| Adresu                           | ciąg          | Źródłowy adres IP                        |
| ObjectId                            | ciąg          | Identyfikator obiektu użytkownika                           |
| TenantId                            | ciąg          | Identyfikator dzierżawy CSP                            |
| Głównej                                 | ciąg          | Główna nazwa użytkownika                      |
| ApplicationId                       | ciąg          | Twoja aplikacja                         |
| MfaCompliant                        | bool            | Wskaż żądanie z usługą MFA lub bez niej |
