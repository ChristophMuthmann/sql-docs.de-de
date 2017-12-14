---
title: Laden von Daten mithilfe des OLE DB-Ziels | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- loading data
- OLE DB destination [Integration Services]
- destinations [Integration Services], OLE DB
ms.assetid: 78899498-725e-4300-a7af-f983f4ea384b
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e97279231fbdefb263d071d6b6f0a2d975104247
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="load-data-by-using-the-ole-db-destination"></a>Laden von Daten mithilfe des OLE DB-Ziels
  Das Paket muss bereits mindestens einen Datenflusstask und eine Quelle enthalten, damit Sie ein OLE DB-Ziel hinzufügen und konfigurieren können.  
  
### <a name="to-load-data-using-an-ole-db-destination"></a>So laden Sie Daten mithilfe eines OLE DB-Zieles  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus **Toolbox**das OLE DB-Ziel auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie das OLE DB-Ziel mit dem Datenfluss, indem Sie einen Konnektor von einer Datenquelle oder einer vorherigen Transformation auf das Ziel ziehen.  
  
5.  Doppelklicken Sie auf das OLE DB-Ziel.  
  
6.  Wählen Sie im Dialogfeld **Ziel-Editor für OLE DB** auf der Seite **Verbindungs-Manager** einen vorhandenen OLE DB-Verbindungs-Manager aus, oder klicken Sie auf **Neu** , um einen neuen Verbindungs-Manager zu erstellen. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Wählen Sie die Datenzugriffsmethode aus:  
  
    -   **Tabelle oder Sicht** Wählen Sie eine Tabelle oder Sicht in der Datenbank aus, die die Daten enthält.  
  
    -   **Tabelle oder Sicht – schnelles Laden** Wählen Sie eine Tabelle oder Sicht in der Datenbank aus, die die Daten enthält, und legen Sie dann die Optionen für schnelles Laden fest: **Identität beibehalten**, **NULL-Werte beibehalten**, **Tabellensperre**, **Einschränkungen überprüfen**, **Zeilen pro Batch**oder **Maximale Einfügungscommitgröße**.  
  
    -   **Variable für Tabellenname oder Sichtname** Wählen Sie die benutzerdefinierte Variable aus, die den Namen einer Tabelle oder Sicht in der Datenbank enthält.  
  
    -   **Variable für Tabellenname oder Sichtname – schnelles Laden** Wählen Sie die benutzerdefinierte Variable aus, die den Namen einer Tabelle oder Sicht in der Datenbank enthält, in der die Daten gespeichert sind, und legen Sie dann die Optionen für schnelles Laden fest.  
  
    -   **SQL-Befehl** Geben Sie einen SQL-Befehl ein, oder klicken Sie auf **Abfrage erstellen** , um mit **Abfrage-Generator**einen SQL-Befehl zu erstellen.  
  
8.  Klicken Sie auf **Zuordnungen** , und ordnen Sie Spalten aus der Liste **Verfügbare Eingabespalten** Spalten in der Liste **Verfügbare Zielspalten** zu, indem Sie Spalten von einer Liste in eine andere Liste ziehen.  
  
    > [!NOTE]  
    >  Vom OLE DB-Ziel werden automatisch gleichnamige Spalten zugeordnet.  
  
9. Klicken Sie auf **Fehlerausgabe**, um die Fehlerausgabe zu konfigurieren. Weitere Informationen finden Sie unter [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
10. Klicken Sie auf **OK**.  
  
11. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Ziel](../../integration-services/data-flow/ole-db-destination.md)   
 [SQL Server Integration Services-Transformationen](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services Paths](../../integration-services/data-flow/integration-services-paths.md)  (Integration Services-Pfade)  
 [Datenflusstask](../../integration-services/control-flow/data-flow-task.md)  
  
  
