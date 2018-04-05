---
title: Herstellen einer Verbindung mit Sqlcmd | Microsoft Docs
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
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
caps.latest.revision: 45
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: c08f390860a35ccbd5dd743317a52df80c05ef52
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="connecting-with-sqlcmd"></a>Herstellen einer Verbindung mit sqlcmd
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Die [Sqlcmd](http://go.microsoft.com/fwlink/?LinkID=154481) Dienstprogramm finden Sie in der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] auf Linux- und MacOS.
  
Die folgenden Befehle demonstrieren, wie Sie Windows-Authentifizierung (Kerberos) und [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Authentifizierung bzw.:
  
```  
sqlcmd –E –Sxxx.xxx.xxx.xxx  
sqlcmd –Sxxx.xxx.xxx.xxx –Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>Verfügbare Optionen

In der aktuellen Version sind die folgenden Optionen verfügbar:  
  
- -? Anzeige `sqlcmd` Verwendung.  
  
- – eine Anforderung eine Paketgröße.  
  
- -b terminieren Stapelverarbeitung, wenn ein Fehler vorliegt.  
  
- -C *Batch_terminator* das Batchabschlusszeichen angeben.  
  
- C# - Serverzertifikat vertrauen.  

- -d: *Database_name* Problem eine `USE ` *Database_name* -Anweisung, wenn Sie starten `sqlcmd`.  

- -D bewirkt, dass den an übergebenen Wert den `sqlcmd` Option "-S" als einen Datenquellennamen (DSN) interpretiert werden. Weitere Informationen finden Sie unter "DSN-Unterstützung in `sqlcmd` und `bcp`" am Ende dieses Themas.  
  
- -e, Schreiben Sie eingabeskripts in das Standardausgabegerät (Stdout).

- -E: verwendet die vertrauenswürdige Verbindung (integrierte Authentifizierung). Weitere Informationen zum vornehmen von vertrauenswürdigen Verbindungen, die integrierte Authentifizierung von einem Client für Linux oder MacOS verwenden, finden Sie unter [mithilfe der integrierten Authentifizierung](../../../connect/odbc/linux-mac/using-integrated-authentication.md).

- -h *Number_of_rows* Geben Sie die Anzahl der Zeilen, die zwischen den Spaltenüberschriften gedruckt.  
  
- -H Geben Sie einen Arbeitsstationsnamen.  
  
- -i *Input_file*[,*Input_file*[,...]] Identifizieren Sie die Datei, die einen Stapel von SQL-Anweisungen oder gespeicherten Prozeduren enthält.  
  
- -I: Satz der `SET QUOTED_IDENTIFIER` -Verbindungsoption auf ON.  
  
- -k entfernen oder Ersetzen von Zeichen.  
  
- **-K***application_intent*  
Deklariert den Arbeitsauslastungstyp der Anwendung beim Herstellen einer Verbindung mit einem Server. Der einzige derzeit unterstützte Wert ist **ReadOnly**. Wenn **-K** nicht angegeben ist, `sqlcmd` unterstützt keine Konnektivität zu einem sekundären Replikat in einer AlwaysOn-verfügbarkeitsgruppe. Weitere Informationen finden Sie unter [ODBC-Treiber unter Linux und Mac OS - High Availability and Disaster Recovery](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> **-K** wird in der CTP-Version für SUSE Linux nicht unterstützt. Sie können jedoch angeben, die **ApplicationIntent = ReadOnly** -Schlüsselwort in einer DSN-Datei übergeben, um `sqlcmd`. Weitere Informationen finden Sie unter "DSN-Unterstützung in `sqlcmd` und `bcp`" am Ende dieses Themas.  
  
- -l *Timeout* Geben Sie die Anzahl der Sekunden, bevor ein `sqlcmd` -Anmeldung ein Timeout eintritt, wenn Sie versuchen, eine Verbindung mit einem Server herstellen.

- m - *Error_level* Steuerung, welche Fehlermeldungen an Stdout gesendet werden.  
  
- **-M***multisubnet_failover*  
Geben Sie immer **-M** an, wenn Sie eine Verbindung mit dem Verfügbarkeitsgruppenlistener einer [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]-Verfügbarkeitsgruppe oder einer [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]-Failoverclusterinstanz herstellen. **M -** für schnellere Erkennung von Failover und die Verbindung mit dem (gerade) aktiven Server enthält. Wenn **-M** nicht angegeben ist, ist **-M** deaktiviert. Weitere Informationen zu [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)], finden Sie unter [ODBC-Treiber unter Linux und Mac OS - High Availability and Disaster Recovery](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  
  
> [!NOTE]  
> **-M** wird in der CTP-Version für SUSE Linux nicht unterstützt. Sie können jedoch angeben, die **MultiSubnetFailover = Yes** -Schlüsselwort in einer DSN-Datei übergeben, um `sqlcmd`. Weitere Informationen finden Sie unter "DSN-Unterstützung in `sqlcmd` und `bcp`" am Ende dieses Themas.  
  
- N - Verbindung verschlüsseln.  
  
- -o *Output_file* identifizieren Sie die Datei, die Ausgabe von empfängt `sqlcmd`.  
  
- -p drucken Leistungsstatistiken für jedes Resultset.  
  
- P - Geben Sie ein Benutzerkennwort.  
  
- -q: *Commandline_query* Ausführen einer Abfrage bei `sqlcmd` startet, aber nicht beendet, wenn die Abfrage ausgeführt wurde.  

- -Q: *Commandline_query* Ausführen einer Abfrage bei `sqlcmd` gestartet wird. `sqlcmd`wird beendet, wenn die Abfrage abgeschlossen ist.  

- -R leitet die Fehlermeldungen an Stderr.

- -R bewirkt, dass der Treiber die regionalen Einstellungen des Clients verwendet, Währung und Datums-/ Uhrzeitdaten in Zeichendaten konvertiert werden. Derzeit werden nur en_US-Formatierungen (US-Englisch) verwendet.
  
- -s *Column_separator_char* der Spaltentrennzeichen angeben.  

- -S [*protocol*:] *server*[**,***port*]  
Geben Sie die Instanz des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] für die Verbindung, oder -D wird verwendet, einen DSN. Der ODBC-Treiber unter Linux und MacOS erfordert -S. Beachten Sie, dass **Tcp** ist das einzige gültige Protokoll.  
  
- t - *Query_timeout* Geben Sie die Anzahl der Sekunden bis zum Timeout einer Befehlsklasse (oder eine SQL-Anweisung).  
  
- -u angeben, dass Output_file wird im Unicode-Format, unabhängig vom Format von Input_file gespeichert.  
  
- U - *Anmelde-ID* Geben Sie eine Benutzeranmelde-ID.  
  
- -V *Error_severity_level* steuern Sie den Schweregrad, der zur Festlegung der ERRORLEVEL-Variable verwendet wird.  
  
- -w *Column_width* die Bildschirmbreite für die Ausgabe anzugeben.  
  
- -W nachfolgende Leerzeichen aus einer Spalte zu entfernen.  
  
- Disable-VariablenErsetzung - X.  
  
- X - Befehle, Startskript und Umgebungsvariablen deaktivieren.  
  
- / y *Variable_length_type_display_width* legen Sie die `sqlcmd` Skriptvariable `SQLCMDMAXFIXEDTYPEWIDTH`.
  
- / Y *Fixed_length_type_display_width* legen Sie die `sqlcmd` Skriptvariable `SQLCMDMAXVARTYPEWIDTH`.


## <a name="available-commands"></a>Verfügbare Befehle

In der aktuellen Version sind die folgenden Befehle verfügbar:  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*count*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>Nicht verfügbare Optionen
Die folgenden Optionen sind in der aktuellen Version nicht verfügbar:  

- Ein - melden Sie sich beim [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] mit einer dedizierten Administratorverbindung (DAC). Informationen zum Erstellen einer dedizierten administratorverbindung (DAC) finden Sie unter [Programmierung Richtlinien](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
- -f *Codepage* die Eingabe-und ausgabecodepages Seiten angeben.  
  
- -L aufgelistet, die lokal konfigurierten Servercomputer sowie die Namen der Servercomputer, die im Netzwerk übertragen.  
  
- -V erstellen eine `sqlcmd` Skriptvariable, die verwendet werden können eine `sqlcmd` Skript.  
  
Sie können die folgende alternative Methode verwenden: Schreiben Sie die Parameter in einer Datei, die Sie dann in eine andere Datei anhängen können. Dies hilft Ihnen dabei, eine Parameterdatei zu verwenden, um die Werte zu ersetzen. Erstellen Sie z. B. eine Datei namens `a.sql` (die Parameterdatei) mit dem folgenden Inhalt:
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
Erstellen Sie eine Datei namens `b.sql`, mit den Parametern für den Austausch:  
  
    select $(ColumnName) from $(TableName)  

Kombinieren Sie in der Befehlszeile `a.sql` und `b.sql` in `c.sql` mit den folgenden Befehlen:  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
Führen Sie `sqlcmd` und `c.sql` als Eingabedatei:  
  
    slqcmd -S<…> -P<..> –U<..> -I c.sql  

- Z - *Kennwort* Kennwort ändern.  
  
- Z - *Kennwort* Kennwort ändern und beenden.  

## <a name="unavailable-commands"></a>Nicht verfügbare Befehle

In der aktuellen Version sind die folgenden Befehle nicht verfügbar:  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>DSN-Unterstützung in sqlcmd und bcp

Sie können angeben, einen Datenquellennamen (DSN) statt eines Servernamens in der **Sqlcmd** oder **Bcp** `-S` Option (oder **Sqlcmd** : Befehl Verbinden), wenn Sie -D. angeben -D bewirkt, dass **Sqlcmd** oder **Bcp** für die Verbindung mit dem Server, die in der DSN angegeben ist, indem Sie die Option "-S".  
  
System-DSNs werden gespeichert, der `odbc.ini` Datei im ODBC-SysConfigDir-Verzeichnis (`/etc/odbc.ini` auf standard-Installationen). Benutzer-DSNs werden in gespeicherten `.odbc.ini` im Basisverzeichnis des Benutzers (`~/.odbc.ini`).
  
Die folgenden Einträge werden in einem DSN unter Linux oder MacOS unterstützt:

-   **ApplicationIntent = ReadOnly**  

-   **Datenbank =***Database_name*  
  
-   **Treiber Odbcdriver 11 für SQLServer =** oder **Treiber = Odbcdriver 13 für SQLServer**
  
-   **MultiSubnetFailover = Yes**  
  
-   **Server =***Server_name_or_IP_address*  
  
-   **Trusted_Connection=yes**|**no**  
  
In einem DSN ist nur der Eintrag DRIVER erforderlich, aber für die Verbindung mit einem Server `sqlcmd` oder `bcp` den Wert im Eintrag SERVER benötigt.  

Wenn die gleiche Option in beiden DSN angegeben ist und die `sqlcmd` oder `bcp` -Befehlszeile die Befehlszeilenoption überschreibt den Wert, der in der DSN verwendet. Z. B. wenn der DSN ein Datenbankeintrags verfügt und die `sqlcmd` Befehlszeile enthält **-d**, der an übergebene Wert **-d** verwendet wird. Wenn **Trusted_Connection = Yes** in Kerberos-Authentifizierung verwendet wird und den Benutzernamen des DSN angegeben ist (**– U**) und das Kennwort (**– P**), falls vorhanden, werden ignoriert.

Vorhandene Skripts, mit denen aufgerufen `isql` können geändert werden, um verwenden `sqlcmd` durch Definieren von den folgenden Alias: `alias isql="sqlcmd –D"`.  

## <a name="see-also"></a>Siehe auch  
[Herstellen einer Verbindung mit **Bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
