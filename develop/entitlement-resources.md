---
title: Zasoby uprawnień
description: Opisuje zasoby związane z uprawnieniem.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 929004fff804675218e267bb928b432f7b1209bf
ms.sourcegitcommit: 84a6f701190f46d2adcf6edcaeaafa32d58fbaba
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2021
ms.locfileid: "113510112"
---
# <a name="entitlement-resources"></a>Zasoby uprawnień

**Dotyczy:** Partner Center | Partner Center obsługiwana przez firmę 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government

## <a name="entitlement"></a>Uprawnienie

Ten zasób reprezentuje produkty, do których klient ma prawo korzystać z powodu zakupu przez partnera elementów z katalogu.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Odwołanie do zamówienia, które wywłaszło uprawnienie. |
| productId | ciąg | Identyfikator produktu. |
| skuID | ciąg | Identyfikator sku. |
| quantity | int | Liczba uprawnień (z wyłączeniem niewypełnionych/przenoszonych uprawnień). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | Lista szczegółów ilości uprawnień (liczba elementów i stan każdej ilości). |
| entitlementType | ciąg | Typ uprawnienia. (Zaktualizowano do ciągu z [entitlementType](#entitlementtype) w zestawie SDK 1.8). |
| entitledArtifacts | Artefakt<[IEnumerable](#artifact)> | Lista artefaktów skojarzonych z uprawnieniem. |
| IncludedEntitlements | Uprawnienie IEnumerable<[](#artifact)> | Lista uprawnień, które są niejawnie uwzględniane w wyniku zakupu productid/SkuId z katalogu. |
| Data wygaśnięcia | ciąg w formacie daty i godzin UTC  | Data wygaśnięcia uprawnienia (jeśli ma zastosowanie). |

## <a name="referenceorder"></a>ReferenceOrder

Odwołanie do zamówienia uprawnienia.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| identyfikator | ciąg | Identyfikator kolejności, do których się odwołujesz. |
| lineItemId | ciąg | Identyfikator elementu wiersza zamówienia, do których się odwołujesz. |
| alternateId | ciąg | Alternatywny identyfikator elementu wiersza zamówienia, do których się odwołujesz. |

## <a name="quantitydetail"></a>QuantityDetail

Reprezentuje szczegóły ilości uprawnień.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| quantity | int | Liczba elementów. |
| status | ciąg | Stan ilości. |

## <a name="entitlementtype"></a>Typ uprawnień

> [!IMPORTANT]
> Przestarzałe w zestawie SDK w wersji 1.9

[Wyli element](/dotnet/api/system.enum) z wartościami wskazującymi typ uprawnienia.

| Wartość | Opis |
|-------|-------------|
| Oprogramowanie | Wskazuje typ uprawnień powiązany z oprogramowaniem. |
| VirtualMachineReservedInstance | Wskazuje typ uprawnień powiązany z Azure Reserved Virtual Machine Instances. |

## <a name="artifact"></a>Artefakt

Artefakt skojarzony z uprawnieniem.

| Właściwość | Typ | Opis |
|----------|------|-------------|
| artifactType | ciąg | Typ artefaktu. (Zaktualizowano do ciągu [z artifactType](#artifacttype) w zestawie SDK w wersji 1.8) |
| dynamicAttributes | Ciąg &lt; słownika, obiekt&gt; | Atrybuty dynamiczne zawierające wartości specyficzne dla artifacttype. Na przykład gdy artifactType = "reservedinstance" ta właściwość będzie zawierać wartość "reservationType" = "virtualmachines" lub "reservationType" = "sqldatabases" oznaczające wystąpienie zarezerwowane maszyny wirtualnej lub wystąpienie zarezerwowane SQL Azure. (Dostępne od wersji 1.9 zestawu SDK) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> Przestarzałe w zestawie SDK w wersji 1.9

[Wyli element](/dotnet/api/system.enum) z wartościami wskazującymi typ artefaktu uprawnień.

| Wartość                          | Opis                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Wskazuje artefakt pomaga w pobierania Azure Reserved Virtual Machine Instances. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Artefakt skojarzony z uprawnieniem wystąpienia zarezerwowanego platformy Azure. Dziedziczy on z klasy [Artifact.](#artifact)

| Właściwość   | Typ                           | Opis                                        |
|------------|--------------------------------|----------------------------------------------------|
| połącz       | [Link](./utility-resources.md#link) | Link do pobrania wszystkich szczegółów skojarzonego artefaktu.   |
| Resourceid | ciąg                         | Identyfikator zamówienia lub zasobu rezerwacji platformy Azure. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Reprezentuje jednostkę zwróconą po wywołania linku artefaktu wystąpienia zarezerwowanego platformy Azure.

|   Właściwość   |           Typ           |                          Opis                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     typ     |          ciąg          |                     Typ artefaktu.                     |
| Rezerwacje | `IEnumerable<Reservation>` | Wskazuje identyfikator zamówienia rezerwacji lub zasobu platformy Azure. |

## <a name="reservation"></a>Rezerwacja

Reprezentuje pojedynczą rezerwację.

| Właściwość          | Typ                           | Opis                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | ciąg                         | Identyfikator rezerwacji.                                         |
| scopeType (typ zakresu)         | ciąg                         | Typ zakresu skojarzonego z rezerwacją maszyny wirtualnej. |
| displayName       | ciąg                         | Nazwa wyświetlana rezerwacji.                               |
| appliedScopes     | Ienumerable                    | Lista zastosowanych zakresów skojarzonych z rezerwacją. (Dostępne tylko wtedy, gdy typ scopeType nie jest udostępniony). |
| quantity          | int                            | Liczba maszyn wirtualnych w rezerwacji.                 |
| expiryDateTime    | ciąg w formacie daty i czasu UTC | Data wygaśnięcia rezerwacji.                                |
| effectiveDateTime | ciąg w formacie daty i czasu UTC | Data wejścia w życie rezerwacji.                             |
| provisioningState | ciąg                         | Stan aprowizowania rezerwacji.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> Przestarzałe w zestawie SDK w wersji 1.9

Artefakt skojarzony z uprawnieniem wystąpienia zarezerwowanego maszyny wirtualnej platformy Azure. Dziedziczy on z klasy [Artifact.](#artifact)

| Właściwość   | Typ                              | Opis                                        |
|------------|-----------------------------------|----------------------------------------------------|
| połącz       | [Link](utility-resources.md#link) | Link do pobrania wszystkich szczegółów skojarzonego artefaktu.   |
| Resourceid | ciąg                            | Identyfikator zamówienia lub zasobu rezerwacji platformy Azure. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> Przestarzałe w zestawie SDK w wersji 1.9

Reprezentuje jednostkę zwróconą po wywołania linku artefaktu wystąpienia zarezerwowanego maszyny wirtualnej platformy Azure.

| Właściwość                    | Typ                                                                 | Opis           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| typ                        | [ArtifactType](#artifacttype)                                        | Typ artefaktu. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Wskazuje identyfikator zamówienia rezerwacji lub zasobu platformy Azure. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> Przestarzałe w zestawie SDK w wersji 1.9

Reprezentuje rezerwację poszczególnych maszyn wirtualnych.

|     Właściwość      |              Typ              |                                                Opis                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             ciąg             |                                         Identyfikator rezerwacji.                                         |
|     scopeType (typ zakresu)     |             ciąg             |                     Typ zakresu skojarzonego z rezerwacją maszyny wirtualnej.                     |
|    displayName    |             ciąg             |                                    Nazwa wyświetlana rezerwacji.                                    |
|   appliedScopes   |      `IEnumerable<string>`       | Lista zastosowanych zakresów skojarzonych z rezerwacją. (Dostępne tylko wtedy, gdy typ scopeType nie jest udostępniony). |
|     quantity      |              int               |                             Liczba maszyn wirtualnych w rezerwacji.                             |
|  expiryDateTime   | ciąg w formacie daty i czasu UTC |                                    Data wygaśnięcia rezerwacji.                                     |
| effectiveDateTime | ciąg w formacie daty i czasu UTC |                                   Data wejścia w życie rezerwacji.                                   |
| provisioningState |             ciąg             |                                 Stan aprowizowania rezerwacji.                                 |
