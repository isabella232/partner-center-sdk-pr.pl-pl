---
title: Zasoby analizy
description: Zasoby Centrum partnerskiego zawierają dane dotyczące użycia, wdrożenia i zużycia. Zawiera szczegółowe informacje na temat wdrażania licencji i użytkowania przez partnerów i klientów.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 9bd47b99f0abaa181e5f255dd6e46151363917e7
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768542"
---
# <a name="analytics-api-resources-that-help-you-report-on-license-usage-deployment-and-consumption"></a>Zasoby interfejsu API analizy ułatwiające raportowanie użycia licencji, wdrożenia i zużycia

**Dotyczy:**

- Centrum partnerskie

Zasoby zdefiniowane w tym miejscu zawierają dane używane do raportowania użycia, wdrożenia i zużycia.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

Zasób **PartnerLicensesDeploymentInsights** zawiera szczegółowe informacje na temat wdrażania licencji na poziomie partnera.

| Właściwość                  | Typ                                                           | Opis                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | liczba                                                         | Procent wdrożonych licencji.                                                |
| licensesSold              | liczba                                                         | Liczba sprzedanych licencji.                                                        |
| processedDateTime         | ciąg w formacie daty i godziny UTC                                 | Data i godzina agregowania danych.                                     |
| serviceName               | ciąg                                                         | Nazwa usługi (na przykład: O365, CRM).                                                  |
| ukierunkowan                   | ciąg                                                         | Nazwa kanału usługi (na przykład: sprzedawca).                                    |
| atrybuty                | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Zawiera "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

Zasób **PartnerLicensesUsageInsights** zawiera szczegółowe informacje na temat użycia licencji.

| Właściwość                     | Typ                                                           | Opis                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | liczba                                                         | Procent wdrożonych licencji.                                           |
| Nr obciążenia                 | ciąg                                                         | Nazwa obciążenia (na przykład: Exchange).                                             |
| processedDateTime            | ciąg w formacie daty i godziny UTC                                 | Data i godzina agregowania danych.                                |
| serviceName                  | ciąg                                                         | Nazwa usługi (na przykład: O365, CRM).                                             |
| ukierunkowan                      | ciąg                                                         | Nazwa kanału usługi (na przykład: sprzedawca).                               |
| atrybuty                   | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Zawiera "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

Zasób **CustomerLicensesDeploymentInsights** zawiera szczegółowe informacje na temat wdrażania licencji na poziomie klienta.

| Właściwość          | Typ                                                           | Opis                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | liczba                                                         | Liczba wdrożonych licencji.                                                     |
| licensesSold      | liczba                                                         | Liczba sprzedanych licencji.                                                         |
| deploymentPercent | liczba                                                         | Skorygowany procent wdrożonych licencji.                                        |
| customerId        | ciąg                                                         | Identyfikator klienta.                                                             |
| customerName      | ciąg                                                         | Nazwa klienta.                                                                   |
| productName       | ciąg                                                         | Nazwa produktu.                                                                    |
| Kod servicecode       | ciąg                                                         | Kod usługi licencji.                                                     |
| processedDateTime | ciąg w formacie daty i godziny UTC                                 | Data i godzina agregowania danych.                                      |
| serviceName       | ciąg                                                         | Nazwa usługi (na przykład: O365, CRM).                                                   |
| ukierunkowan           | ciąg                                                         | Nazwa kanału usługi (na przykład: sprzedawca).                                     |
| atrybuty        | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Zawiera "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

Zasób **CustomerLicensesUsageInsights** zawiera szczegółowe informacje na temat użycia licencji na poziomie klienta.

| Właściwość          | Typ                                                           | Opis                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | ciąg                                                         | Kod obciążenia.                                                              |
| Nr obciążenia      | liczba                                                         | Nazwa obciążenia (na przykład: Exchange).                                              |
| usagePercent      | liczba                                                         | Dostosowany procent użytych licencji.                                       |
| licensesActive    | liczba                                                         | Liczba aktywnych licencji.                                                  |
| licensesQualified | liczba                                                         | Liczba kwalifikowanych licencji.                                               |
| customerId        | ciąg                                                         | Identyfikator klienta.                                                        |
| customerName      | ciąg                                                         | Nazwa klienta.                                                              |
| productName       | ciąg                                                         | Nazwa produktu.                                                               |
| Kod servicecode       | ciąg                                                         | Kod usługi licencji.                                                |
| processedDateTime | ciąg w formacie daty i godziny UTC                                 | Data i godzina agregowania danych.                                 |
| serviceName       | ciąg                                                         | Nazwa usługi (na przykład: O365, CRM).                                              |
| ukierunkowan           | ciąg                                                         | Nazwa kanału usługi (na przykład: sprzedawca).                                |
| atrybuty        | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych. Zawiera "objectType": "CustomerLicensesUsageInsights" |