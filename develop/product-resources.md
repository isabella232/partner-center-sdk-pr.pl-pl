---
title: Zasoby produktów
description: Zasoby reprezentujące towary lub usługi, które można kupować. Zawiera zasoby służące do opisywania typu i kształtu produktu (SKU) oraz sprawdzania dostępności produktu w spisie.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1d536cb78c070bd06f4ab9434e066e51fb4c008c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445888"
---
# <a name="products-resources"></a>Zasoby produktów

Zasoby reprezentujące towary lub usługi, które można kupować. Zawiera zasoby służące do opisywania typu i kształtu produktu (SKU) oraz sprawdzania dostępności produktu w spisie.

## <a name="product"></a>Produkt

Reprezentuje wartość dobrą lub usługę do zakupu. Sam produkt nie jest elementem do kupienia.

| Właściwość           | Typ                          | Opis                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| identyfikator                 | ciąg                        | Identyfikator tego produktu.                                                 |
| tytuł              | ciąg                        | Tytuł produktu.                                                       |
| description (opis)        | ciąg                        | Opis produktu.                                                 |
| productType        | [Itemtype](#itemtype)         | Obiekt opisujący kategoryzacje typów tego produktu.     |
| isMicrosoftProduct | bool                          | Wskazuje, czy jest to produkt firmy Microsoft.                          |
| publisherName      | ciąg                        | Nazwa wydawcy produktu, jeśli jest dostępna.                          |
| Linki              | [ProductLinks (Linki produktów)](#productlinks) | Linki zasobów zawarte w produkcie.                         |

## <a name="itemtype"></a>ItemType

Reprezentuje typ produktu.

| Właściwość        | Typ                          | Opis                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| identyfikator              | ciąg                        | Identyfikator typu.                                                                 |
| displayName     | ciąg                        | Nazwa wyświetlana dla tego typu.                                                      |
| Podtypu         | [Itemtype](#itemtype)         | Opcjonalny. Obiekt opisujący kategoryzację podtypu dla tego typu elementu.     |

## <a name="productlinks"></a>ProductLinks (Linki produktów)

Zawiera listę linków dla [produktu](#product).

| Właściwość        | Typ                                                          | Opis                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Sku            | [Link](utility-resources.md#link)                             | Link do uzyskiwania dostępu do bazowych jednostki SKU.          |
| Linki           | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki zasobów zawarte w tym zasobie.   |

## <a name="sku"></a>SKU

Reprezentuje zakupną jednostkę magazynową (SKU) w ramach produktu. Reprezentują one różne kształty produktu.

| Właściwość               | Typ             | Opis                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| identyfikator                     | ciąg           | Identyfikator tej sku. Ten identyfikator jest unikatowy tylko w kontekście jego produktu nadrzędnego. |
| tytuł                  | ciąg           | Tytuł sku.                                                                 |
| description (opis)            | ciąg           | Opis sku.                                                           |
| productId              | ciąg           | Identyfikator produktu [nadrzędnego, który](#product) zawiera tę jednostkę SKU.                      |
| minimumQuantity        | int              | Minimalna ilość dozwolona do zakupu.                                            |
| maximumQuantity        | int              | Maksymalna ilość dozwolona do zakupu.                                            |
| isTrial                | bool             | Wskazuje, czy ta wersja SKU jest elementem wersji próbnej.                                           |
| supportedBillingCycles | tablica ciągów | Lista obsługiwanych cykli rozliczeniowych dla tej sku. Obsługiwane wartości to nazwy członków w [typie BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | tablica ciągów | Lista czynności lub akcji wymaganych wstępnie przed zakupem tego elementu. Obsługiwane wartości to:<br/>  "InventoryCheck" — wskazuje, że spis elementu powinien zostać oceniony przed podjęciem próby zakupu tego elementu.<br/> "AzureSubscriptionRegistration" — wskazuje, że subskrypcja platformy Azure jest potrzebna i musi zostać zarejestrowana przed podjęciem próby zakupu tego elementu.  |
| inventoryVariables     | tablica ciągów | Lista zmiennych potrzebnych do wykonania sprawdzania spisu dla tego elementu. Obsługiwane wartości to:<br/> "CustomerId" — identyfikator klienta, dla których zakup będzie mieć identyfikator.<br/> "AzureSubscriptionId" — identyfikator subskrypcji platformy Azure, która będzie używana do zakupu rezerwacji platformy Azure.</br> "ArmRegionName" — region, dla którego ma być weryfikowany spis. Ta wartość musi być dopasowana do "ArmRegionName" z dynamicznegoattributes sku. |
| provisioningVariables  | tablica ciągów | Lista zmiennych, które muszą zostać podane w kontekście aprowowania elementu wiersza [koszyka](cart-resources.md#cartlineitem) podczas zakupu tego elementu. Obsługiwane wartości to:<br/> Zakres — zakres zakupu rezerwacji platformy Azure: "Pojedynczy", "Udostępniony".<br/> "SubscriptionId" — identyfikator subskrypcji platformy Azure, która będzie używana do zakupu rezerwacji platformy Azure.<br/> "Czas trwania" — czas trwania rezerwacji platformy Azure: "1Year", "3Year".  |
| dynamicAttributes      | pary klucz/wartość  | Słownik właściwości dynamicznych, które mają zastosowanie do tego elementu. Właściwości w tym słowniku są dynamiczne i mogą ulec zmianie bez powiadomienia. Nie należy tworzyć silnych zależności od określonych kluczy istniejących w wartości tej właściwości.    |
| Linki                  | [ResourceLinks](utility-resources.md#resourcelinks) | Linki zasobów zawarte w ramach tej sku.                   |

## <a name="availability"></a>Dostępność

Reprezentuje konfigurację, w której można kupić sku (na przykład kraj, waluta i segment branży).

| Właściwość        | Typ                        | Opis                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| identyfikator              | ciąg                        | Identyfikator tej dostępności. Ten identyfikator jest unikatowy tylko w kontekście jego produktu [nadrzędnego i](#product) [jednostki SKU](#sku). **Uwaga** Ten identyfikator może zmieniać się w czasie. Należy polegać na tej wartości tylko w krótkim czasie po jej pobierania.  |
| productId       | ciąg                        | Identyfikator [produktu, który](#product) zawiera tę dostępność.           |
| skuId           | ciąg                        | Identyfikator [sku, który](#sku) zawiera tę dostępność.                   |
| catalogItemId   | ciąg                        | Unikatowy identyfikator tego elementu w katalogu. Jest to identyfikator, który należy wypełnić we [właściwościach OrderLineItem.OfferId](order-resources.md#orderlineitem) lub [CartLineItem.CatalogItemId](cart-resources.md#cartlineitem) podczas zakupu nadrzędnej [jednostki SKU](#sku). **Uwaga** Ten identyfikator może zmieniać się w czasie. Należy polegać na tej wartości tylko w krótkim czasie po jej pobierania. Dostęp do niego powinien być uzyskiwany i używany tylko w momencie zakupu.  |
| defaultCurrency | ciąg                        | Domyślna waluta obsługiwana dla tej dostępności.                               |
| segment         | ciąg                        | Segment branży dla tej dostępności. Obsługiwane wartości to: Komercyjne, Edukacyjne, Rządowe, NonProfit. |
| country         | ciąg                                              | Kraj lub region (w formacie kodu kraju ISO), w którym ma zastosowanie ta dostępność. |
| isPurchasable   | bool                                                | Wskazuje, czy tę dostępność można kupować. |
| isRenewable     | bool                                                | Wskazuje, czy ta dostępność jest odnawializowa. |
| product      | [Product](#product)               | Produkt, który odpowiada tej dostępności. |
| sku          | [Numer jednostki magazynowej](#sku)            | Ta dostępność odpowiada tej dostępności. |
| Warunki           | tablica [zasobów term](#term)  | Kolekcja warunków mających zastosowanie do tej dostępności. |
| Linki           | [ResourceLinks](utility-resources.md#resourcelinks) | Linki zasobów zawarte w dostępności. |

## <a name="term"></a>Okres

Reprezentuje termin, dla którego można kupić dostępność.

| Właściwość              | Typ                                        | Opis                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| czas trwania              | ciąg                                      | Reprezentacja iso 8601 czasu trwania terminu. Obecnie obsługiwane wartości to P1M (1 miesiąc), P1Y (1 rok) i P3Y (3 lata). |
| description (opis)           | ciąg                                      | Opis terminu.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Reprezentuje żądanie sprawdzenia spisu niektórych elementów katalogu.

| Właściwość         | Typ                                                | Opis                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | tablica [elementów InventoryItem](#inventoryitem)            | Lista elementów katalogu, które zostaną ocenione podczas sprawdzania spisu.                           |
| inventoryContext | pary klucz/wartość                                     | Słownik wartości kontekstu, które są potrzebne do przeprowadzenia sprawdzania spisu. Każda [sku](#sku) produktów określi, które wartości (jeśli istnieją) są potrzebne do wykonania tej operacji.  |
| Linki            | [ResourceLinks](utility-resources.md#resourcelinks) | Linki zasobów zawarte w żądaniu sprawdzenia spisu.                            |

## <a name="inventoryitem"></a>InventoryItem

Reprezentuje pojedynczy element w operacji sprawdzania spisu. Ten zasób służy do określania elementów docelowych w żądaniu wejściowym i jest również używany do reprezentowania wyników wyjściowych operacji sprawdzania spisu.

| Właściwość         | Typ                                                              | Opis                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | ciąg                                                            | (Wymagane) Identyfikator [produktu](#product).                            |
| skuId            | ciąg                                                            | Identyfikator [SKU](#sku). W przypadku użycia tego zasobu jako danych wejściowych żądania spisu ta wartość jest opcjonalna. Jeśli ta wartość nie zostanie podany, wszystkie jednostki SKU w ramach produktu będą traktowane jako elementy docelowe operacji sprawdzania spisu.      |
| isRestricted     | bool                                                              | Wskazuje, czy znaleziono, że ten element ma ograniczony spis.            |
| Ograniczenia     | tablica [wartości InventoryRestriction](#inventoryrestriction)            | Szczegóły wszelkich ograniczeń znalezionych dla tego elementu. Ta właściwość zostanie wypełniona tylko wtedy, gdy **isRestricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Reprezentuje szczegóły ograniczenia spisu. Dotyczy to tylko wyników wyjściowych sprawdzania spisu, a nie żądań wejściowych.

| Właściwość         | Typ                  | Opis                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | ciąg                | Kod, który identyfikuje przyczynę ograniczenia.                                    |
| description (opis)      | ciąg                | Opis ograniczenia spisu.                                               |
| properties       | pary klucz/wartość       | Słownik właściwości, który może zawierać dalsze szczegóły dotyczące ograniczenia.           |

## <a name="billingcycletype"></a>BillingCycleType

Element [Enum/dotnet/api/system.enum) z wartościami wskazującymi typ cyklu rozliczeniowego.

| Wartość              | Położenie     | Opis                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Nieznane            | 0            | Inicjator wyliczania.                                                                          |
| Co miesiąc            | 1            | Wskazuje, że partner będzie obciążany comiesięczne opłaty.                                        |
| Roczna             | 2            | Wskazuje, że partnerowi będą naliczane opłaty rocznie.                                       |
| Brak               | 3            | Wskazuje, że partner nie zostanie obciążony. Ta wartość może być używana dla elementów wersji próbnej.    |
| OneTime            | 4            | Wskazuje, że partner zostanie obciążony raz.                                       |
