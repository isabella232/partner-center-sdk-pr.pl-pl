---
title: Zasoby marginesu
description: Zasoby reprezentujące marginesy. Zawiera zasoby do opisywania marginesów.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 83ea2f95c72f4e5074e3396ef226462b5b007878
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646401"
---
# <a name="margin-resources"></a>Zasoby marginesu

Zasoby reprezentujące dostępne marginesy. Zawiera zasoby do opisywania marginesu.  

Niezależny dostawca oprogramowania (ISV) może tworzyć rabaty lub marże dla określonych dostawców rozwiązań w chmurze (CSP). Poniżej przedstawiono zasoby, które reprezentują i opisują marginesy.
                
## <a name="margin"></a>Margin                   
                        
Reprezentuje awalowalny margines dla danego CSP.
                
| Nazwa            | Typ            | Opis                               |
|-----------------|-----------------|-------------------------------------------|
| identyfikator              | ciąg          | Unikatowy identyfikator marginesu.         |
| marginPercentage | liczba         | Rabat procentowy zastosowany do ceny detalicznej CSP.  |
| productId       | ciąg          | Identyfikator produktu, dla których jest dostępny margines.   |
| productTitle    | ciąg          | Tytuł produktu, dla który jest dostępny margines. |
| productType     | ciąg          | Typ produktu, dla jakiego jest dostępny margines.   |
| publisherName   | ciąg          | Nazwa isv, który utworzył margines.  |
| skuId           | ciąg          | Identyfikator SKU, dla których jest dostępny margines.  |
| skuTitle        | ciąg          | Tytuł SKU, dla których jest dostępny margines. |
| Startdate       | ciąg          | Data rozpoczęcia, w przypadku których margines jest dostępny. |
| Enddate         | ciąg          | Data zakończenia, w których jest dostępny margines. |
| status          | ciąg          | Stan indicting, czy margines jest dostępny. |
| statusDate      | ciąg          | Data ostatniej aktualizacji stanu. |

## <a name="definitions"></a>Definicje

Różne typy artefaktów opisujących marginesy.                    

| Nazwa            | Opis          |
|-----------------|----------------------|
| Margin |  Definiuje pojedynczy margines.  |    
| MarginSearchResponse |  Definiuje dane odpowiedzi marginesu.  |  
        
## <a name="related-documentation"></a>Dokumentacja pokrewna

- [Marginesy w Partner Center przeglądu](/partner-center/csp-commercial-marketplace-margins)
- [Kupowanie ofert z platformy handlowej](/partner-center/csp-commercial-marketplace-purchase)
- [Zarządzanie ofertami na platformie handlowej](/partner-center/csp-commercial-marketplace-manage)
- [Uzyskiwanie listy marginesów](get-margins.md)
- [Pobieranie listy marginesów](download-margins.md)
