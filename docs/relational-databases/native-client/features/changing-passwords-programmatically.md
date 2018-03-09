---
title: "Ändern von Kennwörtern programmgesteuert | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb5e1dbff4a9a528690ff3172da2329ae9a5c28e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="changing-passwords-programmatically"></a>Programmgesteuertes Ändern von Kennwörtern
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Vor [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] konnte nur ein Administrator ein abgelaufenes Kennwort eines Benutzers zurücksetzen. Beginnend mit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client unterstützt, die von abgelaufenen Kennwörtern sowohl programmgesteuert über die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter und die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber und über Änderungen an der **SQL Server-Anmeldung** Dialogfelder.  
  
> [!NOTE]  
>  Fordern Sie, wenn möglich, Benutzer dazu auf, ihre Anmeldeinformationen zur Laufzeit einzugeben, um zu vermeiden, diese Informationen in einem persistenten Format speichern zu müssen. Wenn Sie ihre Anmeldeinformationen persistent speichern müssen, verschlüsseln Sie sie mithilfe der [Win32 Crypto-API](http://go.microsoft.com/fwlink/?LinkId=64532). Weitere Informationen zur Verwendung von Kennwörtern finden Sie unter [Strong Passwords](../../../relational-databases/security/strong-passwords.md).  
  
## <a name="sql-server-login-error-codes"></a>Fehlercodes bei der SQL Server-Anmeldung  
 Wenn eine Verbindung aufgrund von Authentifizierungsproblemen nicht hergestellt werden kann, wird für die Anwendung einer der folgenden SQL Server-Fehlercodes bereitgestellt, um Diagnose und Wiederherstellung zu erleichtern.  
  
|SQL Server-Fehlercode|Fehlermeldung|  
|---------------------------|-------------------|  
|15113|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortüberprüfung. Das Konto ist gesperrt.|  
|18463|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort kann zurzeit nicht verwendet werden.|  
|18464|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort erfüllt nicht richtlinienanforderungen ist zu kurz.|  
|18465|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort erfüllt nicht richtlinienanforderungen, weil er zu lang ist.|  
|18466|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort ist nicht komplex genug und erfüllt daher nicht die Anforderungen der Windows-Richtlinie.|  
|18467|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Das Kennwort erfüllt nicht die Anforderungen der Kennwortfilter-DLL.|  
|18468|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Fehler bei der Kennwortänderung. Unerwarteter Fehler während der Kennwortüberprüfung.|  
|18487|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Das Kennwort des Kontos ist abgelaufen.|  
|18488|Fehler bei der Anmeldung für den Benutzer '%.*ls'. Ursache: Das Kennwort des Kontos muss geändert werden.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB-Anbieter  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt das Ablaufen von Kennwörtern, über eine Benutzerschnittstelle und programmgesteuert.  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB-Benutzeroberfläche für abgelaufene Kennwörter  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt das Ablaufen von Kennwörtern durch Änderungen an der **SQL Server-Anmeldung** Dialogfelder. Wenn der Wert DBPROP_INIT_PROMPT auf DBPROMPT_NOPROMPT festgelegt wird, schlägt der erste Verbindungsversuch fehl, wenn das Kennwort abgelaufen ist.  
  
 Wenn DBPROP_INIT_PROMPT in einen anderen Wert festgelegt wurde, sieht der Benutzer die **SQL Server-Anmeldung** Dialogfeld, unabhängig davon, ob das Kennwort abgelaufen ist. Der Benutzer kann dann auf die **Optionen** Schaltfläche aus, und überprüfen Sie **Kennwort ändern** zum Ändern des Kennworts.  
  
 Wenn der Benutzer auf OK klickt und das Kennwort abgelaufen ist, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fordert den Benutzer zur Eingabe und Bestätigung eines neuen Kennworts mithilfe der **SQL Server-Kennwort ändern** Dialogfeld.  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB-Eingabeaufforderungsverhalten und gesperrte Konten  
 Verbindungsversuche schlagen möglicherweise fehl, weil das Konto gesperrt wurde. Wenn dies nach der Anzeige des tritt auf, die **SQL Server-Anmeldung** Dialogfeld Fehlermeldung des Servers für den Benutzer angezeigt wird und der Verbindungsversuch wird abgebrochen. Er kann auch auftreten, befolgen die Anzeige der **SQL Server-Kennwort ändern** Dialogfeld, wenn der Benutzer einen falschen Wert für das alte Kennwort eingibt. In diesem Fall wird dieselbe Fehlermeldung angezeigt, und der Verbindungsversuch wird abgebrochen.  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB-Verbindungspooling, Ablauf von Kennwörtern und gesperrte Konten  
 Ein Konto kann gesperrt werden oder das dazugehörige Kennwort ablaufen, solange die Verbindung noch in einem Verbindungspool aktiv ist. Der Server überprüft bei zwei Gelegenheiten auf abgelaufene Kennwörter und gesperrte Konten. Zunächst findet eine Überprüfung statt, wenn eine Verbindung hergestellt wird. Die zweite Überprüfung wird nach dem Zurücksetzen einer Verbindung ausgeführt, wenn die Verbindung aus dem Verbindungspool entfernt wird.  
  
 Falls der Zurücksetzungsversuch fehlschlägt, wird die Verbindung aus dem Pool entfernt, und ein Fehler wird zurückgegeben.  
  
### <a name="ole-db-programmatic-password-expiration"></a>Programmgesteuerter Ablauf von Kennwörtern in OLE DB  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt das Ablaufen von Kennwörtern durch das Hinzufügen der Eigenschaft SSPROP_AUTH_OLD_PASSWORD (Typ "VT_BSTR"), die dem DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz hinzugefügt wurde.  
  
 Die vorhandene Password-Eigenschaft verweist auf DBPROP_AUTH_PASSWORD und wird verwendet, um das neue Kennwort zu speichern.  
  
> [!NOTE]  
>  In der Verbindungszeichenfolge legt die "Old Password"-Eigenschaft SSPROP_AUTH_OLD_PASSWORD fest. Dies entspricht dem aktuellen (möglicherweise abgelaufenen) Kennwort, das nicht über eine Anbieterzeichenfolgen-Eigenschaft verfügbar ist.  
  
 Der Anbieter speichert den Wert dieser Eigenschaft nicht persistent. Wenn diese Eigenschaft festgelegt ist, verwendet der Anbieter nicht den Verbindungspool für die erste Verbindung, da eine neue Verbindung hergestellt wird. Wenn die Kennwortänderung ordnungsgemäß vorgenommen werden konnte, kann die aktuelle Verbindung nicht wiederverwendet werden, da sie weiterhin das alte Kennwort verwendet, das nach der Kennwortänderung ungültig wird. Wenn die Anmeldung erfolgreich ist, löscht der Anbieter zudem diese Eigenschaft. Bei späteren Versuchen, das alte Kennwort abzurufen, wird VT_EMPTY zurückgegeben.  
  
> [!NOTE]  
>  SSPROP_AUTH_OLD_PASSWORD sollte nie persistent gespeichert werden, da es nur verwendet wird, wenn ein Kennwort abgelaufen ist.  
  
 Beachten Sie, dass der Anbieter jedes Mal, wenn die Old Password-Eigenschaft festgelegt ist, davon ausgeht, dass versucht wird, das Kennwort zu ändern, es sei denn, es ist auch die Windows-Authentifizierung angegeben, die immer Vorrang hat.  
  
 Wenn Windows-Authentifizierung verwendet wird, führt das alte Kennwort anzugeben entweder zu DB_E_ERRORSOCCURRED oder DB_S_ERRORSOCCURRED abhängig davon, ob das alte Kennwort bzw. als erforderlich oder OPTIONAL angegeben wurde, und der Statuswert der DBPROPSTATUS_ CONFLICTINGBADVALUE wird zurückgegeben, *DwStatus*. Dies wird erkannt, wenn **IDBInitialize:: Initialize** aufgerufen wird.  
  
 Wenn ein Versuch, das Kennwort zu ändern, unerwartet fehlschlägt, gibt der Server den Fehlercode 18468 zurück. Für den Verbindungsversuch wird ein Standard-OLEDB-Fehler zurückgegeben.  
  
 Weitere Informationen zum DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>ODBC-Treiber für SQL Server Native Client  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt das Ablaufen von Kennwörtern, über eine Benutzerschnittstelle und programmgesteuert.  
  
### <a name="odbc-user-interface-password-expiration"></a>ODBC-Benutzeroberfläche für abgelaufene Kennwörter  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt das Ablaufen von Kennwörtern durch Änderungen an der **SQL Server-Anmeldung** Dialogfelder.  
  
 Wenn [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) aufgerufen wird und der Wert des **DriverCompletion** auf SQL_DRIVER_NOPROMPT festgelegt, der erste Verbindungsversuch fehl, wenn das Kennwort abgelaufen ist. Der SQLSTATE-Wert 28000 und der systemeigene Fehlercodewert 18487 zurückgegeben, durch nachfolgende Aufrufe **SQLError** oder **SQLGetDiagRec**.  
  
 Wenn **DriverCompletion** festgelegt wurde auf einen anderen Wert, der Benutzer sieht die **SQL Server-Anmeldung** Dialogfeld, unabhängig davon, ob das Kennwort abgelaufen ist. Der Benutzer kann dann auf die **Optionen** Schaltfläche aus, und überprüfen Sie **Kennwort ändern** zum Ändern des Kennworts.  
  
 Wenn der Benutzer auf OK klickt und das Kennwort abgelaufen ist, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aufforderungen zur Eingabe und Bestätigung eines neuen Kennworts mithilfe der **SQL Server-Kennwort ändern** Dialogfeld.  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>ODBC-Eingabeaufforderungsverhalten und gesperrte Konten  
 Verbindungsversuche schlagen möglicherweise fehl, weil das Konto gesperrt wurde. Wenn dies nach der Anzeige des tritt auf, die **SQL Server-Anmeldung** Dialogfeld Fehlermeldung des Servers für den Benutzer angezeigt wird und der Verbindungsversuch wird abgebrochen. Er kann auch auftreten, befolgen die Anzeige der **SQL Server-Kennwort ändern** Dialogfeld, wenn der Benutzer einen falschen Wert für das alte Kennwort eingibt. In diesem Fall wird dieselbe Fehlermeldung angezeigt, und der Verbindungsversuch wird abgebrochen.  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>ODBC-Verbindungspooling, Ablauf von Kennwörtern und gesperrte Konten  
 Ein Konto kann gesperrt werden oder das dazugehörige Kennwort ablaufen, solange die Verbindung noch in einem Verbindungspool aktiv ist. Der Server überprüft bei zwei Gelegenheiten auf abgelaufene Kennwörter und gesperrte Konten. Zunächst findet eine Überprüfung statt, wenn eine Verbindung hergestellt wird. Die zweite Überprüfung wird nach dem Zurücksetzen einer Verbindung ausgeführt, wenn die Verbindung aus dem Verbindungspool entfernt wird.  
  
 Falls der Zurücksetzungsversuch fehlschlägt, wird die Verbindung aus dem Pool entfernt, und ein Fehler wird zurückgegeben.  
  
### <a name="odbc-programmatic-password-expiration"></a>Programmgesteuerter Ablauf von Kennwörtern in ODBC  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt das Ablaufen von Kennwörtern durch das Hinzufügen von SQL_COPT_SS_OLDPWD-Attribut der festgelegt wird, bevor Sie eine Verbindung mit dem Server die [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) Funktion.  
  
 Das SQL_COPT_SS_OLDPWD-Attribut des Verbindungshandles verweist auf das abgelaufene Kennwort. Es gibt kein Verbindungszeichenfolgenattribut für dieses Attribut, da dies mit dem Verbindungspooling nicht übereinstimmen würde. Wenn die Anmeldung erfolgreich ist, löscht der Treiber zudem dieses Attribut.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt SQL_ERROR zurück in vier Kategorien für dieses Feature: Ablauf des Kennworts, Konflikte mit den Kennwortrichtlinien, kontosperrung und wenn das alte Kennwort als Eigenschaft festgelegt ist, während die Windows-Authentifizierung verwenden. Der Treiber die entsprechenden Fehlermeldungen an den Benutzer zurückgegeben. wenn [SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md) aufgerufen wird.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Features](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
