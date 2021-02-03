---
title: Zasoby wdrażania urządzeń
description: Zasoby związane z wdrażaniem urządzeń w centrum partnerskim.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a464cdad3979c305df16a3bdc9133ce70a7ac688
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767730"
---
# <a name="device-deployment-resources"></a>Zasoby wdrażania urządzeń

**Dotyczy:**

- Centrum partnerskie
- Centrum partnerskie dla Microsoft Cloud Niemcy

Następujące zasoby są powiązane z wdrażaniem urządzeń.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** zawiera informacje o zasadach konfiguracji.

| Właściwość             | Typ                                                           | Opis                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                                       | Ciąg sformatowany przy użyciu identyfikatora GUID, który identyfikuje zasady.                                  |
| name                 | ciąg                                       | Przyjazna nazwa dla zasad.                                                    |
| category             | ciąg                                       | Kategoria.                                                                        |
| description (opis)          | ciąg                                       | Opis zasad.                                                              |
| devicesAssignedCount | liczba                                       | Liczba urządzeń przypisanych do tych zasad.                                       |
| policySettings       | tablica ciągów                             | Ustawienia zasad: "none", "Usuń \_ \_ preinstalls OEM", "User OOBE \_ \_ nie \_ Local \_ admin", "Pomiń \_ Ustawienia ekspresowe \_ ", "Pomiń \_ rejestrację OEM" \_ , "Pomiń \_ umowę EULA".    |
| createdDate          | ciąg w formacie daty i godziny UTC               | Data i godzina utworzenia zasad.                                            |
| lastModifiedDate     | ciąg w formacie daty i godziny UTC               | Data i godzina ostatniej modyfikacji zasad.                                      |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                            |

## <a name="device"></a>Urządzenie

**Urządzenie** zawiera informacje o urządzeniu.

| Właściwość            | Typ                                                           | Opis                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| identyfikator                  | ciąg                                                         | Ciąg w formacie GUID, który identyfikuje urządzenie.                      |
| serialNumber        | ciąg                                                         | Numer seryjny unikatowy z urządzeniem.                   |
| productKey          | ciąg                                                         | Klucz produktu jest unikatowy z urządzeniem.                     |
| hardwareHash        | ciąg                                                         | Skrót sprzętowy unikatowy skojarzony z urządzeniem.                   |
| modelName           | ciąg                                                         | Nazwa modelu skojarzona z urządzeniem.                               |
| oemManufacturerName | ciąg                                                         | Nazwa producenta OEM skojarzona z urządzeniem.             |
| policies            | Tablica obiektów                                               | Lista zasad przypisanych do urządzenia.                             |
| uploadedDate        | ciąg w formacie daty i godziny UTC                                 | Data i godzina przekazania szczegółów urządzenia.                      |
| allowedOperations   | tablica ciągów                                               | Lista metod HTTP dozwolonych na potrzeby synchronizacji urządzeń jako GET, PATCH i DELETE. |
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** opisuje stan zbiorczego przekazywania informacji o poszczególnych urządzeniach na liście urządzeń.

| Właściwość        | Typ     | Opis                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | ciąg   | Ciąg w formacie GUID, który jest skojarzony z wsadem przekazanych urządzeń. |
| status          | ciąg   | Stan przekazywania wsadowego: "nieznany", "w kolejce", "przetwarzanie", "Zakończono", "Zakończono \_ z \_ błędami". |
| startedTime     | ciąg w formacie daty i godziny UTC | Data i godzina rozpoczęcia procesu przekazywania wsadowego.   |
| completedTime   | ciąg w formacie daty i godziny UTC  | Data i godzina ukończenia procesu przekazywania wsadowego.   |
| devicesStatus   | Tablica zasobów [DeviceUploadDetails](#deviceuploaddetails) | Tablica obiektów, która określa stan każdego przekazywania informacji o urządzeniu. |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** opisuje stan przekazywania informacji o urządzeniu.

| Właściwość         | Typ                    | Opis                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | ciąg                  | Ciąg w formacie GUID, który jest skojarzony z urządzeniem. |
| serialNumber     | ciąg                  | Numer seryjny unikatowy z urządzeniem. |
| productKey       | ciąg                  | Klucz produktu jest unikatowy z urządzeniem. |
| status           | ciąg                  | Stan przekazywania informacji o urządzeniu: "w toku", "gotowe", "zakończone \_ z \_ błędami". |
| errorCode        | ciąg                  | Kod błędu stanu HTTP zwracany, jeśli przekazywanie urządzenia nie powiedzie się. |
| errorDescription | ciąg                  | Opis błędu HTTP w przypadku niepowodzenia przekazywania urządzenia. |
| atrybuty       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** reprezentuje kolekcję urządzeń.

| Właściwość     | Typ                                                           | Opis                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| identyfikator           | ciąg                                                         | Ciąg w formacie GUID, który jest skojarzony z partii urządzeń. |
| createdBy    | ciąg                                                         | Nazwa dzierżawy, która utworzyła kolekcję.                   |
| creationDate | ciąg w formacie daty i godziny UTC                                 | Data i godzina utworzenia kolekcji.                    |
| Liczba urządzeń  | liczba                                                         | Liczba urządzeń w kolekcji.                              |
| devicesLink  | [Łącze](utility-resources.md#link)                              | Łącze do urządzeń znajdujących się w tej partii.                        |
| atrybuty   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** zawiera informacje wymagane do utworzenia partii urządzeń i wypełnienie jej urządzeniami.

| Właściwość     | Typ                                                           | Opis                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Identyfikator partii      | ciąg                                                         | Ciąg w formacie GUID, który jest skojarzony z partii urządzeń. |
| devices      | Tablica obiektów [urządzeń](#device)                             | Każdy obiekt określa urządzenie. Następujące kombinacje pól służących do identyfikacji urządzenia są akceptowane: hardwareHash + productKey, hardwareHash + numer seryjny, hardwareHash + productKey + numer seryjny, hardwareHash Only, tylko productKey, numer_seryjny + oemManufacturerName + ModelName. |
| atrybuty   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** zawiera informacje wymagane do zaktualizowania listy urządzeń za pomocą zasad.

| Właściwość     | Typ                                                           | Opis                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | Tablica obiektów [urządzeń](#device)                             | Każdy obiekt określa urządzenie. Wymagane są następujące właściwości: ID, zasady. |
| atrybuty   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                              |
