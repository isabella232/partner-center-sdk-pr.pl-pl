---
title: Witryna sklepu internetowego klienta CSP
description: Ten przykładowy kod witryny internetowej przedstawia roboczy sklep online, w ramach który klienci mogą kupować subskrypcje produktów firmy Microsoft.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d68f17d707731f426cb980a566b6478790d3507c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973336"
---
# <a name="csp-customer-web-storefront"></a>Witryna sklepu internetowego klienta CSP

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Ta przykładowa aplikacja ma zastosowanie tylko do globalnego wystąpienia Partner Center.

Witryna [Partner Center storefront](https://github.com/Microsoft/Partner-Center-Storefront) to  przykładowa witryna internetowa sklepu online, za pomocą których klienci mogą kupować subskrypcje produktów firmy Microsoft. Możesz zmodyfikować ten **przykładowy kod** na własny użytek, aby skonfigurować [oferty,](#configure-offers)dodać znakowanie [i](#configure-branding)dodać formę [płatności.](#configure-payment-types)

## <a name="sample-code"></a>Przykładowy kod

Pobierz [przykładowy kod Partner Center storefront z](https://github.com/Microsoft/Partner-Center-Storefront) GitHub.

## <a name="configure-authentication"></a>Konfigurowanie uwierzytelniania

Przed skompilowanie aplikacji zaktualizuj następujące wartości w pliku Web.config, aby odzwierciedlić informacje uwierzytelniania usługi Azure AD utworzone w ramach [Partner Center uwierzytelniania.](partner-center-authentication.md) Ustawień konta piaskownicy integracji należy używać na wczesnym etapie opracowywania lub do testowania w środowisku produkcyjnym (TiP).

- **partnerCenter.applicationId**
- **partnerCenter.applicationSecret**
- **partnerCenter.domain**
- **webPortal.clientId**
- **webPortal.clientSecret**
- **webPortal.domain**
- **webPortal.azureStorageConnectionString**

## <a name="configure-offers"></a>Konfigurowanie ofert

Zestaw ofert **(MicrosoftOffer)** można skonfigurować w modelu **OfferCatalogViewModel.**

## <a name="configure-branding"></a>Konfigurowanie znakowania

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