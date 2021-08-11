---
title: Partner Center webhook
description: Dowiedz się, jak testować i używać zdarzeń webhook, aby zanotować zmiany subskrypcji i innych zdarzeń w Partner Center.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: f329f7aa59ee5127c8275c7c9d8c59e5ea2cf12e9c888419f1ce35e2db3604d1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997570"
---
# <a name="partner-center-webhook-events"></a>Partner Center webhook

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Partner Center webhook to zdarzenia zmiany zasobów dostarczane do zarejestrowanego adresu URL w postaci punktów POP protokołu HTTP. Aby odebrać zdarzenie z Partner Center, hostuj wywołanie zwrotne, w którym Partner Center post zdarzenia. Zdarzenie jest podpisane cyfrowo, aby można było sprawdzić, czy zostało ono wysłane z Partner Center.

Aby uzyskać informacje na temat sposobu odbierania zdarzeń, uwierzytelniania wywołania zwrotnego i używania interfejsów API element webhook usługi Partner Center do tworzenia, wyświetlania i aktualizowania rejestracji zdarzeń, zobacz Partner Center Webhook ( Elementy [webhook).](partner-center-webhooks.md)

## <a name="supported-events"></a>Obsługiwane zdarzenia

Następujące zdarzenia elementy webhook są obsługiwane przez Partner Center.

### <a name="test-event"></a>Zdarzenie testowe

To zdarzenie umożliwia samodzielne dołączanie i testowanie rejestracji, żądając zdarzenia testowego, a następnie śledząc jego postęp. Podczas próby dostarczenia zdarzenia będą wyświetlane komunikaty o błędach odbierane od firmy Microsoft. Dotyczy to tylko zdarzeń "utworzonych przez test", a dane starsze niż siedem dni zostaną przeczyszone.

>[!NOTE]
>Istnieje limit ograniczenia do 2 żądań na minutę podczas publikowania zdarzenia utworzonego przez test.

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W postaci {zasób}-{akcja}. Dla tego zdarzenia wartość to "test-created".                                          |
| ResourceUri               | URI                                | URI do uzyskania zasobu. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | ciąg                             | Nazwa zasobu, który wyzwoli zdarzenie. W przypadku tego zdarzenia wartość to "test".                                  |
| AuditUri                  | URI                                | (Opcjonalnie) Jeśli rekord inspekcji istnieje, ma być on rejestrem URI. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i czasu UTC | Data i godzina zmiany zasobu.                                                         |

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

### <a name="subscription-updated-event"></a>Zdarzenie aktualizacji subskrypcji

To zdarzenie jest wywoływane po zmianie określonej subskrypcji. Zdarzenie Aktualizacja subskrypcji jest generowane w przypadku zmiany wewnętrznej oprócz zmiany wprowadzonej za pośrednictwem interfejsu API Partner Center API.  To zdarzenie zostanie wygenerowane tylko w przypadku zmiany poziomu handlowego, na przykład w przypadku zmodyfikowania liczby licencji i zmiany stanu subskrypcji. Nie zostanie on wygenerowany podczas tworzenia zasobów w ramach subskrypcji.

>[!NOTE]
>Między zmianą subskrypcji a wyzwoleniem zdarzenia Aktualizacja subskrypcji istnieje opóźnienie do 48 godzin.

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W postaci {zasób}-{akcja}. W przypadku tego zdarzenia wartość to "subskrypcja-zaktualizowana".                                  |
| ResourceUri               | URI                                | URI do uzyskania zasobu. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | ciąg                             | Nazwa zasobu, który wyzwoli zdarzenie. W przypadku tego zdarzenia wartością jest "subskrypcja".                          |
| AuditUri                  | URI                                | (Opcjonalnie) Jeśli rekord inspekcji istnieje, ma być on rejestrem URI. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i czasu UTC | Data i godzina zmiany zasobu.                                                         |

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

To zdarzenie jest wywoływane, gdy Microsoft Azure użycia dla dowolnego klienta przekracza budżet wydatków na użycie (próg). Aby uzyskać więcej informacji, zobacz [Ustawianie budżetu wydatków na platformę Azure dla klientów/centrum partnerskie/set-an-azure-spending-budget-for-your-customers).

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W postaci {zasób}-{akcja}. Dla tego zdarzenia wartość to "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | URI                                | URI do uzyskania zasobu. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName              | ciąg                             | Nazwa zasobu, który wyzwoli zdarzenie. W przypadku tego zdarzenia wartość to "usagerecords".                          |
| AuditUri                  | URI                                | (Opcjonalnie) Jeśli rekord inspekcji istnieje, ma być on rejestrem URI. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i czasu UTC | Data i godzina zmiany zasobu.                                                         |

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

To zdarzenie jest wywoływane podczas tworzenia odwołania.

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W postaci {zasób}-{akcja}. W przypadku tego zdarzenia wartość to "utworzono polecenie".                                  |
| ResourceUri               | URI                                | URI do uzyskania zasobu. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | ciąg                             | Nazwa zasobu, który wyzwoli zdarzenie. W przypadku tego zdarzenia wartość to "odwołanie".                          |
| AuditUri                  | URI                                | (Opcjonalnie) Jeśli rekord inspekcji istnieje, ma być on rejestrem URI. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i czasu UTC | Data i godzina zmiany zasobu.                                                         |

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

### <a name="referral-updated-event"></a>Zdarzenie zaktualizowanego polecenia

To zdarzenie jest wywoływane po zaktualizowaniu polecenia.

#### <a name="properties"></a>Właściwości

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | ciąg                             | Nazwa zdarzenia. W postaci {zasób}-{akcja}. W przypadku tego zdarzenia wartość to "referral-updated".                                  |
| ResourceUri               | URI                                | URI do uzyskania zasobu. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | ciąg                             | Nazwa zasobu, który wyzwoli zdarzenie. W przypadku tego zdarzenia wartość to "odwołanie".                          |
| AuditUri                  | URI                                | (Opcjonalnie) Jeśli rekord inspekcji istnieje, ma być on rejestrem URI. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | ciąg w formacie daty i czasu UTC | Data i godzina zmiany zasobu.                                                         |

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

### <a name="invoice-ready-event"></a>Zdarzenie gotowe na fakturę

To zdarzenie jest wywoływane, gdy nowa faktura jest gotowa.

| Właściwość                  | Typ                               | Opis                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | ciąg | Nazwa zdarzenia. W postaci {zasób}-{akcja}. W przypadku tego zdarzenia wartość to "faktura jest gotowa". |
| ResourceUri | URI | URI do uzyskania zasobu. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" |
| ResourceName | ciąg | Nazwa zasobu, który wyzwoli zdarzenie. W przypadku tego zdarzenia wartością jest "faktura". |
| AuditUri |  URI | (Opcjonalnie) Jeśli rekord inspekcji istnieje, ma być on rejestrem URI. Używa składni: "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}") |
| ResourceChangeUtcDate | ciąg w formacie daty i czasu UTC | Data i godzina zmiany zasobu. |

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
