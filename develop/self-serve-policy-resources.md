---
title: Zasoby zasad samoobsługi
description: Partner ustawia zasady samoobsługi dla klienta.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446721"
---
# <a name="selfservepolicy-resource"></a>Zasób SelfServePolicy

Partner ustawia zasady samoobsługi dla klienta.

## <a name="selfservepolicy"></a>SelfServePolicy

Opisuje koszyk.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator zasad samoobsługi, który jest dostarczany po pomyślnym utworzeniu zasad samoobsługi.     |
| SelfServeEntity       | SelfServeEntity  | Jednostka samoobsługowa, która ma udzielany dostęp.                                                     |
| Grantor               | Grantor          | Grantor, który udziela dostępu.                                                                    |
| Uprawnienia           | Tablica uprawnień| Tablica [zasobów](#permission) uprawnień.                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

Reprezentuje jednostkę, która ma przyznane uprawnienia.

| Właściwość             | Typ|Opis|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | ciąg                           | Jednostka, do których jest udzielany dostęp, zaakceptowane wartości: Klient.                                 |
| TenantID             | ciąg                           | Identyfikator dzierżawy jednostki, do których jest udzielany dostęp.                                   |

## <a name="grantor"></a>Grantor

Reprezentuje grantor udzielanie uprawnień.

| Właściwość             | Typ|Opis|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | ciąg                           | Grantor, który udziela dostępu, zaakceptowane wartości: BillToPartner.                               |
| TenantID             | ciąg                           | Identyfikator dzierżawy jednostki, która udziela dostępu.                                       |


## <a name="permission"></a>Uprawnienie

Reprezentuje uprawnienie w zasadach samoobsługi.

| Właściwość             | Typ|Opis|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Zasób             | ciąg                           | Udzielany jest również dostęp do zasobów: AzureReservedInstances.                          |
| Akcja               | ciąg                           | Udzielany jest dostęp do akcji: Zakup                                           |
