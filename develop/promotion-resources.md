---
title: Zasoby podyscytowe
description: Opisuje zasoby dotyczące promocji stosowanych do transakcji dla nowych subskrypcji handlowych.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 6a0b38576f5756a127fe6ba787f970db9ac59be3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715994"
---
# <a name="promotions-resources"></a>Zasoby promocji

**Dotyczy**

- Centrum partnerskie

**Odpowiednie role**

- Administrator globalny
- Agent administracyjny

> [!Note] 
> Nowe zmiany handlowe są obecnie dostępne tylko dla partnerów, którzy są częścią nowego Microsoft 365 i dynamics 365 w wersji Technical Preview.

Opisuje zasoby dotyczące promocji stosowanych do transakcji dla nowych subskrypcji handlowych.

## <a name="promotion"></a>Promocja

Rabat stosowany podczas zakupu sku produktu, jeśli są spełnione kryteria kwalifikowalności.

| Właściwość          | Typ                    | Opis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| identyfikator | ciąg                  | Identyfikator promocji. |
| name | ciąg                  | Przyjazna nazwa promocji. |
| description (opis) | ciąg                  | Opis promocji. |
| Startdate | ciąg | Data rozpoczęcia promocji. |
| Enddate | ciąg  | Data zakończenia promocji. |
| requiredProducts (wymaganeprodukty) | lista wymaganych produktów | Produkt, szczegóły dotyczące sku i zasady cenowe, których dotyczy promocja. | 
| properties | lista właściwości | Właściwości podwyrównania, w tym informacje o tym, czy promocja ma zastosowanie automatycznie. | 

## <a name="requiredproducts"></a>RequiredProducts (Wymaganeprodukty)

Produkt, szczegóły dotyczące sku i zasady cenowe, których dotyczy promocja.

| Właściwość          | Typ                    | Opis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| productId| ciąg | Dostępny jest identyfikator produktu, dla których jest dostępna poddana promocji. |
| skuId | ciąg | Dostępny jest identyfikator jednostki SKU, dla których jest poddana promocji. |
| Termin | Okres | Dostępny jest okres obejmujący okres i cykl rozliczeniowy, dla których jest dostępna poddana promocji. |
| pricingPolicies| Lista pricingPolicies | Lista zasad, które definiują typy i wartości rabatów na promocję. |

## <a name="term"></a>Okres

Reprezentuje termin, dla którego można kupić promocję.

| Właściwość          | Typ                    | Opis                                                                                  |
|-------------------|-------------------------|----------------------------------------------------------------------------------------------|
| czas trwania          | ciąg                  | Reprezentacja czasu trwania terminu w standardach ISO 8601. Obecnie obsługiwane wartości to P1M (jeden miesiąc), P1Y (jeden rok) i P3Y (trzy lata). 
| billingCycle      | ciąg | Opisuje częstotliwość stosowania promocji do rozliczeń. Mogą to być wartości miesięczne, roczne, onetime lub nieznane. | 

## <a name="pricingpolicies"></a>PricingPolicies

Opis typów i wartości rabatów na promocję.

| Właściwość          | Typ               | Opis                                                                  |          
|-------------------|--------------------|------------------------------------------------------------------------------|
| typ | ciąg | Opisz, czy rabat jest oparty na wartościach procentowych, czy z rabatami z stawkę płaską. |
| wartość | ciąg  | Definiuje kwotę zastosowanego rabatu. |

## <a name="properties"></a>Właściwości

Właściwości poddaną promocji.

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| isAutoApplicable  | bool  | Wskazuje, czy promocja jest stosowana automatycznie, czy musi zostać przekazana przez partnera. |


## <a name="promotioneligibilitiesrequestitem"></a>PromotionEligibilitiesRequestItem

Właściwości reprezentujące transakcję i uprawnienia do promocji.

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| identyfikator | int| Identyfikator elementu uprawnień do promocji. |
| catalogItemId | ciąg | Identyfikator elementu katalogu, do których zostanie zastosowane podszycie. Obejmuje identyfikator produktu, identyfikator SKU i identyfikator dostępności. |
| quantity | int | Liczba licencji lub wystąpień. |
| termDuration | ciąg | Reprezentacja czasu trwania terminu w standardach ISO 8601. Obecnie obsługiwane wartości to P1M (jeden miesiąc), P1Y (jeden rok) i P3Y (trzy lata). |
| billingCycle | ciąg | Opisuje częstotliwość stosowania promocji do rozliczeń. Mogą to być wartości miesięczne, roczne, onetime lub nieznane. | 
| promotionID | ciąg | Identyfikator promocji. |

## <a name="promotioneligibilities"></a>Uprawnienia do promocji

Lista produktów, jednostki SKU i ich uprawnień do promocji.

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| identyfikator | int| Identyfikator elementu uprawnień do promocji. |
| catalogItemId | ciąg | Identyfikator elementu katalogu, do których zostanie zastosowane podszycie. Obejmuje identyfikator produktu, identyfikator SKU i identyfikator dostępności. |
| quantity | int | Liczba licencji lub wystąpień. |
| termDuration | ciąg | Reprezentacja czasu trwania terminu w standardach ISO 8601. Obecnie obsługiwane wartości to P1M (jeden miesiąc), P1Y (jeden rok) i P3Y (trzy lata). |
| billingCycle | ciąg | Opisuje częstotliwość stosowania promocji do rozliczeń. Mogą to być wartości miesięczne, roczne, onetime lub nieznane. | 
| uprawnienia | Lista uprawnień do promocji | Reprezentuje listę wyników uprawnień do promocji. |

## <a name="promotioneligibility"></a>Uprawnienia do poddania promocji

Lista produktów, jednostki SKU i ich uprawnień do promocji.

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| promotionId | ciąg | Identyfikator promocji. |
| isEligible | bool | Opisuje, czy promocja kwalifikuje się do danego elementu żądania uprawnień. |
| błędy | Lista elementów PromotionEligibilityErrors | Błędy opisujące, dlaczego element żądania uprawnień do promocji nie kwalifikuje się. | 

## <a name="promotioneligibilityerror"></a>PromotionEligibilityError

Wyjaśnia, dlaczego element żądania uprawnień do promocji nie kwalifikuje się. 

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| typ | ciąg | Typy błędów uprawnień do promocji mogą obejmować InvalidCatalogItemId, InvalidPromotion, PrerequisiteProductOwnership, RedemptionLimit, SeatCount, OfferPurchasedPreviously lub Term. |
| description (opis) | ciąg | Opisuje, czy promocja kwalifikuje się do danego elementu żądania uprawnień. |

## <a name="redemptionlimitpromotioneligibilityerror"></a>RedemptionLimitPromotionEligibilityError

Zawiera szczegółowe informacje o tym, dlaczego przekroczono limit wykupu.

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| maxPromotionRedemptionCount | int | Maksymalna liczba, która może zostać uzyskana w ramach promocji. |
| remainingPromotionRedemptionCount| int | Pozostała liczba, która może zostać uzyskana w ramach promocji. |

## <a name="seatcountpromotioneligibilityerror"></a>SeatCountPromotionEligibilityError

Zawiera szczegółowe informacje o tym, dlaczego przekroczono limit liczby miejsc. Obie wartości mogą dopuszczać wartość null.

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| minimumRequiredSeats | Int? | Minimalna liczba licencji, które będzie wspierana w ramach promocji. |
| maximumRequiredSeats | Int? | Maksymalna liczba licencji, które będą zapewniane w ramach promocji. |

## <a name="termpromotioneligibilityerror"></a>TermPromotionEligibilityError

Zawiera szczegółowe informacje o tym, dlaczego okres promocji nie został zaakceptowany.

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| eligibleTerms | PromotionTerm | Warunki kwalifikujące się do promocji będą objęte wsparciem. |

## <a name="promotionterm"></a>PromotionTerm

Zawiera szczegółowe informacje o tym, dlaczego przekroczono limit liczby miejsc.

| Właściwość          | Typ               | Opis                                        |
|-------------------|--------------------|----------------------------------------------------|
| billingCycle | ciąg | Opisuje częstotliwość stosowania promocji do rozliczeń. Mogą to być wartości miesięczne, roczne, onetime lub nieznane. |
| czas trwania | ciąg | Czas trwania zakupionego okresu. |




