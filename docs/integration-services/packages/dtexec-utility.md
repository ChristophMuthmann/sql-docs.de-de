---
title: DTExec (Hilfsprogramm) | Microsoft Docs
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: f76aa1cfbcad38e383abca8a79005b3851767e2a
ms.contentlocale: de-de
ms.lasthandoff: 09/21/2017

---
# <a name="dtexec-utility"></a>dtexec (Hilfsprogramm)
  Das Befehlszeilen-Hilfsprogramm **dtexec** dient zum Konfigurieren und Ausführen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen. Das Hilfsprogramm **dtexec** ermöglicht den Zugriff auf alle Features zur Paketkonfiguration und -ausführung, z.B. Parameter, Verbindungen, Eigenschaften, Variablen und Statusanzeigen. Das Hilfsprogramm **dtexec** ermöglicht das Laden von Paketen aus diesen Quellen: dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server, einer ISPAC-Projektdatei, einer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank, dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paketspeicher und dem Dateisystem.  
  
> **HINWEIS:** Bei Verwendung der aktuellen Version des Hilfsprogramms **dtexec** zum Ausführen eines Pakets, das mit einer früheren Version von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]erstellt wurde, aktualisiert das Hilfsprogramm das Paket vorübergehend in das aktuelle Paketformat. Sie können das Hilfsprogramm **dtexec** jedoch nicht verwenden, um diese aktualisierten Pakete zu speichern. Weitere Informationen zum dauerhaften Aktualisieren eines Pakets auf die aktuelle Version finden Sie unter [Aktualisieren von Integration Services-Paketen](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Integration Services-Server und Projektdatei](#server)  
  
-   [Überlegungen zur Installation auf 64-Bit-Computern](#bit)  
  
-   [Überlegungen zu Computern mit parallelen Installationen](#side)  
  
-   [Ausführungsphasen](#phases)  
  
-   [Zurückgegebene Exitcodes](#exit)  
  
-   [Syntaxregeln](#syntaxRules)  
  
-   [Aufrufen von dtexec mit xp_cmdshell](#cmdshell)  
  
-   [Syntax](#syntax)  
  
-   [Parameter](#parameter)  
  
-   [Hinweise](#remark)  
  
-   [Beispiele](#example)  
  
##  <a name="server"></a> Integration Services-Server und Projektdatei  
 Bei Verwendung von **dtexec** zum Ausführen von Paketen auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Server ruft **dtexec** die gespeicherten Prozeduren [catalog.create_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) und [catalog.start_execution &#40;SSISDB-Datenbank&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) auf, um eine Ausführung zu erstellen, Parameterwerte festzulegen und die Ausführung zu starten. Alle Ausführungsprotokolle können in den verwandten Sichten vom Server oder über Standardberichte in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] angezeigt werden. Weitere Informationen zu den Berichten finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
 Im Folgenden finden Sie ein Beispiel zum Ausführen eines Pakets auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server.  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 Wenn Sie **dtexec** verwenden, um ein Paket von der ISPAC-Projektdatei auszuführen, lauten die entsprechenden Optionen: /Proj[ect] und /Pack[age], womit der Projektpfad und der Datenstromname des Pakets angegeben werden. Wenn Sie ein Projekt in das Projektbereitstellungsmodell konvertieren, indem Sie den **Assistenten für die Konvertierung von Integration Services-Projekten** von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ausführen, wird vom Assistenten eine ISPAC-Datei erstellt. Weitere Informationen finden Sie unter [Bereitstellen von Integration Services (SSIS)-Projekten und Paketen](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Sie können **dtexec** mit Planungstools von Drittanbietern verwenden, um Pakete zu planen, die auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt werden.  
  
##  <a name="bit"></a> Überlegungen zur Installation auf 64-Bit-Computern  
 Auf einem 64-Bit-Computer installiert [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine 64-Bit-Version des Hilfsprogramms **dtexec** (dtexec.exe). Wenn Sie bestimmte Pakete im 32-Bit-Modus ausführen möchten, müssen Sie die 32-Bit-Version des Hilfsprogramms **dtexec** installieren. Wählen Sie zum Installieren der 32-Bit-Version des Hilfsprogramms **dtexec** während des Setups entweder Clienttools oder [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
 Standardmäßig wird auf einem 64-Bit-Computer, auf dem sowohl die 64-Bit-Version als auch die 32-Bit-Version eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Befehlszeilen-Hilfsprogramms installiert ist, die 32-Bit-Version an der Eingabeaufforderung ausgeführt. Die 32-Bit-Version wird ausgeführt, da der Verzeichnispfad für die 32-Bit-Version in der PATH-Umgebungsvariablen vor dem Verzeichnispfad für die 64-Bit-Version aufgeführt wird. (Die 32-Bit-Verzeichnispfad ist normalerweise * \<Laufwerk >*: \Programme Dateien (x86) \Microsoft SQL Server\110\DTS\Binn, während der 64-Bit-Verzeichnispfad * \<Laufwerk >*: \Programme\Microsoft SQL Server\110\DTS\Binn.)  
  
> **HINWEIS:** Wenn Sie das Hilfsprogramm mithilfe des SQL Server-Agents ausführen, verwendet dieser automatisch die 64-Bit-Version des Hilfsprogramms. Der SQL Server-Agent sucht die richtige ausführbare Datei für das Hilfsprogramm in der Registrierung und nicht in der PATH-Umgebungsvariablen.  
  
 Wenn Sie sicherstellen möchten, dass die 64-Bit-Version des Hilfsprogramms an der Eingabeaufforderung ausgeführt wird, können Sie einen der folgenden Schritte ausführen:  
  
-   Öffnen Sie ein Eingabeaufforderungsfenster, wechseln Sie zum Verzeichnis mit der 64-Bit-Version des Hilfsprogramms (*\<Laufwerk >*: \Programme\Microsoft SQL Server\110\DTS\Binn), und führen Sie das Hilfsprogramm aus diesem Verzeichnis.  
  
-   Führen Sie das Hilfsprogramm an der Eingabeaufforderung, indem Sie den vollständigen Pfad eingeben (*\<Laufwerk >*: \Programme\Microsoft SQL Server\110\DTS\Binn) auf die 64-Bit-Version des Hilfsprogramms.  
  
-   Ändern Sie die Reihenfolge der Pfade in der PATH-Umgebungsvariablen dauerhaft, indem platzieren den 64-Bit-Pfad (*\<Laufwerk >*: \Programme\Microsoft SQL Server\110\DTS\Binn) vor dem 32-Bit-Pfad (*\<Laufwerk >*: \ Programm Dateien (x86) \Microsoft SQL Server\110\DTS\Binn) in der Variablen.  
  
##  <a name="side"></a> Überlegungen zu Computern mit parallelen Installationen  
 Wenn [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] auf einem Computer installiert wird, auf dem [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] oder [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] installiert ist, sind mehrere Versionen des Hilfsprogramms **dtexec** installiert.  
  
 Um sicherzustellen, dass Sie die richtige Version des Hilfsprogramms, führen Sie an der Eingabeaufforderung das Hilfsprogramm ausführen, indem Sie den vollständigen Pfad eingeben (*\<Laufwerk >*: \Programme\Microsoft SQL Server\\< Version\>\DTS\Binn).  
  
##  <a name="phases"></a> Ausführungsphasen  
 Bei der Ausführung des Hilfsprogramms werden vier Phasen durchlaufen. Es handelt sich um die folgenden Phasen:  
  
1.  Befehlsermittlungsphase: Die Eingabeaufforderung liest die Liste der Optionen und Argumente, die angegeben wurden. Alle weiteren Phasen werden übersprungen, wenn eine **/?**- oder **/HELP** -Option festgestellt wird.  
  
2.  Paketladephase: Das durch die Option **/SQL**, **/FILE**oder **/DTS** angegebene Paket wird geladen.  
  
3.  Konfigurationsphase: Die Optionen werden in der folgenden Reihenfolge verarbeitet:  
  
    -   Optionen, die Paketflags, -variablen und -eigenschaften festlegen.  
  
    -   Optionen, die die Paketversion und den Paketbuild überprüfen.  
  
    -   Optionen, die das Laufzeitverhalten des Hilfsprogramms konfigurieren, z. B. die Berichterstellung.  
  
4.  Überprüfungs- und Ausführungsphase: Das Paket wird ausgeführt bzw. ohne Ausführung überprüft, falls die Option **/VALIDATE** angegeben wurde.  
  
##  <a name="exit"></a> Zurückgegebene Exitcodes  
 **Exitcodes, die vom dtexec-Hilfsprogramm zurückgegeben werden**  
  
 Wenn ein Paket ausgeführt wird, kann **dtexec** einen Exitcode zurückgeben. Der Exitcode wird dazu verwendet, die ERRORLEVEL-Variable aufzufüllen, deren Wert anschließend in bedingten Anweisungen oder in einer Verzweigungslogik innerhalb einer Batchdatei getestet werden kann. In der folgenden Tabelle sind die Werte aufgeführt, die das Hilfsprogramm **dtexec** beim Beenden festlegen kann.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Das Paket wurde erfolgreich ausgeführt.|  
|1|Bei der Paketausführung ist ein Fehler aufgetreten.|  
|3|Die Paketausführung wurde vom Benutzer abgebrochen.|  
|4|Das Hilfsprogramm konnte das angeforderte Paket nicht finden. Das Paket konnte nicht gefunden werden.|  
|5|Das Hilfsprogramm konnte das angeforderte Paket nicht laden. Das Paket konnte nicht geladen werden.|  
|6|Das Hilfsprogramm hat einen internen Fehler aufgrund syntaktischer oder semantischer Fehler in der Befehlszeile erkannt.|  
  
##  <a name="syntaxRules"></a> Syntaxregeln  
 **Syntaxregeln für das Hilfsprogramm**  
  
 Alle Optionen müssen mit einem Schrägstrich (/) oder einem Minuszeichen (-) beginnen. Die hier aufgeführten Optionen beginnen mit einem Schrägstrich (/); dieser kann jedoch durch ein Minuszeichen (-) ersetzt werden.  
  
 Enthält ein Argument ein Leerzeichen, muss es in Anführungszeichen eingeschlossen werden. Wenn das Argument nicht in Anführungszeichen eingeschlossen ist, darf es keine Leerzeichen enthalten.  
  
 Doppelte Anführungszeichen innerhalb von Zeichenfolgen, die selbst in Anführungszeichen eingeschlossen sind, stellen einzelne Anführungszeichen mit Escapezeichen dar.  
  
 Bei Optionen und Argumenten wird die Groß- und Kleinschreibung nicht beachtet; ausgenommen hiervon sind Kennwörter.  
  
##  <a name="cmdshell"></a> Aufrufen von dtexec mit xp_cmdshell  
 **Aufrufen von dtexec mit xp_cmdshell**  
  
 Sie können dtexec über die Eingabeaufforderung **xp_cmdshell** ausführen. Das folgende Beispiel zeigt, wie das Paket namens UpsertData.dtsx ausgeführt und sein Rückgabecode ignoriert wird:  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 Das folgende Beispiel zeigt, wie dasselbe Paket ausgeführt und sein Rückgabecode aufgezeichnet wird:  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> **WICHTIG!** In [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ist die Option **xp_cmdshell** für neue Installationen standardmäßig deaktiviert. Die Option kann durch Ausführen der gespeicherten Systemprozedur **sp_configure** aktiviert werden. Weitere Informationen finden Sie unter [xp_cmdshell (Serverkonfigurationsoption)](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
##  <a name="syntax"></a> Syntax  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameter"></a> Parameter  
  
-   **/?** [*Optionsname*]: (Optional). Zeigt die Befehlszeilenoptionen oder die Hilfe zu der in *Optionsname* angegebenen Option an und beendet dann das Hilfsprogramm.  
  
     Wenn Sie ein *Optionsname* -Argument angeben, startet **dtexec** die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation und zeigt das Thema für das Hilfsprogramm „dtexec“ an.  
  
-   **/Ca[llerInfo]**: (Optional). Gibt weitere Informationen für eine Paketausführung an. Wenn Sie mit dem SQL Server-Agent ein Paket ausführen, legt der Agent dieses Argument fest, um anzuzeigen, dass die Paketausführung vom SQL Server-Agent aufgerufen wird. Dieser Parameter wird ignoriert, wenn das Hilfsprogramm **dtexec** in der Befehlszeile ausgeführt wird.  
  
-   **/CheckF[Ile]** *Dateiangabe*: (Optional). Legt den Pfad und die Datei, der bzw. die in der **Dateiangabe** angegeben ist, als Wert für die *CheckpointFileName*-Eigenschaft des Pakets fest. Diese Datei wird beim erneuten Starten des Pakets verwendet. Wird diese Option angegeben, ohne einen Wert für den Dateinamen bereitzustellen, wird für die **CheckpointFileName** -Eigenschaft des Pakets eine leere Zeichenfolge festgelegt. Wenn diese Option nicht angegeben wird, werden die Werte im Paket beibehalten.  
  
-   **/CheckP[ointing]** *{on\off}* : (Optional). Legt einen Wert fest, der bestimmt, ob das Paket während der Paketausführung Prüfpunkte verwendet. Der Wert **on** gibt an, dass das fehlerhafte Paket erneut ausgeführt wird. Wenn das fehlerhafte Paket erneut ausgeführt wird, verwendet das Laufzeitmodul die Prüfpunktdatei, um das Paket von dem Punkt an, an dem der Fehler aufgetreten ist, erneut auszuführen.  
  
     Der Standardwert ist "on", wenn die Option ohne Angabe eines Wertes deklariert wird. Die Paketausführung erzeugt einen Fehler, wenn der Wert auf "on" festgelegt wurde und die Prüfpunktdatei nicht gefunden werden kann. Wenn diese Option nicht angegeben wird, wird der im Paket festgelegte Wert beibehalten. Weitere Informationen finden Sie unter [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
     Das Festlegen der Prüfpunktausführungsoption **/CheckPointing** von dtexec auf „on“ entspricht der **SaveCheckpoints** -Eigenschaft des Pakets „True“ oder der **CheckpointUsage** -Eigenschaft „Immer“.  
  
-   **/Com[mandFile]** *Dateiangabe*: (Optional). Gibt die Befehlsoptionen an, die mit **dtexec**ausgeführt werden. Die in *Dateiangabe* angegebene Datei wird geöffnet, und Optionen aus der Datei werden gelesen, bis EOF in der Datei gefunden wird. *Dateiangabe* ist eine Textdatei. Mit dem *Dateiangabe* -Argument werden der Dateiname und der Pfad der Befehlsdatei angegeben, die mit dem Ausführen des Pakets verknüpft werden soll.  
  
-   **/Conf[igFile]** *Dateiangabe*: (Optional). Gibt eine Konfigurationsdatei an, aus der Werte extrahiert werden sollen. Mithilfe dieser Option können Sie eine Laufzeitkonfiguration festlegen, die sich von der Konfiguration unterscheidet, die zur Entwurfszeit für das Paket angegeben wurde. Sie können abweichende Konfigurationseinstellungen in einer XML-Konfigurationsdatei speichern und die Einstellungen dann mithilfe der Option **/ConfigFile** vor der Paketausführung laden.  
  
     Sie können die Option **/ConfigFile** verwenden, um zur Laufzeit zusätzliche Konfigurationen zu laden, die Sie zur Entwurfszeit nicht angegeben haben. Sie können die Option **/ConfigFile** jedoch nicht verwenden, um konfigurierte Werte zu ersetzen, die Sie auch zur Entwurfszeit angegeben haben. Weitere Informationen zur Anwendung von Paketkonfigurationen finden Sie unter [Paketkonfigurationen](../../integration-services/packages/package-configurations.md).  
  
-   **/Conn[ection]** *ID_oder_Name;Verbindungszeichenfolge [[;ID_oder_Name;Verbindungszeichenfolge]…]*: (Optional). Gibt an, dass sich der Verbindungs-Manager mit dem angegebenen Namen oder GUID im Paket befindet. Eine Verbindungszeichenfolge wird ebenfalls angegeben.  
  
     Wenn diese Option verwendet wird, müssen beide Parameter angegeben werden: Der Name oder die GUID des Verbindungs-Managers muss mit dem *ID_oder_Name*-Argument bereitgestellt werden, und mit dem *Verbindungszeichenfolge*-Argument muss eine gültige Verbindungszeichenfolge angegeben werden. Weitere Informationen finden Sie unter [Integration Services-Verbindungen &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
     Sie können zur Laufzeit die Option **/Connection** verwenden, um Paketkonfigurationen von einem anderen Speicherort als dem zur Entwurfszeit angegebenen Speicherort zu laden. Die Werte dieser Konfigurationen ersetzen dann die Werte, die ursprünglich angegeben wurden. Sie können die Option **/Connection** jedoch nur für Konfigurationen verwenden, die einen Verbindungs-Manager verwenden (z.B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurationen). Um zu verstehen, wie Paketkonfigurationen angewendet werden, lesen Sie [SSIS-Paketkonfigurationen](../../integration-services/packages/package-configurations.md) und [Behavior Changes to Integration Services Features in SQL Server 2016](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)(Verhaltensänderungen von Integration Services Features in SQL Server 2016).  
  
-   **/Cons[oleLog]** [[*Anzeigeoptionen*];[*Listenoptionen*;*Quellname_oder_-GUID*]...]: (Optional). Zeigt während der Paketausführung bestimmte Protokolleinträge an der Konsole an. Wenn die Option nicht angegeben wird, werden keine Protokolleinträge an der Konsole angezeigt. Wenn die Option ohne Parameter zur Begrenzung der Anzeige angegeben wird, werden alle Protokolleinträge angezeigt. Wenn Sie die an der Konsole angezeigten Einträge begrenzen möchten, können Sie die anzuzeigenden Spalten mithilfe des *Anzeigeoptionen* -Parameters angeben und die Protokolleintragstypen mithilfe des *Listenoptionen* -Parameters begrenzen.  
  
    > **HINWEIS:**  Beim Ausführen eines Pakets auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server mithilfe des **/ISSERVER** -Parameters ist die Konsolenausgabe begrenzt, und die meisten der **/Cons[oleLog]** -Optionen sind nicht anwendbar. Alle Ausführungsprotokolle können in den verwandten Sichten vom Server oder über Standardberichte in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]angezeigt werden. Weitere Informationen zu den Berichten finden Sie unter [Berichte für den Integration Services-Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
     Die *Anzeigeoptionen* -Werte lauten wie folgt:  
  
    -   N (Name)  
  
    -   C (Computer)  
  
    -   O (Operator)  
  
    -   S (Name der Quelle)  
  
    -   G (GUID der Quelle)  
  
    -   X (Ausführungs-GUID)  
  
    -   M (Meldung)  
  
    -   T (Start- und Beendigungszeit)  
  
     Die *Listenoptionen* -Werte lauten wie folgt:  
  
    -   *I* – gibt die Inklusionsliste an. Es werden nur Protokolleinträge für die angegebenen Quellnamen oder -GUIDs erfasst.  
  
    -   *E* – gibt die Ausschlussliste an. Für die angegebenen Quellnamen oder -GUIDs werden keine Protokolleinträge erfasst.  
  
    -   Bei dem *Quellname_oder_-GUID* -Parameter, der für die Inklusions- oder Ausschlussliste verwendet wird, handelt es sich um einen Ereignisnamen, den Namen einer Quelle oder die GUID einer Quelle.  
  
     Wenn Sie die Option **/ConsoleLog** mehrmals in einer Befehlszeile verwenden, werden die einzelnen Optionen folgendermaßen verarbeitet:  
  
    -   Die Reihenfolge der Optionen spielt keine Rolle.  
  
    -   Wenn in der Befehlszeile keine Inklusionsliste angegeben wurde, gelten die Ausschlusslisten für alle Protokolleintragstypen.  
  
    -   Wenn in der Befehlszeile Inklusionslisten angegeben wurden, werden die Ausschlusslisten auf die Gesamtheit aller Inklusionslisten angewendet.  
  
     Im Abschnitt **Hinweise** finden Sie mehrere Beispiele für die Verwendung der **/ConsoleLog** -Option.  
  
-   **/D[ts](/sql-docs/docs/integration-services/packages/deploy-integration-services-ssis-projects-and-packages).  
  
     Mit dem *Paketpfad* -Argument wird der relative Pfad des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Pakets, der am Stammverzeichnis des SSIS-Paketspeichers beginnt, sowie der Name des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Pakets angegeben. Enthält der im *Paketpfad* -Argument angegebene Pfad- oder Dateiname ein Leerzeichen, müssen Sie das *Paketpfad* -Argument in Anführungszeichen setzen.  
  
     Die Option **/DTS** kann nicht zusammen mit der Option **/File** oder **/SQL** verwendet werden. Wenn mehrere Optionen angegeben werden, misslingt die Ausführung von **dtexec** .  
  
-   **/De[crypt]**  *Kennwort*: (Optional). Legt das Entschlüsselungskennwort fest, das beim Laden eines Pakets mit Kennwortverschlüsselung verwendet wird.  
  
-   (Optional) Erstellt die Debugdumpdateien (MDMP und TMP), wenn bei der Ausführung des Pakets ein oder mehrere angegebene Ereignisse auftreten. Das Argument *Fehlercode* gibt den Typ des Ereigniscodes – Fehler, Warnung oder Information – an, der auslöst, dass das System die Debugdumpdateien erstellt. Trennen Sie die *Fehlercode* -Argumente durch ein Semikolon (;), um mehrere Ereigniscodes anzugeben. Schließen Sie keine Anführungszeichen in das *Fehlercode* -Argument ein.  
  
     Im folgenden Beispiel werden die Debugdumpdateien generiert, wenn der DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER-Fehler auftritt.  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     **/ Dump** *Fehlercode*: standardmäßig [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] speichert die debugdumpdateien im Ordner * \<Laufwerk >*: \Programme\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > **HINWEIS:** Debugdumpdateien können vertrauliche Informationen enthalten. Verwenden Sie eine Zugriffssteuerungsliste, um den Zugriff auf die Dateien einzuschränken oder die Dateien in einen Ordner mit eingeschränktem Zugriff zu kopieren. Bevor Sie Ihre Debugdateien beispielsweise an Microsoft Support Services senden, wird empfohlen, vertrauliche Informationen zu entfernen.  
  
     Fügen Sie dem Registrierungsschlüssel HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath den REG_SZ-Wert **DumpOnCodes** hinzu, um diese Option auf alle vom Hilfsprogramm **dtexec** ausgeführten Pakete anzuwenden. Der Datenwert in **DumpOnCodes** gibt den oder die Fehlercodes an, die auslösen, dass das System die Debugdumpdateien erstellt. Mehrere Fehlercodes müssen durch ein Semikolon (;) getrennt werden.  
  
     Wenn Sie dem Registrierungsschlüssel einen **DumpOnCodes** -Wert hinzufügen und die Option **/Dump** verwenden, erstellt das System Debugdumpdateien, die auf beiden Einstellungen basieren.  
  
     Weitere Informationen zum Debuggen von Dumpdateien finden Sie unter [Generieren von Dumpdateien für die Paketausführung](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/DumpOnError**: (Optional) Erstellt die Debugdumpdateien mit der Erweiterung MDMP und TMP, wenn bei der Ausführung des Pakets ein beliebiger Fehler auftritt.  
  
     Standardmäßig [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] speichert die debugdumpdateien im Ordner * \<Laufwerk >*: Ordner "\Programme\Microsoft SQL Server\110\Shared\ErrorDumps".  
  
    > **HINWEIS:** Debugdumpdateien können vertrauliche Informationen enthalten. Verwenden Sie eine Zugriffssteuerungsliste, um den Zugriff auf die Dateien einzuschränken oder die Dateien in einen Ordner mit eingeschränktem Zugriff zu kopieren. Bevor Sie Ihre Debugdateien beispielsweise an Microsoft Support Services senden, wird empfohlen, vertrauliche Informationen zu entfernen.  
  
     Fügen Sie dem Registrierungsschlüssel HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath den REG_DWORD-Wert **DumpOnError** hinzu, um diese Option auf alle vom Hilfsprogramm **dtexec** ausgeführten Pakete anzuwenden. Der Wert des REG_DWORD-Werts **DumpOnError** bestimmt, ob die Option **/DumpOnError** mit dem Hilfsprogramm **dtexec** verwendet werden muss:  
  
    -   Ein Datenwert ungleich null (0) gibt an, dass das System beim Auftreten beliebiger Fehler Debugdumpdateien erstellt, unabhängig davon, ob Sie die Option **/DumpOnError** mit dem Hilfsprogramm **dtexec** verwenden.  
  
    -   Ein Datenwert gleich null (0) gibt an, dass das System keine Debugdumpdateien erstellt, sofern Sie nicht die Option **/DumpOnError** mit dem Hilfsprogramm **dtexec** verwenden.  
  
     Weitere Informationen zum Debuggen von Dumpdateien finden Sie unter [Generieren von Dumpdateien für die Paketausführung](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/ Env[Verweis]** *Umgebung Verweis-ID*: (Optional). Gibt die Umgebungsverweis-ID an, die von der Paketausführung verwendet wird, für ein Paket an, das auf dem Server mit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bereitgestellt ist. Die Parameter, die konfiguriert wurden, um an Variablen gebunden zu sein, verwenden die Werte der Variablen, die in der Umgebung enthalten sind.  
  
     Verwenden Sie die **/Env[Verweis]** -Option zusammen mit der **/ISServer** - und **/Server** -Option.  
  
     Dieser Parameter wird vom SQL Server-Agent verwendet.  
  
-   ** / F[Ile](/sql-docs/docs/integration-services/packages/deploy-integration-services-ssis-projects-and-packages)  
  
     Mit dem *Dateiangabe* -Argument werden Pfad und Dateiname des Pakets angegeben. Sie können den Pfad entweder als UNC-Pfad (Universal Naming Convention) oder als lokalen Pfad angeben. Enthält der im *Dateiangabe* -Argument angegebene Pfad- oder Dateiname ein Leerzeichen, muss das *Dateiangabe* -Argument in Anführungszeichen gesetzt werden.  
  
     Die Option **/File** kann nicht zusammen mit der Option **/DTS** oder **/SQL** verwendet werden. Wenn mehrere Optionen angegeben werden, misslingt die Ausführung von **dtexec** .  
  
-   **/H[elp]** [*Optionsname*]: (Optional). Zeigt die Hilfe zu den Optionen oder die Hilfe zu der mit *Optionsname* angegebenen Option an und beendet das Hilfsprogramm.  
  
     Wenn Sie ein *Optionsname* -Argument angeben, startet **dtexec** die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation und zeigt das Thema für das Hilfsprogramm „dtexec“ an.  
  
-   **/ISServer** *Paketpfad*: (Optional). Führt ein Paket aus, das auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt wurde. Mit dem *Paketpfad* -Argument wird der vollständige Pfad- und Dateiname des Pakets angegeben, das auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellt ist. Enthält der im *Paketpfad* -Argument angegebene Pfad- oder Dateiname ein Leerzeichen, müssen Sie das *Paketpfad* -Argument in Anführungszeichen setzen.  
  
     Das Paketformat lautet wie folgt:  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     Verwenden Sie die **/Server** -Option zusammen mit der **/ISSERVER** -Option. Nur die Windows-Authentifizierung kann ein Paket auf dem SSIS-Server ausführen. Der aktuelle Windows-Benutzer wird verwendet, um auf das Paket zuzugreifen. Wird die Option „/Server“ nicht angegeben, wird die standardmäßige lokale Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet.  
  
     Die Option **/ISSERVER** kann nicht zusammen mit der Option **/DTS**, **/SQL** oder **/File** verwendet werden. Wenn mehrere Optionen angegeben werden, misslingt die Ausführung von dtexec.  
  
     Dieser Parameter wird vom SQL Server-Agent verwendet.  
  
-   **/L[ogger]** *Klassen-ID_oder_Programm-ID;Konfigurationszeichenfolge*: (Optional). Ordnet das Ausführen eines [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Pakets einem oder mehreren Protokollanbietern zu. Mit dem *Klassen-ID_oder_Programm-ID* -Parameter wird der Protokollanbieter angegeben; diese Angabe kann in Form einer Klassen-GUID erfolgen. Die *Konfigurationszeichenfolge* ist die Zeichenfolge, die zum Konfigurieren des Protokollanbieters verwendet wird.  
  
     In der folgenden Liste sind die verfügbaren Protokollanbieter aufgeführt:  
  
    -   Textdatei:  
  
        -   ProgID: DTS.LogProviderTextFile.1  
  
        -   ClassID: {59B2C6A5-663F-4C20-8863-C83F9B72E2EB}  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLProfiler.1  
  
        -   ClassID: {5C0B8D21-E9AA-462E-BA34-30FF5F7A42A1}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLServer.1  
  
        -   ClassID: {6AA833A1-E4B2-4431-831B-DE695049DC61}  
  
    -   Windows-Ereignisprotokoll:  
  
        -   ProgID: DTS.LogProviderEventLog.1  
  
        -   ClassID: {97634F75-1DC7-4F1F-8A4C-DAF0E13AAA22}  
  
    -   XML-Datei:  
  
        -   ProgID: DTS.LogProviderXMLFile.1  
  
        -   ClassID: {AFED6884-619C-484F-9A09-F42D56E1A7EA}  
  
-   **/M[axConcurrent]** *gleichzeitig_ausführbare_Dateien*: (Optional). Gibt die Anzahl von ausführbaren Dateien an, die das Paket gleichzeitig ausführen kann. Der angegebene Wert muss entweder eine nicht negative ganze Zahl oder -1 sein. Ein Wert von „-1“ bedeutet, dass [!INCLUDE[ssIS](../../includes/ssis-md.md)] eine maximale Anzahl gleichzeitig aktiver ausführbarer Dateien zulässt, die der Gesamtanzahl von Prozessoren plus zwei des Computers entspricht, auf dem das Paket ausgeführt wird.  
  
-   **/Pack[age]** *Paketname*: (Optional). Gibt das Paket an, das ausgeführt wird. Dieser Parameter wird hauptsächlich verwendet, wenn Sie das Paket von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]ausführen.  
  
-   **/P[assword]** *Kennwort*: (Optional). Ermöglicht das Abrufen eines Pakets, das durch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung geschützt ist. Diese Option wird zusammen mit der Option **/User** verwendet. Wird die Option **/Password** nicht angegeben und die Option **/User** verwendet, wird ein leeres Kennwort verwendet. Der Wert *Kennwort* kann in Anführungszeichen eingeschlossen werden.  
  
    > **WICHTIG!** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par[ameter]** [$Package:: | $Project:: | $ServerOption::] *Parametername* [(Datentyp)]; *Literalwert*: (Optional). Gibt Parameterwerte an. Es können mehrere **/Parameter** -Optionen angegeben werden. Die Datentypen sind CLR TypeCodes als Zeichenfolgen. Für einen Nicht-Zeichenfolge-Parameter wird der Datentyp in Klammern angegeben und folgt dem Parameternamen.  
  
     Die **/Parameter** -Option kann nur mit der **/ISServer** -Option angegeben werden.  
  
     Sie verwenden die Präfixe "$Package", "$Project" und "$ServerOption", um einen Paket-, Projekt- oder Serveroptionsparameter anzugeben. Der standardmäßige Parametertyp ist "Paket".  
  
     Im Folgenden finden Sie ein Beispiel zum Ausführen eines Pakets und Bereitstellen von "myvalue" für den Projektparameter (myparam) und eines ganzzahligen Werts "12" für den Projektparameter (anotherparam).  
  
     `Dtexec /isserver “SSISDB\MyFolder\MyProject\MyPackage.dtsx” /server “.” /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     Eigenschaften des Verbindungs-Managers können auch mithilfe von Parametern festgelegt werden. Sie verwenden das Präfix "CM", um einen Parameter des Verbindungs-Managers zu kennzeichnen.  
  
     Im folgenden Beispiel wird die InitialCatalog-Eigenschaft des SourceServer-Verbindungs-Managers auf `ssisdb`festgelegt.  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     Im folgenden Beispiel wird die ServerName-Eigenschaft des SourceServer-Verbindungs-Managers auf einen Punkt (.) festgelegt, um den lokalen Server anzugeben.  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj[ect]** *Projektdatei*: (Optional). Gibt das Projekt an, von dem das ausgeführte Paket abgerufen wird. Das *Projektdatei* -Argument gibt den ISPAC-Dateinamen an. Dieser Parameter wird hauptsächlich verwendet, wenn Sie das Paket von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]ausführen.  
  
-   **/Rem** *Kommentar*: (Optional). Schließt einen Kommentar in die Befehlszeile oder in Befehlsdateien ein. Das Argument ist optional. Der Wert für *Kommentar* ist eine Zeichenfolge, die entweder in Anführungszeichen eingeschlossen werden muss oder keine Leerzeichen enthalten darf. Wird kein Argument angegeben, wird eine leere Zeile eingefügt. Während der Befehlsermittlungsphase werden*Kommentar* -Werte nicht berücksichtigt.  
  
-   **/Rep[orting]** *Ebene* [*;Ereignis-GUID_ oder_-name*[*;Ereignis-GUID_ oder_-name*[...]]: (Optional). Gibt an, welche Meldungstypen gemeldet werden sollen. Für *Ebene* stehen folgende Berichtsoptionen zur Verfügung:  
  
     **N** Keine Berichterstellung.  
  
     **E** Fehler werden gemeldet.  
  
     **W** Warnungen werden gemeldet.  
  
     **I** Informationsmeldungen werden gemeldet.  
  
     **C** Benutzerdefinierte Ereignisse werden gemeldet.  
  
     **D** Datenfluss-Taskereignisse werden gemeldet.  
  
     **P** Der Status wird gemeldet.  
  
     **V** Ausführliche Berichterstellung.  
  
     Die Argumente V und N schließen sich gegenseitig und alle anderen Argumente aus; sie müssen allein angegeben werden. Wenn die Option **/Reporting** nicht angegeben wird, umfasst die Standardebene die Optionen **E** (Fehler), **W** (Warnungen) und **P** (Status).  
  
     Vor allen Ereignissen wird ein Zeitstempel im Format "DD.MM.YY HH:MM:SS" sowie ggf. ein GUID oder ein Anzeigename aufgeführt.  
  
     Der optionale *Ereignis-GUID_ oder_-name* -Parameter ist eine Ausnahmeliste für die Protokollanbieter. Die Ausnahmeliste gibt die normalerweise protokollierten Ereignisse an, die nicht protokolliert werden.  
  
     Sie müssen ein Ereignis nur ausschließen, wenn dieses standardmäßig protokolliert wird.  
  
-   **/Res[tart]** {*deny | force | ifPossible*}: (Optional). Gibt einen neuen Wert für die <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> -Eigenschaft des Pakets an. Die Parameter haben folgende Bedeutung:  
  
     *Deny* legt die <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> -Eigenschaft auf <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>.  
  
     *Force* legt die <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> -Eigenschaft auf <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>.  
  
     *ifPossible* legt die <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> -Eigenschaft auf <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>.  
  
     Der Standardwert **force** wird verwendet, wenn kein Wert angegeben wird.  
  
-   **/Set** [$Sensitive::]*Eigenschaftspfad;Wert*: (Optional). Überschreibt die Konfiguration eines Parameters, einer Variablen, einer Eigenschaft, eines Containers, eines Protokollanbieters, eines Foreach-Enumerators oder einer Verbindung innerhalb eines Pakets. Wenn diese Option verwendet wird, ändert **/Set** das *Eigenschaftspfad* -Argument in den angegebenen Wert. Es können mehrere **/Set** -Optionen angegeben werden.  
  
     Zusätzlich zur Verwendung der **/Set** -Option mit der **/F[ile]-Option** können Sie die **/Set** -Option auch mit der **/ISServer** -Option oder der **/Project-** Option verwenden. Bei Verwendung von **/Set** mit **/Project**legt **/Set** Parameterwerte fest. Bei Verwendung von **/Set** mit **/ISServer**legt **/Set** Eigenschaftenüberschreibungen fest. Wenn Sie zusätzlich **/Set** mit **/ISServer**verwenden, können Sie das optionale Präfix „$Sensitive“ verwenden, um anzugeben, dass die Eigenschaft auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server als vertraulich behandelt werden soll.  
  
     Der Wert des *Eigenschaftspfads* kann mithilfe des Paketkonfigurations-Assistenten bestimmt werden. Die Pfade für die von Ihnen ausgewählten Elemente werden auf der letzten Seite des Assistenten, **Assistenten abschließen** , angezeigt und können von dort kopiert werden. Wenn Sie den Assistenten nur für diesen Zweck verwendet haben, können Sie ihn nach dem Kopieren der Pfade abbrechen.  
  
     Das folgende Beispiel zeigt, wie ein im Dateisystem gespeichertes Paket ausgeführt und ein neuer Wert für eine Variable angegeben wird:  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     Im folgenden Beispiel wird das Ausführen eines Pakets von einer ISPAC-Projektdatei sowie das Festlegen des Pakets und der Projektparameter gezeigt.  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     Sie können die Option **/Set** verwenden, um den Speicherort zu ändern, von dem Paketkonfigurationen geladen werden. Sie können die Option **/Set** jedoch nicht verwenden, um einen Wert zu überschreiben, der zur Entwurfszeit von einer Konfiguration angegeben wurde. Um zu verstehen, wie Paketkonfigurationen angewendet werden, lesen Sie [SSIS-Paketkonfigurationen](../../integration-services/packages/package-configurations.md) und [Behavior Changes to Integration Services Features in SQL Server 2016](http://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794)(Verhaltensänderungen von Integration Services Features in SQL Server 2016).  
  
-   **/Ser[ver]** *Server*: (Optional). Wenn die Option **/SQL** oder **/DTS** verwendet wurde, gibt diese Option den Namen des Servers an, von dem das Paket abgerufen werden soll. Wenn Sie die Option **/Server** nicht angeben, die Option **/SQL** oder **/DTS** jedoch angegeben wird, wird versucht, das Paket auf den lokalen Server anzuwenden. Der *Serverinstanz* -Wert kann in Anführungszeichen eingeschlossen werden.  
  
     Die Option **/Ser[ver]** ist erforderlich, wenn die Option **/ISServer** angegeben wird.  
  
-   ** / SQ[L](/sql-docs/docs/integration-services/packages/deploy-integration-services-ssis-projects-and-packages).  
  
     Mit dem *Paketpfad* -Argument wird der Name des abzurufenden Pakets angegeben. Werden Ordner in die Pfadangabe eingeschlossen, werden sie mit umgekehrten Schrägstrichen („\\“) abgeschlossen. Der *Paketpfad* -Wert kann in Anführungszeichen eingeschlossen werden. Enthält der im *Paketpfad* -Argument angegebene Pfad- oder Dateiname ein Leerzeichen, müssen Sie das *Paketpfad* -Argument in Anführungszeichen setzen.  
  
     Sie können die Optionen **/User**, **/Password**und **/Server** zusammen mit der **/SQL** -Option verwenden.  
  
     Wenn Sie die Option **/User** nicht angeben, wird die Windows-Authentifizierung für den Zugriff auf das Paket verwendet. Wenn Sie die Option **/User** verwenden, wird der mit **/User** angegebene Anmeldename der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung zugeordnet.  
  
     Die Option **/Password** wird nur zusammen mit der **/User** -Option verwendet. Wenn Sie die Option **/Password** verwenden, erfolgt der Zugriff auf das Paket mit den angegebenen Benutzernamen- und Kennwortinformationen. Wird die Option **/Password** nicht angegeben, wird ein leeres Kennwort verwendet.  
  
    > **WICHTIG!** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
     Wird die Option **/Server** nicht angegeben, wird die standardmäßige lokale Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet.  
  
     Die Option **/SQL** kann nicht zusammen mit der Option **/DTS** oder **/File** verwendet werden. Wenn mehrere Optionen angegeben werden, misslingt die Ausführung von **dtexec** .  
  
-   **/Su[m]**: (Optional). Zeigt einen inkrementellen Zähler an, der die Anzahl der Zeilen enthält, die von der nächsten Komponente empfangen werden.  
  
-   **/U[ser]** *Benutzername*: (Optional). Ermöglicht das Abrufen eines Pakets, das durch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung geschützt ist. Diese Option wird nur verwendet, wenn die Option **/SQL** angegeben wird. Der *Benutzername* -Wert kann in Anführungszeichen eingeschlossen werden.  
  
    > **WICHTIG!**  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va[lidate]**: (Optional). Beendet das Ausführen des Pakets nach der Überprüfungsphase, ohne das Paket tatsächlich auszuführen. Während der Überprüfung bewirkt die Verwendung von **/WarnAsError** , dass **dtexec** eine Warnung wie einen Fehler behandelt. Daher erzeugt das Paket einen Fehler, wenn während des Überprüfens eine Warnung ausgegeben wird.  
  
-   **/VerifyB[uild]** *Hauptversion*[*;Nebenversion*[*;Build*]]: (Optional). Überprüft die Buildnummer eines Pakets anhand der Buildnummern, die während der Überprüfungsphase mit den Argumenten *Hauptversion*, *Nebenversion*und *Build* angegeben wurden. Stimmen die Buildnummern nicht überein, wird das Paket nicht ausgeführt.  
  
     Bei den Werten handelt es sich um lange ganze Zahlen. Das Argument kann eine von drei Formen annehmen, wobei ein Wert für *Hauptversion* immer erforderlich ist:  
  
    -   *Hauptversion*  
  
    -   *Hauptversion*;*Nebenversion*  
  
    -   *Hauptversion*; *Nebenversion*; *Build*  
  
-   **/VerifyP[ackageID]** *Paket-ID*: (Optional). Überprüft die GUID des auszuführenden Pakets anhand des Werts, der im *Paket-ID* -Argument angegeben wurde.  
  
-   **/VerifyS[igned]**: (Optional). Veranlasst [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dazu, die digitale Signatur des Pakets zu überprüfen. Wenn das Paket nicht signiert oder die Signatur nicht gültig ist, schlägt das Paket fehl. Weitere Informationen finden Sie unter [Identifizieren der Quelle von Paketen mit digitalen Signaturen](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).  
  
    > **WICHTIG!** Wenn Sie die Überprüfung der Signatur des Pakets konfiguriert haben, prüft [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] lediglich, ob die digitale Signatur vorhanden und gültig ist und ob die Quelle vertrauenswürdig ist. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] überprüft nicht, ob Änderungen am Paket vorgenommen wurden.  
  
    > **HINWEIS** : Der optionale Registrierungswert **BlockedSignatureStates** kann eine Einstellung angeben, die restriktiver ist als die Option für die digitale Signatur, die in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder in der **dtexec** -Befehlszeile festgelegt wurde. In dieser Situation überschreibt die restriktivere Registrierungseinstellung die andere Einstellung.  
  
-   **/VerifyV[ersionID]** *Versions-ID*: (Optional). Überprüft die Versions-GUID eines auszuführenden Pakets; diese wird mit dem Wert verglichen, der während der Paketüberprüfungsphase im *Versions-ID* -Argument angegeben wurde.  
  
-   **/VLog** *[Dateiangabe]*: (Optional). Schreibt alle Integration Services-Paketereignisse an die Protokollanbieter, die beim Entwurf des Pakets aktiviert wurden. Geben Sie im *Dateiangabe* -Parameter einen Pfad- und Dateinamen an, damit Integration Services einen Protokollanbieter für Textdateien aktiviert und Protokollereignisse in eine festgelegte Textdatei schreibt.  
  
     Wenn Sie den *Dateiangabe* -Parameter nicht einschließen, aktiviert Integration Services keinen Protokollanbieter für Textdateien. Integration Services schreibt dann Protokollereignisse nur an die Protokollanbieter, die beim Entwurf des Pakets aktiviert wurden.  
  
-   **/W[arnAsError]**: (Optional). Bewirkt, dass das Paket eine Warnung wie einen Fehler behandelt. Das Paket erzeugt daher einen Fehler, wenn während des Überprüfens eine Warnung ausgegeben wird. Wenn während des Überprüfens keine Warnung ausgegeben wird und die Option **/Validate** nicht angegeben wurde, wird das Paket ausgeführt.  
  
-   **/X86**: (Optional). Veranlasst den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent, das Paket im 32-Bit-Modus auf einem 64-Bit-Computer auszuführen. Diese Option wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent festgelegt, wenn die folgenden Bedingungen den Wert True haben:  
  
    -   Der Auftragsschritt lautet **SQL Server Integration Services-Paket**.  
  
    -   Die Option **32 Bit-Laufzeit verwenden** auf der Registerkarte **Ausführungsoptionen** des Dialogfelds **Neuer Auftragsschritt** wird aktiviert.  
  
     Sie können diese Option auch für einen Auftragsschritt des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents festlegen, indem Sie die gespeicherten Prozeduren oder SQL Server Management Objects (SMO) verwenden, um den Auftrag programmgesteuert zu erstellen.  
  
     Diese Option wird nur von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent verwendet. Diese Option wird ignoriert, wenn Sie das Hilfsprogramm **dtexec** an der Eingabeaufforderung ausführen.  
  
##  <a name="remark"></a> Hinweise  
 Die Reihenfolge, in der Sie die Befehlsoptionen angeben, kann sich auf die Art und Weise der Paketausführung auswirken:  
  
-   Optionen werden in der Reihenfolge verarbeitet, in der sie in der Befehlszeile erkannt werden. Befehlsdateien werden eingelesen, wenn sie in der Befehlszeile erkannt werden. Die Befehle in der Befehlsdatei werden ebenfalls in der Reihenfolge verarbeitet, in der sie erkannt werden.  
  
-   Wenn eine Option, ein Parameter oder eine Variable mehrmals in derselben Befehlszeilenanweisung angegeben wird, hat die letzte Instanz der Option Vorrang.  
  
-   Die Optionen**/Set** und **/ConfigFile** werden in der Reihenfolge verarbeitet, in der sie erkannt werden.  
  
##  <a name="example"></a> Beispiele  
 Die folgenden Beispiele zeigen, wie das Eingabeaufforderungs-Hilfsprogramm **dtexec** verwendet wird, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete zu konfigurieren und auszuführen.  
  
 **Ausführen von Paketen**  
  
 Verwenden Sie folgenden Code, um ein in [!INCLUDE[ssIS](../../includes/ssis-md.md)] gespeichertes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Paket auszuführen, das die Windows-Authentifizierung verwendet:  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 Wenn Sie ein [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paket ausführen möchten, das im Ordner „Dateisystem“ im SSIS-Paketspeicher gespeichert wird, verwenden Sie folgenden Code:  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 Verwenden Sie folgenden Code, um ein Paket, das die Windows-Authentifizierung verwendet und in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert ist, zu überprüfen, ohne das Paket auszuführen:  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 Verwenden Sie folgenden Code, um ein im Dateisystem gespeichertes [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paket auszuführen:  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 Verwenden Sie folgenden Code, um ein im Dateisystem gespeichertes [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paket auszuführen und Protokollierungsoptionen anzugeben:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 Verwenden Sie folgenden Code, um ein Paket auszuführen, das die Windows-Authentifizierung verwendet und in der standardmäßigen lokalen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeichert ist, und um die Paketversion vor dem Ausführen zu überprüfen:  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 Verwenden Sie folgenden Code, um ein im Dateisystem gespeichertes und extern konfiguriertes [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Paket auszuführen:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> **HINWEIS:** Die *Paketpfad* - oder *Dateiangabe* -Argumente der Optionen /SQL, /DTS oder /FILE müssen in Anführungszeichen eingeschlossen werden, wenn der Pfad- oder Dateiname ein Leerzeichen enthält. Wenn das Argument nicht in Anführungszeichen eingeschlossen ist, darf es keine Leerzeichen enthalten.  
  
 **Protokollierungsoption**  
  
 Sind beispielsweise die Protokolleintragstypen A, B und C vorhanden, zeigt die Option **ConsoleLog** ohne Parameter alle drei Protokolltypen mit allen Feldern an:  
  
```  
/CONSOLELOG  
```  
  
 Die folgende Option zeigt alle Protokolltypen an, aber nur mit der Namens- und der Meldungsspalte:  
  
```  
/CONSOLELOG NM  
```  
  
 Die folgende Option zeigt alle Spalten an, aber nur für den Protokolleintragstyp A:  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 Die folgende Option zeigt nur den Protokolleintragstyp A mit der Namens- und der Meldungsspalte an:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 Die folgende Option zeigt Protokolleinträge für die Protokolleintragstypen A und B an:  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 Sie können die gleichen Ergebnisse erzielen, indem Sie mehrere **ConsoleLog** -Optionen verwenden:  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 Wird die Option **ConsoleLog** ohne Parameter verwendet, werden alle Felder angezeigt. Die Angabe des *Listenoptionen* -Parameters bewirkt, dass nur der Protokolleintragstyp A mit allen Feldern angezeigt wird:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 Durch folgenden Code werden alle Protokolleintragstypen mit Ausnahme des Protokolleintragstyps A angezeigt; d. h. es werden nur die Protokolleintragstypen B und C angezeigt:  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 Im folgenden Beispiel werden die gleichen Ergebnisse erzielt, indem die Option **ConsoleLog** mehrmals verwendet und eine einzelne Ausnahme definiert wird:  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 Im folgenden Beispiel werden keine Protokollmeldungen angezeigt, da ein Protokolleintragstyp, der in der Inklusions- und der Ausschlussliste enthalten ist, ausgeschlossen wird.  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **Option SET**  
  
 Im folgenden Beispiel wird die Verwendung der Option **/SET** gezeigt, mit der Sie den Wert der Paketeigenschaft oder -variablen ändern können, wenn Sie das Paket über die Befehlszeile starten.  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **Projektoption**  
  
 Im folgenden Beispiel wird die Verwendung der Optionen **/Project** und **/Package** gezeigt.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 Im folgenden Beispiel werden die Verwendung der Optionen **/Project** und **/Package** sowie das Festlegen von Paket- und Projektparametern gezeigt.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **ISServer-Option**  
  
 Im folgenden Beispiel wird die Verwendung der Option **/ISServer** gezeigt.  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 Im folgenden Beispiel werden die Verwendung der Option **/ISServer** sowie das Festlegen der Projekt- und Verbindungs-Manager-Parameter gezeigt.  
  
```  
/Server localhost /ISServer “\SSISDB\MyFolder\Integration Services Project1\Package.dtsx” /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Blogeintrag zu [Exitcodes, DTEXEC und SSIS-Katalog](http://www.mattmasson.com/2012/02/exit-codes-dtexec-and-ssis-catalog/)auf www.mattmasson.com.  
  
  

