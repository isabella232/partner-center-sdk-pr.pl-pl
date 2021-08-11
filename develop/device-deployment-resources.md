---
title: Zasoby wdrażania urządzeń
description: Zasoby związane z Partner Center wdrożenia urządzenia.
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8e2429fea88a89873955d9af9253492934e40e5be1a1b7600446485d13f5bd7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994850"
---
# <a name="device-deployment-resources"></a>Zasoby wdrażania urządzeń

**Dotyczy:** Partner Center | Partner Center for Microsoft Cloud Germany

Następujące zasoby są związane z wdrażaniem urządzeń.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**Zasady ConfigurationPolicy** zawierają informacje o zasadach konfiguracji.

| Właściwość             | Typ                                                           | Opis                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| identyfikator                   | ciąg                                       | Ciąg w formacie identyfikatora GUID, który identyfikuje zasady.                                  |
| name                 | ciąg                                       | Przyjazna nazwa zasad.                                                    |
| category             | ciąg                                       | Kategoria.                                                                        |
| description (opis)          | ciąg                                       | Opis zasad.                                                              |
| devicesAssignedCount | liczba                                       | Liczba urządzeń przypisanych do tych zasad.                                       |
| ustawienia zasad       | tablica ciągów                             | Ustawienia zasad: "none", "remove \_ oem \_ preinstalls", "oobe \_ user not local \_ \_ \_ admin","skip \_ express \_ settings","skip \_ oem \_ registration", "skip \_ eula".    |
| createdDate          | ciąg w formacie daty i czasu UTC               | Data i godzina utworzenia zasad.                                            |
| lastModifiedDate     | ciąg w formacie daty i czasu UTC               | Data i godzina ostatniej modyfikacji zasad.                                      |
| atrybuty           | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.                                            |

## <a name="device"></a>Urządzenie

**Urządzenie** udostępnia informacje o urządzeniu.

| Właściwość            | Typ                                                           | Opis                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| identyfikator                  | ciąg                                                         | Ciąg w formacie identyfikatora GUID, który identyfikuje urządzenie.                      |
| serialNumber        | ciąg                                                         | Numer seryjny jednoznacznie skojarzony z urządzeniem.                   |
| Productkey          | ciąg                                                         | Klucz produktu jednoznacznie skojarzony z urządzeniem.                     |
| hardwareHash        | ciąg                                                         | Skrót sprzętu jednoznacznie skojarzony z urządzeniem.                   |
| Modelname           | ciąg                                                         | Nazwa modelu skojarzona z urządzeniem.                               |
| oemManufacturerName | ciąg                                                         | Nazwa producenta OEM skojarzonego z urządzeniem.             |
| policies            | tablica obiektów                                               | Lista zasad przypisanych do urządzenia.                             |
| uploadedDate        | ciąg w formacie daty i czasu UTC                                 | Data i godzina przesłania szczegółów urządzenia.                      |
| allowedOperations   | tablica ciągów                                               | Lista metod HTTP dozwolonych na synchronizacji urządzenia w następujący sposób: GET, PATCH, DELETE. |
| atrybuty          | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** opisuje stan przekazywania wsadowego urządzenia informacji o poszczególnych urządzeniach na liście urządzeń.

| Właściwość        | Typ     | Opis                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | ciąg   | Ciąg w formacie identyfikatora GUID skojarzony z partią przekazanych urządzeń. |
| status          | ciąg   | Stan przekazywania wsadowego: "nieznany", "w kolejce", "przetwarzanie", "zakończone", "zakończone \_ z \_ błędami". |
| startedTime     | ciąg w formacie daty i czasu UTC | Data i godzina rozpoczęcia procesu przekazywania wsadowego.   |
| completedTime   | ciąg w formacie daty i czasu UTC  | Data i godzina zakończenia procesu przekazywania wsadowego.   |
| devicesStatus   | tablica [zasobów DeviceUploadDetails](#deviceuploaddetails) | Tablica obiektów, które określają stan przekazywania informacji o poszczególnych urządzeniach. |
| atrybuty      | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** opisuje stan przekazywania informacji o urządzeniu.

| Właściwość         | Typ                    | Opis                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | ciąg                  | Ciąg w formacie identyfikatora GUID skojarzony z urządzeniem. |
| serialNumber     | ciąg                  | Numer seryjny jednoznacznie skojarzony z urządzeniem. |
| Productkey       | ciąg                  | Klucz produktu jednoznacznie skojarzony z urządzeniem. |
| status           | ciąg                  | Stan przekazywania informacji o urządzeniu: "w toku", "gotowe", "zakończone \_ z \_ błędami". |
| errorCode        | ciąg                  | Kod błędu stanu HTTP jest zwracany, jeśli przekazywanie urządzenia nie powiedzie się. |
| errorDescription (opis błędu) | ciąg                  | Opis błędu HTTP w przypadku niepowodzenia przekazywania urządzenia. |
| atrybuty       | [ResourceAttributes](utility-resources.md#resourceattributes) | Atrybuty metadanych.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** reprezentuje kolekcję urządzeń.

| Właściwość     | Typ                                                           | Opis                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| identyfikator           | ciąg                                                         | Ciąg w formacie identyfikatora GUID skojarzony z partią urządzeń. |
| Createdby    | ciąg                                                         | Nazwa dzierżawy, która utworzyła kolekcję.                   |
| Creationdate | ciąg w formacie daty i czasu UTC                                 | Dane i czas utworzenia kolekcji.                    |
| deviceCount  | liczba                                                         | Liczba urządzeń w kolekcji.                              |
| devicesLink  | [Link](utility-resources.md#link)                              | Link do urządzeń zawartych w tej partii.                        |
| atrybuty   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest udostępnia** informacje wymagane do utworzenia partii urządzeń i wypełnia je urządzeniami.

| Właściwość     | Typ                                                           | Opis                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| Batchid      | ciąg                                                         | Ciąg w formacie identyfikatora GUID skojarzony z partią urządzeń. |
| devices      | tablica [obiektów](#device) Urządzenia                             | Każdy obiekt określa urządzenie. Akceptowane są następujące kombinacje pól do identyfikacji urządzenia: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash only, productKey only, serialNumber + oemManufacturerName + modelName. |
| atrybuty   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest zawiera** informacje wymagane do zaktualizowania listy urządzeń przy użyciu zasad.

| Właściwość     | Typ                                                           | Opis                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | tablica [obiektów](#device) Urządzenia                             | Każdy obiekt określa urządzenie. Wymagane są następujące właściwości: Identyfikator, Zasady. |
| atrybuty   | [ResourceAttributes](utility-resources.md#resourceattributes)  | Atrybuty metadanych.                                              |
