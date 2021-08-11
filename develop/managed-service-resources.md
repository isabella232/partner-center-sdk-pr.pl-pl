---
title: Zasoby usługi zarządzanej
description: Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora. Partnerzy mogą zapewnić obsługę żądań obsługi plików i żądań obsługi w imieniu swoich zarządzanych usług.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 066c9f2a0d5ca8d03553508c2b471ca49735406a5a0566bf48b0773385c129f7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994391"
---
# <a name="managed-service-resources"></a>Zasoby usługi zarządzanej

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora. Partnerzy mogą zapewnić obsługę żądań obsługi plików i żądań obsługi w imieniu swoich zarządzanych usług.

## <a name="managedservice"></a>ManagedService

Opisuje usługę zarządzaną.

| Właściwość   | Typ                | Opis                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | ciąg              | Identyfikator usługi zarządzanej.                                  |
| Nazwa       | ciąg              | Nazwa usługi zarządzanej.                         |
| Groupname  | ciąg              | Nazwa grupy, do której należy usługa.      |
| Linki      | ManagedServiceLinks | Link zasobu odpowiadający usłudze zarządzanej. |
| Atrybuty | ResourceAttributes  | Atrybuty metadanych odpowiadające umowie.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Zawiera linki, które umożliwiają partnerowi z delegowanymi uprawnieniami administratora zapewnienie pomocy technicznej dla usługi.

| Właściwość      | Typ | Opis                 |
|---------------|------|-----------------------------|
| AdminService  | Link | URI usługi administracyjnej.      |
| ServiceHealth | Link | URI kondycji usługi.     |
| ServiceTicket | Link | URI biletu usługi.     |
| Self          | Link | Własny URI.               |
| Następne          | Link | Następna strona elementów.     |
| Poprzednie      | Link | Poprzednia strona elementów. |

