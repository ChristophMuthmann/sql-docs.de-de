---
title: "Schritt 3: Hinzufügen und konfigurieren einen OLE DB-Verbindungs-Manager | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: e7b74cba-a0e5-4478-af12-3f81b9484e9e
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 252ca86357f628b5b859c248bf13b1fea5bfcf75
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-3---adding-and-configuring-an-ole-db-connection-manager"></a>Lektion 1 bis 3-hinzufügen und konfigurieren einen OLE DB-Verbindungs-Manager
Nach dem Hinzufügen eines Flatfile-Verbindungs-Managers zum Herstellen einer Verbindung mit der Datenquelle besteht die nächste Aufgabe im Hinzufügen eines OLE DB-Verbindungs-Managers zum Herstellen einer Verbindung mit dem Ziel. Ein OLE DB-Verbindungs-Manager ermöglicht einem Paket das Extrahieren von Daten aus einer oder das Laden von Daten in eine OLE DB-kompatible(n) Datenquelle. Mithilfe des OLE DB-Verbindungs-Managers können Sie den Server, die Authentifizierungsmethode und die Standarddatenbank für die Verbindung angeben.  
  
In dieser Lektion erstellen Sie einen OLE DB-Verbindungs-Manager, der die Windows-Authentifizierung zum Herstellen einer Verbindung mit der lokalen Instanz von **AdventureWorksDB2012**verwendet. Der von Ihnen erstellte OLE DB-Verbindungs-Manager wird auch von anderen Komponenten referenziert, die Sie später in diesem Lernprogramm erstellen werden. Dazu gehören die Transformation zum Suchen und das OLE DB-Ziel.  
  
### <a name="add-and-configure-an-ole-db-connection-manager-to-the-ssis-package"></a>Hinzufügen und Konfigurieren eines OLE DB-Verbindungs-Managers zum SSIS-Paket  
  
1.  Klicken Sie mit der rechten Maustaste auf eine beliebige Stelle im **Verbindungs-Manager** -Bereich und anschließend auf **Neue OLE DB-Verbindung**.  
  
2.  Klicken Sie im Dialogfeld **OLE DB-Verbindungs-Manager konfigurieren** auf **Neu**.  
  
3.  Geben Sie für **Servername**den Namen **localhost**ein.  
  
    Wenn Sie localhost als Servernamen angeben, stellt der Verbindungs-Manager eine Verbindung mit der Standardinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf dem lokalen Computer her. Wenn Sie eine Remoteinstanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]verwenden möchten, ersetzen Sie localhost durch den Namen des Servers, mit dem Sie eine Verbindung herstellen möchten.  
  
4.  Überprüfen Sie in der Gruppe **Am Server anmelden** , ob **Windows-Authentifizierung verwenden** ausgewählt ist.  
  
5.  Geben Sie in der Gruppe **Mit Datenbank verbinden** im Feld **Datenbanknamen eingeben oder auswählen** den Wert **AdventureWorksDW2012**ein, oder wählen Sie ihn aus.  
  
6.  Klicken Sie auf **Verbindung testen** , um zu überprüfen, ob die von Ihnen angegebenen Verbindungseinstellungen gültig sind.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie auf **OK**.  
  
9. Überprüfen Sie im Dialogfeld **OLE DB-Verbindungs-Manager konfigurieren** im Bereich **Datenverbindungen** , ob **localhost.AdventureWorksDW2012** ausgewählt ist.  
  
10. Klicken Sie auf **OK**.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Schritt 4: Hinzufügen eines Datenflusstasks zum Paket](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
## <a name="see-also"></a>Siehe auch  
[OLE DB-Verbindungs-Manager](../integration-services/connection-manager/ole-db-connection-manager.md)  
  

