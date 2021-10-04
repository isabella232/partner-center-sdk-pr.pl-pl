---
title: Zasoby subskrypcji
description: Zasoby subskrypcji mogą dostarczać dalsze informacje o subskrypcjach w całym cyklu życia, takie jak pomoc techniczna, zwroty kosztów, uprawnienia platformy Azure.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 461df9cdb909fc44be9069cb7eb4b41fa2a5f170
ms.sourcegitcommit: 3ee00d9fe9da6b9df0fb7027ae506e2abe722770
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/04/2021
ms.locfileid: "129417291"
---
# <a name="subscription-resources"></a>Zasoby subskrypcji

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Subskrypcja umożliwia klientowi korzystanie z usługi przez określony czas. Nie wszystkie pola będą stosowane do wszystkich subskrypcji. Wiele pól ma zastosowanie tylko w niektórych punktach cyklu życia, takich jak wstrzymanie lub anulowanie subskrypcji.

## <a name="subscription"></a>Subskrypcja

>[!NOTE]
>Zasób **subskrypcja** ma limit szybkości 500 żądań na minutę na identyfikator dzierżawy.

**Zasób** Subskrypcja reprezentuje cykl życia subskrypcji i zawiera właściwości, które definiują stany w całym cyklu życia subskrypcji.

| Właściwość             | Typ                                                          | Opis                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                                                        | Identyfikator subskrypcji.                                                                                                                                                  |
| offerId              | ciąg                                                        | Identyfikator oferty.                                                                                                                                                         |
| entitlementId        | ciąg                                                        | Identyfikator uprawnień (identyfikator subskrypcji platformy Azure).                                                                                                                        |
| nazwa_oferty            | ciąg                                                        | Nazwa oferty.                                                                                                                                                               |
| Friendlyname         | ciąg                                                        | Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu uujednoznania.                                                                                           |
| quantity             | liczba                                                        | Ilość. Na przykład w przypadku rozliczeń opartych na licencjach ta właściwość jest ustawiana na liczbę licencji.                                                            |
| Unittype             | ciąg                                                        | Jednostki definiujące ilość dla subskrypcji.                                                                                                                             |
| parentSubscriptionId | ciąg                                                        | Pobiera lub ustawia identyfikator subskrypcji nadrzędnej.                                                                                                                              |
| Creationdate         | ciąg                                                        | Pobiera lub ustawia datę utworzenia w formacie data/godzina.                                                                                                                          |
| effectiveStartDate   | ciąg w formacie daty i godzin UTC                                | Pobiera lub ustawia datę rozpoczęcia wejścia w życie dla tej subskrypcji w formacie data/godzina. Służy do datowania zmigrowanych subskrypcji lub do wyrównywania jej z inną.                |
| commitmentEndDate    | ciąg w formacie daty i godzin UTC                                | Data zakończenia zobowiązania dla tej subskrypcji w formacie data/godzina. W przypadku subskrypcji, które nie są automatycznieodnawialnych, oznacza to datę daleko w przyszłości.       |
| status               | ciąg                                                        | Stan subskrypcji: "none", "active", "pending", "suspended", "expired" lub "deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Pobiera wartość wskazującą, czy subskrypcja jest odnawiana automatycznie.                                                                                                    |
| typ rozliczeń          | ciąg                                                        | Określa sposób, w jaki subskrypcja jest rozliczana: "brak", "użycie" lub "licencja".                                                                                                      |
| billingCycle         | ciąg                                                        | Wskazuje częstotliwość, z jaką partner jest rozliczany za to zamówienie. Obsługiwane wartości to nazwy członków w [**typie BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Pobiera lub ustawia wartość wskazującą, czy subskrypcja ma dodatki do zakupu.                                                                                             |
| isTrial              | boolean                                                       | Wartość wskazująca, czy jest to subskrypcja wersji próbnej.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Wartość wskazująca, czy jest to produkt firmy Microsoft.                                                                                                                       |
| publisherName        | ciąg                                                        | Nazwa wydawcy.                                                                                                                                                           |
| akcje              | tablica ciągów                                              | Pobiera lub ustawia dozwolone akcje. Możliwe wartości: "edytuj", "anuluj"                                                                                                  |
| partnerId            | ciąg                                                        | Identyfikator MPN odsprzedawcy rekordu używany w modelu partnera pośredniego.                                                                                                     |
| suspensionReasons    | tablica ciągów                                              | Tylko do odczytu. Jeśli subskrypcja została wstrzymana, wskazuje przyczynę.                                                                                                                  |
| Contracttype         | ciąg                                                        | Tylko do odczytu. Typ kontraktu: "subscription", "productKey" lub "redemptionCode".                                                                                           |
| refundOptions        | tablica [zasobów RefundOption](#refundoption)   | Tylko do odczytu. Zestaw opcji zwrotu kosztów dostępnych dla tej subskrypcji.                                                                                              |
| Linki                | [SubscriptionLinks](#subscriptionlinks)                       | Pobiera lub ustawia linki subskrypcji.                                                                                                                                          |
| Idzamówienia              | ciąg                                                        | Identyfikator zamówienia, które zostało złożone w celu rozpoczęcia subskrypcji.                                                                                                                |
| termDuration         | ciąg                                                        | Reprezentacja iso 8601 czasu trwania terminu. Obecnie obsługiwane wartości to **P1M (1** miesiąc), **P1Y** (1 rok) **i P3Y** (3 lata).                                                        |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające subskrypcji.                                                                                                                    |
| renewalTermDuration  | ciąg                                                        | Reprezentacja iso 8601 czasu trwania terminu. Obecnie obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok).                                                        |
| Producttype  | [Itemtype](product-resources.md#itemtype)                             | Tylko do odczytu. Typ produktu, dla jakiego jest subskrypcja.     |
| consumptionType  | tablica [zasobów z przesłoniami](subscription-resources.md#overage)   | Pobiera lub ustawia nadgorę dla danego klienta.     |

## <a name="subscriptionlinks"></a>SubscriptionLinks

Zasób **SubscriptionLinks** opisuje kolekcję linków dołączonych do zasobu subskrypcji.

| Właściwość           | Typ                               | Opis                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Link](utility-resources.md#link) | Pobiera lub ustawia ofertę.               |
| parentSubscription | [Link](utility-resources.md#link) | Pobiera lub ustawia subskrypcję nadrzędną. |
| product            | [Link](utility-resources.md#link) | Pobiera produkt skojarzony z subskrypcją. |
| sku                | [Link](utility-resources.md#link) | Pobiera skojarzoną z subskrypcją sku produktu. |
| availability       | [Link](utility-resources.md#link) | Pobiera dostępność sku produktu skojarzoną z subskrypcją. |
| activationLinks    | [Link](utility-resources.md#link) | Pobiera listę linków aktywacji skojarzonych z subskrypcją. |
| Własny               | [Link](utility-resources.md#link) | Własny URI.                         |
| dalej               | [Link](utility-resources.md#link) | Następna strona elementów.               |
| Poprzednich           | [Link](utility-resources.md#link) | Poprzednia strona elementów.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

Zasób **SubscriptionProvisioningStatus** zawiera informacje o stanie aprowizowania subskrypcji.

| Właściwość   | Typ                                                           | Opis                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | ciąg                                                         | Ciąg w formacie IDENTYFIKATORA GUID, który identyfikuje sku produktu.             |
| status     | ciąg                                                         | Wskazuje stan aprowizowania: "powodzenie", "oczekiwanie" lub "niepowodzenie". |
| quantity   | liczba                                                         | Dostarcza ilość subskrypcji po aprowizeniu.               |
| Enddate    | ciąg w formacie daty i godzin UTC                                 | Data zakończenia subskrypcji.                                    |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

Zasób **SubscriptionRegistrationStatus** opisuje kolekcję linków dołączonych do zasobu subskrypcji.

| Właściwość           | Typ                               | Opis                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | ciąg                             | Identyfikator subskrypcji.                                                          |
| status             | ciąg                             | Wskazuje stan rejestracji: "registered", "registering" lub "notregistered".    |

## <a name="supportcontact"></a>SupportContact

Zasób **SupportContact** reprezentuje kontakt z pomocą techniczną dla subskrypcji klienta.

| Właściwość        | Typ                                                           | Opis                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | ciąg                                                         | Ciąg sformatowany za pomocą identyfikatora GUID, który wskazuje identyfikator dzierżawy kontaktu pomocy technicznej. |
| supportMpnId    | ciąg                                                         | Identyfikator Microsoft Partner Network (MPN).                       |
| name            | ciąg                                                         | Nazwa kontaktu pomocy technicznej.                                                |
| Linki           | [ResourceLinks](utility-resources.md#resourcelinks)            | Linki dotyczące kontaktu z pomocą techniczną.                                              |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych. Zawiera "objectType": " SupportContact".              |

## <a name="overage"></a>Nadwyżka

Zasób **overage** reprezentuje, do których można przypisać zasób użycia subskrypcji, niezależnie od tego, czy jest przypisany i przypisany odsprzedawca.

| Właściwość        | Typ               | Opis                                                                     |
|-----------------|--------------------|---------------------------------------------------------------------------------|
| azureEntitlementId | ciąg       | Ciąg w formacie IDENTYFIKATORA GUID, który wskazuje identyfikator subskrypcji zużycia. |
| partnerId    | ciąg            | Identyfikator Microsoft Partner Network (MPN) odsprzedawcy skojarzonego z subskrypcją.        |
| typ    | ciąg       | Typem nadanych usług może być "PhoneServices"       |
| Nadmiar            | boolean      | Wartość wskazująca, czy jest włączona nadgorę.       |
| Linki           | [ResourceLinks](utility-resources.md#resourcelinks)            | Linki związane z nadgorami.                          |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych. Zawiera "objectType": "Overage".  |



## <a name="registersubscription"></a>RegisterSubscription

Zasób **RegisterSubscription** zwraca link, który może służyć do wykonywania zapytań o stan rejestracji subskrypcji. Stan rejestracji jest zwracany w treści odpowiedzi pomyślnie zaakceptowanego żądania zarejestrowania subskrypcji platformy Azure.

| Właściwość                | Typ                               | Opis                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Zwraca kod stanu HTTP 202 "Accepted" z nagłówkiem Location zawierającym link do zapytania o stan rejestracji. Na przykład `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>Zwrot kosztów

Zasób **RefundOption** reprezentuje możliwą opcję zwrotu dla subskrypcji.

| Właściwość          | Typ | Opis                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| typ | ciąg | Typ zwrotu pieniędzy. Obsługiwane wartości to "Częściowe" i "Pełne" |
| expiresAfter      | ciąg w formacie daty i godzin UTC | Znacznik czasu, gdy ta opcja wygaśnie. Jeśli wartość null, oznacza to, że nie wygasa. |

## <a name="azureentitlement"></a>AzureEntitlement

Zasób **AzureEntitlement** reprezentuje uprawnienia platformy Azure dla subskrypcji.

| Właściwość          | Typ | Opis                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| identyfikator | ciąg | Identyfikator uprawnień |
| Friendlyname      | ciąg | Przyjazna nazwa uprawnienia. |
| status | ciąg | Stan uprawnień. |
| subscriptionId | ciąg | Identyfikator subskrypcji, do której należy uprawnienie. |
