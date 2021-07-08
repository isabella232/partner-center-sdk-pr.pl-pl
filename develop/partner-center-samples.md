---
title: Centrum partnerskie — przykłady
description: Aby ułatwić szybkie uruchomienie aplikacji za pomocą interfejsów API Partner Center, oferujemy przykładowy program, fragmenty kodu zarządzanego C\ oraz przykładowe żądania i odpowiedzi REST.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 36d1c74e12ae680facef1414ce35ac2d6fb5322c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547839"
---
# <a name="partner-center-samples"></a>Centrum partnerskie — przykłady

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Aby ułatwić szybkie uruchomienie przy użyciu interfejsów API Partner Center, oferujemy przykładowy program, fragmenty kodu zarządzane w języku C# oraz przykładowe żądania i odpowiedzi REST.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Przykład                                                        | Szczegóły                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Fragmenty kodu                                                 | W przypadku wskaźników i fragmentów kodu .NET, Java i PowerShell, które pokazują, jak używać zarządzanego interfejsu API usługi Partner Center do zarządzania kontami klientów, uzyskać analizę, składać zamówienia, zarządzać rozliczeniami i subskrypcjami, zapewniać pomoc techniczną oraz zarządzać kontami i profilami, zobacz [Scenariusze](scenarios.md).                                                                          |
| Przykłady dla interfejsu REST                                                  | Aby uzyskać przykładowe żądania i odpowiedzi, które pokazują, jak za pomocą interfejsu API REST usługi Partner Center zarządzać kontami klientów, pobierać analizy, składać zamówienia, zarządzać rozliczeniami i subskrypcjami, zapewniać pomoc techniczną oraz zarządzać kontami i profilami, zobacz [Scenariusze](scenarios.md).                                                                                                       |
| [Aplikacja testowa konsoli](console-test-app.md)                       | Ta aplikacja jest dostępna w językach C# i Java, udostępnia kod i obsługę błędów dla wszystkich scenariuszy wymienionych w sekcji scenariuszy.                                                                        |
| [Witryna sklepu internetowego klienta CSP](csp-customer-web-storefront.md) | W tej witrynie przedstawiono roboczy sklep online, za pomocą których klienci mogą kupować subskrypcje produktów firmy Microsoft. Witrynę internetową dla swojej firmy można łatwo utworzyć za pomocą przewodnika Szybki start [CSP Customer Storefront Builder](csp-customer-storefront-builder-quick-start-guide-.md).                                                              |
| Store web site (Witryna sklepu)                                                | Ta aplikacja pokazuje, jak utworzyć sklep internetowy na podstawie katalogu ofert dostępnych dla Dostawca rozwiązań w chmurze partnerów. Klienci mogą tworzyć konta sklepu i zamówić subskrypcje oprogramowania za pośrednictwem witryny.<br/><br/>                  **Pobierz kod:**<br/> [Pobieranie przykładowego kodu](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Co należy skonfigurować przed wydaniem:**<br/><br/> - Uwierzytelnianie: identyfikator aplikacji & tajny<br/> - Znakowanie: logo i nazwa firmy<br/> — Wiadomość powitana<br/> - Oferty, w tym opisy i ceny. W aplikacji przyjęto założenie, że ceny na liście obejmują wszelkie odpowiednie podatki. Alternatywnie możesz dodać dodatkową logikę do obliczania podatku podczas finalizacji zakupu.<br/> — Informacje o płatności: podaj własne opcje kart kredytowych, PayPal lub inne typy płatności. Przed skonfigurowaniem tej części przeczytaj przewodnik [Non-payment, fraud, or misuse (Brak płatności, oszustwo lub nadużycie).](/partner-center/non-payment-fraud-misuse) |