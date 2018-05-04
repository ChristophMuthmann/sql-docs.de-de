---
title: Xp_cmdshell (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8f9296b1ff21ee5412aa83f7a5edc2736793777f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="xpcmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erzeugt eine Windows-Befehlsshell und übergibt eine Zeichenfolge für die Ausführung. Die Ausgabe wird ggf. in Textzeilen zurückgegeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Command_string* **"**  
 Die Zeichenfolge, die einen an das Betriebssystem zu übergebenden Befehl enthält. *Command_string* ist **vom Datentyp varchar(8000)** oder **nvarchar(4000)**, hat keinen Standardwert. *Command_string* kann nicht mehr als ein Satz doppelter Anführungszeichen enthalten. Ein einzelnes Paar von Anführungszeichen ist erforderlich, wenn keine Leerzeichen vorhanden, in den Dateipfaden sind oder verwiesen wird Programmnamen, *Command_string*. Wenn Probleme mit eingebetteten Leerzeichen auftreten, sollten Sie FAT 8.3-Dateinamen verwenden, um dieses Problem zu umgehen.  
  
 **Keine_Ausgabe**  
 Ein optionaler Parameter, der angibt, dass keine Ausgabe an den Client zurückgegeben werden soll.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Mit der folgenden `xp_cmdshell`-Anweisung wird eine Verzeichnisaufstellung des aktuellen Verzeichnisses zurückgegeben.  
  
```  
EXEC xp_cmdshell 'dir *.exe';  
GO  
```  
  
 Die Zeilen werden zurückgegeben, eine **nvarchar(255)** Spalte. Wenn die **Keine_Ausgabe** Option verwendet wird, wird nur Folgendes zurückgegeben:  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>Hinweise  
 Vom Windows-Prozesses erzeugte **Xp_cmdshell** hat die gleichen Sicherheitsrechte wie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto.  
  
 **Xp_cmdshell** erfolgt synchron. Die Steuerung wird erst dann an den Aufrufer zurückgegeben, wenn der Befehl der Befehlsshell abgeschlossen wurde.  
  
 **Xp_cmdshell** können aktiviert und deaktiviert werden, mithilfe der richtlinienbasierten Verwaltung oder durch Ausführen **Sp_configure**. Weitere Informationen finden Sie unter [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md) und [Xp_cmdshell Serverkonfigurationsoption](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
> [!IMPORTANT]  
>  Wenn **Xp_cmdshell** innerhalb eines Batches ausgeführt wird und einen Fehler zurückgibt, der Batch schlägt fehl. Dies ist eine Änderung des Verhaltens. In früheren Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] der Batch weiterhin ausgeführt.  
  
## <a name="xpcmdshell-proxy-account"></a>xp_cmdshell-Proxykonto  
 Bei Aufruf von einem Benutzer, der nicht Mitglied ist die **Sysadmin** festen Serverrolle **Xp_cmdshell** verbindet sich mit Windows mit dem Kontonamen und das Kennwort, die in den Anmeldeinformationen, die mit dem Namen gespeicherten **## Xp_cmdshell_proxy_account ##**. Falls diese Proxyanmeldeinformationen nicht vorhanden ist, **Xp_cmdshell** schlägt fehl.  
  
 Die Proxykonto-Anmeldeinformationen erstellt werden, indem ausführen **Sp_xp_cmdshell_proxy_account**. Als Argumente besitzt diese gespeicherte Prozedur einen Windows-Benutzernamen und ein Kennwort. Mit dem folgenden Befehl werden z. B. Proxyanmeldeinformationen für den Windows-Domänenbenutzer `SHIPPING\KobeR` erstellt, der das Windows-Kennwort `sdfh%dkc93vcMt0` besitzt.  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 Weitere Informationen finden Sie unter [Sp_xp_cmdshell_proxy_account &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Da böswillige Benutzer manchmal versuchen, ihre rechteerweiterung mithilfe von **Xp_cmdshell**, **Xp_cmdshell** ist standardmäßig deaktiviert. Verwendung **Sp_configure** oder **richtlinienbasierte Verwaltung** zu aktivieren. Weitere Informationen finden Sie unter [xp_cmdshell (Serverkonfigurationsoption)](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
 Beim aktiviert ist, werden **Xp_cmdshell** erfordert die CONTROL SERVER-Berechtigung zum Ausführen und die Windows-Prozess erstellt, indem **Xp_cmdshell** hat den gleichen Sicherheitskontext wie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto verfügt oft über mehr Berechtigungen, als erforderlich sind, für die Arbeit ausgeführt wird, durch den Prozess erstellt, indem **Xp_cmdshell**. Zur Erhöhung der Sicherheit den Zugriff auf **Xp_cmdshell** hoch privilegierte Benutzer eingeschränkt werden soll.  
  
 Nicht-Administratoren verwenden **Xp_cmdshell**, und ermöglichen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um untergeordnete Prozesse mit dem Sicherheitstoken eines Kontos mit eingeschränkteren rechten zu erstellen, gehen Sie folgendermaßen vor:  
  
1.  Erstellen Sie ein lokales Windows-Benutzerkonto oder ein Domänenkonto mit den geringsten Berechtigungen, die von den Prozessen benötigt werden, und passen Sie es an.  
  
2.  Verwenden Sie die **Sp_xp_cmdshell_proxy_account** Systemprozedur so konfigurieren Sie **Xp_cmdshell** dieses Kontos mit geringen Privilegien verwenden.  
  
    > [!NOTE]  
    >  Sie können auch konfigurieren, diese Proxy-Konto mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] durch Rechtsklicken auf **Eigenschaften** auf Ihrem Server benennen Sie im Objekt-Explorer, und suchen Sie auf der **Sicherheit** auf der Registerkarte die **Server Proxykonto** Abschnitt.  
  
3.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], führen Sie mit der master-Datenbank, die `GRANT exec ON xp_cmdshell TO '<somelogin>'` Anweisung, um bestimmten nicht-erteilen**Sysadmin** Benutzer die Fähigkeit zur Ausführung **Xp_cmdshell**. Der angegebene Anmeldename muss einem Benutzer in der master-Datenbank zugeordnet sein.  
  
 Jetzt Nichtadministratoren Betriebssystemprozesse mit starten können **Xp_cmdshell** , und führen Sie die Prozesse mit den Berechtigungen des Proxykontos, die Sie konfiguriert haben. Benutzer mit CONTROL SERVER-Berechtigung (Mitglieder der der **Sysadmin** festen Serverrolle "") erhalten weiterhin die Berechtigungen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkontos für untergeordnete Prozesse, die durch gestartet werden **Xp_cmdshell** .  
  
 Um zu bestimmen, das Windows-Konto, das vom verwendeten **Xp_cmdshell** beim Starten von Betriebssystemprozessen führen Sie die folgende Anweisung:  
  
```  
xp_cmdshell 'whoami.exe'  
  
```  
  
 Um den Sicherheitskontext für einen anderen Anmeldenamen zu bestimmen, führen Sie folgende Anweisung aus:  
  
```  
EXECUTE AS LOGIN = '<other_login>' ;  
GO  
xp_cmdshell 'whoami.exe' ;  
REVERT ;  
  
```  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-a-list-of-executable-files"></a>A. Zurückgeben einer Liste der ausführbaren Dateien  
 Im folgenden Beispiel wird mithilfe der erweiterten gespeicherten Prozedur `xp_cmdshell` der Befehl DIR ausgeführt.  
  
```  
EXEC master..xp_cmdshell 'dir *.exe''  
```  
  
### <a name="b-returning-no-output"></a>B. Unterdrücken der Ausgabe  
 Im folgenden Beispiel wird mit `xp_cmdshell` eine Befehlszeichenfolge ausgeführt, ohne dass die Ausgabe an den Client zurückgegeben wird.  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks, NO_OUTPUT';  
GO  
```  
  
### <a name="c-using-return-status"></a>C. Verwenden des Rückgabestatus  
 Im folgenden Beispiel die `xp_cmdshell` erweiterte gespeicherte Prozedur auch der Rückgabestatus vorgeschlagen. Der Rückgabecodewert wird in der Variablen `@result` gespeichert.  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>D. Schreiben des Inhalts von Variablen in eine Datei  
 Im folgenden Beispiel wird der Inhalt der `@var`-Variablen in die Datei `var_out.txt` im aktuellen Serververzeichnis geschrieben.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>E. Aufzeichnen des Ergebnisses eines Befehls in einer Datei  
 Im folgenden Beispiel wird der Inhalt des aktuellen Verzeichnisses in die Datei `dir_out.txt` im aktuellen Serververzeichnis geschrieben.  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte allgemeine erweiterte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Xp_cmdshell – Serverkonfigurationsoption](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [Oberflächenkonfiguration](../../relational-databases/security/surface-area-configuration.md)   
 [Sp_xp_cmdshell_proxy_account &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
