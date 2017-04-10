---
title: "Anzeigen eines SQL Server-&#220;berwachungsprotokolls | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Überwachungen [SQL Server], Anzeigen von Protokollen"
  - "Anzeigen von Überwachungsprotokollen"
  - "Protokolle [SQL Server], Überwachung"
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Anzeigen eines SQL Server-&#220;berwachungsprotokolls
  In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]ein SQL Server-Überwachungsprotokoll anzeigen können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **So zeigen Sie ein SQL Server-Überwachungsprotokoll an mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die **CONTROL SERVER** -Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### So zeigen Sie ein SQL Server-Überwachungsprotokoll an  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner **Sicherheit** .  
  
2.  Erweitern Sie den Ordner **Überwachungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf das Überwachungsprotokoll, das Sie anzeigen möchten, und klicken Sie auf **Überwachungsprotokolle anzeigen**. Dadurch wird das Dialogfeld **Protokolldatei-Viewer –***Servername* geöffnet. Weitere Informationen finden Sie unter [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md).  
  
4.  Wenn Sie fertig sind, klicken Sie auf **Schließen**.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfiehlt, das Überwachungsprotokoll mit dem Protokolldatei-Viewer anzuzeigen. Wenn Sie jedoch ein automatisiertes Überwachungssystem erstellen, können die Informationen in der Überwachungsdatei direkt mit der Funktion [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) gelesen werden. Beim direkten Lesen der Datei werden die Daten in einem etwas anderen (unverarbeiteten) Format zurückgegeben. Weitere Informationen finden Sie unter **sys.fn_get_audit_file**.  
  
## Siehe auch  
 [SQL Server Audit &#40;Datenbankmodul&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Schreiben von SQL-Serverüberwachungsereignissen in das Sicherheitsprotokoll](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  