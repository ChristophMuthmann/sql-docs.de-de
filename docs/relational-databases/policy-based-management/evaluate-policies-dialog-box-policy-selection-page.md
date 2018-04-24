---
title: Dialogfeld „Richtlinien auswerten“, Seite „Richtlinienauswahl“ | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 05dacf5eace0756499d007a53151abc6d90dddb5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>Dialogfeld 'Richtlinien auswerten', Seite 'Richtlinienauswahl'
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe dieses Dialogfelds können Sie richtlinienbasierte Verwaltungsrichtlinien auswerten. Durch Auswahl der Seite **Auswertungsergebnisse** können Sie Richtlinien auf die Elemente in einem Zielsatz anwenden, die mit den Richtlinien nicht übereinstimmen.  
  
## <a name="options"></a>Tastatur  
 **Quelle**  
 Gibt die Quelle der Richtlinien an. Um die Quelle zu ändern, klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um das Dialogfeld **Quelle auswählen** zu öffnen.  
  
 **Dateien**  
 Geben Sie den Pfad zu einer Datei ein, die eine richtlinienbasierte Verwaltungsrichtlinie enthält, oder klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), um die Datei auszuwählen.  
  
 **Server**  
 Wählen Sie diese Option aus, um eine Verbindung zu einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] herzustellen, die die gewünschte Richtlinie enthält.  
  
 **Richtlinien: Richtlinie**  
 Klicken Sie, um das Dialogfeld für die angegebene Richtlinie zu öffnen.  
  
 **Richtlinien: Kategorie**  
 Die Kategorie der Richtlinie. Dieses Feld ist schreibgeschützt.  
  
 **Richtlinien: Facet**  
 Das von der Richtlinie implementierte Facet. Dieses Feld ist schreibgeschützt.  
  
 **Auswerten**  
 Führt die Richtlinie im Auswertungsmodus aus. Dadurch wird ein Kompatibilitätsbericht für den Zielsatz generiert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird jedoch nicht neu konfiguriert, und es wird auch keine zukünftige Kompatibilität durchgesetzt.  
  
## <a name="possible-errors"></a>Mögliche Fehler  
  
-   **Keine Ziele gefunden**  
  
     Der Zielsatz könnte aus einem der folgenden Gründe leer sein:  
  
    -   Auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] des von der Richtlinie angegebenen Typs sind keine Ziele vorhanden.  
  
    -   Die Servereinschränkung könnte die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , die das Ziel enthält, ausschließen.  
  
    -   Wenn sich die Richtlinie auf einem Objekt in einer Datenbank (z. B. einer Tabelle, einer Ansicht oder einem Benutzer befindet), kann die Datenbank die Kategorie der Richtlinie möglicherweise nicht abonnieren.  
  
    -   Der Zielsatzfilter könnte alle Ziele auf dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausschließen.  
  
    -   Der Typ des Zielservers unterscheidet sich dem des Servers, auf dem die Richtlinie ausgewertet wird. Wenn Sie in [!INCLUDE[ssDE](../../includes/ssde-md.md)]beispielsweise versuchen, eine Richtlinie auszuwerten, die für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erstellt wurde, erhalten Sie einen leeren Zielsatz.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Dialogfeld 'Richtlinien auswerten', Seite 'Auswertungsergebnisse'](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  
