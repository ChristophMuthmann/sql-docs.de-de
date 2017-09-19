---
title: "Reservierte Wörter (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
caps.latest.revision: 11
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: af5326c054f80b376e43db0d18dfeb2b9ef85997
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="reserved-words-master-data-services"></a>Reservierte Wörter (Master Data Services)
  Wenn Sie Modellobjekte oder Elemente erstellen, können in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]einige Wörter nicht verwendet werden. Die Verwendung dieser Wörter verursacht möglicherweise Fehler.  
  
> [!NOTE]  
>  Sie sollten auch die Verwendung von Sonderzeichen (Symbole, Silbentrennung usw.) einschränken.  
  
-   [Modelle](../master-data-services/reserved-words-master-data-services.md#models)  
  
-   [Entitäten](../master-data-services/reserved-words-master-data-services.md#entities)  
  
-   [Explizite Hierarchien](../master-data-services/reserved-words-master-data-services.md#exhierarchies)  
  
-   [Attribute](../master-data-services/reserved-words-master-data-services.md#attributes)  
  
-   [Element](../master-data-services/reserved-words-master-data-services.md#members)  
  
##  <a name="models"></a> Modelle  
 Wenn Sie ein Modell erstellen, dessen Name auf **Name** oder **Code**festgelegt ist, darf **Entität mit demselben Namen wie das Modell erstellen** nicht ausgewählt werden, weil **Name** oder **Code** nicht für den Namen einer Entität verwendet werden kann.  
  
##  <a name="entities"></a> Entitäten  
 **Name** oder **Code**kann für Entitätsnamen nicht verwendet werden.  
  
##  <a name="exhierarchies"></a> Explizite Hierarchien  
 Für explizite Hierarchienamen können Sie **Name** oder **Code**verwenden.  
  
##  <a name="attributes"></a> Attribute  
  
-   **ID**  
  
-   **Code**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
-   **Name**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> Element  
 Bei Elementen kann **MDMMemberStatus**, **MDMUnused**oder **ROOT** nicht für den Attributwert **Code** verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
  
