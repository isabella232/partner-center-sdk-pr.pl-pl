---
title: Zasoby relacji
description: Opisuje zasoby związane z relacjami.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dba1e99a6c97c759e3c61cde1e7565faa2ef4d1
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445735"
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
