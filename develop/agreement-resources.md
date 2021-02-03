---
title: Zasoby umowy
description: Zasób umowy reprezentuje umowę klienta w chmurze firmy Microsoft, która zawiera szczegółowe informacje o certyfikatach dostarczonych przez partnera.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768554"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Zasoby umowy reprezentujące umowę klienta w chmurze firmy Microsoft

**Dotyczy:**

- Centrum partnerskie

Zasób z **umową** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft. Nie dotyczy:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Zasób **umowy** reprezentuje umowę klienta w chmurze firmy Microsoft.

## <a name="agreement"></a>Umowa

Zasób **umowy** reprezentuje szczegóły certyfikacji dostarczone przez partnera.

| Właściwość       | Typ   | Opis                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | ciąg                         | Identyfikator obiektu zalogowanego użytkownika w dzierżawie partnera, który zapewnia potwierdzenie w imieniu organizacji partnerskiej. W przypadku tworzenia zasobu umowy przy użyciu aplikacji + uwierzytelnianie użytkownika centrum partnerskie automatycznie dziedziczy wartość atrybutu **userId** z tokenu App + User.                                                                             |
| primaryContact | [Kontakt](./utility-resources.md#contact) | Informacje o użytkowniku z organizacji klienta, które zaakceptowali umowę, w tym:  **FirstName**, **nazwisko**, **adres e-mail** i numer **telefonu** (opcjonalnie). |
| dateAgreed     | ciąg w formacie daty i godziny czasu UTC | Data zaakceptowania umowy przez klienta.                                 |
| templateId     |ciąg                          | Unikatowy identyfikator umowy zaakceptowanej przez klienta. |
| typ           |ciąg                          | Typ umowy. Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement**.|
| agreementLink  | ciąg                         | Adres URL szablonu umowy.                                                    |
