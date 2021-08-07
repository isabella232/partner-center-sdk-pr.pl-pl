---
title: Zasoby metadanych umowy
description: W kolekcji zasobów AgreementMetadata opisano typy umów, których partnerzy mogą używać w celu potwierdzenia akceptacji przez klienta.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 7c09dc2a8dd88e3d3a6a7925f6f61737cbbd410eabda6ecb4c3ead13d889de04
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991263"
---
# <a name="agreement-metadata-resources"></a>Zasoby metadanych umowy

**Dotyczy:** Partner Center

**Nie dotyczy:** Partner Center obsługiwane przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Zasób **AgreementMetaData** jest obecnie obsługiwany Partner Center tylko w chmurze publicznej firmy Microsoft. 

Kolekcja **AgreementMetaData** zawiera metadane dotyczące wszystkich typów umów. Partnerzy mogą użyć tej kolekcji, aby potwierdzić akceptację umów przez klienta. Kolekcja **AgreementMetaData** zwraca metadane dla obu typów umów **(** Umowa dotycząca platformy Microsoft Cloud i **Umowa z Klientem Microsoft**).

## <a name="agreementmetadata"></a>AgreementMetaData

Zwrócone metadane umowy obejmują następujące właściwości:

| Właściwość      | Typ               | Opis                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | ciąg             | Unikatowy identyfikator szablonu umowy.                                       |
| typ          | ciąg             | Typ umowy. Obecnie obsługiwane wartości to **MicrosoftCloudAgreement** i **MicrosoftCustomerAgreement** (wersja zapoznawcza). |
| agreementLink | ciąg             | Adres URL szablonu umowy.                                                    |
