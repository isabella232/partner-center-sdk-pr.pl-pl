---
title: Samoobsługowe zasoby zasad
description: Partner ustawia zasady samoobsługowe dla klienta.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767842"
---
# <a name="selfservepolicy-resource"></a>Zasób SelfServePolicy

**Dotyczy:**

- Centrum partnerskie

Partner ustawia zasady samoobsługowe dla klienta.

## <a name="selfservepolicy"></a>SelfServePolicy

Opisuje koszyk.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Samoobsługowy identyfikator zasad, który jest dostarczany po pomyślnym utworzeniu zasad samoobsługi.     |
| SelfServeEntity       | SelfServeEntity  | Jednostka samoobsługi, do której uzyskuje się dostęp.                                                     |
| Użytkownik udzielający uprawnienia               | Użytkownik udzielający uprawnienia          | Użytkownik udzielający uprawnienia udzielający dostępu.                                                                    |
| Uprawnienia           | Tablica uprawnień| Tablica zasobów [uprawnień](#permission) .                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Reprezentuje przyznany obiekt uprawnienia.

| Właściwość             | Typ|Opis|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | ciąg                           | Jednostka, której udzielono dostępu, zaakceptowanych wartości: klient.                                 |
| TenantID             | ciąg                           | Identyfikator dzierżawy jednostki, której udzielono dostępu.                                   |

## <a name="grantor"></a>Użytkownik udzielający uprawnienia

Reprezentuje użytkownik udzielający uprawnienia przyznającą uprawnienia.

| Właściwość             | Typ|Opis|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | ciąg                           | Użytkownik udzielający uprawnienia udzielanie dostępu, zaakceptowane wartości: BillToPartner.                               |
| TenantID             | ciąg                           | Identyfikator dzierżawy jednostki, która udziela dostępu.                                       |


## <a name="permission"></a>Uprawnienie

Reprezentuje uprawnienie w zasadach samoobsługi.

| Właściwość             | Typ|Opis|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Zasób             | ciąg                           | Dostęp do zasobu jest przyznany zbyt: AzureReservedInstances.                          |
| Akcja               | ciąg                           | Przyznano dostęp do akcji dla: zakup                                           |
