---
title: Verwalten von Objekten mittels Objekt-Explorer | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.SWB.SQLSERVEROBJECTEXPLORER.DHELP
helpviewer_keywords:
- Object Explorer F1 Help
- OE F1 Help
- OE Help
ms.assetid: e60367a7-3fdd-40b8-82bb-9e819d78de5a
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9ef28c37c3232ad747129925c6259975b4005a40
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="manage-objects-by-using-object-explorer"></a>Verwalten von Objekten mittels Objekt-Explorer
Mit dem Objekt-Explorer können Sie Objekte, z. B. Datenbanken, Tabellen und gespeicherte Prozeduren, verwalten.  
  
## <a name="viewing-objects-in-object-explorer"></a>Anzeigen von Objekten im Objekt-Explorer  
Der Objekt-Explorer verwendet zum Gruppieren von Informationen in Ordnern eine Baumstruktur. Zum Erweitern von Ordnern klicken Sie auf das Pluszeichen (+), oder doppelklicken Sie auf den Ordner. Erweitern Sie die Ordner, um detailliertere Informationen anzuzeigen. Klicken Sie mit der rechten Maustaste auf Ordner oder Objekte, um allgemeine Aufgaben auszuführen. Doppelklicken Sie auf Objekte, um die gängigste Aufgabe auszuführen.  
  
Wenn Sie zum ersten Mal einen Ordner erweitern, startet der Objekt-Explorer an den Server eine Abfrage nach Informationen zum Auffüllen der Struktur. Sie können andere Funktionen ausführen, während die Struktur aufgefüllt wird. Während die Struktur vom Objekt-Explorer aufgefüllt wird, können Sie auf **Beenden** klicken, um den Prozess abzubrechen. Weitere Aktionen, z. B. Filtern der Liste, können nur für den Teil des Ordners ausgeführt werden, der aufgefüllt wurde, es sei denn, Sie aktualisieren den Ordner, um die Auffüllung erneut zu starten.  
  
Um Ressourcen zu sparen, wenn viele Objekte vorhanden sind, werden die Inhaltslisten der Ordner in der Struktur im Objekt-Explorer nicht automatisch aktualisiert. Um die Liste mit Objekten in einem Ordner zu aktualisieren, klicken Sie mit der rechten Maustaste auf den Ordner, und klicken Sie dann auf **Aktualisieren**.  
  
Der Objekt-Explorer kann maximal 65.536 Objekte anzeigen. Wenn die Anzahl der sichtbaren Objekte über 65.536 liegt, können Sie nicht durch weitere Objekte in der Strukturansicht des Objekt-Explorers einen Bildlauf durchführen. Zum Anzeigen weiterer Objekte im Objekt-Explorer schließen Sie nicht verwendete Knoten, oder wenden Sie Filter an, um die Anzahl der Objekte zu verringern.  
  
## <a name="filtering-the-list-of-objects-in-object-explorer"></a>Filtern der Objektliste im Objekt-Explorer  
Wenn ein Ordner eine große Anzahl an Objekten enthält, ist es möglicherweise schwierig, das gesuchte Objekt zu finden. In diesen Fällen können Sie mit der Filterfunktion des Objekt-Explorers die Liste verkleinern. Beispiel: Sie möchten in Listen mit Hunderten von Objekten nach einem bestimmten Datenbankbenutzer oder der zuletzt erstellten Tabelle suchen. Klicken Sie auf den Ordner, auf den Sie die Filterfunktion anwenden möchten, und klicken Sie dann auf die Filterschaltfläche, um das Dialogfeld **Filtereinstellungen** zu öffnen. Sie können die Liste nach Namen, Erstellungsdatum und u. U. Schema filtern und weitere Filteroperatoren verwenden, z. B. **Beginnt mit**, **Enthält**und **Zwischen**.  
  
## <a name="multi-select"></a>Mehrfachauswahl  
Im Objekt-Explorer kann nur jeweils ein Objekt ausgewählt werden. Wenn Sie mehrere Elemente auswählen möchten, drücken Sie **F7** , um die Seite **Details zum Objekt-Explorer**zu öffnen. Für die Seite **Details zum Objekt-Explorer** wird die Mehrfachauswahl unterstützt.  
  
## <a name="register-a-server-from-object-explorer"></a>Registrieren eines Servers aus dem Objekt-Explorer  
Wenn eine Verbindung mit einem Server besteht, können Sie den Server auf einfache Weise zur späteren Verwendung registrieren. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Servernamen, und klicken Sie dann auf **Registrieren**. Geben Sie im Dialogfeld **Server registrieren** an, an welcher Stelle in der Servergruppenstruktur sich der Server befinden soll. Im Feld **Servername** können Sie den Servernamen durch einen aussagekräftigeren Servernamen ersetzen. So können Sie z. B. den Server **APSQL02** mit einem aussagekräftigeren Namen, etwa**Kreditorenkonten**, registrieren.  
  
## <a name="performing-actions-on-object-explorer-nodes"></a>Ausführen von Aktionen in Objekt-Explorer-Knoten  
Sie führen Aktionen bei Objekten aus, indem Sie direkt auf den Objekt-Explorer-Knoten klicken, der das Objekt darstellt. Jeder Typ des Objekts unterstützt einen eindeutigen Satz von Rechtsklickaktionen. Sie können beispielsweise folgende Aktionstypen mithilfe des Kontextmenüs ausführen:  
  
### <a name="open-a-connected-query-editor"></a>Öffnen eines verbundenen Abfrage-Editors  
Wenn der Objekt-Explorer mit einem Server verbunden ist, können Sie mit den Verbindungseinstellungen des Objekt-Explorers ein neues Fenster des Code-Editors öffnen. Um ein neues Code-Editor-Fenster im Objekt-Explorer zu öffnen, klicken mit der rechten Maustaste auf den Servernamen, und klicken Sie dann auf **Neue Abfrage**. Um ein Code-Editor-Fenster mit einer bestimmten Datenbank zu öffnen, klicken Sie mit der rechten Maustaste auf den Datenbanknamen, und klicken Sie dann auf **Neue Abfrage**. Beim Öffnen einer neuen Abfrage für einen Server mit Analysis Services können Sie DMX-, MDX- oder XMLA-Abfragen auswählen.  
  
### <a name="start-powershell"></a>Starten von PowerShell  
Zum Starten einer PowerShell-Sitzung können Sie mit der rechten Maustaste auf den Großteil der Ordner und Objekte in der Struktur des Objekt-Explorers klicken und **PowerShell starten**auswählen. Hierdurch wird eine PowerShell-Sitzung mit aktivierter PowerShell-Unterstützung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gestartet. Gleichzeitig ist der Pfad auf den Speicherort des Objekts festgelegt, auf das Sie mit der rechten Maustaste im Objekt-Explorer geklickt haben. Sie können PowerShell-Befehle anschließend in einer interaktiven PowerShell-Umgebung eingeben. Weitere Informationen finden Sie unter [SQL Server PowerShell](http://msdn.microsoft.com/en-us/89b70725-bbe7-4ffe-a27d-2a40005a97e7).  
  
## <a name="see-also"></a>Siehe auch  
[Objekt-Explorer](../../ssms/object/object-explorer.md)  
[Öffnen und Konfigurieren des Objekt-Explorers](../../ssms/object/open-and-configure-object-explorer.md)  
[Verbinden mit einer Instanz mit dem Objekt-Explorer](../../ssms/object/connect-to-an-instance-from-object-explorer.md)  
[Detailbereich des Objekt-Explorers](../../ssms/object/object-explorer-details-pane.md)  
[Benutzerdefinierte Berichte in Management Studio](../../ssms/object/custom-reports-in-management-studio.md)  
  

