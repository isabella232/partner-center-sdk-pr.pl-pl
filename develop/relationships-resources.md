---
title: Relacje zasobów
description: Opisuje zasoby związane z relacjami.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767793"
---
# <a name="relationships-resources"></a>Relacje zasobów

**Dotyczy**

- Centrum partnerskie

Opisuje zasoby związane z relacjami.

## <a name="partnerrelationship"></a>PartnerRelationship

Reprezentuje relację między dwoma partnerami.

| Właściwość         | Typ                                                           | Opis                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| identyfikator               | ciąg                                                         | Identyfikator partnera. Identyfikator partnera określa identyfikator dzierżawcy partnera, który znajduje się w relacji odbiorcy (od). |
| location         | ciąg                                                         | Lokalizacja partnera.                                                                                                                   |
| mpnId            | ciąg                                                         | Identyfikator Microsoft Partner Network (MPN) partnera.                                                                                 |
| name             | ciąg                                                         | Nazwa partnera.                                                                                                                       |
| Atrybut | ciąg                                                         | Typ relacji.                                                                                                                      |
| stan            | ciąg                                                         | Stan relacji (na przykład `active` ).                                                                                                 |
| atrybuty       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Określa adres URL, za pomocą którego klient może ustanowić relację z partnerem.

| Właściwość   | Typ                                                           | Opis                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | ciąg                                                         | Adres URL żądania relacji. |
| atrybuty | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.      |
