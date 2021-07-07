---
title: Zasoby umowy
description: Zasób Umowa reprezentuje umowę klienta chmury firmy Microsoft ze szczegółami certyfikacji dostarczonymi przez partnera.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025625"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Zasoby umowy reprezentujące umowę klienta chmury firmy Microsoft

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Zasób **Umowy** jest obecnie obsługiwany przez Partner Center tylko w chmurze publicznej firmy Microsoft.

Zasób **Umowa** reprezentuje umowę klienta chmury firmy Microsoft.

## <a name="agreement"></a>Umowa

**Zasób** Umowa reprezentuje szczegóły certyfikacji dostarczone przez partnera.

| Właściwość       | Typ   | Opis                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | ciąg                         | Identyfikator obiektu zalogowanego użytkownika w dzierżawie partnera, który zapewnia potwierdzenie w imieniu organizacji partnerskiej. W przypadku tworzenia zasobu umowy przy użyciu uwierzytelniania App+User Partner Center automatycznie pobiera wartość atrybutu **userId** z tokenu App+User.                                                                             |
| primaryContact | [Kontakt](./utility-resources.md#contact) | Informacje o użytkowniku z organizacji klienta, który zaakceptował umowę, w tym:  **firstName,** **lastName,** **email** i **phoneNumber** (opcjonalnie). |
| dateAgreed     | ciąg w formacie daty i czasu UTC | Data zaakceptowania umowy przez klienta.                                 |
| templateId     |ciąg                          | Unikatowy identyfikator umowy zaakceptowanej przez klienta. |
| typ           |ciąg                          | Typ umowy. Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement.**|
| agreementLink  | ciąg                         | Adres URL szablonu umowy.                                                    |
