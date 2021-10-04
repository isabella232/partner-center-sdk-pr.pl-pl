---
title: Zasoby subskrypcji
description: Zasoby subskrypcji mogą dostarczać dalsze informacje o subskrypcjach w całym cyklu życia, takie jak pomoc techniczna, zwroty kosztów, uprawnienia platformy Azure.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: e1b95165eeb335c5426df876cbade3190dd447ac
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/02/2021
ms.locfileid: "129378748"
---
# <a name="subscription-resources"></a>Zasoby subskrypcji

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Subskrypcja umożliwia klientowi korzystanie z usługi przez określony czas. Nie wszystkie pola będą stosowane do wszystkich subskrypcji. Wiele pól ma zastosowanie tylko w niektórych punktach cyklu życia, takich jak wstrzymanie lub anulowanie subskrypcji.

## <a name="subscription"></a>Subskrypcja

>[!NOTE]
>**Zasób** Subskrypcji ma limit szybkości 500 żądań na minutę na identyfikator dzierżawy.

**Zasób** Subskrypcja reprezentuje cykl życia subskrypcji i zawiera właściwości, które definiują stany w całym cyklu życia subskrypcji.

| Właściwość             | Typ                                                          | Opis                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                                                        | Identyfikator subskrypcji.                                                                                                                                                  |
| offerId              | ciąg                                                        | Identyfikator oferty.                                                                                                                                                         |
| entitlementId        | ciąg                                                        | Identyfikator uprawnień (identyfikator subskrypcji platformy Azure).                                                                                                                        |
| offerName (nazwa oferty)            | ciąg                                                        | Nazwa oferty.                                                                                                                                                               |
| Friendlyname         | ciąg                                                        | Przyjazna nazwa subskrypcji zdefiniowanej przez partnera w celu ujednoznacznienia.                                                                                           |
| quantity             | liczba                                                        | Ilość. Na przykład w przypadku rozliczeń opartych na licencjach ta właściwość jest ustawiana na liczbę licencji.                                                            |
| Unittype             | ciąg                                                        | Jednostki definiujące ilość dla subskrypcji.                                                                                                                             |
| parentSubscriptionId | ciąg                                                        | Pobiera lub ustawia identyfikator subskrypcji nadrzędnej.                                                                                                                              |
| Creationdate         | ciąg                                                        | Pobiera lub ustawia datę utworzenia w formacie daty i godzin.                                                                                                                          |
| effectiveStartDate   | ciąg w formacie daty i czasu UTC                                | Pobiera lub ustawia datę rozpoczęcia wejścia w życie dla tej subskrypcji w formacie data/godzina. Służy do zawrócenia zmigrowanych subskrypcji lub do wyrównania jej z inną.                |
| commitmentEndDate    | ciąg w formacie daty i czasu UTC                                | Data zakończenia zobowiązania dla tej subskrypcji w formacie data/godzina. W przypadku subskrypcji, które nie są automatycznieodnawialnych, reprezentuje datę daleko od przyszłości.       |
| status               | ciąg                                                        | Stan subskrypcji: "none", "active", "pending", "suspended", "expired" lub "deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Pobiera wartość wskazującą, czy subskrypcja jest odnawiana automatycznie.                                                                                                    |
| typ rozliczeń          | ciąg                                                        | Określa sposób na rachunku za subskrypcję: "brak", "użycie" lub "licencja".                                                                                                      |
| billingCycle         | ciąg                                                        | Wskazuje częstotliwość, za pomocą której partner jest rozliczany za to zamówienie. Obsługiwane wartości to nazwy członków w [**typie BillingCycleType**](product-resources.md#billingcycletype). |
| hasPurchasableAddons | boolean                                                       | Pobiera lub ustawia wartość wskazującą, czy subskrypcja ma dodatki do zakupu.                                                                                             |
| isTrial              | boolean                                                       | Wartość wskazująca, czy jest to subskrypcja wersji próbnej.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Wartość wskazująca, czy jest to produkt firmy Microsoft.                                                                                                                       |
| publisherName        | ciąg                                                        | Nazwa wydawcy.                                                                                                                                                           |
| akcje              | tablica ciągów                                              | Pobiera lub ustawia dozwolone akcje. Możliwe wartości: "edytuj", "anuluj"                                                                                                  |
| partnerId            | ciąg                                                        | Identyfikator MPN odsprzedawcy rekordu używany w modelu partnera pośredniego.                                                                                                     |
| suspensionReasons (elementy suspensionReason)    | tablica ciągów                                              | Tylko do odczytu. Jeśli subskrypcja została wstrzymana, wskazuje przyczynę.                                                                                                                  |
| Contracttype         | ciąg                                                        | Tylko do odczytu. Typ kontraktu: "subscription", "productKey" lub "redemptionCode".                                                                                           |
| refundOptions        | tablica [zasobów RefundOption](#refundoption)   | Tylko do odczytu. Zestaw opcji zwrotu kosztów dostępnych dla tej subskrypcji.                                                                                              |
| Linki                | [SubscriptionLinks](#subscriptionlinks)                       | Pobiera lub ustawia linki subskrypcji.                                                                                                                                          |
| Idzamówienia              | ciąg                                                        | Identyfikator zamówienia, które zostało złożone w celu rozpoczęcia subskrypcji.                                                                                                                |
| termDuration         | ciąg                                                        | Reprezentacja czasu trwania terminu w standardach ISO 8601. Obecnie obsługiwane wartości to **P1M (1** miesiąc), **P1Y** (1 rok) **i P3Y** (3 lata).                                                        |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych odpowiadające subskrypcji.                                                                                                                    |
| renewalTermDuration  | ciąg                                                        | Reprezentacja czasu trwania terminu w standardach ISO 8601. Obecnie obsługiwane wartości to **P1M** (1 miesiąc) i **P1Y** (1 rok).                                                        |
| Producttype  | [Itemtype](product-resources.md#itemtype)                             | Tylko do odczytu. Typ produktu, dla jakiego jest subskrybna.     |
| consumptionType  | tablica [zasobów nadanych](subscription-resources.md#overage)   | Pobiera lub ustawia nadgorę dla danego klienta.     |

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
| Własny               | [Link](utility-resources.md#link) | Samodzielnego URI.                         |
| dalej               | [Link](utility-resources.md#link) | Następna strona elementów.               |
| Poprzednich           | [Link](utility-resources.md#link) | Poprzednia strona elementów.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

Zasób **SubscriptionProvisioningStatus** zawiera informacje o stanie aprowizowania subskrypcji.

| Właściwość   | Typ                                                           | Opis                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | ciąg                                                         | Ciąg w formacie identyfikatora GUID, który identyfikuje sku produktu.             |
| status     | ciąg                                                         | Wskazuje stan aprowizowania: "powodzenie", "oczekiwanie" lub "niepowodzenie". |
| quantity   | liczba                                                         | Podaje ilość subskrypcji po aprowieniu.               |
| Enddate    | ciąg w formacie daty i czasu UTC                                 | Data zakończenia subskrypcji.                                    |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

Zasób **SubscriptionRegistrationStatus opisuje** kolekcję linków dołączonych do zasobu subskrypcji.

| Właściwość           | Typ                               | Opis                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | ciąg                             | Identyfikator subskrypcji.                                                          |
| status             | ciąg                             | Wskazuje stan rejestracji: "zarejestrowane", "zarejestrowane" lub "nierejestrowane".    |

## <a name="supportcontact"></a>SupportContact

Zasób **SupportContact** reprezentuje kontakt z pomocą techniczną dla subskrypcji klienta.

| Właściwość        | Typ                                                           | Opis                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | ciąg                                                         | Ciąg sformatowany za pomocą identyfikatora GUID, który wskazuje identyfikator dzierżawy kontaktu pomocy technicznej. |
| supportMpnId    | ciąg                                                         | Identyfikator Microsoft Partner Network (MPN) kontaktu.                       |
| name            | ciąg                                                         | Nazwa kontaktu pomocy technicznej.                                                |
| Linki           | [ResourceLinks](utility-resources.md#resourcelinks)            | Linki dotyczące kontaktu z pomocą techniczną.                                              |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych. Zawiera "objectType": " SupportContact".              |

## <a name="overage"></a>Nadwyżka

Zasób **opłat za** nadsieć reprezentuje, do których można przypisać zasób subskrypcji zużycia, niezależnie od tego, czy została przypisana i czy odsprzedawca jest przypisany.

| Właściwość        | Typ               | Opis                                                                     |
|-----------------|--------------------|---------------------------------------------------------------------------------|
| azureEntitlementId | ciąg       | Ciąg w formacie identyfikatora GUID, który wskazuje identyfikator subskrypcji zużycia. |
| partnerId    | ciąg            | Identyfikator Microsoft Partner Network (MPN) odsprzedawcy skojarzonego z subskrypcją.        |
| typ    | ciąg       | Typem nadanych usług może być "PhoneServices"       |
| Nadmiar            | boolean      | Wartość wskazująca, czy jest to subskrypcja wersji próbnej.       |
| Linki           | [ResourceLinks](utility-resources.md#resourcelinks)            | Linki dotyczące kontaktu z pomocą techniczną.                          |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych. Zawiera "objectType": "Overage".  |



## <a name="registersubscription"></a>RegisterSubscription

Zasób **RegisterSubscription** zwraca link, który może służyć do wykonywania zapytań o stan rejestracji subskrypcji. Stan rejestracji jest zwracany w treści odpowiedzi pomyślnie zaakceptowanego żądania rejestracji subskrypcji platformy Azure.

| Właściwość                | Typ                               | Opis                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Zwraca kod stanu HTTP 202 "Accepted" z nagłówkiem Location zawierającym link do zapytania o stan rejestracji. Na przykład `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>Zwrot kosztów

Zasób **RefundOption** reprezentuje możliwą opcję zwrotu dla subskrypcji.

| Właściwość          | Typ | Opis                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| typ | ciąg | Typ zwrotu pieniędzy. Obsługiwane wartości to "Partial" (Częściowe) i "Full" (Pełne). |
| expiresAfter      | ciąg w formacie daty i czasu UTC | Znacznik czasu, gdy ta opcja wygaśnie. Jeśli ma wartość null, oznacza to, że nie wygasa. |

## <a name="azureentitlement"></a>AzureEntitlement

Zasób **AzureEntitlement** reprezentuje uprawnienia platformy Azure dla subskrypcji.

| Właściwość          | Typ | Opis                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| identyfikator | ciąg | Identyfikator uprawnień |
| Friendlyname      | ciąg | Przyjazna nazwa uprawnienia. |
| status | ciąg | Stan uprawnienia. |
| subscriptionId | ciąg | Identyfikator subskrypcji, do której należy uprawnienie. |
