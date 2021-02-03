---
title: Witryna sklepu internetowego klienta CSP
description: Ten przykładowy kod witryny sieci Web przedstawia roboczy sklep online, który umożliwia klientom kupowanie subskrypcji produktów firmy Microsoft.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd488b9b9bf2c1df4bebc8513d230a02b06b2ce4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767741"
---
# <a name="csp-customer-web-storefront"></a>Witryna sklepu internetowego klienta CSP

**Dotyczy:**

- Centrum partnerskie

> [!NOTE]
> Ta przykładowa aplikacja dotyczy tylko globalnego wystąpienia Centrum partnerskiego. Nie dotyczy Centrum partnerskiego dla Microsoft Cloud Niemiec lub Centrum partnerskiego dla Microsoft Cloud dla instytucji rządowych USA.

Witryna sklepu w [centrum partnerskim](https://github.com/Microsoft/Partner-Center-Storefront) to **Przykładowa Witryna internetowa** dla sklepu online, za pomocą której klienci mogą kupować subskrypcje produktów firmy Microsoft. Możesz zmodyfikować ten **przykładowy kod** do własnych potrzeb, aby [skonfigurować oferty](#configure-offers), [dodać markę](#configure-branding) i [dodać metodę płatności](#configure-payment-types).

## <a name="sample-code"></a>Przykładowy kod

Pobierz [przykładowy kod sklepu Centrum partnerskiego](https://github.com/Microsoft/Partner-Center-Storefront) z usługi GitHub.

## <a name="configure-authentication"></a>Konfigurowanie uwierzytelniania

Przed skompilowaniem aplikacji zaktualizuj następujące wartości w pliku Web.config w celu odzwierciedlenia informacji o uwierzytelnianiu usługi Azure AD utworzonych w ramach [uwierzytelniania w usłudze Partner Center](partner-center-authentication.md). Podczas wczesnego programowania lub testowania w środowisku produkcyjnym należy używać ustawień konta piaskownicy do integracji.

- **partnerCenter. Identyfikator aplikacji**
- **partnerCenter.applicationSecret**
- **partnerCenter. domena**
- **webports. clientId**
- **webports. clientSecret**
- **WebPortal. domena**
- **webports. azureStorageConnectionString**

## <a name="configure-offers"></a>Konfiguruj oferty

Zestaw ofert (**MicrosoftOffer**) można skonfigurować w **OfferCatalogViewModel**.

## <a name="configure-branding"></a>Konfigurowanie znakowania

Ta przykładowa witryna sieci Web śledzi następujące informacje firmowe i markowe w *BrandingConfiguration.cs* i *PortalBranding.cs*:

- Nazwa organizacji
- Logo organizacji
- Obraz nagłówka
- Umowa dotycząca prywatności
- Kontaktowy adres e-mail
- Kontaktowy numer telefonu
- Adres e-mail pomocy technicznej
- Numer telefonu pomocy technicznej

### <a name="configure-payment-types"></a>Konfigurowanie typów płatności

Aplikacja aktualnie używa bramy systemu PayPal zaimplementowaną w *PayPalGateway.cs*.