---
title: Uaktualnianie zasobów
description: Opisuje zasoby używane do uaktualniania użytkownika z subskrypcji źródłowej do subskrypcji docelowej.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ea7499a21312378f4fad3d47eaa9e10993ee3ce7ddb1498f161fac16e09b8a5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992480"
---
# <a name="upgrade-resources"></a>Uaktualnianie zasobów

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Opisuje zasoby używane do uaktualniania użytkownika z subskrypcji źródłowej do subskrypcji docelowej.

## <a name="upgrade"></a>Uaktualnienie

Opisuje zachowanie pojedynczego zasobu uaktualnienia.

| Właściwość      | Typ                   | Opis                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Oferta                  | Oferta subskrypcji docelowej.                                                        |
| UpgradeType   | ciąg                 | Typ uaktualnienia: "brak", "tylko \_ uaktualnienie" lub "uaktualnianie \_ z \_ \_ przeniesieniem licencji".         |
| IsEligible    | boolean                | Określa, czy można wykonać uaktualnienie.                                                  |
| Liczba      | liczba całkowita                | Ilość nowej oferty do zakupienia. Wartość domyślna to ilość subskrypcji źródłowej. |
| UpgradeErrors | tablica elementów UpgradeErrors | Powody, dla których nie można przeprowadzić uaktualnienia, jeśli ma to zastosowanie.                                      |
| Atrybuty    | ResourceAttributes     | Atrybuty metadanych odpowiadające uaktualnieniu.                                        |

## <a name="upgradeerror"></a>UpgradeError

Opisuje przyczynę, dla których nie można wykonać uaktualnienia.

| Właściwość          | Typ               | Opis                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kod              | ciąg             | Kod błędu skojarzony z problemem: "inne", "wyłączone delegowane uprawnienia administratora", "stan subskrypcji nie jest aktywny", "konfliktowe typy usług", "konflikty współbieżności", "wymagany kontekst użytkownika", "dodatek subskrypcji jest obecny", "subskrypcja nie ma żadnych ścieżek \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ uaktualnienia", "nie \_ \_ \_ \_ \_ \_ znaleziono oferty docelowej subskrypcji" lub "subskrypcja nie została aprowizowana". |
| Opis       | ciąg             | Przyjazny tekst opisujący błąd.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | ciąg             | Dodatkowe szczegóły dotyczące błędu.                                                                                                                                                                                                                                                                                                                                                         |
| Atrybuty        | ResourceAttributes | Atrybuty metadanych odpowiadające błędowi.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>Upgraderesult

Opisuje wynik procesu uaktualniania subskrypcji.

| Właściwość             | Typ                        | Opis                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | ciąg                      | Identyfikator subskrypcji źródłowej.                                           |
| TargetSubscriptionID | ciąg                      | Identyfikator subskrypcji docelowej.                                           |
| UpgradeType          | ciąg                      | Typ uaktualnienia: "brak", "tylko \_ uaktualnienie" lub "uaktualnianie \_ z \_ \_ przeniesieniem licencji". |
| UpgradeErrors        | tablica elementów UpgradeErrors      | Błędy napotkane podczas próby wykonania uaktualnienia, jeśli ma to zastosowanie.           |
| LicenseErrors (Wystawcy licencji)        | tablica elementów UserLicenseErrrors | Wystąpiły błędy podczas próby migracji licencji użytkowników, jeśli ma to zastosowanie.          |
| Atrybuty           | ResourceAttributes          | Atrybuty metadanych odpowiadające licencji.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Opisuje błędy wynikające z nieudanych transferów licencji użytkowników.

| Właściwość     | Typ                   | Opis                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | ciąg                 | Unikatowa zidentyfikowana obiektu użytkownika.                                 |
| Nazwa         | ciąg                 | Nazwa użytkownika.                                                     |
| E-mail        | ciąg                 | adres e-mail użytkownika.                                                    |
| błędy       | tablica elementów ServiceFault | Lista wyjątków zgłaszanych podczas próby przeniesienia licencji użytkownika. |
| Atrybuty   | ResourceAttributes     | Atrybuty metadanych odpowiadające licencji.                     |

