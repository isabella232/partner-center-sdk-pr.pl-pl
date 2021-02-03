---
title: Zasoby subskrypcji
description: Zasoby subskrypcji mogą zapewnić dodatkowe informacje o subskrypcjach w całym cyklu życia, takich jak pomoc techniczna, zwroty, uprawnienia platformy Azure.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd835e46e99b1fcb1e0b0e694ad73b1dca1240c9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767850"
---
# <a name="subscription-resources"></a>Zasoby subskrypcji

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Subskrypcja umożliwia klientowi korzystanie z usługi przez określony czas. Nie wszystkie pola zostaną zastosowane do wszystkich subskrypcji. Wiele pól ma zastosowanie tylko w określonych punktach cyklu życia, na przykład jeśli subskrypcja została zawieszona lub anulowana.

## <a name="subscription"></a>Subskrypcja

>[!NOTE]
>Zasób **subskrypcji** ma limit szybkości wynoszący 500 żądań na minutę na identyfikator dzierżawy.

Zasób **subskrypcji** reprezentuje cykl życia subskrypcji i zawiera właściwości, które definiują Stany w całym cyklu życia subskrypcji.

| Właściwość             | Typ                                                          | Opis                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                                                        | Identyfikator subskrypcji.                                                                                                                                                  |
| offerId              | ciąg                                                        | Identyfikator oferty.                                                                                                                                                         |
| entitlementId        | ciąg                                                        | Identyfikator uprawnienia (Identyfikator subskrypcji platformy Azure).                                                                                                                        |
| offerName            | ciąg                                                        | Nazwa oferty.                                                                                                                                                               |
| friendlyName         | ciąg                                                        | Przyjazna nazwa dla subskrypcji zdefiniowanej przez partnera, która pomaga w odróżnieniu od siebie.                                                                                           |
| quantity             | liczba                                                        | Ilość. Na przykład, w przypadku rozliczania opartego na licencji, ta właściwość jest ustawiona na wartość Liczba licencji.                                                            |
| unitType             | ciąg                                                        | Jednostki definiujące liczbę dla subskrypcji.                                                                                                                             |
| parentSubscriptionId | ciąg                                                        | Pobiera lub ustawia identyfikator subskrypcji nadrzędnej.                                                                                                                              |
| creationDate         | ciąg                                                        | Pobiera lub ustawia datę utworzenia w formacie daty i godziny.                                                                                                                          |
| effectiveStartDate   | ciąg w formacie daty i godziny czasu UTC                                | Pobiera lub ustawia obowiązującą datę początkową dla tej subskrypcji w formacie daty i godziny. Jest on używany do przywrócenia daty migracji subskrypcji lub dopasowania jej do innej.                |
| commitmentEndDate    | ciąg w formacie daty i godziny czasu UTC                                | Data zakończenia zobowiązania dla tej subskrypcji w formacie daty i godziny. W przypadku subskrypcji, które nie są autoodnawiane, oznacza to, że jest to data dotąd, daleko w przyszłość.       |
| status               | ciąg                                                        | Stan subskrypcji: "none", "Active", "Pending", "SUSPENDED" lub "deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Pobiera wartość wskazującą, czy subskrypcja jest odnawiana automatycznie.                                                                                                    |
| rozliczenia          | ciąg                                                        | Określa sposób rozliczania subskrypcji: "Brak", "użycie" lub "Licencja".                                                                                                      |
| billingCycle         | ciąg                                                        | Wskazuje częstotliwość, z jaką jest rozliczany partner dla tego zamówienia. Obsługiwane wartości to nazwy elementów członkowskich Znalezione w [**BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Pobiera lub ustawia wartość wskazującą, czy subskrypcja ma Dodatki jednostek.                                                                                             |
| istrial              | boolean                                                       | Wartość wskazująca, czy jest to subskrypcja wersji próbnej.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Wartość wskazująca, czy jest to produkt firmy Microsoft.                                                                                                                       |
| publisherName        | ciąg                                                        | Nazwa wydawcy.                                                                                                                                                           |
| akcje              | tablica ciągów                                              | Pobiera lub ustawia akcje, które są dozwolone. Możliwe wartości: "Edytuj", "Anuluj"                                                                                                  |
| partnerId            | ciąg                                                        | IDENTYFIKATOR MPN odsprzedawcy rekordu używany w modelu partnera pośredniego.                                                                                                     |
| suspensionReasons    | tablica ciągów                                              | Tylko do odczytu. Jeśli subskrypcja została zawieszona, wskazuje dlaczego.                                                                                                                  |
| element ContractType         | ciąg                                                        | Tylko do odczytu. Typ kontraktu: "Subscription", "productKey" lub "redemptionCode".                                                                                           |
| refundOptions        | Tablica zasobów [RefundOption](#refundoption)   | Tylko do odczytu. Zestaw opcji zwrotu dostępnych dla tej subskrypcji.                                                                                              |
| linki                | [SubscriptionLinks](#subscriptionlinks)                       | Pobiera lub ustawia linki subskrypcji.                                                                                                                                          |
| Wartooć              | ciąg                                                        | Identyfikator zamówienia, który został umieszczony w celu rozpoczęcia subskrypcji.                                                                                                                |
| termDuration         | ciąg                                                        | Reprezentacja ISO 8601 okresu ważności. Bieżące obsługiwane wartości to **P1M** (1 miesiąc), **P1Y** (1 rok) i **P3Y** (3 lata).                                                        |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające subskrypcji.                                                                                                                    |
| renewalTermDuration  | ciąg                                                        | Reprezentacja ISO 8601 okresu ważności. Bieżące obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

Zasób **SubscriptionLinks** opisuje kolekcję linków dołączonych do zasobu subskrypcji.

| Właściwość           | Typ                               | Opis                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Łącze](utility-resources.md#link) | Pobiera lub ustawia ofertę.               |
| parentSubscription | [Łącze](utility-resources.md#link) | Pobiera lub ustawia subskrypcję nadrzędną. |
| product            | [Łącze](utility-resources.md#link) | Pobiera produkt skojarzony z subskrypcją. |
| sku                | [Łącze](utility-resources.md#link) | Pobiera jednostkę SKU produktu skojarzoną z subskrypcją. |
| availability       | [Łącze](utility-resources.md#link) | Pobiera dostępność jednostki SKU produktu skojarzonej z subskrypcją. |
| activationLinks    | [Łącze](utility-resources.md#link) | Pobiera listę linków aktywacji skojarzonych z subskrypcją. |
| automatycznej               | [Łącze](utility-resources.md#link) | Własny identyfikator URI.                         |
| dalej               | [Łącze](utility-resources.md#link) | Następna strona elementów.               |
| ubiegł           | [Łącze](utility-resources.md#link) | Poprzednia strona elementów.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

Zasób **SubscriptionProvisioningStatus** zawiera informacje o stanie aprowizacji subskrypcji.

| Właściwość   | Typ                                                           | Opis                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| Identyfikatora skuId      | ciąg                                                         | Ciąg w formacie GUID, który identyfikuje jednostkę SKU produktu.             |
| status     | ciąg                                                         | Wskazuje stan aprowizacji: "powodzenie", "oczekiwanie" lub "Niepowodzenie". |
| quantity   | liczba                                                         | Zapewnia ilość subskrypcji po aprowizacji.               |
| endDate    | ciąg w formacie daty i godziny czasu UTC                                 | Data końcowa subskrypcji.                                    |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

Zasób **SubscriptionRegistrationStatus** opisuje kolekcję linków dołączonych do zasobu subskrypcji.

| Właściwość           | Typ                               | Opis                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | ciąg                             | Identyfikator subskrypcji.                                                          |
| status             | ciąg                             | Wskazuje stan rejestracji: "zarejestrowano", "Rejestrowanie" lub "notregistered".    |

## <a name="supportcontact"></a>SupportContact

Zasób **SupportContact** reprezentuje kontakt z pomocą techniczną dla subskrypcji klienta.

| Właściwość        | Typ                                                           | Opis                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | ciąg                                                         | Ciąg w formacie GUID, który wskazuje identyfikator dzierżawy kontaktu z pomocą techniczną. |
| supportMpnId    | ciąg                                                         | Identyfikator Microsoft Partner Network kontaktu (MPN).                       |
| name            | ciąg                                                         | Nazwa kontaktu z pomocą techniczną.                                                |
| linki           | [ResourceLinks](utility-resources.md#resourcelinks)            | Linki powiązane z kontaktem z pomocą techniczną.                                              |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych. Zawiera "objectType": "SupportContact".              |

## <a name="registersubscription"></a>RegisterSubscription

Zasób **RegisterSubscription** zwraca link, którego można użyć do zbadania stanu rejestracji subskrypcji. Stan rejestracji jest zwracany w treści odpowiedzi pomyślnie zaakceptowanego żądania zarejestrowania subskrypcji platformy Azure.

| Właściwość                | Typ                               | Opis                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Zwraca kod stanu HTTP 202 "zaakceptowane" z nagłówkiem lokalizacji zawierającym link umożliwiający utworzenie zapytania o stan rejestracji. Na przykład `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption

Zasób **RefundOption** reprezentuje możliwą opcję zwrotu dla subskrypcji.

| Właściwość          | Typ | Opis                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| typ | ciąg | Typ zwrotu. Obsługiwane wartości to "częściowe" i "Full". |
| expiresAfter      | ciąg w formacie daty i godziny czasu UTC | Sygnatura czasowa, gdy ta opcja wygasa. Jeśli wartość jest równa null, oznacza to, że nie ma ona wygaśnięcia. |

## <a name="azureentitlement"></a>AzureEntitlement

Zasób **AzureEntitlement** reprezentuje uprawnienia platformy Azure do subskrypcji.

| Właściwość          | Typ | Opis                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| identyfikator | ciąg | Identyfikator uprawnienia |
| friendlyName      | ciąg | Przyjazna nazwa uprawnienia. |
| status | ciąg | Stan uprawnienia. |
| subscriptionId | ciąg | Identyfikator subskrypcji, do której należy uprawnienie. |
