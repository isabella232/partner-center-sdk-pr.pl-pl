---
title: Zasoby dotyczące uprawnień
description: Opisuje zasoby związane z uprawnieniem.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 428ac6f8b4d67894092119a6246279045a04dac0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768074"
---
# <a name="entitlement-resources"></a>Zasoby dotyczące uprawnień

**Dotyczy**

- Centrum partnerskie
- Centrum partnerskie obsługiwane przez firmę 21Vianet
- Centrum partnerskie dla Microsoft Cloud Niemcy
- Centrum partnerskie Microsoft Cloud for US Government

## <a name="entitlement"></a>Uprawnienie

Ten zasób reprezentuje produkty, do których klient ma prawo do użycia z powodu zakupu przez partnera elementów z wykazu.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Odwołanie do zamówienia, które spowodowało odpowiednie uprawnienia. |
| productId | ciąg | Identyfikator produktu. |
| Identyfikatora skuId | ciąg | Identyfikator jednostki SKU. |
| quantity | int | Liczba uprawnień (bez niezrealizowanych/przeniesionych uprawnień). |
| quantityDetails | Interfejs IEnumerable<[QuantityDetail](#quantitydetail)> | Lista szczegółów dotyczących liczby uprawnień (liczba elementów i stan każdej z nich). |
| uprawnienietype | ciąg | Typ uprawnienia. (Zaktualizowano do ciągu z poziomu [uprawnień](#entitlementtype) w zestawie SDK 1,8). |
| entitledArtifacts | [Artefakt](#artifact)<IEnumerable> | Lista artefaktów skojarzonych z uprawnieniem. |
| IncludedEntitlements | [Uprawnienia](#artifact)<interfejsu IEnumerable> | Lista uprawnień, które są niejawnie uwzględniane w wyniku zakupu ProductId/identyfikatora skuId z katalogu. |
| ExpiryDate | ciąg w formacie daty i godziny UTC  | Data wygaśnięcia uprawnień (jeśli dotyczy). |

## <a name="referenceorder"></a>ReferenceOrder

Odwołanie do zamówienia.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| identyfikator | ciąg | Identyfikator zamówienia, do którego istnieje odwołanie. |
| lineItemId | ciąg | Identyfikator elementu wiersza zamówienia, do którego się odwoływano. |
| alternateId | ciąg | Alternatywny identyfikator elementu wiersza zamówienia, do którego się odwoływano. |

## <a name="quantitydetail"></a>QuantityDetail

Przedstawia szczegóły ilości uprawnień.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| quantity | int | Liczba elementów. |
| status | ciąg | Stan liczby. |

## <a name="entitlementtype"></a>Uprawnienietype

> [!IMPORTANT]
> Przestarzałe w zestawie SDK v 1.9

[Wyliczenie](/dotnet/api/system.enum) z wartościami, które wskazują typ uprawnienia.

| Wartość | Opis |
|-------|-------------|
| Oprogramowanie | Wskazuje typ uprawnień związany z oprogramowaniem. |
| VirtualMachineReservedInstance | Wskazuje typ uprawnień związany z Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefakt

Artefakt skojarzony z uprawnieniem.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| artefakttype | ciąg | Typ artefaktu. (Zaktualizowano do ciągu z [artefakttype](#artifacttype) w zestawie SDK v 1.8) |
| dynamicAttributes | &lt;Ciąg słownika, obiekt&gt; | Atrybuty dynamiczne zawierające określone wartości artefaktu. Na przykład jeśli artefakttype = "reservedinstance", ta właściwość będzie zawierać "reservationtype" = "virtualmachines" lub "reservationtype" = "sqldatabases", co oznacza wystąpienie zarezerwowane maszyny wirtualnej lub wystąpienie zarezerwowane SQL platformy Azure. (Dostępne począwszy od zestawu SDK v 1.9) |

## <a name="artifacttype"></a>Artefakttype

> [!IMPORTANT]
> Przestarzałe w zestawie SDK v 1.9

[Wyliczenie](/dotnet/api/system.enum) z wartościami wskazującymi typ artefaktu uprawnienia.

| Wartość                          | Opis                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Wskazuje pomoc artefaktów z pobieraniem Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefakt skojarzony z uprawnieniem do wystąpienia zarezerwowanego platformy Azure. Dziedziczy z klasy [artefaktu](#artifact) .

| Właściwość   | Typ                           | Opis                                        |
|------------|--------------------------------|----------------------------------------------------|
| połącz       | [Łącze](./utility-resources.md#link) | Link, aby pobrać wszystkie szczegóły skojarzonego artefaktu.   |
| Identyfikator | ciąg                         | Identyfikator zamówienia lub zasobu rezerwacji platformy Azure. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Reprezentuje jednostkę zwracaną podczas wywołania artefaktu wystąpienia zastrzeżonego platformy Azure.

|   Właściwość   |           Typ           |                          Opis                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          ciąg          |                     Typ artefaktu.                     |
| dokonując | IEnumerable<Reservation> | Wskazuje identyfikator zamówienia zasobu platformy Azure lub rezerwacji. |

## <a name="reservation"></a>Rezerwacja

Reprezentuje pojedynczą rezerwację.

| Właściwość          | Typ                           | Opis                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | ciąg                         | Identyfikator rezerwacji.                                         |
| zakrestype         | ciąg                         | Typ zakresu skojarzonego z rezerwacją maszyny wirtualnej. |
| displayName       | ciąg                         | Nazwa wyświetlana rezerwacji.                               |
| appliedScopes     | IEnumerable                    | Lista zastosowanych zakresów skojarzonych z rezerwacją. (Dostępne tylko wtedy, gdy zakres ScopeType nie jest udostępniony). |
| quantity          | int                            | Liczba maszyn wirtualnych w rezerwacji.                 |
| expiryDateTime    | ciąg w formacie daty i godziny UTC | Data wygaśnięcia rezerwacji.                                |
| effectiveDateTime | ciąg w formacie daty i godziny UTC | Data wprowadzenia rezerwacji.                             |
| provisioningState | ciąg                         | Stan aprowizacji rezerwacji.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Przestarzałe w zestawie SDK v 1.9

Artefakt skojarzony z uprawnieniem wystąpienia zarezerwowanej maszyny wirtualnej platformy Azure. Dziedziczy z klasy [artefaktu](#artifact) .

| Właściwość   | Typ                              | Opis                                        |
|------------|-----------------------------------|----------------------------------------------------|
| połącz       | [Łącze](utility-resources.md#link) | Link, aby pobrać wszystkie szczegóły skojarzonego artefaktu.   |
| Identyfikator | ciąg                            | Identyfikator zamówienia lub zasobu rezerwacji platformy Azure. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Przestarzałe w zestawie SDK v 1.9

Reprezentuje jednostkę zwracaną podczas wywołania artefaktu wystąpienia zarezerwowanej maszyny wirtualnej platformy Azure.

| Właściwość                    | Typ                                                                 | Opis           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| typ                        | [Artefakttype](#artifacttype)                                        | Typ artefaktu. |
| virtualMachineReservations  | Interfejs IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Wskazuje identyfikator zamówienia zasobu platformy Azure lub rezerwacji. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Przestarzałe w zestawie SDK v 1.9

Reprezentuje pojedynczą rezerwację maszyny wirtualnej.

|     Właściwość      |              Typ              |                                                Opis                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             ciąg             |                                         Identyfikator rezerwacji.                                         |
|     zakrestype     |             ciąg             |                     Typ zakresu skojarzonego z rezerwacją maszyny wirtualnej.                     |
|    displayName    |             ciąg             |                                    Nazwa wyświetlana rezerwacji.                                    |
|   appliedScopes   |      IEnumerable<string>       | Lista zastosowanych zakresów skojarzonych z rezerwacją. (Dostępne tylko wtedy, gdy zakres ScopeType nie jest udostępniony). |
|     quantity      |              int               |                             Liczba maszyn wirtualnych w rezerwacji.                             |
|  expiryDateTime   | ciąg w formacie daty i godziny UTC |                                    Data wygaśnięcia rezerwacji.                                     |
| effectiveDateTime | ciąg w formacie daty i godziny UTC |                                   Data wprowadzenia rezerwacji.                                   |
| provisioningState |             ciąg             |                                 Stan aprowizacji rezerwacji.                                 |
