---
title: Zasoby dokumentu umowy
description: Zasób AgreementDocument jest dokumentem umowy firmy Microsoft na potrzeby wersji zapoznawczej i pobierania. Jest ona obsługiwana przez centrum partnerskie w chmurze publicznej firmy Microsoft.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768561"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>Zasoby dokumentu umowy obsługiwane przez centrum partnerskie w chmurze publicznej firmy Microsoft

**Dotyczy:**

- Centrum partnerskie

Zasób **AgreementDocument** jest obecnie obsługiwany przez centrum partnerskie tylko w *chmurze publicznej firmy Microsoft*. Ten zasób nie ma zastosowania do:

- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Zasób **AgreementDocument** reprezentuje dokument umowy Microsoft, który jest dostępny do zaprezentowania i pobrania.

## <a name="agreementdocument"></a>AgreementDocument

Zasób **AgreementDocument** zawiera następujące właściwości:

| Właściwość       | Typ   | Opis                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | ciąg | Kraj lub rynek, do którego odnosi się ten dokument. |
| language | ciąg | Język, w którym znajduje się ten dokument. |
| displayUri | ciąg | Link umożliwiający wyświetlenie podglądu dokumentu umowy w przeglądarce.  |
| downloadUri |ciąg | Link umożliwiający pobranie dokumentu umowy (w formacie programu Microsoft Word). |
