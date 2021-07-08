---
title: Zamawianie zasobów
description: Partner złozy zamówienie, gdy klient chce kupić subskrypcję z listy ofert.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c993317f288568dd687c3b52bf47e4520fcd18c6
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548060"
---
# <a name="order-resources"></a>Zamawianie zasobów

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Partner złozy zamówienie, gdy klient chce kupić subskrypcję z listy ofert.

>[!NOTE]
>Zasób Order ma limit szybkości 500 żądań na minutę na identyfikator dzierżawy.

## <a name="order"></a>Zamówienie

Opisuje zamówienie partnera.

| Właściwość           | Typ                                               | Opis                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| identyfikator                 | ciąg                                             | Identyfikator zamówienia podany po pomyślnym utworzeniu zamówienia.                                   |
| alternateId        | ciąg                                             | Przyjazny identyfikator zamówienia.                                                                          |
|referenceCustomerId | ciąg                                             | Identyfikator klienta. |
| billingCycle       | ciąg                                             | Wskazuje częstotliwość, z jaką partner jest rozliczany za to zamówienie. Obsługiwane wartości to nazwy członków w [typie BillingCycleType](product-resources.md#billingcycletype). Wartość domyślna to "Monthly" lub "OneTime" podczas tworzenia zamówienia. To pole jest stosowane po pomyślnym utworzeniu zamówienia. |
| Transactiontype    | ciąg                                             | Tylko do odczytu. Typ transakcji zamówienia. Obsługiwane wartości to "UserPurchase", "SystemPurchase" lub "SystemBilling" |
| lineItems          | tablica [zasobów OrderLineItem](#orderlineitem) | Lista ofert, które klient kupuje, wraz z ilością.        |
| currencyCode       | ciąg                                             | Tylko do odczytu. Waluta używana podczas składania zamówienia. Stosowane po pomyślnym utworzeniu zamówienia.           |
| currencySymbol     | ciąg                                             | Tylko do odczytu. Symbol waluty skojarzony z kodem waluty. |
| Creationdate       | datetime                                           | Tylko do odczytu. Data utworzenia zamówienia w formacie data/godzina. Stosowane po pomyślnym utworzeniu zamówienia.                                   |
| status             | ciąg                                             | Tylko do odczytu. Stan zamówienia.  Obsługiwane wartości to nazwy członków w [**orderstatus**](#orderstatus).        |
| Linki              | [OrderLinks](utility-resources.md#resourcelinks)           | Zasób łączy się z zamówieniem.            |
| atrybuty         | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające kolejności.       |

## <a name="orderlineitem"></a>OrderLineItem

Zamówienie zawiera listę ofert, a każdy element jest reprezentowany jako OrderLineItem.

| Właściwość             | Typ                                      | Opis                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Każdy element wiersza w kolekcji otrzymuje unikatowy numer wiersza, licząc od 0 do count-1.                                                                                                                                                 |
| offerId              | ciąg                                    | Identyfikator oferty.                                                                                                                                                                                                                       |
| subscriptionId       | ciąg                                    | Identyfikator subskrypcji.                                                                                                                                                                                                                |
| parentSubscriptionId | ciąg                                    | Opcjonalny. Identyfikator subskrypcji nadrzędnej w ofercie dodatku. Dotyczy tylko patch.                                                                                                                                                     |
| Friendlyname         | ciąg                                    | Opcjonalny. Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu uujednoznania.                                                                                                                                              |
| quantity             | int                                       | Liczba licencji lub wystąpień.                                                                                                                                                                                |
| termDuration         | ciąg                                    | Reprezentacja iso 8601 czasu trwania terminu. Obecnie obsługiwane wartości to **P1M (1** miesiąc), **P1Y** (1 rok) **i P3Y** (3 lata).                               |
| Transactiontype      | ciąg                                    | Tylko do odczytu. Typ transakcji elementu wiersza. Obsługiwane wartości to "new", "renew", "addQuantity", "removeQuantity", "cancel", "convert" lub "customerCredit". |
| partnerIdOnRecord    | ciąg                                    | Gdy dostawca pośredni złozy zamówienie w imieniu odsprzedawcy pośredniego, wypełnij to pole identyfikatorem MPN odsprzedawcy pośredniego **(nigdy** nie identyfikatorem dostawcy pośredniego). Zapewnia to odpowiednią ewidencjonowanie zachęt. |
| provisioningContext  | Słownik<ciąg, ciąg>            | Informacje wymagane do aprowizowania niektórych elementów w wykazie. Właściwość provisioningVariables w sku wskazuje, które właściwości są wymagane dla określonych elementów w wykazie.                                                                                                                                               |
| Linki                | [OrderLineItemLinks](#orderlineitemlinks) | Tylko do odczytu. Zasób łączy się z elementem wiersza zamówienia.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Szczegóły okresu odnowienia.                                                                           |

## <a name="renewsto"></a>RenewsTo

Reprezentuje szczegóły okresu odnowienia.

| Właściwość              | Typ             | Wymagane        | Opis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | ciąg           | Nie              | Reprezentacja iso 8601 czasu trwania okresu odnowienia. Obecnie obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok). |

## <a name="orderlinks"></a>OrderLinks

Reprezentuje linki zasobów odpowiadające kolejności.

| Właściwość           | Typ                                         | Opis                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Link](utility-resources.md#link)            | Po wypełniniu link do pobierania stanu aprowowania dla zamówienia.       |
| Własny               | [Link](utility-resources.md#link)            | Link do pobierania zasobu zamówienia.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Reprezentuje pełną subskrypcję skojarzoną z zamówieniem.

| Właściwość           | Typ                                         | Opis                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Link](utility-resources.md#link)            | Po wypełniniu link do pobierania stanu [aprowowania](#orderlineitemprovisioningstatus) elementu wiersza.       |
| sku                | [Link](utility-resources.md#link)            | Link do pobierania informacji o sku dla zakupionego elementu katalogu.                    |
| subskrypcja       | [Link](utility-resources.md#link)            | Po wypełniniu link do pełnych informacji o subskrypcji.                       |
| activationLinks    | [Link](utility-resources.md#link)            | Po wypełnieniu zasób GET zawiera linki służące do aktywowania subskrypcji.             |

## <a name="orderstatus"></a>OrderStatus

Element [Enum/dotnet/api/system.enum) z wartościami wskazującymi stan zamówienia.

| Wartość              | Położenie     | Opis                                     |
|--------------------|--------------|-------------------------------------------------|
| unknown            | 0            | Inicjator wyliczania.                               |
| Zakończone          | 1            | Wskazuje, że zamówienie jest ukończone.          |
| Oczekiwanie            | 2            | Wskazuje, że zamówienie jest nadal oczekujące.      |
| Anulowane          | 3            | Wskazuje, że zamówienie zostało anulowane.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Reprezentuje stan aprowizowania [orderLineItem](#orderlineitem).

| Właściwość                        | Typ                                | Opis                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | Unikatowy numer wiersza w wierszu zamówienia. Wartości od 0 do count-1.             |
| status                          | ciąg                              | Stan aprowizowania pozycji zamówienia. Wartości są następujące:</br>**Zrealizowane:** realizacja zamówienia została zakończona pomyślnie, a użytkownik będzie mógł korzystać z rezerwacji</br>**Niedopełnione:** niespełnienia z powodu anulowania</br>**PrefulfillmentPending:** Twoje żądanie jest nadal przetwarzane, realizacja nie została jeszcze ukończona |
| quantityProvisioningInformation | Lista<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | Lista informacji o stanie aprowizowania ilości dla pozycji zamówienia. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Reprezentuje stan aprowizowania według ilości.

| Właściwość                           | Typ                                         | Opis                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Liczba elementów.                                 |
| status                             | ciąg                                       | Stan liczby elementów.                   |
