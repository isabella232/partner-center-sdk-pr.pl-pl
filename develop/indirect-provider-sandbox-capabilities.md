---
title: Możliwości dostawcy pośredniego CSP w piaskownicy
description: Dostawcy pośredni mogą tworzyć pośrednich odsprzedawców w piaskownicy do celów testowych.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: 07608fb5f2d2a3ffc418188e0ac1ff367e3c5691aa241554a4a954de8c4f2005
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990678"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>Możliwości piaskownicy dostawcy pośredniego CSP do tworzenia kont odsprzedawcy pośredniego 

**Odpowiednie role:** Dostawca pośredni

Dostawcy pośredni dostawcy CSP mogą utworzyć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.


## <a name="prerequisites"></a>Wymagania wstępne 

Partner Center piaskownicy dostawcy pośredniego (warstwa 2). Scenariusz piaskownicy obsługuje uwierzytelnianie zarówno przy użyciu autonomicznej aplikacji, jak i poświadczeń aplikacji i użytkownika. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Dostawca pośredni piaskownicy — tworzenie odsprzedawcy pośredniego piaskownicy przy użyciu Partner Center interfejsu użytkownika 

 Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy tworzenie konta odsprzedawcy pośredniego piaskownicy za pośrednictwem Partner Center portalu.

Poniżej przedstawiono scenariusze, które dostawcy pośredni mogą wykonać dla odsprzedawców pośrednich w piaskownicy za pośrednictwem Partner Center interfejsu użytkownika: 

1. Dostawcy pośredni dostawcy CSP mogą utworzyć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center Portal.
2. Odsprzedawcy pośredni w programie CSP mogą wyświetlać klientów według dostawców pośrednich. 

1. Odsprzedawcy pośredni programu CSP mogą zarządzać kontem klienta przy użyciu delegowanych uprawnień administratora.

1. Dostawcy pośredni dostawcy CSP mogą zapraszać pośrednich odsprzedawców CSP.
 
1. Dostawcy pośredni dostawcy CSP mogą usunąć konto CSP Indirect Reseller piaskownicy za pośrednictwem własnego konta piaskownicy warstwy 2 w Partner Center portal.

    a.  Gdy dostawca pośredni piaskownicy usunie relację z odsprzedawcą pośrednim piaskownicy, sprawdź, czy odsprzedawca pośredni ma jakiekolwiek inne relacje z innymi dostawcami. Jeśli tak, zostanie usunięta tylko relacja z określonym dostawcą pośrednim.

    c. Jeśli jest to jedyna relacja odsprzedawcy pośredniego, odsprzedawca pośredni zostanie usunięty.

1. Dostawcy pośredni dostawcy CSP mogą usunąć CSP Indirect Reseller.

    a. Jest to funkcja dostępna tylko w piaskownicy, która umożliwia dostawcom pośrednim piaskownicy usuwanie pośrednich odsprzedawców piaskownicy.
     
1. Wymagania wstępne dotyczące usuwania odsprzedawcy pośredniego piaskownicy:

    1. Wstrzymaj subskrypcje dla każdego klienta odsprzedawcy pośredniego piaskownicy.

    1. Usuń wszystkich klientów odsprzedawcy pośredniego.

1. Dozwolony limit pięciu odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy. Po usunięciu odsprzedawcy pośredniego piaskownicy limit przydziału zostanie zresetowany.

### <a name="pre-requisites"></a>Wymagania wstępne

- Dozwolony limit pięciu odsprzedawców pośrednich piaskownicy na dostawcę pośredniego piaskownicy. 

- Ten sam identyfikator MPN może służyć do tworzenia wielu kont piaskownicy odsprzedawcy pośredniego, jeśli kraj identyfikatora MPN i kraj piaskownicy odsprzedawcy pośredniego są takie same. Jeśli masz dostępny testowy identyfikator MPN, możesz go użyć lub uzyskać listę identyfikatorów MPN za pośrednictwem naszego [Yammer kanału .]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ) Jeśli nie masz dostępu do Yammer, Yammer poprosi o dostęp.
 
- Tylko 75 klientów jest dozwolonych na dostawcę pośredniego piaskownicy

## <a name="create-csp-indirect-reseller-sandbox-account"></a>Tworzenie CSP Indirect Reseller piaskownicy

1. Zaloguj się Partner Center za pomocą konta piaskownicy warstwy 2. 

2. Przejdź do pozycji Odsprzedawcy pośredni z menu po lewej stronie. 

3. Wybierz przycisk **Dodaj piaskownicę odsprzedawcy.** 

4. Wypełnij formularz rejestracji konta. Nie wymaga to wyjaśnień, ale pamiętaj, że tworzysz konto piaskownicy dla odsprzedawcy pośredniego. To konto nie zostanie poddane testowi i zostanie aktywowane zaraz po zakończeniu rejestracji konta.  

5. Po utworzeniu konta w portalu otrzymasz poświadczenia administratora globalnego dla konta piaskownicy Odsprzedawca pośredni. Pamiętaj, aby zapisać go natychmiast. W przeciwnym razie nie będzie można zalogować się jako piaskownica odsprzedawcy pośredniego. 

6. Wyloguj się i zaloguj się ponownie Partner Center przy użyciu nowych poświadczeń dla piaskownicy odsprzedawcy pośredniego. Poznaj możliwości, które możesz wykonać jako odsprzedawca pośredni. Niektóre z nich to:  

    - Zarządzanie profilami  

    - Zarządzanie użytkownikami i rolami 

    - Zarządzanie dostawcami pośrednimi 

    - Zarządzanie klientami piaskownicy CSP 

    - Zarządzanie relacjami
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Dostawca pośredni piaskownicy — usuwanie odsprzedawcy pośredniego piaskownicy przy Partner Center interfejsu użytkownika

 Jest to funkcja tylko piaskownicy, która umożliwia dostawcom pośrednim piaskownicy usuwanie istniejącego konta odsprzedawcy pośredniego piaskownicy za pośrednictwem Partner Center portalu. 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a>Wymagania wstępne usuwania odsprzedawcy pośredniego piaskownicy:

Istniejące konto CSP Indirect Reseller piaskownicy skojarzone z Twoim własnym kontem CSP Indirect Provider piaskownicy warstwy 2.  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a>Usuwanie CSP Indirect Reseller piaskownicy

1. Zaloguj się Partner Center przy użyciu konta piaskownicy warstwy 2. 

2. Przejdź do pozycji Odsprzedawcy pośredni z menu po lewej stronie. 

3. Wybierz link **Usuń piaskownicę odsprzedawcy** obok konta piaskownicy odsprzedawcy pośredniego, które chcesz usunąć. Konto piaskownicy odsprzedawcy pośredniego zostanie trwale usunięte i nie będzie można go odzyskać. 

## <a name="api-references"></a>Dokumentacja interfejsu API

- Tworzenie odsprzedawcy pośredniego 
- Usuwanie odsprzedawcy pośredniego 

 

 