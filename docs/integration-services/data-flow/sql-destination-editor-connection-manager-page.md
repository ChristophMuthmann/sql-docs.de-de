---
title: "Ziel-Editor f&#252;r SQL (Seite Verbindungs-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sqlserverdestadapter.connection.f1"
helpviewer_keywords: 
  - "Ziel-Editor für SQL"
ms.assetid: 423e1654-54af-47c6-ab6f-98670534557d
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# Ziel-Editor f&#252;r SQL (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für SQL** können Sie Informationen zur Datenquelle angeben und eine Vorschau der Ergebnisse anzeigen. Das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ziel lädt die Daten in die Tabellen oder Sichten einer Datenbank in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Weitere Informationen zum SQL Server-Ziel finden Sie unter [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md).  
  
## enthalten  
 **OLE DB-Verbindungs-Manager**  
 Wählen Sie eine vorhandene Verbindung aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu** klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OLE DB-Verbindungs-Manager konfigurieren** eine neue Verbindung.  
  
 **Tabelle oder Sicht verwenden**  
 Wählen Sie eine vorhandene Tabelle oder Sicht aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu** klicken.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **Tabelle erstellen** eine neue Tabelle.  
  
> [!NOTE]  
>  Wenn Sie auf **Neu**klicken, generiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Standard-CREATE TABLE-Anweisung auf Grundlage der verbundenen Datenquelle. Diese Standard-CREATE TABLE-Anweisung enthält nicht das FILESTREAM-Attribut, selbst wenn die Quelltabelle eine Spalte mit der Erklärung des FILESTREAM-Attributs enthält. Um eine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Komponente mit dem FILESTREAM-Attribut auszuführen, implementieren Sie zunächst die FILESTREAM-Speicherung in der Zieldatenbank. Fügen Sie dann das FILESTREAM-Attribut der CREATE TABLE-Anweisung im Dialogfeld **Tabelle erstellen** hinzu. Weitere Informationen finden Sie unter [Binary Large Object-Daten &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Vorschau der Abfrageergebnisse anzeigen** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Ziel-Editor für SQL &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)   
 [Ziel-Editor für SQL &#40;Seite „Erweitert“&#41;](../../integration-services/data-flow/sql-destination-editor-advanced-page.md)   
 [Massenladen von Daten mithilfe des SQL Server-Ziels](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  