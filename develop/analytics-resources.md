---
title: Zasoby analityczne
description: Partner Center zawierają dane dotyczące użycia, wdrażania i użycia. Zawiera szczegółowe informacje na temat wdrażania i używania licencji przez partnerów i klientów.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 69c6c195ba1a0d657a91320b2f9b08b5269a8499
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025602"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Zasoby interfejsu API analizy, które ułatwiają zgłaszanie użycia, wdrażania i użycia licencji

Zasoby zdefiniowane w tym miejscu zawierają dane używane do zgłaszania użycia, wdrażania i użycia.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

Zasób **PartnerLicensesDeploymentInsights** zawiera szczegółowe informacje na poziomie partnera dotyczące wdrażania licencji.

| Właściwość                  | Typ                                                           | Opis                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | liczba                                                         | Procent wdrożonych licencji.                                                |
| licensesSold              | liczba                                                         | Liczba sprzedanych licencji.                                                        |
| processedDateTime         | ciąg w formacie daty i godzin UTC                                 | Data i godzina zagregowania danych.                                     |
| Servicename               | ciąg                                                         | Nazwa usługi (na przykład: o365, crm).                                                  |
| Kanał                   | ciąg                                                         | Nazwa kanału usługi (na przykład: odsprzedawca).                                    |
| atrybuty                | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Obejmuje "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

Zasób **PartnerLicensesUsageInsights** zawiera szczegółowe informacje o użyciu licencji na poziomie partnera.

| Właściwość                     | Typ                                                           | Opis                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | liczba                                                         | Procent wdrożonych licencji.                                           |
| nazwa_obciążenia                 | ciąg                                                         | Nazwa obciążenia (na przykład: exchange).                                             |
| processedDateTime            | ciąg w formacie daty i godzin UTC                                 | Data i godzina zagregowania danych.                                |
| Servicename                  | ciąg                                                         | Nazwa usługi (na przykład: o365, crm).                                             |
| Kanał                      | ciąg                                                         | Nazwa kanału usługi (na przykład: odsprzedawca).                               |
| atrybuty                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Obejmuje "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

Zasób **CustomerLicensesDeploymentInsights** zawiera szczegółowe informacje na poziomie klienta dotyczące wdrażania licencji.

| Właściwość          | Typ                                                           | Opis                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licencjeWdeployed  | liczba                                                         | Liczba wdrożonych licencji.                                                     |
| licensesSold      | liczba                                                         | Liczba sprzedanych licencji.                                                         |
| deploymentPercent | liczba                                                         | Skorygowany procent wdrożonych licencji.                                        |
| customerId        | ciąg                                                         | Identyfikator klienta.                                                             |
| Customername      | ciąg                                                         | Nazwa klienta.                                                                   |
| Productname       | ciąg                                                         | Nazwa produktu.                                                                    |
| kod usługi       | ciąg                                                         | Kod usługi licencji.                                                     |
| processedDateTime | ciąg w formacie daty i godzin UTC                                 | Data i godzina zagregowania danych.                                      |
| Servicename       | ciąg                                                         | Nazwa usługi (na przykład: o365, crm).                                                   |
| Kanał           | ciąg                                                         | Nazwa kanału usługi (na przykład: odsprzedawca).                                     |
| atrybuty        | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Obejmuje "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

Zasób **CustomerLicensesUsageInsights** zawiera szczegółowe informacje o użyciu licencji na poziomie klienta.

| Właściwość          | Typ                                                           | Opis                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | ciąg                                                         | Kod obciążenia.                                                              |
| nazwa_obciążenia      | liczba                                                         | Nazwa obciążenia (na przykład: Exchange).                                              |
| usagePercent      | liczba                                                         | Skorygowany procent używanych licencji.                                       |
| licensesActive    | liczba                                                         | Liczba aktywnych licencji.                                                  |
| licensesQualified | liczba                                                         | Liczba kwalifikowanych licencji.                                               |
| customerId        | ciąg                                                         | Identyfikator klienta.                                                        |
| Customername      | ciąg                                                         | Nazwa klienta.                                                              |
| Productname       | ciąg                                                         | Nazwa produktu.                                                               |
| kod usługi       | ciąg                                                         | Kod usługi licencji.                                                |
| processedDateTime | ciąg w formacie daty i czasu UTC                                 | Data i godzina zagregowania danych.                                 |
| Servicename       | ciąg                                                         | Nazwa usługi (na przykład: o365, crm).                                              |
| Kanał           | ciąg                                                         | Nazwa kanału usługi (na przykład: odsprzedawca).                                |
| atrybuty        | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Obejmuje "objectType": "CustomerLicensesUsageInsights" |