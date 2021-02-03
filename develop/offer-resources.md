---
title: Zasoby oferty
description: Opisuje produkt wymieniony w wykazie odsprzedawców, który może zaoferować swoim klientom.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45af02705d2a03c7586ba6bf3a5537c3e4eec3c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767774"
---
# <a name="offer-resources"></a>Zasoby oferty

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Opisuje produkt wymieniony w wykazie odsprzedawców, który może zaoferować swoim klientom.

## <a name="offer"></a>Oferta

| Właściwość                    | Typ                      | Opis                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                          | ciąg                    | Identyfikator oferty.                                                                                           |
| name                        | ciąg                    | Nazwa oferty.                                                                                                 |
| description (opis)                 | ciąg                    | Opis oferty.                                                                                     |
| minimumQuantity             | int                       | Minimalna dostępna ilość.                                                                                 |
| maximumQuantity             | int                       | Maksymalna dostępna ilość.                                                                                 |
| rank                        | int                       | Ranga lub priorytet oferty w porównaniu z innymi kategoriami w tym samym wierszu produktu. Ta właściwość powinna być ustawiona tylko wtedy, gdy istnieje więcej niż jedna oferta dla danego wiersza produktu.  |
| adresu                         | ciąg                    | Identyfikator URI oferty.                                                                                                  |
| locale                      | ciąg                    | Ustawienia regionalne, których dotyczy oferta.                                                                          |
| country                     | ciąg                    | Kraj/region, w którym stosowana jest oferta.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Kategoria oferty.                                                                   |
| limitUnitOfMeasure          | ciąg                    | Wartość, która wskazuje typ ograniczenia zakupu. Możliwe wartości to:<br/> "Brak" — nie ma żadnych ograniczeń dotyczących liczby subskrypcji na podstawie zakupionej oferty.<br/> "Współbieżne" — liczba subskrypcji, które mogą istnieć w dzierżawie klienta w danym momencie obejmuje subskrypcje, które są aktywne lub anulowane. Ta wartość dotyczy głównie ofert małych firm, w których liczba licencji jest mniejsza niż 300. Provisionioned subskrypcje nie są liczone.<br/> "Okres istnienia" — liczba subskrypcji, które mogą istnieć w okresie istnienia dzierżawy klienta. Ta wartość jest najbardziej stosowana do wersji próbnych. Provisionioned subskrypcje nie są liczone.      |
| limit                       | int                       | Ilość subskrypcji, które mogą zostać zakupione w ramach tej oferty w oparciu o limitUnitOfMeasure.                |
| prerequisiteOffers          | ciąg                    | Oferty wymagań wstępnych.                                                                                        |
| isdodatek                     | boolean                   | Wartość wskazująca, czy to wystąpienie jest dodatkiem.                                                           |
| hasAddOns                   | boolean                   | Wartość wskazująca, czy ta oferta ma jakiekolwiek dodatki.                                                           |
| isAvailableForPurchase      | boolean                   | Wartość wskazująca, czy to wystąpienie jest dostępne do zakupu.                                             |
| billing                     | ciąg                    | Określa typ rozliczeń dla zakupu elementu wiersza: "none", "Usage" lub "License".                           |
| supportedBillingCycles      | tablica ciągów          | Wskazuje cykle rozliczeń obsługiwane dla tej oferty. Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | boolean                   | Wartość wskazująca, czy oferta jest automatycznie odnawiana.                                                      |
| upgradeTargetOffers         | tablica ciągów          | Lista ofert, do których można uaktualnić tę ofertę.                                                          |
| conversionTargetOffers      | tablica ciągów          | Lista ofert, do których można dokonać konwersji tej oferty.                                                         |
| reselleeQualifications      | tablica ciągów          | Kwalifikacje wymagane przez klienta w celu zakupienia oferty przez partnera.     |
| resellerQualifications      | tablica ciągów          | Kwalifikacje wymagane przez partnera w celu zakupienia oferty dla klienta.                       |
| salesGroupId                | ciąg                    | Ciąg służący do grupowania ofert w osobnych zamówieniach.                                                             |
| istrial                     | boolean                   | Wartość wskazująca, czy jest to oferta w wersji próbnej.                                                               |
| product                     | [OfferProduct](#offerproduct)           | Pobiera produkt oferty.                                                                           |
| unitType                    | ciąg                    | Typ jednostki.                                                                                      |
| linki                       | [OfferLinks](#offerlinks)               | Link "Dowiedz się więcej".                                                                    |
| atrybuty                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające ofercie.                         |

## <a name="offercategory"></a>OfferCategory

Opisuje kategoryzację oferty. Obejmuje to rangę lub priorytet tej kategorii oferty w porównaniu z innymi w tym samym wierszu produktu.

| Właściwość   | Typ                                                           | Opis                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator         | ciąg                                                         | Identyfikator kategorii.                                                                                                                                                   |
| name       | ciąg                                                         | Nazwa kategorii.                                                                                                                                                         |
| rank       | int                                                            | Ranga kategorii lub priorytet w porównaniu z innymi kategoriami w tej samej ofercie. Tę właściwość należy ustawić tylko wtedy, gdy istnieje więcej niż jedna kategoria oferty dla danej oferty. |
| locale     | ciąg                                                         | Ustawienia regionalne, których dotyczy oferta.                                                                                                                        |
| country    | ciąg                                                         | Kraj/region, w którym stosowana jest oferta.                                                                                                                   |
| linki      | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki do zasobów odpowiadające OfferCategory.                                                                                                                     |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające OfferCategory.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Zawiera linki do uczenia się więcej informacji o ofercie.

| Właściwość  | Typ | Opis                 |
|-----------|------|-----------------------------|
| learnMore | Łącze | Link "Dowiedz się więcej".      |
| automatycznej      | Łącze | Własny identyfikator URI                |
| dalej      | Łącze | Następna strona elementów.     |
| ubiegł  | Łącze | Poprzednia strona elementów. |

## <a name="offerproduct"></a>OfferProduct

Produkt lub usługa, która może mieć więcej niż jedną skojarzoną z nią ofertę, z różnymi zestawami funkcji i przeznaczonymi dla różnych potrzeb klientów.

| Właściwość | Typ   | Opis              |
|----------|--------|--------------------------|
| Id       | ciąg | Identyfikator kategorii. |
| Nazwa     | ciąg | Nazwa kategorii.       |
| Jednostka     | ciąg | Jednostka produktu.        |
