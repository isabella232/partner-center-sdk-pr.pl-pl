---
title: Witryna sklepu internetowego klienta CSP
description: Ten przykładowy kod witryny internetowej przedstawia roboczy sklep online, w ramach który klienci mogą kupować subskrypcje produktów firmy Microsoft.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07020c365db2ad578e7ff75602519d06eabb2a3bebf0913899fcd8b5345a0365
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995207"
---
# <a name="csp-customer-web-storefront"></a>Witryna sklepu internetowego klienta CSP

**Dotyczy:** Partner Center

**Nie dotyczy programu**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Ta przykładowa aplikacja ma zastosowanie tylko do globalnego wystąpienia Partner Center.

Witryna [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) to  przykładowa witryna internetowa dla sklepu online, za pomocą których klienci mogą kupować subskrypcje produktów firmy Microsoft. Możesz zmodyfikować ten **przykładowy kod** na własny użytek, aby skonfigurować [oferty,](#configure-offers)dodać znakowanie [i](#configure-branding)dodać formę [płatności.](#configure-payment-types)

## <a name="sample-code"></a>Przykładowy kod

Pobierz [przykładowy kod Partner Center storefront z](https://github.com/Microsoft/Partner-Center-Storefront) GitHub.

## <a name="configure-authentication"></a>Konfigurowanie uwierzytelniania

Przed skompilowanie aplikacji zaktualizuj następujące wartości w pliku Web.config, aby odzwierciedlić informacje o uwierzytelnianiu usługi Azure AD utworzone podczas [Partner Center uwierzytelniania.](partner-center-authentication.md) Ustawień konta piaskownicy integracji należy używać na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym (TiP).

- **partnerCenter.applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter.domain**
- **webPortal.clientId**
- **webPortal.clientSecret**
- **webPortal.domain**
- **webPortal.azureStorageConnectionString**

## <a name="configure-offers"></a>Konfigurowanie ofert

Zestaw ofert **(MicrosoftOffer)** można skonfigurować w modelu **OfferCatalogViewModel.**

## <a name="configure-branding"></a>Konfigurowanie brandowania

Ta przykładowa witryna internetowa śledzi następujące informacje o firmie i marce w *witrynach BrandingConfiguration.cs* i *PortalBranding.cs:*

- Nazwa organizacji
- Logo organizacji
- Obraz nagłówka
- Umowa o ochronie prywatności
- Kontaktowy adres e-mail
- Numer telefonu kontaktowego
- Adres e-mail pomocy technicznej
- Numer telefonu pomocy technicznej

### <a name="configure-payment-types"></a>Konfigurowanie typów płatności

Aplikacja używa obecnie bramy PayPal zaimplementowanej w *payPalGateway.cs.*