---
title: Starten des Hilfsprogramms „sqlcmd“ | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
caps.latest.revision: 41
author: mightypen
ms.author: genemi
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d50eea710cfe23ff59c018b0e1154bab17ba3183
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlcmd---start-the-utility"></a>Starten des Hilfsprogramms „sqlcmd“
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Mit dem Hilfsprogramm [sqlcmd](../../tools/sqlcmd-utility.md) können Sie an der Eingabeaufforderung, im Abfrage-Editor im SQLCMD-Mode, in einer Windows-Skriptdatei oder in einem Auftragsschritt des Betriebssystems (Cmd.exe) eines [!INCLUDE[tsql](../../includes/tsql-md.md)] -Agent-Auftrags [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anweisungen, Systemprozeduren und Skriptdateien eingeben.
> [!NOTE]  
>  Die Windows-Authentifizierung ist der Standardauthentifizierungsmodus für **sqlcmd**. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwenden möchten, müssen Sie einen Benutzernamen und ein Kennwort angeben. Verwenden Sie hierzu die Optionen **-U** und **-P** .  
  
> [!NOTE]  
>  Standardmäßig wird [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] als die benannte Instanz **sqlexpress**installiert.  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>Starten des Hilfsprogramms "sqlcmd" und Herstellen einer Verbindung mit einer Standardinstanz von SQL Server  
  
1.  Klicken Sie im **Startmenü** auf **Ausführen**. Geben Sie im Feld **Öffnen** den Befehl **cmd**ein, und klicken Sie auf **OK** , um ein Eingabeaufforderungsfenster zu öffnen. (Wenn Sie bisher noch keine Verbindung mit dieser Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] hergestellt haben, müssen Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise so konfigurieren, dass Verbindungen akzeptiert werden.)  
  
2.  Geben Sie an der Eingabeaufforderung **sqlcmd**ein.  
  
3.  Drücken Sie die EINGABETASTE.  
  
     Sie verfügen jetzt über eine vertrauenswürdige Verbindung mit der Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf dem Computer ausgeführt wird.  
  
     **1>** ist die Eingabeaufforderung von **sqlcmd** und gibt die Zeilennummer an. Bei jedem Drücken der EINGABETASTE wird die Nummer um eins erhöht.  
  
4.  Geben Sie zum Beenden der **sqlcmd** -Sitzung an der Eingabeaufforderung von **sqlcmd** **EXIT** ein.  
  
### <a name="start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>Starten des Hilfsprogramms "sqlcmd" und Herstellen eine Verbindung mit einer benannten Instanz von SQL Server  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie **sqlcmd -S***myServer\instanceName* ein. Ersetzen Sie *myServer\Instanzname* durch den Namen des Computers und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz, mit der Sie eine Verbindung herstellen möchten.  
  
2.  Drücken Sie die EINGABETASTE.  
  
     Die Eingabeaufforderung von **sqlcmd** (1>) zeigt an, dass Sie mit der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden sind.  
  
    > [!NOTE]  
    >  Eingegebene [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen werden in einem Puffer gespeichert. Sie werden als Batch ausgeführt, wenn der Befehl "GO" erkannt wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ausführen von Transact-SQL-Skriptdateien mithilfe von sqlcmd](../../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)  
  
  
