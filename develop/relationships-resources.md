---
title: Zasoby relacji
description: Opisuje zasoby związane z relacjami.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bbbc973679ae80c3ad6b9d67945c6fbcb087789484939b67f8d8a6b538ce7d37
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997094"
---
# <a name="relationships-resources"></a>Zasoby relacji

Opisuje zasoby związane z relacjami.

## <a name="partnerrelationship"></a>PartnerRelationship

Reprezentuje relację między dwoma partnerami.

| Właściwość         | Typ                                                           | Opis                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator               | ciąg                                                         | Identyfikator partnera. Identyfikator partnera określa identyfikator dzierżawy partnera, który znajduje się po stronie odbiorcy (od) relacji. |
| location         | ciąg                                                         | Lokalizacja partnera.                                                                                                                   |
| mpnId            | ciąg                                                         | Identyfikator Microsoft Partner Network (MPN) partnera.                                                                                 |
| name             | ciąg                                                         | Nazwa partnera.                                                                                                                       |
| Relationshiptype | ciąg                                                         | Typ relacji.                                                                                                                      |
| stan            | ciąg                                                         | Stan relacji (na przykład `active` ).                                                                                                 |
| atrybuty       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Dostarcza adres URL, za pomocą którego klient może ustanowić relację z partnerem.

| Właściwość   | Typ                                                           | Opis                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | ciąg                                                         | Adres URL żądania relacji. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.      |
