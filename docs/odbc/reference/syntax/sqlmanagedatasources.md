---
title: SQLManageDataSources | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1b10fd1109c41d1d19418ce83dd14b60488a85fd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**Konformität**  
 Version eingeführt: ODBC 2.0  
  
 **Zusammenfassung**  
 **SQLManageDataSources** zeigt ein Dialogfeld mit dem Benutzer können einrichten, hinzufügen und Löschen von Datenquellen in die Systeminformationen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>Argumente  
 *HWND*  
 [Eingabe] Handle des übergeordneten Fensters.  
  
## <a name="returns"></a>Rückgabewert  
 **SQLManageDataSources** gibt "false" zurück, wenn *Hwnd* ist es sich nicht um ein gültiges Fensterhandle. Andernfalls wird "Wahr" zurückgegeben.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLManageDataSources** gibt "false", ein zugehöriges  *\*PfErrorCode* Wert abgerufen werden kann, durch den Aufruf **SQLInstallerError**. Die folgende Tabelle enthält die  *\*PfErrorCode* Werte, die von zurückgegeben werden können **SQLInstallerError** und jeweils im Kontext dieser Funktion erläutert.  
  
|*\*pfErrorCode*|Fehler|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Allgemeine Installer-Fehler|Fehler für die kein bestimmtes Installationsfehler aufgetreten.|  
|ODBC_ERROR_REQUEST_FAILED|*Anforderung* fehlgeschlagen|Der Aufruf von **ConfigDSN** ist fehlgeschlagen.|  
|ODBC_ERROR_INVALID__HWND|Ungültige Fensterhandle|Die *Hwnd* Argument war ungültig oder NULL.|  
|ODBC_ERROR_OUT_OF_MEM|Nicht genügend Arbeitsspeicher.|Das Installationsprogramm konnte die Funktion aufgrund unzureichenden Arbeitsspeichers nicht ausgeführt werden.|  
  
## <a name="managing-data-sources"></a>Verwalten von Datenquellen  
 **SQLManageDataSources** zeigt Anfangs der **ODBC-Datenquellenadministrator** (Dialogfeld), wie in der folgenden Abbildung dargestellt.  
  
 ![Dialogfeld ODBC-Datenquellenadministrator](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 Das Dialogfeld zeigt die Datenquellen, die in die Systeminformationen auf drei Registerkarten angezeigt: **Benutzer-DSN**, **System-DSN**, und **Datei-DSN**. Wenn der Benutzer eine Datenquelle doppelklickt oder eine Datenquelle wählt und klickt auf **konfigurieren**, **SQLManageDataSources** Aufrufe **ConfigDSN** im Setup-DLL-Datei mit den ODBC_CONFIG_ DSN-Option.  
  
 Wenn der Benutzer klickt **hinzufügen**, **SQLManageDataSources** zeigt die **neue Datenquelle erstellen** (Dialogfeld), in der folgenden Abbildung gezeigt.  
  
 ![Erstellen Sie im Dialogfeld Neue Datenquelle](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 Das Dialogfeld zeigt eine Liste der installierten Treiber. Wenn der Benutzer einen Treiber doppelklickt oder ein Treibers klickt und **OK**, **SQLManageDataSources** Aufrufe **ConfigDSN** in der Setup-DLL und übergibt es die ODBC_ADD_DSN-Option.  
  
 Wenn der Benutzer eine Datenquelle wählt, und klickt auf **entfernen**, **SQLManageDataSources** gefragt, ob der Benutzer möchte die Datenquelle löschen. Wenn der Benutzer klickt **Ja**, **SQLManageDataSources** Aufrufe **ConfigDSN** in der Setup-DLL mit der Option ODBC_REMOVE_DSN.  
  
 Die **neue Datenquelle erstellen** Dialogfeld dient zum Hinzufügen oder Löschen einer Datenquelle für den Benutzer, eine Systemdatenquelle oder eine Dateidatenquelle.  
  
## <a name="user-dsns"></a>Benutzer-DSNs  
 DSNs für einzelne Benutzer erstellt wurde, werden der Benutzer-DSNs, um die Unterscheidung von System-DSNs aufgerufen. Benutzer-DSNs werden in die Systeminformationen wie folgt registriert:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>System-DSNs  
 Die **neue Datenquelle erstellen** Dialogfeld können Sie eine Systemdatenquelle auf Ihrem lokalen Computer oder löschen Sie eines hinzufügen oder die Konfiguration für eine Systemdatenquelle festgelegt.  
  
 Eine Datenquelle einrichten, die mit einer System-Datenquellennamen (DSN) kann von mehr als ein Benutzer auf dem gleichen Computer verwendet werden. Sie können auch von einem Dienst systemweiten verwendet werden die dann an die Datenquelle zugreifen können, auch wenn kein Benutzer mit dem Computer angemeldet ist.  
  
 Ein System-DSN wird in der HKEY_LOCAL_MACHINE-Eintrag in die Systeminformationen anstatt in der HKEY_CURRENT_USER-Eintrag registriert. Es ist nicht an einen Benutzer, die mit bestimmten Benutzernamen und Kennwort anmeldet, jedoch kann verwendet werden, von jedem Benutzer dieses Computers oder von einem Dienst Automatische systemweiten gebunden. System-DSN ist, jedoch an einem Computer gebunden. Die Möglichkeit der Verwendung von remote-DSNs zwischen Computern wird nicht unterstützt. System-DSNs werden in die Systeminformationen wie folgt registriert:  
  
 HKEY_LOCAL_MACHINE SOFTWARE ODBC Odbc.ini  
  
## <a name="file-dsns"></a>Datei-DSNs  
 Eine Datei als Datenquelle einen Datenquellennamen keinen ist eine Datenquelle für den Computer, und nicht auf einen Benutzer oder Computer registriert ist. Die Verbindungsinformationen für diese Datenquelle wird in einer DSN-Datei enthalten, die auf einem beliebigen Computer kopiert werden können. Eine Dateidatenquelle kann freigegeben ist, befindet sich in diesem Fall die DSN-Datei in einem Netzwerk und gleichzeitig verwendet werden kann von mehreren Benutzern im Netzwerk als der Benutzer den entsprechenden Treiber installiert hat. Eine Dateidatenquelle kann auch Dateidatenquelle, werden in diesem Fall kann es nur auf einem einzelnen Computer verwendet werden.  
  
 Weitere Informationen zu Datenquellen, finden Sie unter [Herstellen einer Verbindung mithilfe von Dateidatenquellen](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), oder finden Sie unter [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="managing-drivers"></a>Verwalten von Treibern  
 Wenn der Benutzer klickt auf die **Treiber** Registerkarte die **ODBC-Datenquellen-Administrator** (Dialogfeld), **SQLManageDataSources** zeigt eine Liste der ODBC-Treiber auf dem System installierten sowie Informationen zu den Treiber. Der angezeigte Datum ist das Erstellungsdatum des Treibers, wie in der folgenden Abbildung dargestellt.  
  
 ![Registerkarte "ODBC-Datenquellen-Administrator-Treiber"](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>Ablaufverfolgungsoptionen  
 Wenn der Benutzer klickt der **Ablaufverfolgung** Registerkarte die **ODBC-Datenquellen-Administrator** (Dialogfeld), **SQLManageDataSources** Ablaufverfolgungsoptionen, zeigt, wie das folgende Beispiel zeigt Abbildung.  
  
 ![Registerkarte "Tracing ODBC-Datenquellen-Administrator"](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 Wenn der Benutzer klickt **Ablaufverfolgung jetzt starten** und klickt dann auf **OK**, **SQLManageDataSources** aktiviert die Ablaufverfolgung manuell für alle Anwendungen, die derzeit auf dem Computer ausgeführt.  
  
 Wenn der Benutzer den Namen einer Ablaufverfolgungsdatei in angibt der **Protokolldatei Pfad** Textfeld und klickt dann auf **OK**, **SQLManageDataSources** legt die **TraceFile** Schlüsselwort im Abschnitt [ODBC], Informationen zu dem angegebenen Namen.  
  
> [!IMPORTANT]  
>  Unterstützung für Visual Studio Analyzer wurde entfernt ab Windows 8 (Visual Studio Analyzer wurde nur in früheren Versionen von Visual Studio enthalten.). Verwenden Sie eine Alternative zur Problembehandlung Mechanismus BID-Ablaufverfolgung.  
  
 Wenn der Benutzer klickt **starten Sie Visual Studio Analyzer** und klickt dann auf **OK**, Visual Studio Analyzer aktiviert ist. Es bleibt bis aktiviert **beenden Sie Visual Studio Analyzer** geklickt wird.  
  
 Weitere Informationen zur Ablaufverfolgung finden Sie unter [Ablaufverfolgung](../../../odbc/reference/develop-app/tracing.md). Weitere Informationen zu den **Ablaufverfolgung** und **TraceFile** Schlüsselwörter finden Sie unter [ODBC-Unterschlüssel](../../../odbc/reference/install/odbc-subkey.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Erstellen von Datenquellen|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
