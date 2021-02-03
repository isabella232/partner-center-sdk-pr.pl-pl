---
title: Zasoby produktów
description: Zasoby, które reprezentują jednostek towary lub usługi. Obejmuje zasoby do opisywania typu produktu i kształtu (jednostki SKU) oraz sprawdzanie dostępności produktu w spisie.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a3cfacd3654e85a9824759295f97792ff740d85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768026"
---
# <a name="products-resources"></a>Zasoby produktów

**Dotyczy**

- Centrum partnerskie

Zasoby, które reprezentują jednostek towary lub usługi. Obejmuje zasoby do opisywania typu produktu i kształtu (jednostki SKU) oraz sprawdzanie dostępności produktu w spisie.

## <a name="product"></a>Produkt

Reprezentuje jednostek dobry lub Service. Produkt nie jest elementem jednostek.

| Właściwość           | Typ                          | Opis                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| identyfikator                 | ciąg                        | Identyfikator tego produktu.                                                 |
| tytuł              | ciąg                        | Nazwa produktu.                                                       |
| description (opis)        | ciąg                        | Opis produktu.                                                 |
| productType        | [ItemType](#itemtype)         | Obiekt, który opisuje kategoryzacje typów tego produktu.     |
| isMicrosoftProduct | bool                          | Wskazuje, czy jest to produkt firmy Microsoft.                          |
| publisherName      | ciąg                        | Nazwa wydawcy produktu, jeśli jest dostępna.                          |
| linki              | [ProductLinks](#productlinks) | Linki do zasobów zawarte w produkcie.                         |

## <a name="itemtype"></a>ItemType

Reprezentuje typ produktu.

| Właściwość        | Typ                          | Opis                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| identyfikator              | ciąg                        | Identyfikator typu.                                                                 |
| displayName     | ciąg                        | Nazwa wyświetlana dla tego typu.                                                      |
| Podtyp         | [ItemType](#itemtype)         | Opcjonalny. Obiekt, który opisuje kategoryzację podtypu dla tego typu elementu.     |

## <a name="productlinks"></a>ProductLinks

Zawiera listę linków dla [produktu](#product).

| Właściwość        | Typ                                                          | Opis                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| SKU            | [Łącze](utility-resources.md#link)                             | Link do uzyskiwania dostępu do podstawowych jednostek SKU.          |
| linki           | [ResourceLinks](utility-resources.md#resourcelinks)           | Linki zasobów zawarte w tym zasobie.   |

## <a name="sku"></a>SKU

Reprezentuje jednostkę magazynową (SKU) jednostek w ramach produktu. Reprezentują one różne kształty produktu.

| Właściwość               | Typ             | Opis                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| identyfikator                     | ciąg           | Identyfikator dla tej jednostki SKU. Ten identyfikator jest unikatowy tylko w kontekście jego produktu nadrzędnego. |
| tytuł                  | ciąg           | Tytuł jednostki SKU.                                                                 |
| description (opis)            | ciąg           | Opis jednostki SKU.                                                           |
| productId              | ciąg           | Identyfikator [produktu](#product) nadrzędnego, który zawiera tę jednostkę SKU.                      |
| minimumQuantity        | int              | Minimalna ilość dozwolona do zakupu.                                            |
| maximumQuantity        | int              | Maksymalna ilość dozwolona do zakupu.                                            |
| istrial                | bool             | Wskazuje, czy ta jednostka SKU jest elementem wersji próbnej.                                           |
| supportedBillingCycles | tablica ciągów | Lista obsługiwanych cykli rozliczeń dla tej jednostki SKU. Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [BillingCycleType](#billingcycletype). |
| purchasePrerequisites  | tablica ciągów | Lista wstępnie wymaganych kroków lub akcji, które są wymagane przed zakupem tego elementu. Obsługiwane są następujące wartości:<br/>  "InventoryCheck" — wskazuje, że spis elementu powinien być oceniany przed próbą zakupu tego elementu.<br/> "AzureSubscriptionRegistration" — wskazuje, że subskrypcja platformy Azure jest wymagana i musi być zarejestrowana przed podjęciem próby zakupienia tego elementu.  |
| inventoryVariables     | tablica ciągów | Lista zmiennych, które są konieczne do wykonania kontroli spisu dla tego elementu. Obsługiwane są następujące wartości:<br/> "CustomerId" — identyfikator klienta, dla którego będzie przeznaczony zakup.<br/> "AzureSubscriptionId" — Identyfikator subskrypcji platformy Azure, który będzie używany na potrzeby zakupu rezerwacji na platformie Azure.</br> "ArmRegionName" — region, dla którego ma zostać zweryfikowany spis. Ta wartość musi być zgodna z wartością "ArmRegionName" z DynamicAttributes jednostki SKU. |
| provisioningVariables  | tablica ciągów | Lista zmiennych, które muszą być dostępne w kontekście aprowizacji [elementu wiersza](cart-resources.md#cartlineitem) w przypadku zakupu tego elementu. Obsługiwane są następujące wartości:<br/> Zakres — zakres zakupu rezerwacji platformy Azure: "Single", "Shared".<br/> "Subskrypcji" — Identyfikator subskrypcji platformy Azure, który będzie używany na potrzeby zakupu rezerwacji na platformie Azure.<br/> "Czas trwania" — czas trwania rezerwacji platformy Azure: "1Year", "3Year".  |
| dynamicAttributes      | pary klucz/wartość  | Słownik właściwości dynamicznych, które są stosowane do tego elementu. Należy pamiętać, że właściwości w tym słowniku są dynamiczne i mogą ulec zmianie bez powiadomienia. Nie należy tworzyć silnych zależności dla określonych kluczy istniejących w wartości tej właściwości.    |
| linki                  | [ResourceLinks](utility-resources.md#resourcelinks) | Linki zasobów zawarte w jednostce SKU.                   |

## <a name="availability"></a>Dostępność

Reprezentuje konfigurację, w której jednostka SKU jest dostępna do zakupu (na przykład kraje, waluty i segment branżowy).

| Właściwość        | Typ                        | Opis                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| identyfikator              | ciąg                        | Identyfikator dla tej dostępności. Ten identyfikator jest unikatowy tylko w kontekście jego [produktu](#product) nadrzędnego i [jednostki SKU](#sku). **Uwaga** Ten identyfikator może ulec zmianie z upływem czasu. Należy polegać tylko na tej wartości w krótkim czasie po jej pobraniu.  |
| productId       | ciąg                        | Identyfikator [produktu](#product) , który zawiera tę dostępność.           |
| Identyfikatora skuId           | ciąg                        | Identyfikator [jednostki SKU](#sku) , która zawiera tę dostępność.                   |
| catalogItemId   | ciąg                        | Unikatowy identyfikator dla tego elementu w wykazie. Jest to identyfikator, który musi zostać wypełniony we właściwościach [OrderLineItem. OfferId](order-resources.md#orderlineitem) lub [CartLineItem. CatalogItemId](cart-resources.md#cartlineitem) podczas zakupu nadrzędnej [jednostki SKU](#sku). **Uwaga** Ten identyfikator może ulec zmianie z upływem czasu. Należy polegać tylko na tej wartości w krótkim czasie po jej pobraniu. Jest on dostępny tylko w momencie zakupu i jest używany.  |
| defaultCurrency | ciąg                        | Domyślna waluta obsługiwana dla tej dostępności.                               |
| segment         | ciąg                        | Segment branżowy dla tej dostępności. Obsługiwane wartości to: komercyjne, edukacyjne, rządowe, niedochodowe. |
| country         | ciąg                                              | Kraj lub region (w formacie kodu kraju ISO), w którym ma zastosowanie ta dostępność. |
| isPurchasable   | bool                                                | Wskazuje, czy ta dostępność jest jednostek. |
| isrenew     | bool                                                | Wskazuje, czy ta dostępność jest odnawiana. |
| product      | [Product](#product)               | Produkt, do którego odnosi się ta dostępność. |
| sku          | [Magazyn](#sku)            | Jednostka SKU, do której odnosi się ta dostępność. |
| odsetk           | Tablica zasobów [warunkowych](#term)  | Kolekcja warunków, które mają zastosowanie do tej dostępności. |
| linki           | [ResourceLinks](utility-resources.md#resourcelinks) | Linki do zasobów zawarte w dostępności. |

## <a name="term"></a>Termin

Reprezentuje termin, dla którego można zakupić dostępność.

| Właściwość              | Typ                                        | Opis                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| czas trwania              | ciąg                                      | Reprezentacja ISO 8601 okresu ważności. Bieżące obsługiwane wartości to P1M (1 miesiąc), P1Y (1 rok) i P3Y (3 lata). |
| description (opis)           | ciąg                                      | Opis warunku.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Reprezentuje żądanie sprawdzenia spisu dla niektórych elementów katalogu.

| Właściwość         | Typ                                                | Opis                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | Tablica [InventoryItem](#inventoryitem)            | Lista elementów wykazu, które zostaną obliczone przez sprawdzanie spisu.                           |
| inventoryContext | pary klucz/wartość                                     | Słownik wartości kontekstu, które są konieczne do przeprowadzenia kontroli spisu. Każda [jednostka SKU](#sku) produktów określi, które wartości (jeśli istnieją) są potrzebne do przeprowadzenia tej operacji.  |
| linki            | [ResourceLinks](utility-resources.md#resourcelinks) | Linki do zasobów zawarte w żądaniu sprawdzenia spisu.                            |

## <a name="inventoryitem"></a>InventoryItem

Reprezentuje pojedynczy element w operacji sprawdzania spisu. Ten zasób służy do określania elementów docelowych w żądaniu wejściowym i jest również używany do reprezentowania wyników operacji sprawdzania spisu.

| Właściwość         | Typ                                                              | Opis                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | ciąg                                                            | Potrzeb Identyfikator [produktu](#product).                            |
| Identyfikatora skuId            | ciąg                                                            | Identyfikator [jednostki SKU](#sku). Gdy ten zasób jest używany jako dane wejściowe do żądania spisu, ta wartość jest opcjonalna. Jeśli ta wartość nie zostanie podana, wszystkie jednostki SKU w ramach produktu będą traktowane jako elementy docelowe operacji sprawdzania spisu.      |
| z ograniczeniami     | bool                                                              | Wskazuje, czy ten element został znaleziony w spisie ograniczonym.            |
| dotyczących     | Tablica [InventoryRestriction](#inventoryrestriction)            | Szczegóły wszelkich ograniczeń znalezionych dla tego elementu. Ta właściwość zostanie wypełniona tylko wtedy, gdy **Isstricted** = "true". |

## <a name="inventoryrestriction"></a>InventoryRestriction

Reprezentuje szczegóły ograniczenia spisu. Ma to zastosowanie tylko w przypadku wyników kontroli spisu, a nie dla żądań wejściowych.

| Właściwość         | Typ                  | Opis                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | ciąg                | Kod, który identyfikuje przyczynę ograniczenia.                                    |
| description (opis)      | ciąg                | Opis ograniczenia spisu.                                               |
| properties       | pary klucz/wartość       | Słownik właściwości, który może dostarczyć dalsze szczegóły dotyczące ograniczenia.           |

## <a name="billingcycletype"></a>BillingCycleType

[Enum/dotnet/API/System. enum) z wartościami wskazującymi typ cyklu rozliczeniowego.

| Wartość              | Położenie     | Opis                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Nieznane            | 0            | Inicjator wyliczenia.                                                                          |
| Miesięcznie            | 1            | Oznacza, że partner zostanie obciążony miesięcznie.                                        |
| Roczna             | 2            | Wskazuje, że w przypadku partnera zostanie naliczona roczna opłata.                                       |
| Brak               | 3            | Wskazuje, że nie będzie naliczana opłata za partnera. Ta wartość może być używana w przypadku elementów wersji próbnej.    |
| Jednorazowej            | 4            | Oznacza, że partner zostanie obciążony jeden raz.                                       |
