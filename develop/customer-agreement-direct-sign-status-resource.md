---
title: Stan bezpośredniej rejestracji (bezpośredniego akceptacji) umowy klienta.
description: Zasób DirectSignedCustomerAgreementStatus reprezentuje stan bezpośredniej rejestracji (bezpośrednie zatwierdzenie) umowy klienta.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767738"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>Status bezpośredniej rejestracji (bezpośredniej akceptacji) umowy klienta

**Dotyczy:**

- Centrum partnerskie

Zasób **DirectSignedCustomerAgreementStatus** jest obecnie obsługiwany przez centrum partnerskie tylko w chmurze publicznej firmy Microsoft.

Ten zasób *nie ma zastosowania* do:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Zasób **DirectSignedCustomerAgreementStatus** reprezentuje stan bezpośredniego akceptacji umowy klienta.

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

Zasób **DirectSignedCustomerAgreementStatus** zawiera następujące właściwości:

| Właściwość       | Typ   | Opis                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| IsSigned | boolean | Wskazuje, czy umowa klienta została bezpośrednio podpisana (zaakceptowana) przez klienta. |
