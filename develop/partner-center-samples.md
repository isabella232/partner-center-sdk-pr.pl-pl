---
title: Centrum partnerskie — przykłady
description: Aby ułatwić szybkie rozpoczęcie pracy z interfejsami API Centrum partnerskiego, udostępniamy Przykładowy program, kod języka C \ Managed fragmenty kodu, a przykładowe żądania i odpowiedzi REST.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2098544e8607eabc4d25d90dcd7cad41510778a9
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768205"
---
# <a name="partner-center-samples"></a>Centrum partnerskie — przykłady

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Aby ułatwić szybkie rozpoczęcie pracy z interfejsami API Centrum partnerskiego, udostępniamy Przykładowy program, kod zarządzany w języku C# oraz przykładowe żądania i odpowiedzi REST.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Przykład                                                        | Szczegóły                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Fragmenty kodu                                                 | W przypadku wskaźników i fragmentów kodu platformy .NET, środowiska Java i programu PowerShell, które pokazują, jak używać zarządzanego interfejsu API Centrum partnerskiego do zarządzania kontami klientów, uzyskiwania analiz, umieszczania zamówień, zarządzania rozliczeniami i subskrypcjami, zapewniania pomocy technicznej oraz zarządzania kontami i profilami, zobacz [scenariusze](scenarios.md).                                                                          |
| Przykłady dla interfejsu REST                                                  | W przypadku przykładowych żądań i odpowiedzi, które pokazują, jak używać interfejsu API REST Centrum partnerskiego do zarządzania kontami klientów, uzyskiwania analiz, umieszczania zamówień, zarządzania rozliczeniami i subskrypcjami, zapewniania pomocy technicznej oraz zarządzania kontami i profilami, zobacz [scenariusze](scenarios.md).                                                                                                       |
| [Aplikacja testowa konsoli](console-test-app.md)                       | Ta aplikacja jest dostępna w języku C# i Java, udostępnia kod i obsługę błędów dla wszystkich scenariuszy wymienionych w sekcji scenariusze.                                                                        |
| [Witryna sklepu internetowego klienta CSP](csp-customer-web-storefront.md) | Ta witryna pokazuje działający magazyn online, którego klienci mogą używać do kupowania subskrypcji produktów firmy Microsoft. Możesz łatwo utworzyć witrynę sieci Web dla swojej firmy, korzystając z [przewodnika Szybki Start dla programu CSP Customer](csp-customer-storefront-builder-quick-start-guide-.md)w sklepie.                                                              |
| Witryna sieci Web w sklepie                                                | Ta aplikacja pokazuje, jak utworzyć magazyn internetowy na podstawie wykazu ofert dostępnych dla partnerów dostawcy rozwiązań w chmurze. Klienci mogą utworzyć konto sklepu i zamówić subskrypcje oprogramowania w Twojej witrynie.<br/><br/>                  **Pobierz kod:**<br/> [Pobieranie przykładowego kodu](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Co należy skonfigurować przed wydaniem:**<br/><br/> -Uwierzytelnianie: Identyfikator aplikacji & wpis tajny<br/> -Znakowanie: logo i nazwa firmy<br/> — Komunikat powitalny<br/> -Oferty, w tym opisy i ceny. W aplikacji przyjęto założenie, że Cennik zawiera wszelkie stosowane podatki. Alternatywnie możesz dodać dodatkową logikę, aby obliczyć podatek podczas wyewidencjonowania.<br/> — Informacje o płatności: Podaj własne opcje karty kredytowej, PayPal lub inne typy płatności. Przed skonfigurowaniem tej części zapoznaj się z przewodnikiem [bez płatności, oszustwa lub nieprawidłowego użycia](/partner-center/non-payment-fraud-misuse). |