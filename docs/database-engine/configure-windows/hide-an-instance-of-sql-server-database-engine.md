---
title: "Ausblenden einer Instanz des SQL Server-Datenbankmoduls | Microsoft Docs"
ms.custom: ""
ms.date: "08/19/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbankmodul [SQL Server], Ausblenden von Instanzen"
  - "Ausblenden von Instanzen des Datenbankmoduls"
ms.assetid: 392de21a-57fa-4a69-8237-ced8ca86ed1d
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Ausblenden einer Instanz des SQL Server-Datenbankmoduls
  In diesem Thema wird beschrieben, wie Sie eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe des SQL Server-Konfigurations-Managers ausblenden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browser-Dienst zum Aufzählen der Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] , die auf dem Computer installiert sind. Auf diese Weise können Clientanwendungen nach einem Server suchen, und Clients wird die Unterscheidung zwischen mehreren Instanzen von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf dem gleichen Computer vereinfacht. Sie können die folgende Prozedur verwenden, um zu verhindern, dass der SQL Server Browser-Dienst eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] für Clientcomputer verfügbar macht, die versuchen, die Instanz durch Auswahl der Schaltfläche **Durchsuchen** zu finden.  
  
##  <a name="SSMSProcedure"></a> Verwenden des SQL Server-Konfigurations-Managers  
  
#### So blenden Sie eine Instanz des SQL Server-Datenbankmoduls aus:  
  
1.  Erweitern Sie im **SQL Server-Konfigurations-Manager** den Eintrag **SQL Server-Netzwerkkonfiguration**, klicken Sie mit der rechten Maustaste auf **Protokolle für ** *<Serverinstanz>\>*, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Aktivieren Sie auf der Registerkarte **Flags** im Feld **HideInstance** die Option **Ja**, und klicken Sie dann auf **OK** , um das Dialogfeld zu schließen. Die Änderung wird für neue Verbindungen sofort wirksam.  
  
## Hinweise  
 Wenn Sie eine benannte Instanz ausblenden, müssen Sie die Portnummer in der Verbindungszeichenfolge angeben, um eine Verbindung mit der ausgeblendeten Instanz herzustellen, auch bei ausgeführtem Browserdienst. Sie sollten für die ausgeblendete benannte Instanz einen statischen Port anstelle eines dynamischen Ports verwenden.  
  Weitere Informationen finden Sie unter [Konfigurieren eines Servers zur Überwachung eines bestimmten TCP-Ports &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/configure a server to listen on a specific tcp port.md).  
  
### Clustering  
 Wenn Sie ein benannte Clusterinstanz ausblenden, ist der Clusterdienst möglicherweise nicht imstande, eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]herzustellen. Dies führt zu einem Fehler bei der **IsAlive** -Prüfung der Clusterinstanz, daraufhin wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offline gesetzt. Es empfiehlt sich, in allen Knoten einen Alias der Clusterinstanz zu erstellen, um den statischen Port anzugeben, den Sie für die Instanz konfiguriert haben.  
 Weitere Informationen finden Sie unter [Erstellen oder Löschen eines Serveralias für die Verwendung durch einen Client &#40;SQL Server-Konfigurations-Manager&#41;](../../database-engine/configure-windows/create or delete a server alias for use by a client.md).  
  
 Wenn Sie eine benannte Clusterinstanz ausblenden, kann der Clusterdienst möglicherweise keine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen, wenn der Registrierungsschlüssel **LastConnect** (**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI11.0\LastConnect**) einen anderen Port als den von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] überwachten Port angibt. Wenn der Clusterdienst keine Verbindung mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen kann, wird möglicherweise ein Fehler wie der Folgende angezeigt:  
**Ereignis-ID: 1001: Ereignisname: Gegenseitiges Sperren von Failoverclusterressourcen.**  
  
## Siehe auch  
 [Server-Netzwerkkonfiguration](../../database-engine/configure-windows/server-network-configuration.md)   
 [Beschreibung der Clientverbindungen mit einem virtuellen SQL Server](https://support.microsoft.com/kb/273673)   
 [Zuweisen eines statischen Ports zu einer benannten SQL Server-Instanz – und Vermeiden eines häufigen Fehlers](http://blogs.msdn.com/b/arvindsh/archive/2012/09/08/how-to-assign-a-static-port-to-a-sql-server-named-instance-and-avoid-a-common-pitfall.aspx)  
  
  