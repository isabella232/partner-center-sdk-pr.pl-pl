---
title: Zasoby dotyczące wymagań dotyczących zabezpieczeń partnerów
description: Poznaj szczegóły wdrożenia usługi Multi-Factor Authentication (MFA), aby spełnić wymagania dotyczące zabezpieczeń partnerów.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: b41a0e46fa6e0643e82a5a2dbfb7141f54a0f824
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445548"
---
# <a name="partner-security-requirements-resources"></a>Zasoby dotyczące wymagań dotyczących zabezpieczeń partnerów

Ten artykuł ułatwia zrozumienie szczegółów wdrożenia uwierzytelniania wieloskładnikowego (MFA) w celu spełnienia przez organizację wymagań dotyczących zabezpieczeń partnera. 

## <a name="portal-request-without-mfa"></a>Żądanie portalu bez uwierzytelniania wieloskładnikowego

Wskaż użytkownika, który uzyskuje dostęp Partner Center portalu bez uwierzytelniania MFA.

| Właściwość                            | Typ            | Opis                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | ciąg          | Identyfikator obiektu użytkownika                        |
| TenantId                            | ciąg          | Identyfikator dzierżawy CSP                         |
| Upn                                 | ciąg          | Główna nazwa użytkownika                   |
| LastNonMfaCompliantLoginDateTime    | datetime        | Najnowszy czas logowania użytkownika bez uwierzytelniania wieloskładnikowego |


## <a name="api-request-summarized-by-application"></a>Żądanie interfejsu API podsumowane przez aplikację

Podsumowanie żądania interfejsu API wykonanego przez poświadczenia aplikacji i użytkownika zagregowane według daty żądania i identyfikatora aplikacji.

| Właściwość                            | Typ            | Opis               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | Data żądania interfejsu API          |
| MfaCompliantRequestCount            | długi            | Liczba żądań z uwierzytelniania wieloskładnikowego    |
| TotalRequestCount                   | długi            | Łączna liczba żądań       |
| ApplicationId                       | ciąg          | Identyfikator aplikacji        |
| ApplicationName                     | ciąg          | Nazwa aplikacji      |


## <a name="api-request-details"></a>Szczegóły żądania interfejsu API

Żądanie interfejsu API wykonane przez poświadczenia aplikacji i użytkownika. 

| Właściwość                            | Typ            | Opis                              |
|-------------------------------------|-----------------|------------------------------------------|
| Requestid                           | ciąg          | MS-RequestId                             |
| CorrelationId                       | ciąg          | MS-CorrelationId                         |
| OperationName                       | ciąg          | Ścieżka interfejsu API z metodą żądania         |
| RequestDateTime                     | DateTime        | Czas żądania interfejsu API                     |
| Ipaddress                           | ciąg          | Źródłowy adres IP                        |
| ObjectId                            | ciąg          | Identyfikator obiektu użytkownika                           |
| TenantId                            | ciąg          | Identyfikator dzierżawy CSP                            |
| Upn                                 | ciąg          | Główna nazwa użytkownika                      |
| ApplicationId                       | ciąg          | Twoja aplikacja                         |
| MfaCompliant                        | bool            | Wskazanie żądania z uwierzytelniania wieloskładnikowego lub bez niego |
