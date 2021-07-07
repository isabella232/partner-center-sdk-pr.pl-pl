---
title: Zasoby metadanych umowy
description: Kolekcja zasobów AgreementMetadata opisuje typy umów, których partnerzy mogą używać do potwierdzania akceptacji przez klientów.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025635"
---
# <a name="agreement-metadata-resources"></a>Zasoby metadanych umowy

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Zasób **AgreementMetaData** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft. 

Kolekcja **AgreementMetaData** udostępnia metadane dotyczące wszystkich typów umów. Partnerzy mogą użyć tej kolekcji, aby potwierdzić akceptację umów przez klienta. Kolekcja **AgreementMetaData** zwraca metadane dla obu typów umów **(** Umowa dotycząca platformy Microsoft Cloud i **Umowa z Klientem Microsoft**).

## <a name="agreementmetadata"></a>AgreementMetaData

Zwrócone metadane umowy obejmują następujące właściwości:

| Właściwość      | Typ               | Opis                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | ciąg             | Unikatowy identyfikator szablonu umowy.                                       |
| typ          | ciąg             | Typ umowy. Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement** (wersja zapoznawcza). |
| agreementLink | ciąg             | Adres URL szablonu umowy.                                                    |
