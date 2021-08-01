---
title: Zasoby koszyka
description: Partner umieszcza zamówienie w koszyku, gdy klient chce kupić subskrypcję z listy ofert.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ebe6e628d5bb3b66186d5c4f428f69e46415892b
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009154"
---
# <a name="cart-resources"></a>Zasoby koszyka

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Partner umieszcza zamówienie, gdy klient chce kupić subskrypcję z listy ofert.

## <a name="cart"></a>Koszyk

Opisuje koszyk.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.                               |
| creationTimeStamp     | DateTime         | Data utworzenia koszyka w formacie data/godzina. Stosowane po pomyślnym utworzeniu koszyka.      |
| lastModifiedTimeStamp | DateTime         | Data ostatniej aktualizacji koszyka w formacie daty i godziny. Stosowane po pomyślnym utworzeniu koszyka. |
| expirationTimeStamp   | DateTime         | Data wygaśnięcia koszyka w formacie data/godzina. Stosowane po pomyślnym utworzeniu koszyka.          |
| lastModifiedUser      | ciąg           | Użytkownik, który ostatnio zaktualizował koszyk. Stosowane po pomyślnym utworzeniu koszyka.                          |
| lineItems             | Tablica obiektów | Tablica [zasobów CartLineItem.](#cartlineitem)                                                   |
| status                | ciąg           | Stan koszyka. Możliwe wartości to "Aktywne" (można je zaktualizować/przesłać) i "Zamówione" (zostały już przesłane). |

## <a name="cartlineitem"></a>CartLineItem

Reprezentuje jeden element zawarty w koszyku.

| Właściwość             | Typ                             | Opis                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                           | Unikatowy identyfikator elementu wiersza koszyka. Stosowane po pomyślnym utworzeniu koszyka.                                                                   |
| catalogItemId        | ciąg                           | Identyfikator elementu katalogu.                                                                                                                          |
| Friendlyname         | ciąg                           | Opcjonalny. Przyjazna nazwa elementu zdefiniowanego przez partnera w celu uujednoznania.                                                                 |
| quantity             | int                              | Liczba licencji lub wystąpień.                                                                                                                  |
| currencyCode         | ciąg                           | Kod waluty.                                                                                                                                    |
| billingCycle         | Obiekt                           | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                                                                                 |
| termDuration         | ciąg                           | Reprezentacja czasu trwania terminu w standardach ISO 8601. Obecnie obsługiwane wartości to P1M (1 miesiąc), P1Y (1 rok) i P3Y (3 lata).                                |
| uczestnicy         | Lista par ciągów obiektów      | Kolekcja identyfikatorów PartnerId w rekordzie (identyfikator MPN) przy zakupie.                                                                                          |
| provisioningContext  | Ciąg<, ciąg>       | Dodatkowy kontekst używany podczas aprowizowania zakupionego elementu. Aby ustalić, które wartości są potrzebne dla określonego elementu, zapoznaj się z właściwością provisioningVariables dla tej usługi. |
| orderGroup           | ciąg                           | Grupa wskazująca, które elementy mogą być przesyłane razem w tej samej kolejności.                                                                          |
| addonItems           | Lista obiektów **CartLineItem** | Kolekcja elementów wiersza koszyka dla dodatków. Te elementy zostaną zakupione w ramach subskrypcji podstawowej, która jest skutkiem zakupu pozycji koszyka głównego. |
| error                | Obiekt                           | Zastosowane po utworzeniu koszyka w przypadku wystąpienia błędu.                                                                                                    |
| renewsTo             | Tablica obiektów                 | Tablica zasobów [RenewsTo.](#renewsto)                                                                            |
| AttestationAccepted             | bool                 | Wskazuje umowę na ofertę lub warunki dotyczące sku. Wymagane tylko w przypadku ofert lub jednostki SKU, gdzie SkuAttestationProperties lub OfferAttestationProperties wymuszaJednacja ma wartość True.                                                                            |

## <a name="renewsto"></a>RenewsTo

Reprezentuje jeden element zawarty w wierszu koszyka.

| Właściwość              | Typ             | Wymagane        | Opis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | ciąg           | Nie              | Reprezentacja czasu trwania okresu odnowienia w standardach ISO 8601. Obecnie obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok). |

### <a name="response-success-and-error-codes"></a>Kody powodzenia i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie, oraz dodatkowe informacje o debugowaniu. Użyj narzędzia śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [Partner Center kodów błędów](error-codes.md).

## <a name="carterror"></a>CartError

Reprezentuje błąd, który występuje po utworzeniu koszyka.

| Właściwość         | Typ                                   | Opis                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CareErrorCode](#carterrorcode) | Typ błędu koszyka.                                                                       |
| errorDescription | ciąg                                 | Opis błędu, w tym wszelkie uwagi dotyczące obsługiwanych wartości, wartości domyślnych lub limitów. |


## <a name="carterrorcode"></a>CartErrorCode

Typy błędów koszyka.

| Nazwa                             | ErrorCode   | Opis
|----------------------------------|-------------|-----------------------------------------------------------------------------------------------|
| CurrencyIsNotSupported           | 10 000   | Waluta nie jest obsługiwana dla danego rynku  |
| CatalogItemIdIsNotValid          | 10001   | Identyfikator elementu katalogu jest nieprawidłowy  |
| Limit przydziałuNotAvailable                | 10002   | Za mało dostępnego limitu przydziału  |
| InventoryNotAvailable            | 10003   | Spis nie jest dostępny dla wybranej oferty  |
| ParticipantsIsNotSupportedForPartner  | 10004   | Ustawianie uczestników nie jest obsługiwane w przypadku partnerów  |
| UnableToProcessCartLineItem      | 10006   | Nie można przetworzyć elementu wiersza koszyka.  |
| SubscriptionIsNotValid           | 10007   | Subskrypcja jest nieprawidłowy.  |
| SubscriptionIsNotEnabledForRI    | 10008   | Subskrypcja nie jest włączona dla zakupu RI.  |
| SandboxLimitExceeded             | 10009   | Przekroczono limit piaskownicy.  |
| InvalidInput                     | 10010   | Ogólne dane wejściowe są nieprawidłowe.  |
| SubscriptionNotRegistered        | 10011   | Subskrypcja jest nieprawidłowy.  |
| AttestationNotAccepted           | 10012   | Zaświadczenia nie zostały zaakceptowane.  |
| Nieznane                          | 0   | Wartość domyślna   |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Reprezentuje wynik wyewidencjonowania koszyka.

| Właściwość    | Typ                                              | Opis                     |
|-------------|---------------------------------------------------|---------------------------------|
| orders      | Lista [obiektów Order.](order-resources.md#order)         | Kolekcja zamówień.       |
| orderErrors | Lista [obiektów OrderError.](#ordererror) | Kolekcja błędów kolejności. |

## <a name="ordererror"></a>OrderError

Reprezentuje błąd, który występuje podczas finalizacji zakupu koszyka podczas tworzenia zamówienia.

| Właściwość     | Typ   | Opis                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | ciąg | Identyfikator grupy zamówień zamówienia z błędem. |
| kod         | int    | Kod błędu.                                 |
| description (opis)  | ciąg | Opis błędu.                   |
