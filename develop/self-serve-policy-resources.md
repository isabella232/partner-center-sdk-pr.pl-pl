---
title: Zasoby zasad samoobsługi
description: Partner ustawia zasady samoobsługi dla klienta.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffca78481572e201d3ef9f488e7d594a9c1176249b4415a347b488f4b9b81c51
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996771"
---
# <a name="selfservepolicy-resource"></a>Zasób SelfServePolicy

Partner ustawia zasady samoobsługi dla klienta.

## <a name="selfservepolicy"></a>SelfServePolicy

Opisuje koszyk.

| Właściwość              | Typ             | Opis                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| identyfikator                    | ciąg           | Identyfikator zasad samoobsługi, który jest dostarczany po pomyślnym utworzeniu zasad samoobsługi.     |
| SelfServeEntity       | SelfServeEntity  | Jednostka samoobsługi, która ma udzielany dostęp.                                                     |
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
| GrantorType          | ciąg                           | Grantor udzielanie dostępu, zaakceptowane wartości: BillToPartner.                               |
| TenantID             | ciąg                           | Identyfikator dzierżawy jednostki, która udziela dostępu.                                       |


## <a name="permission"></a>Uprawnienie

Reprezentuje uprawnienie w zasadach samoobsługi.

| Właściwość             | Typ|Opis|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Zasób             | ciąg                           | Udzielany jest również dostęp do zasobów: AzureReservedInstances.                          |
| Akcja               | ciąg                           | Udzielany jest dostęp do akcji: Zakup                                           |
