---
title: Ein SQL Server-Überwachungsprotokoll anzeigen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1b1f2528b4dd6c247c37f7c1d33b91ce32b52366
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-a-sql-server-audit-log"></a>Anzeigen eines SQL Server-Überwachungsprotokolls
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]ein SQL Server-Überwachungsprotokoll anzeigen können.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So zeigen Sie ein SQL Server-Überwachungsprotokoll an mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die **CONTROL SERVER** -Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>So zeigen Sie ein SQL Server-Überwachungsprotokoll an  
  
1.  Erweitern Sie im Objekt-Explorer den Ordner **Sicherheit** .  
  
2.  Erweitern Sie den Ordner **Überwachungen** .  
  
3.  Klicken Sie mit der rechten Maustaste auf das Überwachungsprotokoll, das Sie anzeigen möchten, und klicken Sie auf **Überwachungsprotokolle anzeigen**. Dadurch wird das Dialogfeld **Protokolldatei-Viewer –***server_name* geöffnet. Weitere Informationen finden Sie unter [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md).  
  
4.  Wenn Sie fertig sind, klicken Sie auf **Schließen**.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] empfiehlt, das Überwachungsprotokoll mit dem Protokolldatei-Viewer anzuzeigen. Wenn Sie jedoch ein automatisiertes Überwachungssystem erstellen, können die Informationen in der Überwachungsdatei direkt mit der Funktion [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) gelesen werden. Beim direkten Lesen der Datei werden die Daten in einem etwas anderen (unverarbeiteten) Format zurückgegeben. Weitere Informationen finden Sie unter **sys.fn_get_audit_file** .  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Audit &#40;Datenbankmodul&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Schreiben von SQL-Serverüberwachungsereignissen in das Sicherheitsprotokoll](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  
