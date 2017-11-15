---
title: "Veröffentlichen einer Datenbank (SQL Server Management Studio) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98b2914e-7147-40af-ba7d-87253bbe8bf9
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 17a79ced336be18f0a83bba5b18a432eb24bbdd5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="publish-a-database-sql-server-management-studio"></a>Veröffentlichen einer Datenbank (SQL Server Management Studio)
  Mit dem **Assistenten zum Generieren und Veröffentlichen von Skripts** können Sie eine ganze Datenbank oder einzelne Datenbankobjekte in einem Webhostinganbieter veröffentlichen.  
  
> [!NOTE]  
>  Die in diesem Thema beschriebene Funktionalität wurde früher vom Datenbankveröffentlichungs-Assistenten bereitgestellt. Dessen Veröffentlichungsfunktionalität wurde dem Assistenten zum Generieren und Veröffentlichen von Skripts hinzugefügt, und der Datenbankveröffentlichungs-Assistent wird in der alten Form nicht mehr bereitgestellt.  
  
## <a name="generate-and-publish-scripts-wizard"></a>Assistenten zum Generieren und Veröffentlichen von Skripts  
 Der Assistent zum Generieren und Veröffentlichen von Skripts kann verwendet werden, um eine Datenbank oder ausgewählte Datenbankobjekte in einem Webhostinganbieter zu veröffentlichen. Ein SQL Server-Webhostinganbieter ist eine Konnektivitätsschnittstelle zu einem Webdienst. Der Webdienst wird mithilfe eines Datenbank-Veröffentlichungsdienste-Projekts vom SQL Server Hosting Toolkit aus auf der CodePlex-Website erstellt. Mithilfe des Webdiensts können Webhoster-Kunden ihre Datenbanken problemlos im Dienst veröffentlichen. Sie verwenden dazu den Assistenten zum Generieren und Veröffentlichen von Skripts. Weitere Informationen zum Herunterladen des SQL Server Hosting Toolkits finden Sie unter [SQL Server Database Publishing Services](http://go.microsoft.com/fwlink/?LinkId=142025).  
  
 Der Assistent zum Generieren und Veröffentlichen von Skripts kann außerdem verwendet werden, um ein Skript zum Übertragen einer Datenbank zu erstellen.  
  
#### <a name="to-publish-a-database-to-a-web-service"></a>So veröffentlichen Sie eine Datenbank in einem Webdienst  
  
1.  Erweitern Sie im Objekt-Explorer **Datenbanken**, klicken Sie mit der rechten Maustaste auf eine Datenbank, zeigen Sie auf **Tasks**, und klicken Sie dann auf **Skripts generieren und veröffentlichen**. Führen Sie die im Assistenten angegebenen Schritte aus, um ein Skript für die Veröffentlichung der Datenbankobjekte zu erstellen.  
  
2.  Wählen Sie auf der Seite **Objekte auswählen** die Objekte aus, die im Webhostingdienst veröffentlicht werden sollen.  
  
3.  Wählen Sie auf der Seite **Skriptoptionen festlegen** die Option **In Webdienst veröffentlichen**aus.  
  
    1.  Geben Sie im Feld **Anbieter** den Anbieter für den Webdienst an. Wenn Sie keinen Webhostinganbieter konfiguriert haben, wählen Sie **Anbieter verwalten** aus und verwenden das Dialogfeld **Anbieter verwalten** , um einen Anbieter für den Webdienst zu konfigurieren.  
  
    2.  Um erweiterte Veröffentlichungsoptionen anzugeben, klicken Sie im Abschnitt **In Webdienst veröffentlichen** auf die Schaltfläche **Erweitert** .  
  
4.  Überprüfen Sie die Auswahl auf der Seite **Zusammenfassung** . Klicken Sie auf **Zurück** , um die Auswahl zu ändern. Klicken Sie auf **Weiter** , um die ausgewählten Objekte zu veröffentlichen.  
  
5.  Überwachen Sie auf der Seite **Skripts speichern oder veröffentlichen** den Status der Veröffentlichung.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen von Skripts &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)   
 [Kopieren von Datenbanken auf andere Server](../../relational-databases/databases/copy-databases-to-other-servers.md)  
  
  
