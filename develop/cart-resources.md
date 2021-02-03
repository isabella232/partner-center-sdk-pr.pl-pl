---
title: Zasoby koszyka
description: Partner umieszcza zamówienie w koszyku, gdy klient chce kupić subskrypcję z listy ofert.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3aea428064654077ae67974132ec05918edfee65
ms.sourcegitcommit: a8fe6268fed2162843e7c92dca41c3919b25647d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/26/2020
ms.locfileid: "97768017"
---
# <a name="cart-resources"></a>Zasoby koszyka

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Partner umieszcza zamówienie, gdy klient chce kupić subskrypcję z listy ofert.

## <a name="cart"></a>Koszyk

Opisuje koszyk.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator koszyka, który jest dostarczany po pomyślnym utworzeniu koszyka.                               |
| creationTimeStamp     | DateTime         | Data i godzina utworzenia koszyka. Stosowane po pomyślnym utworzeniu koszyka.      |
| lastModifiedTimeStamp | DateTime         | Data ostatniej aktualizacji koszyka w formacie daty i godziny. Stosowane po pomyślnym utworzeniu koszyka. |
| expirationTimeStamp   | DateTime         | Data wygaśnięcia koszyka w formacie daty i godziny. Stosowane po pomyślnym utworzeniu koszyka.          |
| lastModifiedUser      | ciąg           | Użytkownik, który ostatnio zaktualizował koszyk. Stosowane po pomyślnym utworzeniu koszyka.                          |
| lineItems             | Tablica obiektów | Tablica zasobów [CartLineItem](#cartlineitem) .                                                   |
| status                | ciąg           | Stan koszyka. Możliwe wartości to "Active" (można je zaktualizować/przesłać) i "uporządkowane" (zostały już przesłane). |

## <a name="cartlineitem"></a>CartLineItem

Reprezentuje jeden element zawarty w koszyku.

| Właściwość             | Typ                             | Opis                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                           | Unikatowy identyfikator dla elementu w wierszu koszyka. Stosowane po pomyślnym utworzeniu koszyka.                                                                   |
| catalogItemId        | ciąg                           | Identyfikator elementu katalogu.                                                                                                                          |
| friendlyName         | ciąg                           | Opcjonalny. Przyjazna nazwa dla elementu zdefiniowanego przez partnera, która pomaga w odróżnieniu od siebie.                                                                 |
| quantity             | int                              | Liczba licencji lub wystąpień.                                                                                                                  |
| currencyCode         | ciąg                           | Kod waluty.                                                                                                                                    |
| billingCycle         | Obiekt                           | Typ cyklu rozliczeniowego ustawiony dla bieżącego okresu.                                                                                                 |
| termDuration         | ciąg                           | Reprezentacja ISO 8601 okresu ważności. Bieżące obsługiwane wartości to P1M (1 miesiąc), P1Y (1 rok) i P3Y (3 lata).                                |
| uczestnicy         | Lista par ciągów obiektów      | Kolekcja PartnerId on Record (MPNID) na zakupie.                                                                                          |
| provisioningContext  | Ciąg<słownika, ciąg>       | Dodatkowy kontekst używany podczas aprowizacji zakupionego elementu. Aby określić, które wartości są potrzebne dla określonego elementu, zapoznaj się z właściwością provisioningVariables jednostki SKU. |
| kolejność           | ciąg                           | Grupa wskazująca, które elementy mogą być przesyłane razem w tej samej kolejności.                                                                          |
| addonItems           | Lista obiektów **CartLineItem** | Kolekcja elementów wiersza koszyka dla dodatków. Te elementy zostaną zakupione na podstawie podstawowej subskrypcji, która wynika z zakupu elementu wiersza koszyka głównego. |
| error                | Obiekt                           | Zastosowano po utworzeniu koszyka w przypadku wystąpienia błędu.                                                                                                    |
| renewsTo             | Tablica obiektów                 | Tablica zasobów [RenewsTo](#renewsto) .                                                                            |

## <a name="renewsto"></a>RenewsTo

Reprezentuje jeden element zawarty w elemencie wiersza koszyka.

| Właściwość              | Typ             | Wymagane        | Opis |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | ciąg           | Nie              | Reprezentacja ISO 8601 okresu ważności. Bieżące obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok). |

### <a name="response-success-and-error-codes"></a>Kody sukcesu i błędów odpowiedzi

Każda odpowiedź zawiera kod stanu HTTP, który wskazuje powodzenie lub niepowodzenie i dodatkowe informacje debugowania. Użyj narzędzia do śledzenia sieci, aby odczytać ten kod, typ błędu i dodatkowe parametry. Aby uzyskać pełną listę, zobacz [kody błędów Centrum partnerskiego](error-codes.md).

## <a name="carterror"></a>CartError

Reprezentuje błąd występujący po utworzeniu koszyka.

| Właściwość         | Typ                                   | Opis                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [Kody błędów Centrum partnerskiego](error-codes.md) | Typ błędu koszyka.                                                                       |
| errorDescription | ciąg                                 | Opis błędu, w tym wszelkie uwagi dotyczące obsługiwanych wartości, wartości domyślnych lub limitów. |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Reprezentuje wynik wyewidencjonowania koszyka.

| Właściwość    | Typ                                              | Opis                     |
|-------------|---------------------------------------------------|---------------------------------|
| orders      | Lista obiektów [kolejności](order-resources.md#order) .         | Kolekcja zamówień.       |
| orderErrors | Lista obiektów [OrderError](#ordererror) . | Kolekcja błędów kolejności. |

## <a name="ordererror"></a>OrderError

Reprezentuje błąd występujący podczas wyewidencjonowania koszyka, gdy zamówienie zostanie utworzone.

| Właściwość     | Typ   | Opis                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | ciąg | Identyfikator grupy kolejności z błędem. |
| kod         | int    | Kod błędu.                                 |
| description (opis)  | ciąg | Opis błędu.                   |
