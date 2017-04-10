---
title: "dtutil (Hilfsprogramm) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Verifizieren von Paketen"
  - "Überprüfen von Paketen"
  - "Verschieben von Paketen"
  - "Pakete [Integration Services], Befehlszeilenoptionen"
  - "Eingabeaufforderung [Integration Services]"
  - "SQL Server Integration Services-Pakete, Befehlszeilenoptionen"
  - "Kopieren von Paketen"
  - "Testen auf Vorhandensein [Integration Services]"
  - "Integration Services-Pakete, Befehlszeilenoptionen"
  - "SSIS-Pakete, Befehlszeilenoptionen"
  - "Löschen von Paketen"
  - "dtutil (Hilfsprogramm)"
  - "Entfernen von Paketen"
  - "Verlagern von Paketen"
ms.assetid: 6c7975ff-acec-4e6e-82e5-a641e3a98afe
caps.latest.revision: 114
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 114
---
# dtutil (Hilfsprogramm)
  Das Eingabeaufforderungs-Hilfsprogramm **dtutil** dient zum Verwalten von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Paketen. Mit dem Hilfsprogramm kann ein Paket kopiert, verschoben oder gelöscht und das Vorhandensein eines Pakets überprüft werden. Diese Aktionen können für jedes [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paket ausgeführt werden, das sich an einem der drei folgenden Speicherorte befindet: in einer [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Datenbank, im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paketspeicher oder im Dateisystem. Falls das Hilfsprogramm auf ein Paket zugreift, das in **msdb** gespeichert ist, werden Sie möglicherweise zur Eingabe eines Benutzernamens und eines Kennworts aufgefordert. Wenn die Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung verwendet, ist sowohl ein Benutzername als auch ein Kennwort erforderlich. Falls der Benutzername fehlt, versucht **dtutil** sich bei [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mit der Windows-Authentifizierung anzumelden. Der Speichertyp des Pakets wird durch die Optionen **/SQL**, **/FILE** und **/DTS** identifiziert.  
  
 Die Verwendung von Befehlsdateien, oder die Umleitung wird vom Eingabeaufforderungs-Hilfsprogramm **dtutil** nicht unterstützt.  
  
 Das Eingabeaufforderungs-Hilfsprogramm **dtutil** schließt die folgenden Funktionen ein:  
  
-   Hinweise an der Eingabeaufforderung, um die Befehlszeilenaktion zu dokumentieren und die Verwendung zu erleichtern.  
  
-   Schutz vor Überschreiben. Wenn Sie Pakete kopieren oder verschieben, werden Sie vor dem Überschreiben eines vorhandenen Pakets zur Bestätigung des Vorgangs aufgefordert.  
  
-   Konsolenhilfe, um Informationen zu den Befehlsoptionen für **dtutil** bereitzustellen.  
  
> [!NOTE]  
>  Zahlreiche dtutil-Vorgänge können auch visuell über eine Instanz von [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ausgeführt werden. Weitere Informationen finden Sie unter [Paketverwaltung &#40;SSIS-Dienst&#41;](../integration-services/service/package-management-ssis-service.md).  
  
 Die Optionen können in beliebiger Reihenfolge eingegeben werden. Der senkrechte Strich („|“) dient als **OR**-Operator und wird verwendet, um mögliche Werte anzuzeigen. Sie müssen eine der Optionen verwenden, die durch den **OR**-Operator in Form des senkrechten Striches getrennt sind.  
  
 Alle Optionen müssen mit einem Schrägstrich (/) oder einem Minuszeichen (-) beginnen. Verwenden Sie jedoch kein Leerzeichen zwischen dem Schrägstrich oder Minuszeichen und dem Text für die Option. Andernfalls schlägt der Befehl fehl.  
  
 Bei den Argumenten muss es sich um Zeichenfolgen handeln, die entweder in Anführungszeichen eingeschlossen sind oder keine Leerzeichen enthalten.  
  
 Doppelte Anführungszeichen innerhalb von Zeichenfolgen, die selbst in Anführungszeichen eingeschlossen sind, sind als einzelne Anführungszeichen mit Escapezeichen aufzufassen.  
  
 Mit Ausnahme von Argumenten für Kennwörter wird bei Optionen und Argumenten die Groß- und Kleinschreibung nicht beachtet.  
  
 **Überlegungen zur Installation auf 64-Bit-Computern**  
  
 Auf einem 64-Bit-Computer installiert [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] eine 64-Bit-Version des Hilfsprogramms **dtexec** (dtexec.exe) und des Hilfsprogramms **dtutil** (dtutil.exe). Wählen Sie zum Installieren der 32-Bit-Versionen dieser [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Tools während des Setups entweder Clienttools oder [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Standardmäßig wird auf einem 64-Bit-Computer, auf dem sowohl die 64-Bit-Version als auch die 32-Bit-Version eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Befehlszeilen-Hilfsprogramms installiert ist, die 32-Bit-Version an der Eingabeaufforderung ausgeführt. Die 32-Bit-Version wird ausgeführt, da der Verzeichnispfad für die 32-Bit-Version in der PATH-Umgebungsvariablen vor dem Verzeichnispfad für die 64-Bit-Version aufgeführt wird. (Typischerweise ist der 32-Bit-Verzeichnispfad „*\<Laufwerk>*:\Programme(x86)\Microsoft SQL Server\130\DTS\Binn“, während der 64-Bit-Verzeichnispfad „*\<Laufwerk>*:\Programme\Microsoft SQL Server\130\DTS\Binn“ lautet.)  
  
> [!NOTE]  
>  Wenn Sie das Hilfsprogramm mithilfe des SQL Server-Agents ausführen, verwendet dieser automatisch die 64-Bit-Version des Hilfsprogramms. Der SQL Server-Agent sucht die richtige ausführbare Datei für das Hilfsprogramm in der Registrierung und nicht in der PATH-Umgebungsvariablen.  
  
 Wenn Sie sicherstellen möchten, dass die 64-Bit-Version des Hilfsprogramms an der Eingabeaufforderung ausgeführt wird, können Sie einen der folgenden Schritte ausführen:  
  
-   Öffnen Sie eine Eingabeaufforderung, wechseln Sie in das Verzeichnis mit der 64-Bit-Version des Hilfsprogramms *(\<Laufwerk>*:\Programme\Microsoft SQL Server\130\DTS\Binn), und führen Sie anschließend das Hilfsprogramm aus diesem Verzeichnis aus.  
  
-   Führen Sie an der Eingabeaufforderung das Hilfsprogramm aus, indem Sie den vollständigen Pfad (*\<Laufwerk>*:\Programme\Microsoft SQL Server\130\DTS\Binn) der 64-Bit-Version des Hilfsprogramms eingeben.  
  
-   Ändern Sie die Reihenfolge der Pfade in der PATH-Umgebungsvariablen dauerhaft, indem Sie den 64-Bit-Pfad (*\<Laufwerk>*:\Programme\Microsoft SQL Server\130\DTS\Binn) in der Variablen vor dem 32-Bit-Pfad (*\<Laufwerk>*:\Programme(x86)\Microsoft SQL Server\130\DTS\Binn) platzieren.  
  
## Syntax  
  
```  
  
dtutil /option [value] [/option [value]]...  
```  
  
#### Parameter  
  
|Option|Description|  
|------------|-----------------|  
|/?|Zeigt die Befehlszeilenoptionen an.|  
|/C[opy] *location;destinationPathandPackageName*|Gibt eine Kopieraktion für ein [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paket an. Sie müssen zunächst mithilfe der Option **/FI**, **/SQ** oder **DT** den Speicherort des Pakets angeben, um diesen Parameter verwenden zu können. Geben Sie anschließend den Zielspeicherort und den Zielpaketnamen an. Das *destinationPathandPackageName*-Argument gibt an, wohin das [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paket kopiert wird. Wenn **SQL** als Ziel-*location* angegeben wird, müssen im Befehl auch die Argumente *DestUser*, *DestPassword* und *DestServer* angegeben werden.<br /><br /> Wenn bei der **Copy**-Aktion ein vorhandenes Paket am Ziel gefunden wird, fordert **dtutil** den Benutzer auf, das Löschen des Pakets zu bestätigen. Die Angabe von **Y** bewirkt, dass das Paket überschrieben wird; mit **N** wird das Programm beendet. Wenn der Befehl das *Quiet*-Argument einschließt, wird keine Aufforderung angezeigt, und vorhandene Pakete werden ggf. überschrieben.|  
|/Dec[rypt] *Kennwort*|(Optional). Legt das Entschlüsselungskennwort fest, das beim Laden eines Pakets mit Kennwortverschlüsselung verwendet wird.|  
|/Del[ete]|Löscht das durch die Option *SQL*, *DTS* oder *FILE* angegebene Paket. Falls **dtutil** das Paket nicht löschen kann, wird das Programm beendet.|  
|/DestP[assword] *Kennwort*|Gibt das Kennwort an, das mit der Option SQL verwendet wird, um mithilfe der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung eine Verbindung mit der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz herzustellen. Wenn *DESTPASSWORD* in einer Befehlszeile angegeben wird, die die Option *DTSUSER* nicht einschließt, wird ein Fehler generiert.<br /><br /> Hinweis: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)].|  
|/DestS[erver] *Serverinstanz*|Gibt den Servernamen an, der für eine beliebige Aktion verwendet wird, in deren Verlauf ein Zielpaket in einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz gespeichert wird. Mit dieser Option wird beim Speichern eines [!INCLUDE[ssIS](../includes/ssis-md.md)]-Pakets ein nicht lokaler oder ein nicht standardmäßiger Server identifiziert. *DESTSERVER* darf nicht in einer Befehlszeile angegeben werden, die keine Aktion einschließt, die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zugeordnet ist. Geeignete Aktionen, um diese Option anzugeben, wären beispielsweise Aktionen, wie sie durch *SIGN SQL*, *COPY SQL* oder *MOVE SQL* angegeben werden.<br /><br /> Ein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanzname kann angegeben werden, indem dem Servernamen ein umgekehrter Schrägstrich und der Instanzname hinzugefügt wird.|  
|/DestU[ser] *Benutzername*|Gibt den Benutzernamen an, der mit den Optionen *SIGN SQL*, *COPY SQL* und *MOVE SQL* verwendet wird, um eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] herzustellen, die die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung verwendet. *DESTUSER* darf nicht in einer Befehlszeile angegeben werden, die die Optionen *SIGN SQL*, *COPY SQL* oder *MOVE SQL* nicht enthält.|  
|/Dump *Prozess-ID*|(Optional) Veranlasst den angegebenen Prozess, entweder das Hilfsprogramm **dtexec** oder den Prozess **dtsDebugHost.exe**, anzuhalten und die Debugdumpdateien „.mdmp“ und „.tmp“ zu erstellen.<br /><br /> Hinweis: Um die Option **/Dump** verwenden zu können, muss Ihnen das Benutzerrecht für Debugprogramme (SeDebugPrivilege) zugewiesen sein.<br /><br /> Verwenden Sie den Windows Task-Manager, um die *Prozess-ID* für den Prozess zu suchen, den Sie anhalten möchten.<br /><br /> Standardmäßig speichert [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] die Debugdumpdateien im Ordner „*\<Laufwerk>*:\Programme\Microsoft SQL Server\130\Shared\ErrorDumps.“<br /><br /> Weitere Informationen zum **dtexec**-Hilfsprogramm und zum **dtsDebugHost.exe**-Prozess finden Sie unter [dtexec-Hilfsprogramm](../integration-services/packages/dtexec-utility.md) and [Erstellen, Bereitstellen und Debuggen von benutzerdefinierten Objekten](../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).<br /><br /> Weitere Informationen zum Debuggen von Dumpdateien finden Sie unter [Generieren von Dumpdateien für die Paketausführung](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).<br /><br /> Hinweis: Debugdumpdateien können vertrauliche Informationen enthalten. Verwenden Sie eine Zugriffssteuerungsliste, um den Zugriff auf die Dateien einzuschränken oder die Dateien in einen Ordner mit eingeschränktem Zugriff zu kopieren.|  
|/DT[S] *filespec*|Gibt an, dass sich das [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paket, auf das sich der Vorgang bezieht, im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paketspeicher befindet. Das *filespec*-Argument muss den Ordnerpfad beginnend mit dem Stamm des [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paketspeichers enthalten. Standardmäßig lauten die Namen der Stammordner in der Konfigurationsdatei "MSDB" und "Dateisystem". Pfade, die ein Leerzeichen enthalten, müssen in doppelte Anführungszeichen gesetzt werden.<br /><br /> Wenn die Option DT[S] in derselben Befehlszeile wie eine der folgenden Optionen angegeben wird, wird der Fehler DTEXEC_DTEXECERROR zurückgegeben:<br /><br /> **FILE**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/En[crypt] *{SQL &#124; FILE}; Path;ProtectionLevel[;password]*|(Optional). Verschlüsselt das geladene Paket mit der angegebenen Schutzebene und dem angegebenen Kennwort und speichert es an dem in *Path* angegebenen Speicherort. Der Wert für *ProtectionLevel* bestimmt, ob ein Kennwort erforderlich ist.<br /><br /> *SQL* – „Path“ ist der Name des Zielpakets.<br /><br /> *FILE* – „Path“ ist der vollqualifizierte Pfad und Dateiname für das Paket.<br /><br /> *DTS* – Diese Option wird zurzeit nicht unterstützt.<br /><br /> *ProtectionLevel*-Optionen:<br /><br /> Ebene 0: Vertrauliche Informationen werden entfernt.<br /><br /> Ebene 1: Vertrauliche Informationen werden mithilfe der lokalen Benutzeranmeldeinformationen verschlüsselt.<br /><br /> Ebene 2: Vertrauliche Informationen werden mithilfe des erforderlichen Kennworts verschlüsselt.<br /><br /> Ebene 3: Das Paket wird mithilfe des erforderlichen Kennworts verschlüsselt.<br /><br /> Ebene 4: Das Paket wird mithilfe der lokalen Benutzeranmeldeinformationen verschlüsselt.<br /><br /> Ebene 5: Für das Paket wird die Speicherverschlüsselung von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] verwendet.|  
|/Ex[ists]|(Optional). Wird verwendet, um zu bestimmen, ob ein Paket vorhanden ist. **dtutil** versucht, das Paket zu finden, dass entweder von der Option *SQL*, *DTS* oder *FILE* angegeben wurde. Falls **dtutil** das angegebene Paket nicht finden kann, wird der Fehler DTEXEC_DTEXECERROR zurückgegeben.|  
|/FC[reate] {*SQL* &#124; *DTS*};*ParentFolderPath;NewFolderName*|(Optional). Erstellt einen neuen Ordner mit dem in *NewFolderName* angegebenen Namen. Der Speicherort des neuen Ordners wird mit *ParentFolderPath* angegeben.|  
|/FDe[lete] {*SQL* &#124; *DTS*}[;*ParentFolderPath;FolderName]*|(Optional). Löscht den in *FolderName* angegebenen Ordner aus [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oder [!INCLUDE[ssIS](../includes/ssis-md.md)]. Der Speicherort des zu löschenden Ordners wird durch *ParentFolderPath* angegeben.|  
|/FDi[rectory] {*SQL* &#124; *DTS*};*FolderPath[;S]*|(Optional). Listet den Inhalt (Ordner sowie Pakete) eines Ordners in [!INCLUDE[ssIS](../includes/ssis-md.md)] oder [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] auf. Mit dem optionalen *FolderPath*-Parameter wird der Ordner angegeben, dessen Inhalt Sie anzeigen möchten. Mit dem optionalen Parameter *S* wird angegeben, dass Sie für den in *FolderPath* angegebenen Ordner eine Liste mit den Inhalten der Unterordner anzeigen möchten.|  
|/FE[xists ] {*SQL* &#124; *DTS*};*FolderPath*|(Optional). Überprüft, ob der angegebene Ordner in [!INCLUDE[ssIS](../includes/ssis-md.md)] oder [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vorhanden ist. Der *FolderPath*-Parameter gibt den Pfad und den Namen des zu überprüfenden Ordners an.|  
|/Fi[le] *filespec*|Diese Option gibt an, dass sich das [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paket, auf das sich der Vorgang bezieht, im Dateisystem befindet. Der Wert für *filespec* kann als UNC-Pfad (Universal Naming Convention) oder als lokaler Pfad angegeben werden.<br /><br /> Wenn die Option *File* in derselben Befehlszeile wie eine der folgenden Optionen angegeben wird, wird der Fehler DTEXEC_DTEXECERROR zurückgegeben:<br /><br /> **DTS**<br /><br /> **SQL**<br /><br /> **SOURCEUSER**<br /><br /> **SOURCEPASSWORD**<br /><br /> **SOURCESERVER**|  
|/FR[ename] {*SQL* &#124; *DTS*} [;*ParentFolderPath; OldFolderName;NewFolderName]*|(Optional). Benennt einen Ordner in [!INCLUDE[ssIS](../includes/ssis-md.md)] oder [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] um. *ParentFolderPath* gibt den Speicherort des Ordners an, der umbenannt werden soll. *OldFolderName* ist der aktuelle Name des Ordners; *NewFolderName* ist der neue Name, der dem Ordner zugewiesen werden soll.|  
|/H[elp] *option*|Zeigt eine ausführliche Hilfe mit den Optionen von **dtutil** und ihrer jeweiligen Verwendung an. Das option-Argument ist optional. Wenn das Argument angegeben wird, umfasst der Hilfetext ausführliche Informationen zur angegebenen Option. Im folgenden Beispiel wird Hilfe zu allen Optionen angezeigt:<br /><br /> `dtutil /H`<br /><br /> In den folgenden zwei Beispielen wird gezeigt, wie mithilfe der Option */H* die erweiterte Hilfe zu einer bestimmten Option (in diesem Beispiel zur Option */Q [uiet]*) angezeigt wird:<br /><br /> `dtutil /Help Quiet`<br /><br /> `dtutil /H Q`|  
|/I[DRegenerate]|Erstellt einen neuen GUID für das Paket und aktualisiert die Paket-ID. Beim Kopieren eines Pakets wird die Paket-ID nicht geändert. Die Protokolldateien enthalten daher für beide Pakete denselben GUID. Mit dieser Aktion wird ein neuer GUID für das neu kopierte Paket erstellt, damit es vom Originalpaket unterschieden werden kann.|  
|/M[ove] {*SQL* &#124; *File* &#124; *DTS*}; *pathandname*|Gibt eine Verschiebeaktion für ein [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paket an. Um diesen Parameter verwenden zu können, müssen Sie zunächst mithilfe der Option **/FI**, **/SQ**, oder **/DT** den Speicherort des Pakets angeben. Geben Sie anschließend die **Move**-Aktion an. Für diese Aktion sind zwei durch Semikolon getrennte Argumente erforderlich:<br /><br /> Als Zielargument kann *SQL*, *FILE* oder *DTS* angegeben werden. Ein *SQL*-Ziel kann die Optionen *DESTUSER*, *DESTPASSWORD* und *DESTSERVER* umfassen.<br /><br /> Mit dem *pathandname*-Argument wird der Speicherort des Pakets angegeben: *SQL* verwendet den Paketpfad und Paketnamen, *FILE* verwendet einen UNC-Pfad oder lokalen Pfad, und *DTS* verwendet einen Speicherort, der relativ zum Stammverzeichnis des [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paketspeichers ist. Wenn als Ziel *FILE* oder *DTS* angegeben wird, schließt das Pfadargument keinen Dateinamen ein. Stattdessen wird der Paketname am angegebenen Speicherort als Dateiname verwendet.<br /><br /> <br /><br /> Wenn die Aktion **MOVE** ein vorhandenes Paket am Ziel ermittelt, werden Sie von **dtutil** aufgefordert, das Überschreiben des Pakets zu bestätigen. Die Angabe von **Y** bewirkt, dass das Paket überschrieben wird; mit **N** wird das Programm beendet. Wenn der Befehl die Option *QUIET* einschließt, wird keine Aufforderung angezeigt, und vorhandene Pakete werden ggf. überschrieben.|  
|/Q[uiet]|Unterdrückt die Bestätigungsaufforderungen, die angezeigt werden können, wenn ein Befehl, der die Option **COPY**, **MOVE** oder **SIGN** einschließt, ausgeführt wird. Diese Aufforderungen werden angezeigt, wenn auf dem Zielcomputer bereits ein Paket mit demselben Namen wie das angegebene Paket vorhanden ist oder wenn das angegebene Paket bereits signiert ist.|  
|/R[emark] *Text*|Fügt einen Kommentar zur Befehlszeile hinzu. Das Kommentarargument ist optional. Wenn der Kommentartext Leerzeichen enthält, muss der Text in Anführungszeichen eingeschlossen werden. Sie können die REM-Option mehrfach in einer Befehlszeile angeben.|  
|/Si[gn] {*SQL* &#124; *File* &#124; *DTS*}; *path*; *hash*|Signiert ein [!INCLUDE[ssIS](../includes/ssis-md.md)]-Paket. Für diese Aktion sind drei durch Semikolons getrennte Argumente erforderlich; Ziel, Pfad und Hash:<br /><br /> Als Zielargument kann *SQL*, *FILE* oder *DTS* angegeben werden. Ein SQL-Ziel kann die Optionen *DESTUSER*, *DESTPASSWORD* und *DESTSERVER* umfassen.<br /><br /> Mit dem path-Argument wird der Speicherort des Pakets angegeben, für das die Aktion ausgeführt werden soll.<br /><br /> Mit dem hash-Argument wird ein Zertifikatsbezeichner in Form einer Hexadezimalzeichenfolge unterschiedlicher Länge angegeben.<br /><br /> Weitere Informationen finden Sie unter [Identifizieren der Quelle von Paketen mit digitalen Signaturen](../integration-services/packages/identify-the-source-of-packages-with-digital-signatures.md).<br /><br /> <br /><br /> **\*\* Wichtig \*\*** Wenn Sie die Überprüfung der Signatur des Pakets konfiguriert haben, prüft [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] lediglich, ob die digitale Signatur vorhanden und gültig ist und ob die Quelle vertrauenswürdig ist. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] überprüft *nicht*, ob Änderungen am Paket vorgenommen wurden.|  
|/SourceP[assword] *Kennwort*|Gibt das Kennwort an, das mit den Optionen *SQL* und *SOURCEUSER* verwendet wird, um das Abrufen eines [!INCLUDE[ssIS](../includes/ssis-md.md)]-Pakets zu ermöglichen, das in einer Datenbank einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gespeichert ist, die die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung verwendet. *SOURCEPASSWORD* darf nicht in einer Befehlszeile angegeben werden, die die Option **SOURCEUSER** nicht einschließt.<br /><br /> Hinweis: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SourceS[erver] *Serverinstanz*|Gibt den Servernamen an, der mit der Option **SQL** verwendet wird, um das Abrufen eines in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gespeicherten [!INCLUDE[ssIS](../includes/ssis-md.md)]-Pakets zu ermöglichen. *SOURCESERVER* darf nicht in einer Befehlszeile angegeben werden, die die Optionen *SIGN SQL*, *COPY* *SQL* oder *MOVE* *SQL* nicht enthält.<br /><br /> Ein [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanzname kann angegeben werden, indem dem Servernamen ein umgekehrter Schrägstrich und der Instanzname hinzugefügt wird.|  
|/SourceU[ser] *Benutzername*|Gibt den Benutzernamen an, der mit der Option *SOURCESERVER* verwendet wird, um das Abrufen eines [!INCLUDE[ssIS](../includes/ssis-md.md)]-Pakets zu ermöglichen, das mithilfe der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gespeichert wurde. *SOURCEUSER* darf nicht in einer Befehlszeile angegeben werden, die die Optionen *SIGN SQL*, *COPY SQL* oder *MOVE SQL* nicht enthält.<br /><br /> Hinweis: [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]|  
|/SQ[L] *package_path*|Gibt den Speicherort eines [!INCLUDE[ssIS](../includes/ssis-md.md)]-Pakets an. Diese Option gibt an, dass das Paket in der **msdb**-Datenbank gespeichert ist. Mit dem *package_path*-Argument wird der Pfad und der Name des [!INCLUDE[ssIS](../includes/ssis-md.md)]-Pakets angegeben. Ordnernamen enden mit umgekehrten Schrägstrichen.<br /><br /> Wenn die Option *SQL* in derselben Befehlszeile wie eine der folgenden Optionen angegeben wird, wird der Fehler DTEXEC_DTEXECERROR zurückgegeben:<br /><br /> *DTS*<br /><br /> *FILE*<br /><br /> Die Option *SQL* kann mit keiner Instanz oder einer Instanz der folgenden Optionen angegeben werden:<br /><br /> *SOURCEUSER*<br /><br /> *SOURCEPASSWORD*<br /><br /> *SOURCESERVER*<br /><br /> <br /><br /> Wenn Sie die Option *SOURCEUSERNAME* nicht einbezogen wird, wird die Windows-Authentifizierung für den Zugriff auf das Paket verwendet. *SOURCEPASSWORD* ist nur zulässig, wenn *SOURCEUSER* vorhanden ist. Wird *SOURCEPASSWORD* nicht angegeben, wird ein leeres Kennwort verwendet.<br /><br /> **\*\* Wichtig \*\*** [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]|  
  
## dtutil-Exitcodes  
 **dtutil** legt einen Exitcode fest, der Sie informiert, wenn Syntaxfehler erkannt, falsche Argumente verwendet oder ungültige Optionskombinationen angegeben werden. Andernfalls meldet das Hilfsprogramm „Der Vorgang wurde erfolgreich abgeschlossen“. In der folgenden Tabelle sind die Werte aufgeführt, die vom Hilfsprogramm **dtutil** beim Beenden festgelegt werden können.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Das Hilfsprogramm wurde erfolgreich ausgeführt.|  
|1|Beim Ausführen des Hilfsprogramms ist ein Fehler aufgetreten.|  
|4|Das Hilfsprogramm konnte das angeforderte Paket nicht finden.|  
|5|Das Hilfsprogramm konnte das angeforderte Paket nicht laden.|  
|6|Das Hilfsprogramm konnte die Befehlszeile nicht auflösen, da sie syntaktische oder semantische Fehler enthielt.|  
  
## Hinweise  
 Es ist nicht möglich, Befehlsdateien oder Umleitungen für **dtutil** zu verwenden.  
  
 Die Reihenfolge der Optionen in der Befehlszeile ist unerheblich.  
  
## Beispiele  
 In den folgenden Beispielen werden typische Verwendungsszenarios für dieses Befehlszeilenprogramm vorgestellt.  
  
### Beispiele für Kopiervorgänge  
 Verwenden Sie die folgende Syntax, um ein Paket zu kopieren, das in der **msdb**-Datenbank einer lokalen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gespeichert ist, die die Windows-Authentifizierung für den Zugriff auf den SSIS-Paketspeicher verwendet:  
  
```  
dtutil /SQL srcPackage /COPY DTS;destFolder\destPackage   
```  
  
 Verwenden Sie die folgende Syntax, um ein Paket von einem Speicherort im Dateisystem an einen anderen Speicherort zu kopieren und der Kopie einen anderen Namen zuzuweisen:  
  
```  
dtutil /FILE c:\myPackages\mypackage.dtsx /COPY FILE;c:\myTestPackages\mynewpackage.dtsx  
```  
  
 Verwenden Sie die folgende Syntax, um ein Paket im lokalen Dateisystem in eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz zu kopieren, die von einem anderen Computer gehostet wird:  
  
```  
dtutil /FILE c:\sourcepkg.dtsx /DestServer <servername> /COPY SQL;destpkgname  
```  
  
 Da die Optionen */DestU[ser]* und */DestP[assword]* nicht verwendet wurden, wird die Windows-Authentifizierung angenommen.  
  
 Verwenden Sie die folgende Syntax, um für ein kopiertes Paket eine neue ID zu erstellen:  
  
```  
dtutil /I /FILE copiedpkg.dtsx   
```  
  
 Verwenden Sie die folgende Syntax, um für alle Pakete in einem bestimmten Ordner eine neue ID zu erstellen:  
  
```  
for %%f in (C:\test\SSISPackages\*.dtsx) do dtutil.exe /I /FILE %%f  
```  
  
 Verwenden Sie ein einzelnes Prozentzeichen (%), wenn Sie den Befehl an der Eingabeaufforderung eingeben. Verwenden Sie ein doppeltes Prozentzeichen (%%), wenn der Befehl innerhalb einer Batchdatei verwendet wird.  
  
### Beispiele für Löschvorgänge  
 Verwenden Sie die folgende Syntax, um ein Paket zu löschen, das in der **msdb**-Datenbank einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gespeichert ist, die die Windows-Authentifizierung verwendet:  
  
```  
dtutil /SQL delPackage /DELETE  
```  
  
 Verwenden Sie die folgende Syntax, um ein Paket zu löschen, das in der **msdb**-Datenbank einer Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gespeichert ist, die die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung verwendet:  
  
```  
dtutil /SQL delPackage /SOURCEUSER srcUserName /SOURCEPASSWORD #8nGs*w7F /DELETE  
```  
  
> [!NOTE]  
>  Geben Sie die Option **SOURCESERVER** und die zugehörigen Argumente an, um das Paket von einem benannten Server zu löschen. Die Angabe eines Servers ist nur möglich, wenn Sie die Option *SQL* verwenden.  
  
 Verwenden Sie die folgende Syntax, um ein im SSIS-Paketspeicher gespeichertes Paket zu löschen:  
  
```  
dtutil /DTS delPackage.dtsx /DELETE  
```  
  
 Verwenden Sie die folgende Syntax, um ein im Dateisystem gespeichertes Paket zu löschen:  
  
```  
dtutil /FILE c:\delPackage.dtsx /DELETE  
```  
  
### Beispiele für /EXISTS  
 Verwenden Sie die folgende Syntax, um festzustellen, ob ein Paket in der **msdb**-Datenbank einer lokalen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vorhanden ist, die die Windows-Authentifizierung verwendet:  
  
```  
dtutil /SQL srcPackage /EXISTS  
```  
  
 Verwenden Sie die folgende Syntax, um zu bestimmen, ob ein Paket in der **msdb**-Datenbank einer lokalen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vorhanden ist, die die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung verwendet:  
  
```  
dtutil SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD *hY$d56b /EXISTS  
```  
  
> [!NOTE]  
>  Verwenden Sie die Option **SOURCESERVER** und die zugehörigen Argumente, um zu ermitteln, ob das Paket auf einem benannten Server vorhanden ist. Die Angabe eines Servers ist nur möglich, wenn Sie die SQL-Option verwenden.  
  
 Verwenden Sie die folgende Syntax, um zu bestimmen, ob ein Paket im lokalen Paketspeicher vorhanden ist:  
  
```  
dtutil /DTS srcPackage.dtsx /EXISTS  
```  
  
 Verwenden Sie die folgende Syntax, um zu bestimmen, ob ein Paket im lokalen Dateisystem vorhanden ist:  
  
```  
dtutil /FILE c:\srcPackage.dtsx /EXISTS  
```  
  
### Beispiele für Verschiebevorgänge  
 Verwenden Sie die folgende Syntax, um ein im SSIS-Paketspeicher gespeichertes Paket in die **msdb**-Datenbank einer lokalen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zu verschieben, die die Windows-Authentifizierung verwendet:  
  
```  
dtutil /DTS srcPackage.dtsx /MOVE SQL;destPackage  
```  
  
 Verwenden Sie die folgende Syntax, um ein Paket, das in der **msdb**-Datenbank einer lokalen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] gespeichert ist, die die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung verwendet, in die **msdb**-Datenbank einer anderen lokalen Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] zu verschieben, die die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Authentifizierung verwendet:  
  
```  
dtutil /SQL srcPackage /SOURCEUSER srcUserName /SOURCEPASSWORD $Hj45jhd@X /MOVE SQL;destPackage /DESTUSER destUserName /DESTPASSWORD !38dsFH@v  
```  
  
> [!NOTE]  
>  Geben Sie die Optionen **SOURCES** und **DESTS** sowie die zugehörigen Argumente an, um ein Paket von einem benannten Server zu einem anderen benannten Server zu verschieben. Die Angabe von Servern ist nur möglich, wenn Sie die Option *SQL* verwenden.  
  
 Verwenden Sie die folgende Syntax, um ein im SSIS-Paketspeicher gespeichertes Paket zu verschieben:  
  
```  
dtutil /DTS srcPackage.dtsx /MOVE DTS;destPackage.dtsx  
```  
  
 Verwenden Sie die folgende Syntax, um ein im Dateisystem gespeichertes Paket zu verschieben:  
  
```  
dtutil /FILE c:\srcPackage.dtsx /MOVE FILE;c:\destPackage.dtsx  
```  
  
### Beispiele für Signiervorgänge  
 Verwenden Sie die folgende Syntax, um ein Paket zu signieren, das in einer [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Datenbank einer lokalen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Instanz gespeichert ist, die die Windows-Authentifizierung verwendet:  
  
```  
dtutil /FILE srcPackage.dtsx /SIGN FILE;destpkg.dtsx;1767832648918a9d989fdac9819873a91f919  
```  
  
 Verwenden Sie **CertMgr**, um Informationen zu Ihrem Zertifikat zu finden. Sie können den Hashcode im Hilfsprogramm **CertMgr** anzeigen, indem Sie das Zertifikat auswählen und anschließend auf **Anzeigen** klicken, um die Eigenschaften anzuzeigen. Die Registerkarte **Details** enthält zusätzliche Informationen zu dem Zertifikat. Die **Thumbprint**-Eigenschaft wird als Hashwert verwendet, wobei die Leerzeichen entfernt werden.  
  
> [!NOTE]  
>  Bei dem in diesem Beispiel verwendeten Hash handelt es sich nicht um einen echten Hash.  
  
 Weitere Informationen finden Sie im Abschnitt „CertMgr“ unter [Signing and Checking Code with Authenticode](http://go.microsoft.com/fwlink/?LinkId=78100) (Signieren und Überprüfen von Code mit Authenticode).  
  
### Beispiele für Verschlüsselungsvorgänge  
 Im folgenden Beispiel wird das dateibasierte Paket PackageToEncrypt.dtsx mithilfe der vollständigen Paketverschlüsselung mit einem Kennwort verschlüsselt. Das Ergebnis ist das dateibasierte Paket EncryptedPackage.dtsx. Das für die Verschlüsselung verwendete Kennwort lautet *EncPswd*.  
  
```  
dtutil /FILE PackageToEncrypt.dtsx /ENCRYPT file;EncryptedPackage.dtsx;3;EncPswd  
```  
  
## Siehe auch  
 [Ausführen eines Pakets in SQL Server-Datentools](../integration-services/packages/run-a-package-in-sql-server-data-tools.md)  
  
  