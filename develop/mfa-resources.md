---
title: Zasoby dotyczące wymagań dotyczących zabezpieczeń partnerów
description: Poznaj szczegóły wdrożenia usługi Multi-Factor Authentication (MFA), aby spełnić wymagania dotyczące zabezpieczeń partnerów.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 6377dbde574edd1b8d8058f7b8e88ae6497d615b9237bbda91e9c4617486b569
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997893"
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
