---
title: Zaoferuj zasoby
description: Opisuje produkt wymieniony w katalogu odsprzedawców, który może zaoferować swoim klientom.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 704e5580f2cdf84fc82b627e3b2ca165b81a3af5
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548111"
---
# <a name="offer-resources"></a>Zaoferuj zasoby

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Opisuje produkt wymieniony w katalogu odsprzedawców, który może zaoferować swoim klientom.

## <a name="offer"></a>Oferta

| Właściwość                    | Typ                      | Opis                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                          | ciąg                    | Identyfikator oferty.                                                                                           |
| name                        | ciąg                    | Nazwa oferty.                                                                                                 |
| description (opis)                 | ciąg                    | Opis oferty.                                                                                     |
| minimumQuantity             | int                       | Minimalna dostępna ilość.                                                                                 |
| maximumQuantity             | int                       | Maksymalna dostępna ilość.                                                                                 |
| rank                        | int                       | Ranga lub priorytet oferty w porównaniu z innymi kategoriami w tej samej linii produktu. Tę właściwość należy ustawić tylko wtedy, gdy istnieje więcej niż jedna oferta dla danej linii produktu.  |
| Identyfikator uri                         | ciąg                    | URI oferty.                                                                                                  |
| locale                      | ciąg                    | Locale, w których ma zastosowanie oferta.                                                                          |
| country                     | ciąg                    | Kraj/region, w którym ma zastosowanie oferta.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Kategoria oferty.                                                                   |
| limitUnitOfMeasure          | ciąg                    | Wartość wskazująca typ ograniczenia zakupu. Możliwe wartości to:<br/> "Brak" — nie ma żadnych ograniczeń dotyczących liczby subskrypcji na podstawie zakupionej oferty.<br/> "Współbieżne" — liczba subskrypcji, które mogą istnieć w dzierżawie klienta w danym momencie. Obejmuje to subskrypcje, które są aktywne lub anulowane. Ta wartość dotyczy głównie ofert dla małych firm, gdzie liczba licencji jest mniejsza niż 300. Subskrypcje, dla których anulowano aprowizację, nie są liczone.<br/> "LifeTime" — liczba subskrypcji, które mogą istnieć w okresie istnienia dzierżawy klienta. Ta wartość ma największe zastosowanie w przypadku wersji próbnych. Subskrypcje, dla których anulowano aprowizację, nie są liczone.      |
| limit                       | int                       | Liczba subskrypcji, które można kupić w ramach tej oferty, na podstawie wartości limitUnitOfMeasure.                |
| prerequisiteOffers          | ciąg                    | Oferty wymagań wstępnych.                                                                                        |
| isAddOn                     | boolean                   | Wartość wskazująca, czy to wystąpienie jest dodatkówem.                                                           |
| hasAddOns                   | boolean                   | Wartość wskazująca, czy ta oferta ma jakieś dodatki.                                                           |
| isAvailableForPurchase      | boolean                   | Wartość wskazująca, czy to wystąpienie jest dostępne do zakupu.                                             |
| billing                     | ciąg                    | Określa typ rozliczeń zakupu elementu wiersza: "brak", "użycie" lub "licencja".                           |
| supportedBillingCycles      | tablica ciągów          | Wskazuje cykle rozliczeniowe obsługiwane dla tej oferty. Obsługiwane wartości to nazwy członków w [typie BillingCycleType](product-resources.md#billingcycletype)   |
| isAutoRenewable             | boolean                   | Wartość wskazująca, czy oferta jest odnawiana automatycznie.                                                      |
| upgradeTargetOffers         | tablica ciągów          | Lista ofert, do których można uaktualnić tę ofertę.                                                          |
| conversionTargetOffers      | tablica ciągów          | Lista ofert, na które można przekonwertować tę ofertę.                                                         |
| reseleeQualifications      | tablica ciągów          | Kwalifikacje wymagane przez klienta, aby partner zakupił ofertę dla tego klienta.     |
| resellerQualifications      | tablica ciągów          | Kwalifikacje wymagane przez partnera do zakupu oferty dla klienta.                       |
| salesGroupId                | ciąg                    | Ciąg używany do grupowania ofert w oddzielne zamówienia.                                                             |
| isTrial                     | boolean                   | Wartość wskazująca, czy jest to oferta wersji próbnej.                                                               |
| product                     | [OfferProduct](#offerproduct)           | Pobiera produkt oferty.                                                                           |
| Unittype                    | ciąg                    | Typ jednostki.                                                                                      |
| Linki                       | [OfferLinks](#offerlinks)               | Link "Dowiedz się więcej" oferty.                                                                    |
| atrybuty                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające ofercie.                         |

## <a name="offercategory"></a>OfferCategory

Opisuje kategoryzację oferty. Obejmuje to rangę lub priorytet tej kategorii oferty w porównaniu z innymi w tej samej linii produktów.

| Właściwość   | Typ                                                           | Opis                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator         | ciąg                                                         | Identyfikator kategorii.                                                                                                                                                   |
| name       | ciąg                                                         | Nazwa kategorii.                                                                                                                                                         |
| rank       | int                                                            | Ranga kategorii lub priorytet w porównaniu z innymi kategoriami w tej samej ofercie. Tę właściwość należy ustawić tylko wtedy, gdy istnieje więcej niż jedna kategoria oferty dla danej oferty. |
| locale     | ciąg                                                         | Locale, w których ma zastosowanie oferta.                                                                                                                        |
| country    | ciąg                                                         | Kraj/region, w którym ma zastosowanie oferta.                                                                                                                   |
| Linki      | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki zasobów odpowiadające kategorii OfferCategory.                                                                                                                     |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające kategorii OfferCategory.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Zawiera linki do dodatkowych informacji o ofercie.

| Właściwość  | Typ | Opis                 |
|-----------|------|-----------------------------|
| learnWięcej | Link | Link "Dowiedz się więcej".      |
| Własny      | Link | Samodzielnego URI                |
| dalej      | Link | Następna strona elementów.     |
| Poprzednich  | Link | Poprzednia strona elementów. |

## <a name="offerproduct"></a>OfferProduct

Produkt lub usługa, które mogą mieć skojarzoną więcej niż jedną ofertę, z których każda ma różne zestawy funkcji i jest ukierunkowana na różne potrzeby klientów.

| Właściwość | Typ   | Opis              |
|----------|--------|--------------------------|
| Id       | ciąg | Identyfikator kategorii. |
| Nazwa     | ciąg | Nazwa kategorii.       |
| Jednostka     | ciąg | Jednostka produktu.        |
