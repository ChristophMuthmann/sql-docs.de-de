---
title: MSSQLSERVER_18456 | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 18456 (Database Engine error)
ms.assetid: c417631d-be1f-42e0-8844-9f92c77e11f7
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.openlocfilehash: b8b1465feb409dc73ef13899e78e2dd2ab626639
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver18456"></a>MSSQLSERVER_18456
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|18456|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|LOGON_FAILED|  
|Meldungstext|Fehler bei der Anmeldung für den Benutzer '%.*ls'.%.\*ls|  
  
## <a name="explanation"></a>Erklärung  
Wird ein Verbindungsversuch aufgrund eines Authentifizierungsfehlers im Zusammenhang mit einem falschen Kennwort oder Benutzernamen zurückgewiesen, wird eine Meldung vergleichbar mit der folgenden an den Client zurückgegeben: "Fehler bei der Anmeldung für den Benutzer '<Benutzername>'. (Microsoft SQL Server, Fehler: 18456)".  
  
Zusätzlich enthalten die an den Client zurückgegebenen Informationen Folgendes:  
  
"Fehler bei der Anmeldung für den Benutzer <Benutzername>" (.Net SqlClient-Datenanbieter)"  
  
-----------------------------\-  
  
"Servername: <Computername>"  
  
"Fehlernummer: 18456"  
  
"Schweregrad: 14"  
  
"Status: 1"  
  
"Zeilennummer: 65536"  
  
Möglicherweise wird auch die folgende Meldung zurückgegeben:  
  
"Meldung 18456, Ebene 14, Status 1, Server <Computername>, Zeile 1"  
  
"Fehler bei der Anmeldung für den Benutzer <Benutzername>."  
  
## <a name="additional-error-information"></a>Zusätzliche Fehlerinformationen  
Zur Verbesserung der Sicherheit bleibt die Art des Authentifizierungsfehlers in der an den Client zurückgegebenen Fehlermeldung absichtlich verborgen. Im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll hingegen enthält ein entsprechender Fehler einen Fehlerzustand, der einem Authentifizierungsfehler zugeordnet werden kann. Vergleichen Sie den Fehlerzustand mit der folgenden Liste, um den Grund für den Anmeldefehler zu bestimmen.  
  
|Status|Description|  
|---------|---------------|  
|1|Es sind keine Fehlerinformationen verfügbar. Dieser Status bedeutet normalerweise, dass Sie keine Berechtigung haben, die Fehlerdetails zu empfangen. Weitere Informationen erhalten Sie beim [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Administrator.|  
|2|Die Benutzer-ID ist nicht gültig.|  
|5|Die Benutzer-ID ist nicht gültig.|  
|6|Es wurde der Versuch unternommen, einen Windows-Anmeldenamen für die SQL Server-Authentifizierung zu verwenden.|  
|7|Der Anmeldename ist deaktiviert, und das Kennwort ist falsch.|  
|8|Das Kennwort ist falsch.|  
|9|Das Kennwort ist ungültig.|  
|11|Der Anmeldename ist gültig, beim Serverzugriff ist jedoch ein Fehler aufgetreten. Dieser Fehler ist möglicherweise darauf zurückzuführen, dass der Windows-Benutzer als Mitglied der lokalen Administratorgruppe Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat, Windows aber keine Administratoranmeldeinformationen bereitstellt. Starten Sie das Programm zum Herstellen einer Verbindung mit der Option **Als Administrator ausführen**, und fügen Sie anschließend den Windows-Benutzer als spezifischen Anmeldenamen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hinzu.|  
|12|Der Anmeldename ist gültig, beim Serverzugriff ist jedoch ein Fehler aufgetreten.|  
|18|Das Kennwort muss geändert werden.|  
|38, 46|Die vom Benutzer angeforderte Datenbank konnte nicht gefunden werden.|
|102 – 111|AAD-Fehler|
|122 – 124|Fehler wegen eines leeren Benutzernamens oder Kennworts.|
|126|Die vom Benutzer angeforderte Datenbank ist nicht vorhanden.|
|132 – 133|AAD-Fehler|
  
Andere Fehlerzustände liegen vor und weisen auf einen unerwarteten internen Verarbeitungsfehler hin.  
  
**Weitere ungewöhnliche mögliche Ursache**  
  
In folgenden Situationen kann folgender Fehler gemeldet werden: **Fehler bei der Anmeldung mit der SQL-Authentifizierung. Der Server ist nur für die Windows-Authentifizierung konfiguriert.** kann in den folgenden Situationen zurückgegeben werden.  
  
-   Der Server ist für die Authentifizierung im gemischten Modus konfiguriert, für eine ODBC-Verbindung wird das TCP-Protokoll verwendet, und für die Verbindung wurde nicht explizit angegeben, dass eine vertrauenswürdige Verbindung verwendet werden soll.  
  
-   Der Server ist für die Authentifizierung im gemischten Modus konfiguriert, für eine ODBC-Verbindung werden Named Pipes verwendet, mit den vom Client zum Öffnen der Named Pipe verwendeten Anmeldeinformationen wird automatisch die Identität des Benutzers angenommen, und für die Verbindung wurde nicht explizit angegeben, dass eine vertrauenswürdige Verbindung verwendet werden soll.  
  
Um dieses Problem zu beheben, schließen Sie **TRUSTED_CONNECTION = TRUE** in die Verbindungszeichenfolge ein.  
  
## <a name="examples"></a>Beispiele  
In diesem Beispiel ist der Fehlerzustand des Authentifizierungsfehlers 8. Dies zeigt an, dass das Kennwort falsch ist.  
  
|Datum|Quelle|MessageBox|  
|--------|----------|-----------|  
|2007-12-05 20:12:56.34|Anmeldung|Fehler: 18456, Schweregrad: 14, Status: 8.|  
|2007-12-05 20:12:56.34|Anmeldung|Fehler bei der Anmeldung für den Benutzer <Benutzername>. [CLIENT: <ip address>]|  
  
> [!NOTE]  
> Wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des Windows-Authentifizierungsmodus installiert und später in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und den Windows-Authentifizierungsmodus geändert, wird der Anmeldename **sa** zunächst deaktiviert. Dadurch wird ein Fehler mit dem Status 7 ausgelöst: "Fehler bei der Anmeldung für den Benutzer 'sa'". Informationen zum Aktivieren der **sa**-Anmeldung finden Sie unter [Ändern des Serverauthentifizierungsmodus](~/database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="user-action"></a>Benutzeraktion  
Wenn Sie versuchen, eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung herzustellen, überprüfen Sie, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im gemischten Authentifizierungsmodus konfiguriert ist.  
  
Wenn Sie versuchen, eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Authentifizierung herzustellen, überprüfen Sie, dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldeinformationen vorhanden sind und dass sie richtig geschrieben sind.  
  
Wenn Sie versuchen, eine Verbindung mit Windows-Authentifizierung herzustellen, überprüfen Sie, dass Sie ordnungsgemäß bei der richtigen Domäne angemeldet sind.  
  
Wenn der Fehler den Status 1 angibt, wenden Sie sich an den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Administrator.  
  
Wenn Sie mit Ihren Administratoranmeldeinformationen eine Verbindung herstellen möchten, starten Sie die Anwendung mit der Option **Als Administrator ausführen**. Fügen Sie den Windows-Benutzer nach dem Herstellen der Verbindung als einzelne Anmeldung hinzu.  
  
Wenn das [!INCLUDE[ssDE](../../includes/ssde-md.md)] eigenständige Datenbanken unterstützt, vergewissern Sie sich, dass die Anmeldung nach der Migration zu einem Benutzer einer eigenständigen Datenbank nicht gelöscht wurde.  
  
Wenn Sie lokal eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz herstellen, müssen Dienste, die unter **NT AUTHORITY\NETWORK SERVICE** ausgeführt werden, mithilfe des vollqualifizierten Domänennamens des Computers authentifiziert werden. Weitere Informationen finden Sie unter [How To: Use the Network Service Account to Access Resources in ASP.NET (Vorgehensweise: Verwenden des Netzwerkdienstkontos für den Zugriff auf Ressourcen in ASP.NET)](http://msdn.microsoft.com/library/ff647402.aspx)  
  
