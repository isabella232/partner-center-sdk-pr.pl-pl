---
title: Zarządzane zasoby usług
description: Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora. Partnerzy mogą zapewnić obsługę żądań i usług plików w imieniu ich usług zarządzanych.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767782"
---
# <a name="managed-service-resources"></a>Zarządzane zasoby usług

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora. Partnerzy mogą zapewnić obsługę żądań i usług plików w imieniu ich usług zarządzanych.

## <a name="managedservice"></a>ManagedService

Opisuje usługę zarządzaną.

| Właściwość   | Typ                | Opis                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | ciąg              | Identyfikator usługi zarządzanej.                                  |
| Nazwa       | ciąg              | Nazwa usługi zarządzanej.                         |
| GroupName  | ciąg              | Nazwa grupy, do której należy usługa.      |
| Linki      | ManagedServiceLinks | Linki do zasobów odpowiadające usłudze zarządzanej. |
| Atrybuty | ResourceAttributes  | Atrybuty metadanych odpowiadające umowie.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Zawiera linki zezwalające partnerowi z delegowanymi uprawnieniami administratora w celu zapewnienia pomocy technicznej dla usługi.

| Właściwość      | Typ | Opis                 |
|---------------|------|-----------------------------|
| AdminService  | Łącze | Identyfikator URI usługi administracyjnej.      |
| Servicehealth | Łącze | Identyfikator URI kondycji usługi.     |
| Servicebilet | Łącze | Identyfikator URI biletu usługi.     |
| Self          | Łącze | Własny identyfikator URI.               |
| Następne          | Łącze | Następna strona elementów.     |
| Poprzednie      | Łącze | Poprzednia strona elementów. |

