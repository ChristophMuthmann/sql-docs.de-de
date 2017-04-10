---
title: "Editor f&#252;r den Task Anmeldungen &#252;bertragen (Seite Anmeldungen) | Microsoft Docs"
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
  - "sql13.dts.designer.transferloginstask.logins.f1"
helpviewer_keywords: 
  - "Editor für den Task Anmeldungen übertragen"
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Editor f&#252;r den Task Anmeldungen &#252;bertragen (Seite Anmeldungen)
  Verwenden Sie die Seite **Anmeldungen** des Dialogfelds **Editor für den Task 'Anmeldungen übertragen'** , um die Eigenschaften für das Kopieren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen von einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in eine andere anzugeben. Weitere Informationen zu diesem Task finden Sie unter [Transfer Logins Task](../../integration-services/control-flow/transfer-logins-task.md).  
  
> [!IMPORTANT]  
>  Wenn der Task Anmeldungen übertragen ausgeführt wird, werden auf dem Zielserver Anmeldungen mit zufällig erzeugten Kennwörtern erstellt, und die Kennwörter werden deaktiviert. Um diese Anmeldungen zu verwenden, muss ein Mitglied der festen Serverrolle **sysadmin** die Kennwörter ändern und aktivieren. Die Anmeldung **sa** kann nicht übertragen werden.  
  
## enthalten  
 **SourceConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Quellserver zu erstellen.  
  
 **DestinationConnection**  
 Wählen Sie in der Liste einen SMO-Verbindungs-Manager aus, oder klicken Sie auf **\<Neue Verbindung...>**, um eine neue Verbindung mit dem Zielserver zu erstellen.  
  
 **LoginsToTransfer**  
 Wählen Sie die vom Quell- auf den Zielserver zu kopierenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen aus. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**AllLogins**|Alle auf dem Quellserver vorhandenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldungen werden auf den Zielserver kopiert.|  
|**SelectedLogins**|Nur die mit **LoginsList** angegebenen Anmeldungen werden auf den Zielserver kopiert.|  
|**AllLoginsFromSelectedDatabases**|Alle Anmeldungen aus den mit **DatabasesList** angegebenen Datenbanken werden auf den Zielserver kopiert.|  
  
 **LoginsList**  
 Wählen Sie die auf dem Quellserver vorhandenen Anmeldungen aus, die auf den Zielserver kopiert werden sollen. Diese Option ist nur verfügbar, wenn für **LoginsToTransfer** **SelectedLogins**ausgewählt ist.  
  
 **DatabasesList**  
 Wählen Sie die auf dem Quellserver vorhandenen Datenbanken aus, die Anmeldungen enthalten, die auf den Zielserver kopiert werden sollen. Diese Option ist nur verfügbar, wenn für **LoginsToTransfer** **AllLoginsFromSelectedDatabases**ausgewählt ist.  
  
 **IfObjectExists**  
 Wählen Sie aus, wie der Task Anmeldungen behandeln soll, die auf dem Zielserver bereits mit demselben Namen vorhanden sind.  
  
 Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|Wert|Description|  
|-----------|-----------------|  
|**FailTask**|Der Task schlägt fehl, wenn auf dem Zielserver bereits Anmeldungen mit demselben Namen vorhanden sind.|  
|**Overwrite**|Der Task überschreibt auf dem Zielserver Anmeldungen mit demselben Namen.|  
|**Skip**|Der Task lässt Anmeldungen aus, die auf dem Zielserver mit demselben Namen vorhanden sind.|  
  
 **CopySids**  
 Wählen Sie aus, ob die den Anmeldungen zugeordneten Sicherheits-IDs auf den Zielserver kopiert werden sollen. **CopySids** muss auf **True** festgelegt sein, wenn der Task Anmeldungen übertragen zusammen mit dem Task Datenbanken übertragen verwendet wird. Anderenfalls werden die kopierten Anmeldungen von der übertragenen Datenbank nicht erkannt.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services-Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Editor für den Task „Anmeldungen übertragen“ &#40;Seite „Allgemein“&#41;](../../integration-services/control-flow/transfer-logins-task-editor-general-page.md)   
 [Seite Ausdrücke](../../integration-services/expressions/expressions-page.md)   
 [SMO-Verbindungs-Manager](../../integration-services/connection-manager/smo-connection-manager.md)   
 [Sichere Kennwörter](../../relational-databases/security/strong-passwords.md)   
 [Überlegungen zur Sicherheit bei SQL Server-Installationen](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  