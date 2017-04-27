---
title: Offlinezugriff auf die SQL Server-Dokumentation | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 257ed357-8cbb-43bd-b042-254be5fbb977
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1266b0249a96fbc4828b2afee9fb218682501e4d
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-documentation-offline-access"></a>Offlinezugriff auf die SQL Server-Dokumentation

Sie können die technische Dokumentation zu SQL Server 2016 offline anzeigen.
  
## <a name="prerequisites"></a>Voraussetzungen
Für den Offlinezugriff auf die technische Dokumentation zu SQL Server 2016 benötigen Sie HelpViewer 2.2, der mit folgender Software installiert wird: 
- [Visual Studio 2015 (beliebige Edition einschließlich Community)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) oder
- [SQL Server Management Studio (SSMS) April 2016 Preview (13.0.12500.29) oder höher](https://msdn.microsoft.com/library/mt238290.aspx)

Installieren Sie zunächst eines dieser Programme, bevor Sie mit den folgenden Schritten fortfahren.
  
## <a name="install-sql-server-offline-technical-documentation"></a>Installieren der technischen Offlinedokumentation zu SQL Server 

1. Installieren Sie eine beliebige Edition von Visual Studio 2015 oder SSMS April 2016 Preview Build oder höher. 
2. Starten Sie SSMS oder Visual Studio.
3. Wählen Sie im Menü **Hilfe** in der oberen Navigationsleiste die Option  **Hilfeinhalt hinzufügen und entfernen**aus. 

#### <a name="this-action-launches-the-helpviewer"></a>(Diese Aktion startet den HelpViewer)

4. Wählen Sie im HelpViewer die Standardinstallationsquelle aus: **Online** 
5. Klicken Sie neben allen Dokumentationselementen, die Sie installieren möchten, auf **Hinzufügen** .
6. Klicken Sie auf die Schaltfläche **Aktualisieren** auf rechts unten auf dem Bildschirm, um die ausgewählte Dokumentation herunterzuladen und zu installieren.
![Laden von Offlineinhalt](../sql-server/media/load-offline-content.png) 

 >** WICHTIG!!** Nachdem Sie auf Aktualisieren geklickt haben, wird HelpViewer an einem bestimmten Punkt einfrieren/hängen. Die ausgewählte Dokumentation wurde trotzdem heruntergeladen und installiert. **Zum Beheben dieses Problems**beenden Sie HelpViewer im Task-Manager, und starten Sie ihn mit Schritt 3 oben neu. Wenn HelpViewer das erste Mal einfriert/hängt, führen Sie außerdem [diese Schritte](https://msdn.microsoft.com/library/mt654096.aspx) aus. Diese Schritte müssen nur einmal ausgeführt werden, aber Sie müssen HelpViewer wahrscheinlich jedes Mal, wenn Sie Ihren Inhalt aktualisieren, im Task-Manager beenden.  
6. Starten Sie HelpViewer neu, indem Sie erneut „Hilfe“, “Inhalt hinzufügen und entfernen“ auswählen. Die Offlinedokumentation ist jetzt einsatzbereit!



   ![Offlinedokumentation ist einsatzbereit](../sql-server/media/offline-ready-to-use.png)




