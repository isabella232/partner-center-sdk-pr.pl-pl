---
title: Zdarzenia elementu webhook Centrum partnerskiego
description: Dokumentacja wszystkich zdarzeń elementu webhook obsługiwanych przez centrum partnerskie.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 5358aab8efdd68ad52c583936304f99ffae12708
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768041"
---
# <a name="partner-center-webhook-events"></a>Zdarzenia elementu webhook Centrum partnerskiego

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Zdarzenia dotyczące elementów webhook Centrum partnerskiego to zdarzenia zmiany zasobów dostarczone w formie wpisów HTTP do zarejestrowanego adresu URL. Aby odebrać zdarzenie z Centrum partnerskiego, możesz hostować wywołanie zwrotne, gdzie centrum partnerskie może ogłosić zdarzenie. Zdarzenie jest podpisane cyfrowo, aby można było sprawdzić, czy zostało wysłane z Centrum partnerskiego.

Aby uzyskać informacje na temat sposobu odbierania zdarzeń, uwierzytelniania wywołania zwrotnego i używania interfejsów API elementu webhook Centrum partnerskiego do tworzenia, przeglądania i aktualizowania rejestracji zdarzeń, zobacz elementy [webhook Centrum partnerskiego](partner-center-webhooks.md).

## <a name="supported-events"></a>Obsługiwane zdarzenia

Centrum partnerskie obsługuje następujące zdarzenia elementu webhook.

### <a name="test-event"></a>Zdarzenie testowe

To zdarzenie umożliwia samodzielne dołączanie i testowanie rejestracji przez zażądanie zdarzenia testowego, a następnie śledzenie jego postępu. Podczas próby dostarczenia zdarzenia będą widoczne komunikaty o błędach, które są otrzymywane od firmy Microsoft. Dotyczy to tylko zdarzeń "utworzony test" i danych starszych niż 7 dni zostanie przeczyszczona.

>[!NOTE]
>W przypadku publikowania zdarzenia utworzonego testowego istnieje limit ograniczający wynoszący 2 żądania na minutę.

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W formularzu {Resource} — {Action}. Dla tego zdarzenia wartość to "test-created".                                          |
| ResourceUri               | URI                                | Identyfikator URI, w którym ma zostać pobrany zasób. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/V1/Registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | ciąg                             | Nazwa zasobu, który będzie wyzwalać zdarzenie. Dla tego zdarzenia wartością jest "test".                                  |
| AuditUri                  | URI                                | Obowiązkowe Identyfikator URI do pobrania rekordu inspekcji, jeśli istnieje. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/V1/AuditRecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i godziny UTC | Data i godzina wystąpienia zmiany zasobu.                                                         |

#### <a name="example"></a>Przykład

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="subscription-updated-event"></a>Zdarzenie zaktualizowane subskrypcji

To zdarzenie jest zgłaszane, gdy zostanie zmieniona określona subskrypcja. Zdarzenie zaktualizowane subskrypcji jest generowane, gdy istnieje zmiana wewnętrzna poza wprowadzeniem zmian za pomocą interfejsu API Centrum partnerskiego.  To zdarzenie zostanie wygenerowane tylko w przypadku zmiany poziomu handlu, na przykład w przypadku zmodyfikowania liczby licencji i zmiany stanu subskrypcji. Nie zostanie on wygenerowany podczas tworzenia zasobów w ramach subskrypcji.

>[!NOTE]
>Istnieje opóźnienie do 48 godzin między zmianą subskrypcji i wyzwoleniem zdarzenia zaktualizowanej subskrypcji.

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W formularzu {Resource} — {Action}. Dla tego zdarzenia wartością jest "subskrypcja została zaktualizowana".                                  |
| ResourceUri               | URI                                | Identyfikator URI, w którym ma zostać pobrany zasób. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/V1/Customers/{{CustomerID}}/subscriptions/{{SubscriptionID}}" |
| ResourceName              | ciąg                             | Nazwa zasobu, który będzie wyzwalać zdarzenie. Dla tego zdarzenia wartością jest "subskrypcja".                          |
| AuditUri                  | URI                                | Obowiązkowe Identyfikator URI do pobrania rekordu inspekcji, jeśli istnieje. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/V1/AuditRecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i godziny UTC | Data i godzina wystąpienia zmiany zasobu.                                                         |

#### <a name="example"></a>Przykład

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="threshold-exceeded-event"></a>Zdarzenie przekroczenia progu

To zdarzenie jest zgłaszane, gdy wielkość Microsoft Azure użycia dla każdego klienta przekroczy budżet wydatków użytkowania (ich próg). Aby uzyskać więcej informacji, zobacz [Ustawianie budżetu wydatków platformy Azure dla klientów/partnerów-Center/Set-a-Azure-wydatków-budżet-dla klientów).

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W formularzu {Resource} — {Action}. Dla tego zdarzenia wartością jest "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | URI                                | Identyfikator URI, w którym ma zostać pobrany zasób. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/V1/Customers/usagerecords" |
| ResourceName              | ciąg                             | Nazwa zasobu, który będzie wyzwalać zdarzenie. Dla tego zdarzenia wartością jest "usagerecords".                          |
| AuditUri                  | URI                                | Obowiązkowe Identyfikator URI do pobrania rekordu inspekcji, jeśli istnieje. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/V1/AuditRecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i godziny UTC | Data i godzina wystąpienia zmiany zasobu.                                                         |

#### <a name="example"></a>Przykład

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>Zdarzenie utworzenia odwołania

To zdarzenie jest zgłaszane po utworzeniu odwołania.

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W formularzu {Resource} — {Action}. Dla tego zdarzenia wartością jest "utworzono odwołanie".                                  |
| ResourceUri               | URI                                | Identyfikator URI, w którym ma zostać pobrany zasób. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/Engagements/V1/Referrals/{{ReferralID}}" |
| ResourceName              | ciąg                             | Nazwa zasobu, który będzie wyzwalać zdarzenie. Dla tego zdarzenia wartością jest "odwołanie".                          |
| AuditUri                  | URI                                | Obowiązkowe Identyfikator URI do pobrania rekordu inspekcji, jeśli istnieje. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/V1/AuditRecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i godziny UTC | Data i godzina wystąpienia zmiany zasobu.                                                         |

#### <a name="example"></a>Przykład

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>Zdarzenie zaktualizowane odwołania

To zdarzenie jest zgłaszane, gdy odwołanie zostanie zaktualizowane.

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W formularzu {Resource} — {Action}. Dla tego zdarzenia wartością jest "odwołanie-zaktualizowane".                                  |
| ResourceUri               | URI                                | Identyfikator URI, w którym ma zostać pobrany zasób. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/Engagements/V1/Referrals/{{ReferralID}}" |
| ResourceName              | ciąg                             | Nazwa zasobu, który będzie wyzwalać zdarzenie. Dla tego zdarzenia wartością jest "odwołanie".                          |
| AuditUri                  | URI                                | Obowiązkowe Identyfikator URI do pobrania rekordu inspekcji, jeśli istnieje. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/V1/AuditRecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i godziny UTC | Data i godzina wystąpienia zmiany zasobu.                                                         |

#### <a name="example"></a>Przykład

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>Wydarzenie gotowe do fakturowania

To zdarzenie jest zgłaszane w przypadku gotowości nowej faktury.

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | ciąg | Nazwa zdarzenia. W formularzu {Resource} — {Action}. Dla tego zdarzenia wartością jest "faktura-gotowa". |
| ResourceUri | URI | Identyfikator URI, w którym ma zostać pobrany zasób. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/V1/Invoices/{{InvoiceId}}" |
| ResourceName | ciąg | Nazwa zasobu, który będzie wyzwalać zdarzenie. Dla tego zdarzenia wartością jest "Invoice". |
| AuditUri |  URI | Obowiązkowe Identyfikator URI do pobrania rekordu inspekcji, jeśli istnieje. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/V1/AuditRecords/{{AuditId}}") |
| ResourceChangeUtcDate | ciąg w formacie daty i godziny UTC | Data i godzina wystąpienia zmiany zasobu. |

#### <a name="example"></a>Przykład

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```
