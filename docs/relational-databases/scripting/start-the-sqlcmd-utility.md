---
title: "Starten des Hilfsprogramms &quot;sqlcmd&quot; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
caps.latest.revision: 41
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Starten des Hilfsprogramms &quot;sqlcmd&quot;
    
> [!NOTE]  
>  Die Windows-Authentifizierung ist der Standardauthentifizierungsmodus für **sqlcmd**. Wenn Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung verwenden möchten, müssen Sie einen Benutzernamen und ein Kennwort angeben. Verwenden Sie hierzu die Optionen **-U** und **-P**.  
  
> [!NOTE]  
>  Standardmäßig wird [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] als die benannte Instanz **sqlexpress** installiert.  
  
### Starten des Hilfsprogramms "sqlcmd" und Herstellen einer Verbindung mit einer Standardinstanz von SQL Server  
  
1.  Klicken Sie im **Startmenü** auf **Ausführen**. Geben Sie im Feld **Öffnen** den Befehl **cmd** ein, und klicken Sie auf **OK**, um ein Eingabeaufforderungsfenster zu öffnen. (Wenn Sie bisher noch keine Verbindung mit dieser Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] hergestellt haben, müssen Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] möglicherweise so konfigurieren, dass Verbindungen akzeptiert werden.)  
  
2.  Geben Sie an der Eingabeaufforderung **sqlcmd** ein.  
  
3.  Drücken Sie die EINGABETASTE.  
  
     Sie verfügen jetzt über eine vertrauenswürdige Verbindung mit der Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], die auf dem Computer ausgeführt wird.  
  
     **1>** ist die Eingabeaufforderung von **sqlcmd** und gibt die Zeilennummer an. Bei jedem Drücken der EINGABETASTE wird die Nummer um eins erhöht.  
  
4.  Geben Sie zum Beenden der **sqlcmd**-Sitzung an der Eingabeaufforderung von **sqlcmd** **EXIT** ein.  
  
### Starten des Hilfsprogramms "sqlcmd" und Herstellen eine Verbindung mit einer benannten Instanz von SQL Server  
  
1.  Öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie **sqlcmd -S***myServer\Instanzname* ein. Ersetzen Sie *myServer\Instanzname* durch den Namen des Computers und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, mit der Sie eine Verbindung herstellen möchten.  
  
2.  Drücken Sie die EINGABETASTE.  
  
     Die Eingabeaufforderung von **sqlcmd** (1>) zeigt an, dass Sie mit der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbunden sind.  
  
    > [!NOTE]  
    >  Eingegebene [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen werden in einem Puffer gespeichert. Sie werden als Batch ausgeführt, wenn der Befehl "GO" erkannt wird.  
  
## Siehe auch  
 [Ausführen von Transact-SQL-Skriptdateien mithilfe von sqlcmd](../../relational-databases/scripting/run-transact-sql-script-files-using-sqlcmd.md)  
  
  