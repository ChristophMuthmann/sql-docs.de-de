---
title: "Cacheverbindungs-Manager | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Cacheverbindungs-Manager"
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Cacheverbindungs-Manager
  Der Cacheverbindungs-Manager liest Daten aus der Cachetransformation oder einer Cachedatei (.caw) und kann die Daten in einer Cachedatei speichern. Unabhängig davon, ob der Cacheverbindungs-Manager für die Verwendung einer Cachedatei konfiguriert ist, werden die Daten stets im Arbeitsspeicher gespeichert.  
  
 Mit der Transformation für Cachetransformation können Daten aus einer verbundenen Datenquelle im Datenfluss in einen Cacheverbindungs-Manager geschrieben werden. Die Transformation für Suche in einem Paket führt Suchvorgänge in den Daten aus.  
  
> [!NOTE]  
>  Der Cacheverbindungs-Manager unterstützt die BLOB-Datentypen (Binary Large Object) DT_TEXT, DT_NTEXT und DT_IMAGE nicht. Wenn das Verweisdataset einen BLOB-Datentyp enthält, schlägt die Komponente fehl, wenn Sie das Paket ausführen. Sie können den **Cacheverbindungs-Manager-Editor** verwenden, um Spaltendatentypen zu ändern. Weitere Informationen finden Sie unter [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md).  
  
> [!NOTE]  
>  Die Schutzebene des Pakets gilt nicht für die Cachedatei. Wenn die Cachedatei vertrauliche Informationen enthält, schränken Sie den Zugriff auf den Speicherort oder Ordner, in dem Sie die Datei speichern, mithilfe einer Zugriffssteuerungsliste ein. Sie sollten nur bestimmten Konten den Zugriff ermöglichen. Weitere Informationen finden Sie unter [Zugriff auf Dateien, die von Paketen verwendet werden](../../../integration-services/security/access-to-files-used-by-packages.md).  
  
## Konfiguration des Cacheverbindungs-Managers  
 Es gibt folgende Möglichkeiten, um den Cacheverbindungs-Manager zu konfigurieren:  
  
-   Geben Sie an, ob eine Cachedatei verwendet werden soll.  
  
     Wenn Sie den Cacheverbindungs-Manager für die Verwendung einer Cachedatei konfigurieren, führt der Verbindungs-Manager eine der folgenden Aktionen aus:  
  
    -   Speichern der Daten in einer Datei, wenn eine Cachetransformation so konfiguriert ist, dass Daten aus einer Datenquelle im Datenfluss in den Cacheverbindungs-Manager geschrieben werden.  
  
    -   Lesen von Daten aus der Cachedatei  
  
     Weitere Informationen finden Sie unter [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Ändern Sie die Metadaten der im Cache gespeicherten Spalten.  
  
-   Aktualisieren Sie den Cachedateinamen zur Laufzeit mithilfe eines Ausdrucks zum Festlegen der „ConnectionString“-Eigenschaft. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Designer festlegen können, finden Sie unter [Cacheverbindungs-Manager-Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md).  
  
 Weitere Informationen zum programmgesteuerten Konfigurieren eines Verbindungs-Managers finden Sie unter <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> und unter [Programmgesteuertes Hinzufügen von Verbindungen](../../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## Verwandte Aufgaben  
 [Implementieren einer Suchtransformation im Vollcachemodus mit dem Cacheverbindungs-Manager](../../../integration-services/data-flow/transformations/lookup transformation full cache mode - cache connection manager.md)  
  
  