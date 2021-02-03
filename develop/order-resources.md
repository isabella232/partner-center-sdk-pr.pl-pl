---
title: Zamów zasoby
description: Partner umieszcza zamówienie, gdy klient chce kupić subskrypcję z listy ofert.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9db07337a98214b4aaa93e2c8b43b84702249b77
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768029"
---
# <a name="order-resources"></a>Zamów zasoby

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Partner umieszcza zamówienie, gdy klient chce kupić subskrypcję z listy ofert.

>[!NOTE]
>Zasób zamówienia ma limit szybkości wynoszący 500 żądań na minutę na identyfikator dzierżawy.

## <a name="order"></a>Zamówienie

Opisuje zamówienie partnera.

| Właściwość           | Typ                                               | Opis                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| identyfikator                 | ciąg                                             | Identyfikator zamówienia, który jest dostarczany po pomyślnym utworzeniu zamówienia.                                   |
| alternateId        | ciąg                                             | Przyjazny identyfikator zamówienia.                                                                          |
|referenceCustomerId | ciąg                                             | Identyfikator klienta. |
| billingCycle       | ciąg                                             | Wskazuje częstotliwość, z jaką jest rozliczany partner dla tego zamówienia. Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [BillingCycleType](product-resources.md#billingcycletype). Wartość domyślna to "Monthly" lub "jednorazowej" podczas tworzenia kolejności. To pole jest stosowane po pomyślnym utworzeniu zamówienia. |
| transactionType    | ciąg                                             | Tylko do odczytu. Typ transakcji zamówienia. Obsługiwane wartości to "UserPurchase", "SystemPurchase" lub "SystemBilling" |
| lineItems          | Tablica zasobów [OrderLineItem](#orderlineitem) | Lista elementów oferty, do których klient kupuje, wraz z ilością.        |
| currencyCode       | ciąg                                             | Tylko do odczytu. Waluta użyta podczas umieszczania zamówienia. Stosowane po pomyślnym utworzeniu zamówienia.           |
| currencySymbol     | ciąg                                             | Tylko do odczytu. Symbol waluty skojarzony z kodem waluty. |
| creationDate       | datetime                                           | Tylko do odczytu. Data, w której zamówienie zostało utworzone, w formacie daty i godziny. Stosowane po pomyślnym utworzeniu zamówienia.                                   |
| status             | ciąg                                             | Tylko do odczytu. Stan zamówienia.  Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [**OrderStatus**](#orderstatus).        |
| linki              | [OrderLinks](utility-resources.md#resourcelinks)           | Linki do zasobów odpowiadające kolejności.            |
| atrybuty         | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające kolejności.       |

## <a name="orderlineitem"></a>OrderLineItem

Zamówienie zawiera listę elementów oferty, a każdy element jest reprezentowany jako OrderLineItem.

| Właściwość             | Typ                                      | Opis                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Każdy element wiersza w kolekcji pobiera unikatowy numer wiersza, licząc do wartości z przedziału od 0 do count-1.                                                                                                                                                 |
| offerId              | ciąg                                    | Identyfikator oferty.                                                                                                                                                                                                                       |
| subscriptionId       | ciąg                                    | Identyfikator subskrypcji.                                                                                                                                                                                                                |
| parentSubscriptionId | ciąg                                    | Opcjonalny. Identyfikator subskrypcji nadrzędnej w ofercie dodatku. Dotyczy tylko poprawki.                                                                                                                                                     |
| friendlyName         | ciąg                                    | Opcjonalny. Przyjazna nazwa dla subskrypcji zdefiniowanej przez partnera, która pomaga w odróżnieniu od siebie.                                                                                                                                              |
| quantity             | int                                       | Liczba licencji lub wystąpień.                                                                                                                                                                                |
| termDuration         | ciąg                                    | Reprezentacja ISO 8601 okresu ważności. Bieżące obsługiwane wartości to **P1M** (1 miesiąc), **P1Y** (1 rok) i **P3Y** (3 lata).                               |
| transactionType      | ciąg                                    | Tylko do odczytu. Typ transakcji elementu wiersza. Obsługiwane wartości to "New", "Renew", "addilooć", "removeQuantity", "Cancel", "Convert" i "customerCredit". |
| partnerIdOnRecord    | ciąg                                    | Gdy Dostawca pośredni umieści zamówienie w imieniu pośredniego odsprzedawcy, Wypełnij to pole IDENTYFIKATORem MPN **pośredniego odsprzedawcy** (nigdy nie jest identyfikatorem dostawcy pośredniego). Zapewnia to odpowiednie Księgowanie zachęt. |
| provisioningContext  | Ciąg<słownika, ciąg>            | Informacje wymagane do aprowizacji dla niektórych elementów w wykazie. Właściwość provisioningVariables w jednostce SKU wskazuje, które właściwości są wymagane dla określonych elementów w wykazie.                                                                                                                                               |
| linki                | [OrderLineItemLinks](#orderlineitemlinks) | Tylko do odczytu. Linki do zasobów odpowiadające elementowi wiersza zamówienia.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Szczegóły okresu ważności okresu odnawiania.                                                                           |

## <a name="renewsto"></a>RenewsTo

Przedstawia szczegóły okresu ważności okresu odnawiania.

| Właściwość              | Typ             | Wymagane        | Opis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | ciąg           | Nie              | Reprezentacja ISO 8601 okresu ważności. Bieżące obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok). |

## <a name="orderlinks"></a>OrderLinks

Reprezentuje linki do zasobów odpowiadające kolejności.

| Właściwość           | Typ                                         | Opis                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Łącze](utility-resources.md#link)            | Po wypełnieniu link umożliwiający pobranie stanu aprowizacji dla zamówienia.       |
| automatycznej               | [Łącze](utility-resources.md#link)            | Link umożliwiający pobranie zasobu zamówienia.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Reprezentuje pełną subskrypcję skojarzoną z kolejnością.

| Właściwość           | Typ                                         | Opis                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Łącze](utility-resources.md#link)            | Po wypełnieniu link umożliwiający pobranie [stanu aprowizacji](#orderlineitemprovisioningstatus) elementu wiersza.       |
| sku                | [Łącze](utility-resources.md#link)            | Link do pobierania informacji o jednostkach SKU dla elementu katalogu zakupiono.                    |
| subskrypcja       | [Łącze](utility-resources.md#link)            | Po wypełnieniu link do informacji o pełnej subskrypcji.                       |
| activationLinks    | [Łącze](utility-resources.md#link)            | Po wypełnieniu okna Pobierz zasób dla łączy, aby aktywować subskrypcję.             |

## <a name="orderstatus"></a>OrderStatus

[Enum/dotnet/API/System. enum) wartości wskazujące stan zamówienia.

| Wartość              | Położenie     | Opis                                     |
|--------------------|--------------|-------------------------------------------------|
| unknown            | 0            | Inicjator wyliczenia.                               |
| pełni          | 1            | Wskazuje, że zamówienie zostało zakończone.          |
| Oczekiwanie            | 2            | Wskazuje, że kolejność jest nadal w stanie oczekiwania.      |
| zerwan          | 3            | Wskazuje, że zamówienie zostało anulowane.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Reprezentuje stan aprowizacji elementu [OrderLineItem](#orderlineitem).

| Właściwość                        | Typ                                | Opis                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | Unikatowy numer wiersza elementu zamówienia. Wartości mieszczą się w zakresie od 0 do count-1.             |
| status                          | ciąg                              | Stan aprowizacji elementu wiersza zamówienia. Wartości są następujące:</br>"Zrealizowane": realizacja zamówienia zostanie zakończona pomyślnie, a użytkownik będzie mógł użyć rezerwacji</br>"Niezrealizowane": nie zrealizowano z powodu anulowania</br>"PrefulfillmentPending": Twoje żądanie jest nadal przetwarzane, realizacja nie została jeszcze ukończona |
| quantityProvisioningInformation | Lista<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | Lista informacji o stanie aprowizacji ilości dla elementu wiersza zamówienia. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Reprezentuje stan aprowizacji według liczby.

| Właściwość                           | Typ                                         | Opis                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Liczba elementów.                                 |
| status                             | ciąg                                       | Stan liczby elementów.                   |
