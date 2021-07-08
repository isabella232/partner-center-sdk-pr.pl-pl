---
title: Zasoby usługi zarządzanej
description: Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora. Partnerzy mogą zapewniać obsługę żądań obsługi i plików w imieniu swoich zarządzanych usług.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548128"
---
# <a name="managed-service-resources"></a>Zasoby usługi zarządzanej

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

Usługi zarządzane to usługi, do których partner ma delegowane uprawnienia administratora. Partnerzy mogą zapewniać obsługę żądań obsługi i plików w imieniu swoich zarządzanych usług.

## <a name="managedservice"></a>ManagedService (Usługa zarządzana)

Opisuje usługę zarządzaną.

| Właściwość   | Typ                | Opis                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | ciąg              | Identyfikator usługi zarządzanej.                                  |
| Nazwa       | ciąg              | Nazwa usługi zarządzanej.                         |
| Groupname  | ciąg              | Nazwa grupy, do której należy usługa.      |
| Linki      | ManagedServiceLinks | Linki zasobów odpowiadające usłudze zarządzanej. |
| Atrybuty | ResourceAttributes  | Atrybuty metadanych odpowiadające umowie.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Zawiera linki, które umożliwiają partnerowi z delegowanymi uprawnieniami administratora zapewnienie obsługi usługi.

| Właściwość      | Typ | Opis                 |
|---------------|------|-----------------------------|
| Usługa administracyjna  | Link | URI usługi administracyjnej.      |
| ServiceHealth | Link | URI kondycji usługi.     |
| ServiceTicket | Link | URI biletu usługi.     |
| Self          | Link | Samodzielnego URI.               |
| Następne          | Link | Następna strona elementów.     |
| Poprzednie      | Link | Poprzednia strona elementów. |

