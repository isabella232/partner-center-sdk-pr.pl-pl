---
title: Zasoby metadanych umowy
description: Kolekcja zasobów AgreementMetadata zawiera informacje o typach umów, które partnerzy mogą wykorzystać w celu potwierdzenia akceptacji klienta.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767766"
---
# <a name="agreement-metadata-resources"></a>Zasoby metadanych umowy

**Dotyczy:**

- Centrum partnerskie

Zasób **AgreementMetaData** jest obecnie obsługiwany przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*. Ten zasób nie ma zastosowania do:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Kolekcja **AgreementMetaData** zawiera metadane dotyczące wszystkich typów umów. Partnerzy mogą korzystać z tej kolekcji w celu potwierdzenia akceptacji umów przez klienta. Kolekcja **AgreementMetaData** zwraca metadane dla obu typów umów (**Umowa Microsoft Cloud** i **Umowa klienta firmy Microsoft**).

## <a name="agreementmetadata"></a>AgreementMetaData

Zwrócone metadane umowy obejmują następujące właściwości:

| Właściwość      | Typ               | Opis                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | ciąg             | Unikatowy identyfikator szablonu umowy.                                       |
| typ          | ciąg             | Typ umowy. Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement** (wersja zapoznawcza). |
| agreementLink | ciąg             | Adres URL szablonu umowy.                                                    |
