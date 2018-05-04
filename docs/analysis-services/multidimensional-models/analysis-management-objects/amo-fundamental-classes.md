---
title: Grundlegende AMO-Klassen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ffa7973757ce41a3975bcbb70170679109527e42
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="amo-fundamental-classes"></a>Grundlegende AMO-Klassen
  Grundlegende Klassen sind der Ausgangspunkt für die Verwendung von Analysis Management Objects (AMO). Mithilfe dieser Klassen erstellen Sie Ihre Umgebung für die übrigen Objekte, die in Ihrer Anwendung verwendet werden. Grundlegende Klassen beinhalten die folgenden Objekte: <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource> und <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
 Die folgende Abbildung zeigt die Beziehung der in diesem Thema erläuterten Klassen.  
  
 ![Grundlegende AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-fundamentalclasses.gif "grundlegende AMO-Klassen")  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Serverobjekte](#ServerObjects)  
  
-   [Datenbankobjekte](#DatabaseObjects)  
  
-   [DataSource und DataSourceView-Objekte](#DSandDSV)  
  
##  <a name="ServerObjects"></a> Serverobjekte  
 Darüber hinaus haben Sie Zugriff auf die folgenden Methoden:  
  
-   Verbindungsverwaltung: Connect, Disconnect, Reconnect und GetConnectionState.  
  
-   Transaktionsverwaltung: BeginTransaction, CommitTransaction und RollbackTransaction.  
  
-   Backup und Restore.  
  
-   DDL-Ausführung: Execute, CancelCommand, SendXmlaRequest, StartXmlaRequest.  
  
-   Metadaten-Verwaltung: UpdateObjects und Validate.  
  
 Um eine Verbindung mit einem Server herzustellen, benötigen Sie eine Standardverbindungszeichenfolge, wie sie in ADOMD.NET und OLEDB verwendet wird. Weitere Informationen finden Sie unter <xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>. Der Name des Servers kann als Verbindungszeichenfolge angegeben werden, ohne dass ein Format für Verbindungszeichenfolgen verwendet werden muss.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Server> in der <xref:Microsoft.AnalysisServices>.  
  
##  <a name="DatabaseObjects"></a> Datenbankobjekte  
 Wenn Sie in Ihrer Anwendung mit einem <xref:Microsoft.AnalysisServices.Database>-Objekt arbeiten möchten, müssen Sie eine Instanz der Datenbank von der übergeordneten Serverdatenbankauflistung abrufen. Zum Erstellen einer Datenbank fügen Sie einer Serverdatenbankauflistung ein <xref:Microsoft.AnalysisServices.Database>-Objekt hinzu und aktualisieren die neue Instanz auf dem Server. Zum Löschen einer Datenbank löschen Sie das <xref:Microsoft.AnalysisServices.Database>-Objekt mithilfe seiner eigenen Drop-Methode.  
  
 Datenbanken können mithilfe der BackUp-Methode (über das <xref:Microsoft.AnalysisServices.Database>- oder <xref:Microsoft.AnalysisServices.Server>-Objekt) gesichert werden. Sie können jedoch nur über das <xref:Microsoft.AnalysisServices.Server>-Objekt mithilfe der Restore-Methode wiederhergestellt werden.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Database> in der <xref:Microsoft.AnalysisServices>.  
  
##  <a name="DSandDSV"></a> DataSource und DataSourceView-Objekte  
 Datenquellen werden mithilfe der <xref:Microsoft.AnalysisServices.DataSourceCollection> über die Datenbankklasse verwaltet. Eine Instanz von <xref:Microsoft.AnalysisServices.DataSource> kann mithilfe der Add-Methode über ein <xref:Microsoft.AnalysisServices.DataSourceCollection>-Objekt erstellt werden. Eine Instanz von <xref:Microsoft.AnalysisServices.DataSource> kann mithilfe der Remove-Methode über ein <xref:Microsoft.AnalysisServices.DataSourceCollection>-Objekt gelöscht werden.  
  
 <xref:Microsoft.AnalysisServices.DataSourceView>-Objekte werden über das <xref:Microsoft.AnalysisServices.DataSourceViewCollection>-Objekt in der Datenbankklasse verwaltet.  
  
 Weitere Informationen zu den verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.DataSource> und <xref:Microsoft.AnalysisServices.DataSourceView> in <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programmieren AMO Fundamental Objects](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-fundamental-objects.md)  
  
  
