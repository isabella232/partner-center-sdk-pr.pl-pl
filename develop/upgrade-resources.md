---
title: Uaktualnianie zasobów
description: Opisuje zasoby używane do uaktualniania użytkownika z subskrypcji źródłowej do subskrypcji docelowej.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c57994d1b1e7659df5e6448578422f6d9c21fee
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529821"
---
# <a name="upgrade-resources"></a>Uaktualnianie zasobów

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Opisuje zasoby używane do uaktualniania użytkownika z subskrypcji źródłowej do subskrypcji docelowej.

## <a name="upgrade"></a>Uaktualnienie

Opisuje zachowanie pojedynczego zasobu uaktualnienia.

| Właściwość      | Typ                   | Opis                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Oferta                  | Oferta subskrypcji docelowej.                                                        |
| UpgradeType   | ciąg                 | Typ uaktualnienia: "brak", \_ "tylko uaktualnienie" lub "uaktualnianie \_ z \_ \_ przeniesieniem licencji".         |
| IsEligible    | boolean                | Określa, czy można przeprowadzić uaktualnienie.                                                  |
| Liczba      | liczba całkowita                | Ilość nowej oferty do zakupienia. Wartość domyślna to ilość subskrypcji źródłowej. |
| UpgradeErrors | tablica elementów UpgradeErrors | Przyczyny, dla których nie można przeprowadzić uaktualnienia, jeśli ma to zastosowanie.                                      |
| Atrybuty    | ResourceAttributes     | Atrybuty metadanych odpowiadające uaktualnieniu.                                        |

## <a name="upgradeerror"></a>UpgradeError

Opisuje przyczynę, dla którego nie można przeprowadzić uaktualnienia.

| Właściwość          | Typ               | Opis                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kod              | ciąg             | Kod błędu skojarzony z problemem: "inne", "delegowane uprawnienia administratora wyłączone", "stan subskrypcji nie jest aktywny", "sprzeczne typy usług", "konflikty współbieżności", "wymagany kontekst użytkownika", "dodatki subskrypcji są obecne", "subskrypcja nie ma żadnych ścieżek \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ uaktualniania", "nie \_ \_ \_ \_ \_ \_ znaleziono oferty docelowej subskrypcji" lub "subskrypcja nie została aprowizowana". |
| Opis       | ciąg             | Przyjazny tekst opisujący błąd.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | ciąg             | Dodatkowe szczegóły dotyczące błędu.                                                                                                                                                                                                                                                                                                                                                         |
| Atrybuty        | ResourceAttributes | Atrybuty metadanych odpowiadające błędowi.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>Upgraderesult

Opisuje wynik procesu uaktualniania subskrypcji.

| Właściwość             | Typ                        | Opis                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | ciąg                      | Identyfikator subskrypcji źródłowej.                                           |
| TargetSubscriptionID | ciąg                      | Identyfikator subskrypcji docelowej.                                           |
| UpgradeType          | ciąg                      | Typ uaktualnienia: "brak", \_ "tylko uaktualnienie" lub "uaktualnianie \_ z \_ \_ przeniesieniem licencji". |
| UpgradeErrors        | tablica elementów UpgradeErrors      | Błędy napotkane podczas próby wykonania uaktualnienia, jeśli ma to zastosowanie.           |
| LicenseErrors        | tablica elementów UserLicenseErrrors | Błędy napotkane podczas próby migracji licencji użytkowników, jeśli ma to zastosowanie.          |
| Atrybuty           | ResourceAttributes          | Atrybuty metadanych odpowiadające licencji.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Opisuje błędy wynikające z nieudanych transferów licencji użytkownika.

| Właściwość     | Typ                   | Opis                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | ciąg                 | Unikatowa zidentyfikowana obiektu użytkownika.                                 |
| Nazwa         | ciąg                 | Nazwa użytkownika.                                                     |
| E-mail        | ciąg                 | adres e-mail użytkownika.                                                    |
| błędy       | tablica wartości ServiceFaults | Lista wyjątków zgłaszanych podczas próby przeniesienia licencji użytkownika. |
| Atrybuty   | ResourceAttributes     | Atrybuty metadanych odpowiadające licencji.                     |

