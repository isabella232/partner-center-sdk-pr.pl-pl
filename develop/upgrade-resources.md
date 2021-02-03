---
title: Uaktualnianie zasobów
description: Opisuje zasoby używane do uaktualniania użytkownika z subskrypcji źródłowej do subskrypcji docelowej.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bdbef383370761a01eb462f90284ad826a38ddaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767869"
---
# <a name="upgrade-resources"></a>Uaktualnianie zasobów

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Opisuje zasoby używane do uaktualniania użytkownika z subskrypcji źródłowej do subskrypcji docelowej.

## <a name="upgrade"></a>Uaktualnienie

Opisuje zachowanie indywidualnego zasobu uaktualnienia.

| Właściwość      | Typ                   | Opis                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Oferta                  | Oferta subskrypcji docelowej.                                                        |
| Upgradetype   | ciąg                 | Typ uaktualnienia: "none", "upgrade \_ Only" lub "upgrade \_ with \_ License \_ transfer".         |
| Nie kwalifikuj    | boolean                | Określa, czy można wykonać uaktualnienie.                                                  |
| Ilość      | liczba całkowita                | Oszacowanie ilości nowej oferty do zakupu. Wartość domyślna to liczba dla subskrypcji źródłowej. |
| UpgradeErrors | Tablica UpgradeErrors | Powody, dla których nie można przeprowadzić uaktualnienia, jeśli ma to zastosowanie.                                      |
| Atrybuty    | ResourceAttributes     | Atrybuty metadanych odpowiadające uaktualnieniu.                                        |

## <a name="upgradeerror"></a>UpgradeError

Opisuje powód, dla którego nie można przeprowadzić uaktualnienia.

| Właściwość          | Typ               | Opis                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kod              | ciąg             | Kod błędu związany z problemem: "inne", " \_ wyłączono uprawnienia administratora delegowanego" \_ \_ , " \_ stan subskrypcji \_ \_ nieaktywny", "typy usługi powodującej konflikt \_ \_ ", "konflikty współbieżności", "wymagane przez użytkownika nie znaleziono", "subskrypcja nie została \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ zainicjowana" lub "subskrypcja \_ \_ Nieudostępniana". |
| Opis       | ciąg             | Przyjazny tekst opisujący błąd.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | ciąg             | Dodatkowe szczegóły dotyczące błędu.                                                                                                                                                                                                                                                                                                                                                         |
| Atrybuty        | ResourceAttributes | Atrybuty metadanych odpowiadające błędowi.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>UpgradeResult

Opisuje wynik procesu uaktualniania subskrypcji.

| Właściwość             | Typ                        | Opis                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | ciąg                      | Identyfikator subskrypcji źródłowej.                                           |
| TargetSubscriptionID | ciąg                      | Identyfikator subskrypcji docelowej.                                           |
| Upgradetype          | ciąg                      | Typ uaktualnienia: "none", "upgrade \_ Only" lub "upgrade \_ with \_ License \_ transfer". |
| UpgradeErrors        | Tablica UpgradeErrors      | Napotkano błędy podczas próby przeprowadzenia uaktualnienia, jeśli ma to zastosowanie.           |
| LicenseErrors        | Tablica UserLicenseErrrors | Napotkano błędy podczas próby migracji licencji użytkowników, jeśli ma to zastosowanie.          |
| Atrybuty           | ResourceAttributes          | Atrybuty metadanych odpowiadające licencji.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Opisuje błędy wynikające z niepowodzenia transferu licencji użytkownika.

| Właściwość     | Typ                   | Opis                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | ciąg                 | Unikatowy zidentyfikowany obiekt użytkownika.                                 |
| Nazwa         | ciąg                 | Nazwa użytkownika.                                                     |
| E-mail        | ciąg                 | adres e-mail użytkownika.                                                    |
| błędy       | Tablica servicefaults | Lista wyjątków zgłoszonych podczas próby przeprowadzenia transferu licencji użytkownika. |
| Atrybuty   | ResourceAttributes     | Atrybuty metadanych odpowiadające licencji.                     |

