---
title: Fehler- und Meldungsreferenz von Integration Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- error numbers [Integration Services]
- hresults [Integration Services]
- errors [Integration Services], listed
ms.assetid: 2c825c07-5074-42ad-90ea-0dc5a588dcf7
caps.latest.revision: "44"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f3b9bd353109d4e9d96597ad7ac944423b4d9b54
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="integration-services-error-and-message-reference"></a>Fehler- und Meldungsreferenz von Integration Services
  In den folgenden Tabellen sind vordefinierte Fehler-, Warn- und Informationsmeldungen von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in aufsteigender numerischer Reihenfolge innerhalb jeder Kategorie aufgeführt, inklusive der jeweiligen numerischen Codes und symbolischen Namen. Jeder dieser Fehler ist als Feld der Klasse <xref:Microsoft.SqlServer.Dts.Runtime.Hresults> im Namespace <xref:Microsoft.SqlServer.Dts.Runtime> definiert.  
  
 Diese Liste kann nützlich sein, wenn ein Fehlercode ohne zugehörige Beschreibung angezeigt wird. Die Liste enthält zurzeit keine Informationen zur Problembehandlung.  
  
> [!IMPORTANT]  
>  Viele Fehlermeldungen, die bei der Arbeit mit [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] auftreten können, stammen von anderen Komponenten. In diesem Thema finden Sie alle von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Komponenten ausgelösten Fehler. Wenn der bei Ihnen aufgetretene Fehler nicht in der Liste enthalten ist, wurde er von einer Komponente außerhalb von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]ausgelöst. Zu diesen Komponenten zählen OLE DB-Anbieter, andere Datenbankkomponenten wie die [!INCLUDE[ssDE](../includes/ssde-md.md)] und [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oder andere Dienste bzw. Komponenten wie das Dateisystem, der SMTP-Server, Message Queueing (auch als MSMQ bezeichnet) usw. Informationen zu diesen externen Fehlermeldungen finden Sie in der Dokumentation der entsprechenden Komponenten.  
  
 Diese Liste enthält die folgenden Meldungsgruppen:  
  
-   [Fehlermeldungen (DTS_E_*)](#msgError)  
  
-   [Warnmeldungen (DTS_W_*)](#msgWarning)  
  
-   [Informationsmeldungen (DTS_I_*)](#msgInfo)  
  
-   [Allgemeine Meldungen und Ereignismeldungen (DTS_MSG_*)](#msgGeneral)  
  
-   [Erfolgsmeldungen (DTS_S_*)](#msgSuccess)  
  
-   [Fehlermeldungen der Datenflusskomponenten (DTSBC_E_*)](#msgPipeline)  
  
##  <a name="msgError"></a> Fehlermeldungen  
 Die symbolischen Namen von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Fehlermeldungen beginnen mit **DTS_E_**.  
  
|Hexadezimalcode|Dezimalcode|Symbolischer Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x8002F347|-2147290297|DTS_E_STOREDPROCSTASK_OVERWRITINGSPATDESTINATION|Die gespeicherte Prozedur "%1" wird am Ziel überschrieben.|  
|0x8020837E|-2145352834|DTS_E_ADOSRCUNKNOWNTYPEMAPPEDTONTEXT|Der Datentyp "%1"in Spalte %2 wird für %3 nicht unterstützt. Diese Spalte wird in DT_NTEXT umgewandelt.|  
|0x8020838C|-2145352820|DTS_E_XMLSRCSCHEMACOLUMNNOTINEXTERNALMETADATA|Die Spalte %1 in der Tabelle %2 des XML-Schemas weist keine Zuordnung in den externen Metadatenspalten auf.|  
|0xC0000032|-1073741774|DTS_E_NOTINITIALIZED|Ein internes Objekt oder eine interne Variable wurde nicht initialisiert. Dies ist ein interner Produktfehler.  Dieser Fehler wird zurückgegeben, wenn für eine Variable ein gültiger Wert fehlt.|  
|0xC0000033|-1073741773|DTS_E_EXPIRED|Der Evaluierungszeitraum für Integration Services ist abgelaufen.|  
|0xC0000034|-1073741772|DTS_E_NEGATIVEVALUESNOTALLOWED|Dieser Eigenschaft kann kein negativer Wert zugewiesen werden. Dieser Fehler tritt auf, wenn einer Eigenschaft, für die nur positive Werte zulässig sind, ein negativer Wert zugewiesen wird. Dies gilt z. B. für die COUNT-Eigenschaft.|  
|0xC0000035|-1073741771|DTS_E_NEGATIVEINDEXNOTALLOWED|Indizes dürfen nicht negativ sein. Dieser Fehler tritt auf, wenn ein negativer Wert als Index für eine Auflistung verwendet wird.|  
|0xC00060AB|-1073717077|DTS_E_INVALIDSSISSERVERNAME|Ungültiger Servername "%1". Der SSIS-Dienst unterstützt nicht mehrere Instanzen. Verwenden Sie nur den Servernamen anstelle von "Servername\Instanz".|  
|0xC0008445|-1073707963|DTS_E_SCRIPTMIGRATIONFAILED64BIT|Die Migration für VSA-Skripts kann aufgrund fehlender Designer-Unterstützung von Visual Tools for Applications nicht auf 64-Bit-Plattformen ausgeführt werden. Führen Sie die Migration unter WOW64 für 64-Bit-Plattformen aus.|  
|0xC000931A|-1073704166|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_ERRORSINCOMMAND|Die Befehlsausführung hat Fehler generiert.|  
|0xC000F427|-1073679321|DTS_E_SSISSTANDALONENOTINSTALLED|Um ein SSIS-Paket außerhalb von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] auszuführen, müssen Sie %1 oder höher von Integration Services installieren.|  
|0xC0010001|-1073676287|DTS_E_VARIABLENOTFOUND|Die Variable wurde nicht gefunden. Dieses Problem tritt auf, wenn beim Ausführen des Pakets eine Variable aus der Variables-Auflistung in einem Container abgerufen wird und die Variable nicht vorhanden ist. Möglicherweise hat sich der Variablenname geändert oder die Variable wird nicht erstellt.|  
|0xC0010003|-1073676285|DTS_E_VARIABLEREADONLY|Fehler beim Schreiben in die schreibgeschützte "%1"-Variable.|  
|0xC0010004|-1073676284|DTS_E_MANAGEDCOMPONENTSTORENOTFOUND|Die Verzeichnisse mit den Tasks und Datenflusstask-Komponenten wurden nicht gefunden. Überprüfen Sie die Integrität der Installation.|  
|0xC0010006|-1073676282|DTS_E_PACKAGENAMETOOLONG|Der Paketname ist zu lang. Es sind maximal 128 Zeichen zulässig. Verkürzen Sie den Paketnamen.|  
|0xC0010007|-1073676281|DTS_E_PACKAGEDESCRIPTIONTOOLONG|Die Paketbeschreibung ist zu lang. Maximal 1024 Zeichen sind zulässig. Verkürzen Sie die Paketbeschreibung.|  
|0xC0010008|-1073676280|DTS_E_VERCOMMENTSTOOLONG|Die VersionComments-Eigenschaft ist zu lang. Maximal 1024 Zeichen sind zulässig. Verkürzen Sie die VersionComments-Eigenschaft.|  
|0xC0010009|-1073676279|DTS_E_ELEMENTNOTFOUND|Das Element wurde in einer Auflistung nicht gefunden. Dieser Fehler tritt auf, wenn Sie beim Ausführen des Pakets ein Element aus einer Auflistung abrufen und das Element nicht vorhanden ist.|  
|0xC001000A|-1073676278|DTS_E_PACKAGENOTFOUND|Das angegebene Paket konnte nicht aus der SQL Server-Datenbank geladen werden.|  
|0xC001000C|-1073676276|DTS_E_INVALIDVARIABLEVALUE|Die Variablenwertzuweisung ist ungültig. Dieser Fehler tritt auf, wenn der Client oder ein Task ein Laufzeitobjekt einem Variablenwert zuweist.|  
|0xC001000D|-1073676275|DTS_E_RESERVEDNAMESPACE|Fehler beim Zuweisen des Namespace zur Variable. Der Namespace "System" ist für das System reserviert. Dieser Fehler tritt auf, wenn eine Komponente oder ein Task versucht, eine Variable mit dem Namespace "System" zu erstellen.|  
|0xC001000E|-1073676274|DTS_E_CONNECTIONNOTFOUND|Die "%1"-Verbindung wurde nicht gefunden. Dieser Fehler wird von der Connections-Auflistung gemeldet, wenn das betreffende Verbindungselement nicht gefunden wird.|  
|0xC001000F|-1073676273|DTS_E_64BITVARIABLERECAST|Die "%1"-Variable ist eine ganzzahlige 64-Bit-Variable. Diese wird von diesem Betriebssystem nicht unterstützt. Die Variable wurde in eine ganzzahlige 32-Bit-Variable umgewandelt.|  
|0xC0010010|-1073676272|DTS_E_CANTCHANGEREADONLYATRUNTIME|Es wurde versucht, für die "%1"-Variable ein Nur-Lese-Attribut zu ändern. Dieser Fehler tritt auf, wenn ein Nur-Lese-Attribut für eine Variable zur Laufzeit geändert wird. Nur-Lese-Attribute können nur zur Entwurfszeit geändert werden.|  
|0xC0010011|-1073676271|DTS_E_VARIABLEINVALIDCONTAINERREF|Ungültiger Versuch, für eine Variable einen Containerverweis festzulegen.  Variablen können nicht auf Container verweisen.|  
|0xC0010013|-1073676269|DTS_E_INVALIDVARVALUE|Der "%1"-Variable wird ein ungültiger Wert oder ein ungültiges Objekt zugewiesen. Dieser Fehler tritt auf, wenn ein Wert für Variablen nicht zulässig ist.|  
|0xC0010014|-1073676268|DTS_E_GENERICERROR|Mindestens ein Fehler ist aufgetreten. Vor dieser Fehlermeldung sollten genauere Fehler angezeigt worden sein. Diese Meldung wird als Rückgabewert für Funktionen verwendet, bei denen Fehler auftreten.|  
|0xC0010016|-1073676266|DTS_E_INVALIDARRAYVALUE|Fehler beim Abrufen oder Festlegen eines Arraywerts. Der "%1"-Typ ist nicht zulässig. Dieser Fehler tritt beim Laden eines Arrays in eine Variable auf.|  
|0xC0010017|-1073676265|DTS_E_UNSUPPORTEDARRAYTYPE|Nicht unterstützter Typ im Array. Dieser Fehler tritt beim Speichern eines Arrays mit nicht unterstützten Typen in einer Variablen auf.|  
|0xC0010018|-1073676264|DTS_E_PERSISTENCEERROR|Fehler beim Laden des Werts "%1" aus dem Knoten "%2".|  
|0xC0010019|-1073676263|DTS_E_INVALIDNODE|Der Knoten "%1" ist ungültig. Dieses Problem tritt auf, wenn beim Speichern ein Fehler auftritt.|  
|0xC0010020|-1073676256|DTS_E_ERRORLOADINGTASK|Fehler beim Laden des Tasks "%1", Typ "%2". Die Kontaktinformationen für diesen Task lauten "%3".|  
|0xC0010021|-1073676255|DTS_E_ERRORELEMENTNOTINCOLL|Das "%1"-Element ist in der "%2"-Auflistung nicht vorhanden.|  
|0xC0010022|-1073676254|DTS_E_MISSINGOBJECTDATA|Das ObjectData-Element fehlt im XML-Block eines gehosteten Objekts. Dieser Fehler tritt auf, wenn der XML-Parser das Datenelement für ein Objekt nicht findet.|  
|0xC0010023|-1073676253|DTS_E_VARIABLENOTFOUNDINCOLL|Die "%1"-Variable wurde nicht gefunden. Dieser Fehler tritt auf, wenn beim Ausführen des Pakets eine Variable aus einer Variables-Auflistung in einem Container abgerufen wird und die Variable nicht vorhanden ist.  Möglicherweise wurde ein Variablenname geändert oder die Variable wird nicht erstellt.|  
|0xC0010025|-1073676251|DTS_E_HASEMPTYTASKHOSTS|Das Paket kann nicht ausgeführt werden, weil es Tasks enthält, die nicht geladen werden konnten.|  
|0xC0010026|-1073676250|DTS_E_TASKISEMPTY|Fehler beim Laden des Tasks. Die Kontaktinformationen für diesen Task lauten "%1".|  
|0xC0010027|-1073676249|DTS_E_ERRORLOADINGTASKNOCONTACT|Fehler beim Laden des "%1"-Tasks.|  
|0xC0010028|-1073676248|DTS_E_ERRORATLOADTASK|Fehler beim Laden des „%1“-Tasks. Dieses Problem tritt auf, wenn beim Laden eines Tasks aus XML ein Fehler auftritt.|  
|0xC0010200|-1073675776|DTS_E_MULTIPLECACHEWRITES|%1 kann nicht in den Cache schreiben, da %2 bereits in den Cache geschrieben hat.|  
|0xC0010201|-1073675775|DTS_E_SETCACHEFORINSERTFAILED|Fehler beim Vorbereiten des Caches für neue Daten.|  
|0xC0010202|-1073675774|DTS_E_SETCACHEFORFILLFAILED|Fehler beim Kennzeichnen des Caches als mit Daten gefüllt.|  
|0xC0010203|-1073675773|DTS_E_READUNINITIALIZEDCACHE|Der Cache ist nicht initialisiert und kann von %1 nicht gelesen werden.|  
|0xC0010204|-1073675772|DTS_E_SETCACHEFORREADFAILED|Fehler beim Vorbereiten des Caches zum Bereitstellen von Daten.|  
|0xC0010205|-1073675771|DTS_E_READNOTFILLEDCACHE|%1 schreibt in den Cache. Dieser kann von %2 nicht gelesen werden.|  
|0xC0010206|-1073675770|DTS_E_WRITEWHILECACHEINUSE|Der Cache wird von %1 gelesen. %2 kann nicht in den Cache schreiben.|  
|0xC0011001|-1073672191|DTS_E_CANTLOADFROMNODE|Das Laufzeitobjekt kann nicht aus dem angegebenen XML-Knoten geladen werden.  Dieser Fehler tritt auf, wenn ein Paket oder ein anderes Objekt aus einem XML-Knoten geladen wird, der nicht den richtigen Typ aufweist, z. B. ein Knoten, der kein SSIS-XML-Knoten ist.|  
|0xC0011002|-1073672190|DTS_E_OPENPACKAGEFILE|Fehler beim Öffnen der Paketdatei „%1“ aufgrund des Fehlers 0x%2!8.8X! „%3“.  Dieser Fehler tritt auf, wenn ein Paket geladen wird und die Datei im XML-Dokument nicht ordnungsgemäß geöffnet oder geladen werden kann. Dies ist darauf zurückzuführen, dass beim Aufrufen von LoadPackage ein falscher Dateiname angegeben oder für die XML-Datei ein falsches Format angegeben wurde.|  
|0xC0011003|-1073672189|DTS_E_LOADPACKAGEXML|Fehler beim Laden von XML aufgrund des Fehlers 0x%1!8.8X! „%2“. Dieser Fehler tritt auf, wenn ein Paket geladen wird und die Datei im XML-Dokument nicht ordnungsgemäß geöffnet oder geladen werden kann.  Dies ist darauf zurückzuführen, dass für die LoadPackage-Methode ein falscher Dateiname angegeben oder für die XML-Datei ein falsches Format angegeben wurde.|  
|0xC0011004|-1073672188|DTS_E_LOADPACKAGEXMLFILE|Fehler beim Laden von XML aus der Paketdatei „%1“ aufgrund des Fehlers 0x%2!8.8X! „%3“.  Dieser Fehler tritt auf, wenn ein Paket geladen wird und die Datei in einem XML-Dokument nicht ordnungsgemäß geöffnet oder geladen werden kann. Dies ist darauf zurückzuführen, dass für die LoadPackage-Methode ein falscher Dateiname angegeben oder für die XML-Datei ein falsches Format angegeben wurde.|  
|0xC0011005|-1073672187|DTS_E_OPENFILE|Fehler beim Öffnen der Paketdatei. Dieser Fehler tritt auf, wenn ein Paket geladen wird und die Datei in einem XML-Dokument nicht ordnungsgemäß geöffnet oder geladen werden kann. Dies ist darauf zurückzuführen, dass für die LoadPackage-Methode ein falscher Dateiname angegeben oder für die XML-Datei ein falsches Format angegeben wurde.|  
|0xC0011006|-1073672186|DTS_E_UNABLETODECODEBINARYFORMAT|Binäres Format kann im Paket nicht decodiert werden.|  
|0xC0011007|-1073672185|DTS_E_FUNDAMENTALLOADINGERROR|Das Paket kann nicht im XML-Format geladen werden, weil es kein gültiges XML-Format aufweist. Ein XML-Parserfehler wird bereitgestellt.|  
|0xC0011008|-1073672184|DTS_E_LOADFROMXML|Fehler beim Laden von XML. Für dieses Problem sind keine ausführlicheren Informationen verfügbar, weil kein Events-Objekt übergeben wurde, in dem ausführliche Fehlerinformationen gespeichert werden können.|  
|0xC0011009|-1073672183|DTS_E_XMLDOMERROR|Eine Instanz des XML-Dokumentobjektmodells kann nicht erstellt werden. Möglicherweise ist MSXML nicht registriert.|  
|0xC001100D|-1073672179|DTS_E_CANNOTLOADOLDPACKAGES|Das Paket kann nicht geladen werden. Dieser Fehler tritt auf, wenn ein Paket mit einer älteren Version geladen wird oder wenn die Paketdatei auf ein ungültiges strukturiertes Objekt verweist.|  
|0xC001100E|-1073672178|DTS_E_SAVEFILE|Fehler beim Speichern der Paketdatei.|  
|0xC001100F|-1073672177|DTS_E_SAVEPACKAGEFILE|Fehler beim Speichern der Paketdatei „%1“: 0x%2!8.8X! „%3“.|  
|0xC001200D|-1073668083|DTS_E_IDTSNAMENOTSUPPORTED|Das Objekt muss IDTSName100 erben. Dies ist nicht der Fall.|  
|0xC0012018|-1073668072|DTS_E_CONFIGFORMATINVALID_PACKAGEDELIMITER|Der Konfigurationseintrag "%1" weist ein falsches Format auf, weil er nicht mit dem Pakettrennzeichen beginnt. Das Trennzeichen "\package" fehlt.|  
|0xC0012019|-1073668071|DTS_E_CONFIGFORMATINVALID|Der Konfigurationseintrag "%1" weist ein falsches Format auf. Dies kann auf ein fehlendes Trennzeichen oder Formatierungsfehler, z. B ein ungültiges Arraytrennzeichen, zurückzuführen sein.|  
|0xC001201B|-1073668069|DTS_E_CONFIGFILEFAILEDEXPORT|Fehler beim Exportieren der Konfigurationsdatei.|  
|0xC0012021|-1073668063|DTS_E_PROPERTIESCOLLECTIONREADONLY|Die Properties-Auflistung kann nicht geändert werden.|  
|0xC0012022|-1073668062|DTS_E_DTRXMLSAVEFAILURE|Die Konfigurationsdatei kann nicht gespeichert werden. Möglicherweise ist die Datei schreibgeschützt.|  
|0xC0012023|-1073668061|DTS_E_FAILPACKAGEONFAILURENA|Die FailPackageOnFailure-Eigenschaft ist für den Paketcontainer nicht zutreffend.|  
|0xC0012024|-1073668060|DTS_E_TASKPRODUCTLEVEL|Der Task "%1" kann in Integration Services %2 nicht ausgeführt werden. Hierfür ist %3 oder höher erforderlich.|  
|0xC0012029|-1073668055|DTS_E_UNABLETOSAVETOFILE|XML kann nicht in "%1" gespeichert werden. Möglicherweise ist die Datei schreibgeschützt.|  
|0xC0012037|-1073668041|DTS_E_CONFIGTYPECONVERSIONFAILED|Fehler beim Konvertieren eines Typs in der Konfiguration "%1" für den Paketpfad "%2".  Dieser Fehler tritt auf, wenn ein Konfigurationswert nicht von einer Zeichenfolge in den entsprechenden Zieltyp konvertiert werden kann. Stellen Sie sicher, dass der Konfigurationswert in den Typ der Zieleigenschaft oder -variablen konvertiert werden kann.|  
|0xC0012049|-1073668023|DTS_E_CONFIGFAILED|Konfigurationsfehler. Dies ist eine allgemeine Warnung für alle Konfigurationstypen. Dieser Fehlermeldung sollten ausführlichere Warnungen vorausgehen.|  
|0xC0012050|-1073668016|DTS_E_REMOTEPACKAGEVALIDATION|Fehler beim Überprüfen des Pakets durch den ExecutePackage-Task. Das Paket kann nicht ausgeführt werden.|  
|0xC0013001|-1073663999|DTS_E_FAILTOCREATEMUTEX|Fehler beim Erstellen von Mutex "%1": 0x%2!8.8X!.|  
|0xC0013002|-1073663998|DTS_E_MUTEXOWNBYDIFFUSER|Mutex "%1" ist bereits vorhanden und im Besitz eines anderen Benutzers.|  
|0xC0013003|-1073663997|DTS_E_WAITFORMUTEXFAILED|Fehler beim Abrufen von Mutex "%1": 0x%2!8.8X!.|  
|0xC0013004|-1073663996|DTS_E_FAILTORELEASEMUTEX|Fehler beim Freigeben von Mutex "%1": 0x%2!8.8X!.|  
|0xC0014003|-1073659901|DTS_E_INVALIDTASKPOINTER|Der Taskzeiger des Wrappers ist ungültig. Der Wrapper enthält einen ungültigen Zeiger auf einen Task.|  
|0xC0014004|-1073659900|DTS_E_ALREADYADDED|Die ausführbare Datei wurde der Executables-Auflistung eines anderen Containers hinzugefügt. Dieses Problem tritt auf, wenn ein Client eine ausführbare Datei mehreren Executables-Auflistungen hinzufügt. Sie müssen die ausführbare Datei aus der aktuellen Executables-Auflistung entfernen, bevor Sie sie hinzufügen.|  
|0xC0014005|-1073659899|DTS_E_UNKNOWNCONNECTIONMANAGERTYPE|Der für den Verbindungs-Manager "%2" angegebene "%1"-Verbindungstyp wird nicht als gültiger Verbindungs-Manager-Typ erkannt. Dieser Fehler wird zurückgegeben, wenn ein Verbindungs-Manager für einen unbekannten Verbindungstyp erstellt wird. Überprüfen Sie, ob Sie den Namen des Verbindungstyps richtig eingegeben haben.|  
|0xC0014006|-1073659898|DTS_E_COLLECTIONCOULDNTADD|Ein Objekt wurde erstellt, aber beim Hinzufügen zu einer Auflistung ist ein Fehler aufgetreten. Möglicherweise ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0014007|-1073659897|DTS_E_ODBCERRORENV|Fehler beim Erstellen einer ODBC (Open Database Connectivity)-Umgebung.|  
|0xC0014008|-1073659896|DTS_E_ODBCERRORDBC|Fehler beim Erstellen einer ODBC (Open Database Connectivity)-Datenbankverbindung.|  
|0xC0014009|-1073659895|DTS_E_ODBCERRORCONNECT|Fehler beim Einrichten einer ODBC (Open Database Connectivity)-Verbindung mit dem Datenbankserver.|  
|0xC001400A|-1073659894|DTS_E_CONNECTIONMANAGERQUALIFIERALREADYSET|Der Qualifizierer ist in dieser Instanz des Verbindungs-Managers bereits festgelegt. Der Qualifizierer kann pro Instanz einmal festgelegt werden.|  
|0xC001400B|-1073659893|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSET|Der Qualifizierer wurde in dieser Instanz des Verbindungs-Managers nicht festgelegt. Der Qualifizierer muss für die Initialisierung festgelegt werden.|  
|0xC001400C|-1073659892|DTS_E_CONNECTIONMANAGERQUALIFIERNOTSUPPORTED|Für diesen Verbindungs-Manager können keine Qualifizierer angegeben werden.|  
|0xC001400D|-1073659891|DTS_E_CANNOTCLONECONNECTIONMANAGER|Der Verbindungs-Manager "0x%1" kann für die Ausführung außerhalb eines Prozesses nicht geklont werden.|  
|0xC001400E|-1073659890|DTS_E_NOSQLPROFILERDLL|Der Protokollanbieter für SQL Server Profiler konnte die Datei pfclnt.dll nicht laden. Überprüfen Sie, ob SQL Server Profiler installiert ist.|  
|0xC001400F|-1073659889|DTS_E_LOGFAILED|Fehler bei der SSIS-Protokollierungsinfrastruktur (Fehlercode: 0x%1!8.8X!). Dieser Fehler weist darauf hin, dass dieser Protokollierungsfehler nicht auf einen bestimmten Protokollanbieter zurückzuführen ist.|  
|0xC0014010|-1073659888|DTS_E_LOGPROVIDERFAILED|Fehler beim SSIS-Protokollierungsanbieter "%1" (Fehlercode: 0x%2!8.8X!) (%3).  Dieser Fehler weist darauf hin, dass dieser Protokollierungsfehler auf den angegebenen Protokollanbieter zurückzuführen ist.|  
|0xC0014011|-1073659887|DTS_E_SAVETOSQLSERVER_OLEDB|Fehler bei der SaveToSQLServer-Methode (OLE DB-Fehlercode: 0x%1!8.8X! (%2) wurde zurückgegeben.  Die ausgegebene SQL-Anweisung konnte nicht ausgeführt werden.|  
|0xC0014012|-1073659886|DTS_E_LOADFROMSQLSERVER_OLEDB|Fehler bei der LoadFromSQLServer-Methode (OLE DB-Fehlercode: 0x%1!8.8X!) (%2) wurde zurückgegeben.  Die ausgegebene SQL-Anweisung konnte nicht ausgeführt werden.|  
|0xC0014013|-1073659885|DTS_E_REMOVEFROMSQLSERVER_OLEDB|Fehler bei der RemoveFromSQLServer-Methode (OLE DB-Fehlercode: 0x%1!8.8X!) (%2) Die ausgegebene SQL-Anweisung konnte nicht ausgeführt werden.|  
|0xC0014014|-1073659884|DTS_E_EXISTSONSQLSERVER_OLEDB|Fehler bei der ExistsOnSQLServer-Methode (OLE DB-Fehlercode: 0x%1!8.8X!) (%2) wurde zurückgegeben. Die ausgegebene SQL-Anweisung konnte nicht ausgeführt werden.|  
|0xC0014015|-1073659883|DTS_E_CONNECTIONSTRING|OLE DB konnte mit der eingegebenen Verbindungszeichenfolge keine Datenbankverbindung herstellen.|  
|0xC0014016|-1073659882|DTS_E_FROMEXECISNOTCHILD|Beim Hinzufügen einer Rangfolgeneinschränkung wurde eine ausführbare From-Datei angegeben, die kein untergeordnetes Element dieses Containers ist.|  
|0xC0014017|-1073659881|DTS_E_TOEXECISNOTCHILD|Beim Hinzufügen einer Rangfolgeneinschränkung wurde eine ausführbare To-Datei angegeben, die kein untergeordnetes Element dieses Containers ist.|  
|0xC0014018|-1073659880|DTS_E_ODBCTRANSACTIONENLIST|Fehler beim Eintragen einer ODBC-Verbindung in einer Transaktion. Fehler beim Festlegen des SQL_ATTR_ENLIST_IN_DTC-Attributs durch SQLSetConnectAttr.|  
|0xC0014019|-1073659879|DTS_E_CONNECTIONOFFLINE|Der Verbindungs-Manager "%1" ruft keine Verbindung ab, weil die OfflineMode-Eigenschaft des Pakets TRUE ist. Wenn die OfflineMode-Eigenschaft TRUE ist, können keine Verbindungen abgerufen werden.|  
|0xC001401A|-1073659878|DTS_E_BEGINTRANSACTION|SSIS Runtime konnte die verteilte Transaktion aufgrund des Fehlers „0x%1!8.8X!“ nicht starten. „%2“. Fehler beim Starten der DTC-Transaktion. Möglicherweise wird der MSDTC-Dienst nicht ausgeführt.|  
|0xC001401B|-1073659877|DTS_E_SETQUALIFIERDESIGNTIMEONLY|Die SetQualifier-Methode kann in einem Verbindungs-Manager beim Ausführen des Pakets nicht aufgerufen werden. Die Methode wird nur zur Entwurfszeit verwendet.|  
|0xC001401C|-1073659876|DTS_E_SQLPERSISTENCEVERSION|Zum Speichern oder Ändern von Paketen in SQL Server müssen SSIS Runtime und die Datenbank die gleiche Version aufweisen. Das Speichern von Paketen in früheren Versionen wird nicht unterstützt.|  
|0xC001401D|-1073659875|DTS_E_CONNECTIONVALIDATIONFAILED|Fehler beim Überprüfen der "%1"-Verbindung.|  
|0xC001401E|-1073659874|DTS_E_INVALIDFILENAMEINCONNECTION|Der in der Verbindung angegebene Dateiname "%1" war ungültig.|  
|0xC001401F|-1073659873|DTS_E_MULTIPLEFILESONRETAINEDCONNECTION|In einer Verbindung können nicht mehrere Dateinamen angegeben werden, wenn die Retain-Eigenschaft TRUE ist. In der Verbindungszeichenfolge wurden senkrechte Striche gefunden, d. h., es sind mehrere Dateinamen angegeben, und außerdem ist die Retain-Eigenschaft TRUE.|  
|0xC0014020|-1073659872|DTS_E_ODBCERROR|Ein ODBC-Fehler % 1!d! ist aufgetreten.|  
|0xC0014021|-1073659871|DTS_E_PRECEDENCECONSTRAINT|Fehler in der Rangfolgeneinschränkung zwischen "%1" und "%2".|  
|0xC0014022|-1073659870|DTS_E_FAILEDPOPNATIVEFEE|Fehler beim Auffüllen der ForEachEnumeratorInfos-Auflistung mit systemeigenen ForEachEnumerators-Elementen (Fehlercode: %1).|  
|0xC0014023|-1073659869|DTS_E_GETENUMERATOR|Fehler bei der Methode GetEnumerator des Enumerators ForEach (Fehlercode: 0x%1!8.8X!) „%2“. Dieser Fehler tritt auf, wenn der ForEach-Enumerator nicht aufzählen kann.|  
|0xC0014024|-1073659868|DTS_E_CANTGETCERTDATA|Die Rohzertifikatdaten können vom angegebenen Zertifikatobjekt nicht abgerufen werden (Fehlercode: %1). Dieser Fehler tritt auf, wenn CPackage::put_CertificateObject das ManagedHelper-Objekt nicht instanziieren kann, wenn beim ManagedHelper-Objekt ein Fehler auftritt oder wenn das ManagedHelper-Objekt ein ungültiges Array zurückgibt.|  
|0xC0014025|-1073659867|DTS_E_CANTCREATECERTCONTEXT|Fehler beim Erstellen des Zertifikatkontexts (Fehlercode: %1). Dieser Fehler tritt in CPackage::put_CertificateObject oder CPackage::LoadFromXML auf, wenn die entsprechende CryptoAPI-Funktion nicht ausgeführt werden kann.|  
|0xC0014026|-1073659866|DTS_E_CANTOPENCERTSTORE|Fehler beim Öffnen des MY-Zertifikatspeichers (Fehlercode: "%1"). Dieser Fehler tritt in CPackage::LoadUserCertificateByName und CPackage::LoadUserCertificateByHash auf.|  
|0xC0014027|-1073659865|DTS_E_CANTFINDCERTBYNAME|Das im MY-Zertifikatspeicher namentlich angegebene Zertifikat wurde nicht gefunden (Fehlercode: %1). Dieser Fehler tritt in CPackage::LoadUserCertificateByName auf.|  
|0xC0014028|-1073659864|DTS_E_CANTFINDCERTBYHASH|Das angegebene Zertifikat wurde mithilfe des Hash nicht im MY-Zertifikatspeicher gefunden (Fehlercode: %1). Dieser Fehler tritt in CPackage::LoadUserCertificateByHash auf.|  
|0xC0014029|-1073659863|DTS_E_INVALIDCERTHASHFORMAT|Der Hashwert ist kein eindimensionales Bytearray (Fehlercode: %1). Dieser Fehler tritt in CPackage::LoadUserCertificateByHash auf.|  
|0xC001402A|-1073659862|DTS_E_CANTACCESSARRAYDATA|Der Zugriff auf die Daten im Array ist nicht möglich (Fehlercode: %1). Dieser Fehler kann immer auftreten, wenn GetDataFromSafeArray aufgerufen wird.|  
|0xC001402B|-1073659861|DTS_E_CREATEMANAGEDHELPERFAILED|Fehler bei dem von SSIS verwalteten Hilfsobjekt während des Erstellens (Fehlercode: 0x%1!8.8X!) „%2“. Dieser Fehler tritt bei einem Fehler von CoCreateInstance CLSID_DTSManagedHelper auf.|  
|0xC001402C|-1073659860|DTS_E_OLEDBTRANSACTIONENLIST|SSIS Runtime konnte die OLE DB-Verbindung nicht in einer verteilten Transaktion eintragen (Fehlercode: 0x%1!8.8X!) „%2“.|  
|0xC001402D|-1073659859|DTS_E_SIGNPACKAGEFAILED|Fehler bei der Paketsignierung (Fehlercode: 0x%1!8.8X! „%2“. Dieses Problem tritt in Zusammenhang mit einem Fehler bei der ManagedHelper.SignDocument-Methode auf.|  
|0xC001402E|-1073659858|DTS_E_CHECKENVELOPEFAILED|Fehler beim Überprüfen der XML-Signaturumschlags im Paket-XML (Fehlercode: 0x%1!8.8X!). „%2“. Dieser Fehler tritt in CPackage::LoadFromXML auf.|  
|0xC001402F|-1073659857|DTS_E_GETXMLSOURCEFAILED|Fehler beim Abrufen der XML-Quelle vom XML-DOM-Objekt (Fehlercode: 0x%1!8.8X! „%2“. Dieses Problem tritt in Kombination mit einem Fehler bei IXMLDOMDocument::get_xml auf.|  
|0xC0014030|-1073659856|DTS_E_PACKAGEVERIFICATIONFAILED|Fehler bei der Überprüfung der kryptografischen Signatur des Pakets (Fehlercode: 0x%1!8.8X! „%2“. Dieses Problem tritt in Kombination mit einem Fehler bei der Überprüfung der Signatur auf.|  
|0xC0014031|-1073659855|DTS_E_GETKEYFROMCERTFAILED|Fehler beim Abrufen des kryptografischen Schlüsselpaars für das angegebene Zertifikat (Fehlercode: 0x%1!8.8X! „%2“. Überprüfen Sie, ob Sie über das Schlüsselpaar verfügen, für das das Zertifikat ausgestellt wurde. Dieser Fehler tritt gewöhnlich beim Signieren eines Dokuments mithilfe eines Zertifikats auf, für das die betreffende Person nicht über den privaten Schlüssel verfügt.|  
|0xC0014032|-1073659854|DTS_E_INVALIDSIGNATURE|Die digitale Signatur ist ungültig. Der Inhalt des Pakets wurde geändert.|  
|0xC0014033|-1073659853|DTS_E_UNTRUSTEDSIGNATURE|Die digitale Signatur ist gültig; der Unterzeichner ist jedoch nicht vertrauenswürdig. Deshalb kann die Echtheit nicht sichergestellt werden.|  
|0xC0014034|-1073659852|DTS_E_TRANSACTIONENLISTNOTSUPPORTED|Das Eintragen in einer verteilten Transaktion wird von der Verbindung nicht unterstützt.|  
|0xC0014035|-1073659851|DTS_E_PACKAGEPROTECT|Fehler beim Anwenden des Paketschutzes (Fehlercode: 0x%1!8.8X! „%2“. Dieser Fehler tritt beim Speichern als XML auf.|  
|0xC0014036|-1073659850|DTS_E_PACKAGEUNPROTECT|Fehler beim Entfernen des Paketschutzes (Fehlercode: 0x%1!8.8X! „%2“. Dieser Fehler tritt bei der CPackage::LoadFromXML-Methode auf.|  
|0xC0014037|-1073659849|DTS_E_PACKAGEPASSWORD|Das Paket ist mit einem Kennwort verschlüsselt. Das Kennwort wurde nicht angegeben, oder das angegebene Kennwort ist falsch.|  
|0xC0014038|-1073659848|DTS_E_DUPLICATECONSTRAINT|Eine Rangfolgeneinschränkung zwischen den angegebenen ausführbaren Dateien ist bereits vorhanden. Mehrere Rangfolgeneinschränkungen sind nicht zulässig.|  
|0xC0014039|-1073659847|DTS_E_PACKAGELOADFAILED|Fehler beim Laden des Pakets aufgrund des Fehlers 0x%1!8.8X! „%2“. Dieses Problem tritt bei einem Fehler von CPackage::LoadFromXML auf.|  
|0xC001403A|-1073659846|DTS_E_PACKAGEOBJECTNOTENVELOPED|Fehler beim Suchen des Paketobjekts im signierten XML-Umschlag (Fehlercode: 0x%1!8.8X! „%2“. Dieser Fehler tritt auf, wenn ein signiertes XML-Element nicht wie erwartet ein SSIS-Paket enthält.|  
|0xC001403B|-1073659845|DTS_E_JAGGEDEVENTINFO|Die Länge von Parameternamen, Typen und Beschreibungsarrays sind nicht identisch. Die Länge dieser Objekte muss identisch sein. Dieser Fehler tritt auf, wenn die Länge der Arrays nicht übereinstimmt. In jedem Array sollte pro Parameter ein einziger Eintrag vorhanden sein.|  
|0xC001403C|-1073659844|DTS_E_GETPACKAGEINFOS|OLE DB-Fehler 0x%1!8.8X! (%2) beim Aufzählen von Paketen. Eine SQL-Anweisung wurde ausgegeben und hat einen Fehler gemeldet.|  
|0xC001403D|-1073659843|DTS_E_UNKNOWNLOGPROVIDERTYPE|Der für den Protokollanbieter "%2" angegebene Protokollanbietertyp "%1" wird nicht als gültiger Protokollanbietertyp erkannt. Dieser Fehler tritt beim Erstellen eines Protokollanbieters für einen unbekannten Protokollanbietertyp auf. Überprüfen Sie, ob Sie den Namen des Protokollanbietertyps richtig eingegeben haben.|  
|0xC001403E|-1073659842|DTS_E_UNKNOWNLOGPROVIDERTYPENOSUBS|Der Protokollanbietertyp wird nicht als gültiger Protokollanbietertyp erkannt. Dieser Fehler tritt beim Erstellen eines Protokollanbieters für einen unbekannten Protokollanbietertyp auf. Überprüfen Sie, ob Sie den Namen des Protokollanbietertyps richtig eingegeben haben.|  
|0xC001403F|-1073659841|DTS_E_UNKNOWNCONNECTIONMANAGERTYPENOSUBS|Der für den Verbindungs-Manager angegebene Verbindungstyp ist kein gültiger Verbindungs-Manager-Typ. Dieser Fehler tritt beim Erstellen eines Verbindungs-Managers für einen unbekannten Verbindungstyp auf. Überprüfen Sie, ob Sie den Namen des Verbindungstyps richtig eingegeben haben.|  
|0xC0014040|-1073659840|DTS_E_PACKAGEREMOVEFAILED|Fehler beim Entfernen des "%1"-Pakets aus SQL Server.|  
|0xC0014042|-1073659838|DTS_E_FOLDERADDFAILED|Fehler beim Erstellen eines Ordners in SQL Server mit dem Namen "%1" im Ordner "%2".|  
|0xC0014043|-1073659837|DTS_E_CREATEFOLDERONSQLSERVER_OLEDB|Fehler bei der CreateFolderOnSQLServer-Methode (OLE DB-Fehlercode: 0x%1!8.8X!) (%2) Die ausgegebene SQL-Anweisung konnte nicht ausgeführt werden.|  
|0xC0014044|-1073659836|DTS_E_FOLDERRENAMEFAILED|Fehler beim Umbenennen des Ordners „%1\\\\%2“ in „%1\\\\%3“ auf SQL Server.|  
|0xC0014045|-1073659835|DTS_E_RENAMEFOLDERONSQLSERVER_OLEDB|Fehler bei der RenameFolderOnSQLServer-Methode (OLE DB-Fehlercode 0x%1!8.8X! (%2) wurde zurückgegeben. Die ausgegebene SQL-Anweisung konnte nicht ausgeführt werden.|  
|0xC0014046|-1073659834|DTS_E_FOLDERDELETEFAILED|Fehler beim Löschen des SQL Server-Ordners "%1".|  
|0xC0014047|-1073659833|DTS_E_REMOVEFOLDERFROMSQLSERVER_OLEDB|Fehler bei der RemoveFolderOnSQLServer-Methode (OLE DB-Fehlercode 0x%1!8.8X! (%2) wurde zurückgegeben. Die ausgegebene SQL-Anweisung konnte nicht ausgeführt werden.|  
|0xC0014048|-1073659832|DTS_E_INVALIDPATHTOPACKAGE|Der angegebene Paketpfad enthält keinen Paketnamen. Dieser Fehler tritt auf, wenn der Pfad nicht mindestens einen umgekehrten Schrägstrich oder einen Schrägstrich enthält.|  
|0xC0014049|-1073659831|DTS_E_FOLDERNOTFOUND|Der Ordner "%1" wurde nicht gefunden.|  
|0xC001404A|-1073659830|DTS_E_FINDFOLDERONSQLSERVER_OLEDB|Fehler beim Suchen nach einem Ordner in SQL. OLE DB-Fehlercode: 0x%1!8.8X! (%2) wurde zurückgegeben.|  
|0xC001404B|-1073659829|DTS_E_OPENLOGFAILED|Fehler beim Öffnen des Protokolls durch den SSIS-Protokollierungsanbieter. Fehlercode: 0x%1!8.8X!.|  
|0xC001404C|-1073659828|DTS_E_GETCONNECTIONINFOS|Fehler beim Abrufen der ConnectionInfos-Auflistung (Fehlercode: 0x%1!8.8X! „%2“. Dieser Fehler tritt in Kombination mit einem Fehler beim Aufrufen von "IDTSApplication100::get_ConnectionInfos" auf.|  
|0xC001404D|-1073659827|DTS_E_VARIABLEDEADLOCK|Beim Sperren von Variablen wurde ein Deadlock gefunden. Das Sperren wurde 16 Mal vergeblich versucht. Timeout für Sperren.|  
|0xC001404E|-1073659826|DTS_E_NOTDISPENSED|Die Variables-Auflistung wurde von VariableDispenser nicht zurückgegeben. Der ausgeführte Vorgang ist nur für verteilte Auflistungen zulässig.|  
|0xC001404F|-1073659825|DTS_E_VARIABLESALREADYUNLOCKED|Die Sperre für die Variables-Auflistung wurde bereits aufgehoben. Die Unlock-Methode wird in einer verteilten Variables-Auflistung nur einmal aufgerufen.|  
|0xC0014050|-1073659824|DTS_E_VARIABLEUNLOCKFAILED|Fehler beim Aufheben der Sperre für mindestens eine Variable.|  
|0xC0014051|-1073659823|DTS_E_DISPENSEDREADONLY|Die Variables-Auflistung wurde von VariableDispenser zurückgegeben und kann nicht geändert werden. In verteilten Auflistungen können keine Elemente hinzugefügt oder entfernt werden.|  
|0xC0014052|-1073659822|DTS_E_VARIABLEALREADYONREADLIST|Die "%1"-Variable ist bereits in der Leseliste vorhanden. Eine Variable kann nur einmal der Sperrliste für Lese- und Schreibberechtigungen hinzugefügt werden.|  
|0xC0014053|-1073659821|DTS_E_VARIABLEALREADYONWRITELIST|Die "%1"-Variable ist bereits in der Schreibliste vorhanden. Eine Variable kann nur einmal der Sperrliste für Lese- und Schreibberechtigungen hinzugefügt werden.|  
|0xC0014054|-1073659820|DTS_E_LOCKVARIABLEFORREAD|Fehler beim Sperren der %1-Variablen für den Lesezugriff (Fehlercode: 0x%2!8.8X! „%3“.|  
|0xC0014055|-1073659819|DTS_E_LOCKVARIABLEFORWRITE|Fehler beim Sperren der %1-Variablen für den Lese-/Schreibzugriff (Fehlercode: 0x%2!8.8X! „%3“.|  
|0xC0014056|-1073659818|DTS_E_CUSTOMEVENTCONFLICT|Das benutzerdefinierte Ereignis "%1" ist bereits in einer anderen Parameterliste deklariert. Ein Task versucht, ein benutzerdefiniertes Ereignis zu deklarieren, das von einem anderen Task bereits für eine andere Parameterliste deklariert wurde.|  
|0xC0014057|-1073659817|DTS_E_EVENTHANDLERNOTALLOWED|Dieses Ereignis kann aufgrund des Tasks, der das benutzerdefinierte Ereignis "%1" bereitstellt, nicht in dem Paket verarbeitet werden. Das benutzerdefinierte Ereignis wurde mit AllowEventHandlers = FALSE deklariert.|  
|0xC0014059|-1073659815|DTS_E_UNSAFEVARIABLESALREADYSET|VariableDispenser hat eine unsichere Variables-Auflistung erhalten. Dieser Vorgang kann nicht wiederholt werden.|  
|0xC001405A|-1073659814|DTS_E_INVALIDPARENTPACKAGEPATH|GetPackagePath wurde für ForEachEnumerator aufgerufen, aber es wurde kein ForEachLoop-Paketpfad angegeben.|  
|0xC001405B|-1073659813|DTS_E_VARIABLEDEADLOCK_READ|Beim Sperren der "%1"-Variable für den Lesezugriff wurde ein Deadlock gefunden. Das Sperren wurde 16 Mal vergeblich versucht. Timeout für Sperren.|  
|0xC001405C|-1073659812|DTS_E_VARIABLEDEADLOCK_READWRITE|Beim Sperren der "%1"-Variablen für den Lese-/Schreibzugriff wurde ein Deadlock gefunden. Das Sperren wurde 16 Mal vergeblich versucht. Timeout für Sperren.|  
|0xC001405D|-1073659811|DTS_E_VARIABLEDEADLOCK_BOTH|Beim Sperren der "%1"-Variablen für den Lesezugriff sowie beim Sperren der "%2"-Variablen für den Lese-/Schreibzugriff wurde ein Deadlock gefunden. Das Sperren wurde 16 Mal vergeblich versucht. Timeout für Sperren.|  
|0xC001405E|-1073659810|DTS_E_PACKAGEPASSWORDEMPTY|Für die Schutzebene des Pakets ist ein Kennwort erforderlich, aber die PackagePassword-Eigenschaft ist leer.|  
|0xC001405F|-1073659809|DTS_E_DECRYPTXML_PASSWORD|Fehler beim Entschlüsseln eines verschlüsselten XML-Knotens, weil das Kennwort nicht oder ein falsches Kennwort angegeben wurde. Das Laden des Pakets wird ohne die verschlüsselten Informationen fortgesetzt.|  
|0xC0014060|-1073659808|DTS_E_DECRYPTPACKAGE_USERKEY|Fehler beim Entschlüsseln eines Pakets, das mit einem Benutzerschlüssel verschlüsselt ist. Möglicherweise sind Sie nicht der Benutzer, der dieses Paket verschlüsselt hat, oder Sie verwenden nicht denselben Computer wie zum Speichern des Pakets.|  
|0xC0014061|-1073659807|DTS_E_SERVERSTORAGEDISALLOWED|Die Schutzebene ServerStorage kann nicht zum Speichern auf diesem Ziel verwendet werden. Das System konnte nicht überprüfen, ob das Ziel das sichere Speichern unterstützt.|  
|0xC0014062|-1073659806|DTS_E_LOADFROMSQLSERVER|Fehler bei der LoadFromSQLServer-Methode.|  
|0xC0014063|-1073659805|DTS_E_SIGNATUREPOLICYVIOLATION|Das Paket kann nicht geladen werden, weil der Status der digitalen Signatur die Signaturrichtlinie verletzt. Fehler 0x%1!8.8X! "%2"|  
|0xC0014064|-1073659804|DTS_E_SIGNATURENOTPRESENT|Das Paket ist nicht signiert.|  
|0xC0014065|-1073659803|DTS_E_SQLPROFILERDLL_ONLY_X86|Der Protokollanbieter für SQL Server Profiler konnte die Datei pfclnt90.dll nicht laden, weil diese nur auf 32-Bit-Systemen unterstützt wird.|  
|0xC0014100|-1073659648|DTS_E_NAMEALREADYADDED|Das Objekt kann nicht hinzugefügt werden, weil ein anderes Objekt mit demselben Namen bereits in der Auflistung vorhanden ist. Verwenden Sie einen anderen Namen, um diesen Fehler zu beheben.|  
|0xC0014101|-1073659647|DTS_E_NAMEALREADYEXISTS|Der Objektname kann nicht von "%1" in "%2" geändert werden, weil dieser Name bereits von einem anderen Objekt in der Auflistung verwendet wird. Verwenden Sie einen anderen Namen, um diesen Fehler zu beheben.|  
|0xC0014103|-1073659645|DTS_E_FAILEDDEPENDENCIES|Fehler beim Aufzählen der Paketabhängigkeiten. Weitere Informationen finden Sie in anderen Meldungen.|  
|0xC0014104|-1073659644|DTS_E_INVALIDCHECKPOINT_TRANSACTION|Die aktuellen Paketeinstellungen werden nicht unterstützt.  Ändern Sie die SaveCheckpoints-Eigenschaft oder die TransactionOption-Eigenschaft.|  
|0xC001410E|-1073659634|DTS_E_CONNECTIONMANAGERJOINTRANSACTION|Verbindungs-Manager-Fehler beim Austragen aus der Transaktion.|  
|0xC0015001|-1073655807|DTS_E_BPDUPLICATE|Die angegebene Breakpoint-ID ist bereits vorhanden. Dieser Fehler tritt auf, wenn ein Task CreateBreakpoint mit derselben ID mehrmals aufruft. Ein Breakpoint mit derselben ID kann mehrmals erstellt werden, wenn der Task RemoveBreakpoint beim ersten Erstellungsvorgang aufruft, bevor der zweite Breakpoint erstellt wird.|  
|0xC0015002|-1073655806|DTS_E_BPUNKNOWNID|Die angegebene Breakpoint-ID ist nicht vorhanden. Dieser Fehler tritt auf, wenn ein Task auf einen nicht vorhandenen Breakpoint verweist.|  
|0xC0015004|-1073655804|DTS_E_CANTWRITETOFILE|Die Datei "%1" konnte nicht zum Schreiben geöffnet werden. Möglicherweise ist die Datei schreibgeschützt, oder Sie verfügen nicht über die erforderlichen Berechtigungen.|  
|0xC0015005|-1073655803|DTS_E_NOROWSETRETURNED|Der Ausführung dieser Abfrage ist kein Ergebnisrowset zugeordnet. Das Ergebnis ist nicht richtig angegeben.|  
|0xC0015105|-1073655547|DTS_E_DUMP_FAILED|Debugdumpdateien wurden nicht korrekt generiert. Das Ergebnis lautet 0x%1!8.8X!.|  
|0xC0016001|-1073651711|DTS_E_INVALIDURL|Die angegebene URL ist ungültig. Dies ist auf eine Server- oder Proxy-URL gleich NULL oder auf ein falsches Format zurückzuführen. Eine gültige URL entspricht dem Format http://ServerName:Port/ResourcePath oder https://ServerName:Port/ResourcePath.|  
|0xC0016002|-1073651710|DTS_E_INVALIDSCHEME|Die URL %1 ist ungültig. Dieses Problem tritt auf, wenn ein anderes als das http- oder https-Schema angegeben ist oder die URL ein falsches Format aufweist. Eine gültige URL entspricht dem Format http://ServerName:Port/ResourcePath oder https://ServerName:Port/ResourcePath.|  
|0xC0016003|-1073651709|DTS_E_WINHTTPCANNOTCONNECT|Mit dem Server %1 kann keine Verbindung hergestellt werden. Dieser Fehler tritt auf, wenn der Server nicht vorhanden ist oder die Proxyeinstellungen falsch sind.|  
|0xC0016004|-1073651708|DTS_E_CONNECTIONTERMINATED|Die Verbindung mit dem Server wurde zurückgesetzt oder beendet. Versuchen Sie es später noch einmal.|  
|0xC0016005|-1073651707|DTS_E_LOGINFAILURE|Fehler beim Anmeldeversuch für "%1". Dieser Fehler tritt auf, wenn die bereitgestellten Anmeldeinformationen falsch sind. Überprüfen Sie die Anmeldeinformationen.|  
|0xC0016006|-1073651706|DTS_E_INVALIDSERVERNAME|Der in der URL %1 angegebene Servername kann nicht aufgelöst werden.|  
|0xC0016007|-1073651705|DTS_E_PROXYAUTH|Fehler bei der Proxyauthentifizierung. Dieser Fehler tritt auf, wenn keine oder falsche Anmeldeinformationen bereitgestellt werden.|  
|0xC0016008|-1073651704|DTS_E_SECUREFAILURE|Ungültige SSL-Zertifikatantwort vom Server. Die Anforderung kann nicht verarbeitet werden.|  
|0xC0016009|-1073651703|DTS_E_TIMEOUT|Timeout für die Anforderung. Dieser Fehler tritt auf, wenn der angegebene Timeoutzeitraum zu kurz ist oder keine Verbindung mit dem Server oder Proxy hergestellt werden kann. Stellen Sie sicher, dass die Server- und Proxy-URLs richtig sind.|  
|0xC001600A|-1073651702|DTS_E_CLIENTAUTH|Das Clientzertifikat fehlt. Dieser Fehler tritt auf, wenn der Server ein SSL-Clientzertifikat erwartet und der Benutzer ein ungültiges oder kein Zertifikat bereitgestellt hat. Für die Verbindung muss ein Clientzertifikat konfiguriert werden.|  
|0xC001600B|-1073651701|DTS_E_REDIRECTFAILURE|Der angegebene Server mit der URL %1 weist eine Umleitungsanforderung auf, die nicht ausgeführt werden kann.|  
|0xC001600C|-1073651700|DTS_E_SERVERAUTH|Fehler bei der Serverauthentifizierung. Dieser Fehler tritt auf, wenn keine oder falsche Anmeldeinformationen bereitgestellt werden.|  
|0xC001600D|-1073651699|DTS_E_WINHTTPUNKNOWNERROR|Die Anforderung kann nicht verarbeitet werden. Versuchen Sie es später noch einmal.|  
|0xC001600E|-1073651698|DTS_E_UNKNOWNSTATUSCODE|Der Server hat den Statuscode %1!u! zurückgegeben : %2. Dieser Fehler wird gemeldet, wenn auf dem Server Probleme auftreten.|  
|0xC001600F|-1073651697|DTS_E_WINHTTPNOTSUPPORTED|Diese Plattform wird von WinHttp-Diensten nicht unterstützt.|  
|0xC0016010|-1073651696|DTS_E_INVALIDTIMEOUT|Ungültiger Timoutwert. Der Timeout sollte zwischen %1!d! auf „%2!d!“. (in Sekunden).|  
|0xC0016011|-1073651695|DTS_E_INVALIDCHUNKSIZE|Ungültige Segmentgröße. Die ChunkSize-Eigenschaft sollte zwischen %1!d! auf „%2!d!“. (in KB) liegen.|  
|0xC0016012|-1073651694|DTS_E_CERTERROR|Fehler beim Verarbeiten des Clientzertifikats. Dieser Fehler tritt auf, wenn das bereitgestellte Clientzertifikat nicht im persönlichen Zertifikatspeicher gefunden wurde. Überprüfen Sie, ob das Clientzertifikat gültig ist.|  
|0xC0016013|-1073651693|DTS_E_FORBIDDEN|Der Server hat den Fehlercode "403 - Verboten" zurückgegeben. Dieser Fehler tritt auf, wenn die angegebene Ressource https-Zugriff benötigt, aber die Gültigkeitsdauer des Zertifikats abgelaufen ist, das Zertifikat für die angeforderte Verwendung ungültig ist, das Zertifikat gesperrt wurde oder die Sperre nicht geprüft werden kann.|  
|0xC0016014|-1073651692|DTS_E_WINHTTPOPEN|Fehler beim Initialisieren der HTTP-Sitzung mit dem Proxy "%1". Dieser Fehler tritt auf, wenn ein ungültiger Proxy angegeben wurde. Der HTTP-Verbindungs-Manager unterstützt nur Proxys vom Typ CERN.|  
|0xC0016015|-1073651691|DTS_E_OPENCERTSTORE|Fehler beim Öffnen des Zertifikatspeichers.|  
|0xC0016016|-1073651690|DTS_E_UNPROTECTXMLFAILED|Fehler beim Entschlüsseln des geschützten XML-Knotens "%1" (Fehlercode: 0x%2!8.8X! „%3“. Möglicherweise verfügen Sie nicht über die Zugriffsrechte für diese Informationen. Dieser Fehler tritt bei einem kryptografischen Fehler auf. Überprüfen Sie, ob der richtige Schlüssel verfügbar ist.|  
|0xC0016017|-1073651689|DTS_E_UNPROTECTCONNECTIONSTRINGFAILED|Fehler beim Entschlüsseln der geschützten Verbindungszeichenfolge für den Server „%1“ (Fehlercode: 0x%2!8.8X! „%3“. Möglicherweise verfügen Sie nicht über die Zugriffsrechte für diese Informationen. Dieser Fehler tritt bei einem kryptografischen Fehler auf. Überprüfen Sie, ob der richtige Schlüssel verfügbar ist.|  
|0xC0016018|-1073651688|DTS_E_NEGATIVEVERSION|Die Versionsnummer darf nicht negativ sein. Dieser Fehler tritt auf, wenn für die Eigenschaften VersionMajor, VersionMinor oder VersionBuild des Pakets ein negativer Wert festgelegt ist.|  
|0xC0016019|-1073651687|DTS_E_PACKAGEMIGRATED|Das Paket wurde beim Laden auf eine höhere Version migriert. Zum Abschließen des Vorgangs muss das Paket neu geladen werden. Dies ist ein interner Fehlercode.|  
|0xC0016020|-1073651680|DTS_E_PACKAGEMIGRATIONFAILED|Fehler beim Migrieren des Pakets von Version %1!d! auf Version %2!d! (Fehlercode: 0x%3!8.8X!) "%4".|  
|0xC0016021|-1073651679|DTS_E_PACKAGEMIGRATIONMODULELOAD|Fehler beim Laden des Paketmigrationsmoduls.|  
|0xC0016022|-1073651678|DTS_E_PACKAGEMIGRATIONMODULE|Fehler beim Paketmigrationsmodul.|  
|0xC0016023|-1073651677|DTS_E_CANTDETERMINEWHICHPROPTOPERSIST|Das Objekt kann nicht mithilfe der Standardpersistenz gespeichert werden. Dieser Fehler tritt auf, wenn die Standardpersistenz nicht bestimmen kann, welche Objekte für das gehostete Objekt verfügbar sind.|  
|0xC0016024|-1073651676|DTS_E_CANTADDREMOVEWHENEXECUTING|In einem Paket kann im Laufzeitmodus kein Element hinzugefügt oder entfernt werden. Dieser Fehler tritt auf, wenn in einer Auflistung ein Objekt hinzugefügt oder entfernt wird, während das Paket ausgeführt wird.|  
|0xC0016025|-1073651675|DTS_E_NODENOTFOUND|Der "%1"-Knoten wurde in der benutzerdefinierten Standardpersistenz nicht gefunden. Dieser Fehler tritt auf, wenn der gespeicherte XML-Standardcode eines erweiterbaren Objekts so geändert wurde, dass das gespeicherte Objekt nicht mehr gefunden wird, oder wenn das erweiterbare Objekt selbst geändert wurde.|  
|0xC0016026|-1073651674|DTS_E_COLLECTIONLOCKED|Diese Auflistung kann beim Überprüfen oder Ausführen von Paketen nicht geändert werden.|  
|0xC0016027|-1073651673|DTS_E_COLLOCKED|Die "%1"-Auflistung kann beim Überprüfen oder Ausführen von Paketen nicht geändert werden. "%2" kann der Auflistung nicht hinzugefügt werden.|  
|0xC0016029|-1073651671|DTS_E_FTPNOTCONNECTED|Mit dem FTP-Server wurde keine Verbindung hergestellt.|  
|0xC001602A|-1073651670|DTS_E_FTPERROR|Fehler beim angeforderten FTP-Vorgang. Ausführliche Fehlerbeschreibung: %1.|  
|0xC001602B|-1073651669|DTS_E_FTPINVALIDRETRIES|Ungültige Anzahl von Wiederholungsversuchen. Die Anzahl von Wiederholungen sollte zwischen %1!d! und %2!d! liegen.|  
|0xC001602C|-1073651668|DTS_E_LOADWININET|Der FTP-Verbindungs-Manager benötigt die folgende DLL: %1.|  
|0xC001602D|-1073651667|DTS_E_FTPINVALIDCONNECTIONSTRING|Ungültiger Port in der Verbindungszeichenfolge. Das ConnectionString-Format lautet ServerName:Port. Für den Port sollte eine ganze Zahl zwischen %1!d! und %2!d! liegen.|  
|0xC001602E|-1073651666|DTS_E_FTPCREATEFOLDER|Ordner "%1" wird erstellt ... %2.|  
|0xC001602F|-1073651665|DTS_E_FTPDELETEFOLDER|Ordner "%1" wird gelöscht ... %2|  
|0xC0016030|-1073651664|DTS_E_FTPCHANGEFOLDER|Das aktuelle Verzeichnis wird in "%1" geändert. %2.|  
|0xC0016031|-1073651663|DTS_E_FTPFILESEMPTY|Es sind keine zu übertragenden Dateien vorhanden. Dieser Fehler tritt auf, wenn beim Ausführen eines Sende- oder Empfangsvorgangs keine Dateien für die Übertragung angegeben sind.|  
|0xC0016032|-1073651662|DTS_E_FTPINVALIDLOCALPATH|Der angegebene lokale Pfad ist ungültig. Geben Sie einen gültigen lokalen Pfad an. Dieser Fehler tritt auf, wenn der angegebene lokale Pfad NULL ist.|  
|0xC0016033|-1073651661|DTS_E_FTPNOFILESTODELETE|Es sind keine zu löschenden Dateien angegeben.|  
|0xC0016034|-1073651660|DTS_E_WINHTTPCERTDECODE|Interner Fehler beim Laden des Zertifikats. Dieser Fehler tritt auf, wenn die Zertifikatdaten ungültig sind.|  
|0xC0016035|-1073651659|DTS_E_WINHTTPCERTENCODE|Interner Fehler beim Speichern der Zertifikatdaten.|  
|0xC0016049|-1073651639|DTS_E_CHECKPOINTMISMATCH|Die Prüfpunktdatei "%1" stimmt nicht mit diesem Paket überein. Die ID des Pakets und die ID in der Prüfpunktdatei stimmen nicht überein.|  
|0xC001604A|-1073651638|DTS_E_CHECKPOINTFILEALREADYEXISTS|Es wurde eine vorhandene Prüfpunktdatei gefunden, deren Inhalte nicht für dieses Paket bestimmt sind. Deshalb kann die Datei nicht überschrieben werden, um neue Prüfpunkte zu speichern. Entfernen Sie die vorhandene Prüfpunktdatei, und versuchen Sie es noch einmal. Dieser Fehler tritt auf, wenn eine Prüfpunktdatei vorhanden ist und für das Paket festgelegt ist, dass keine Prüfpunktdatei verwendet wird, sondern Prüfpunkte gespeichert werden. Die vorhandene Prüfpunktdatei wird nicht überschrieben.|  
|0xC001604B|-1073651637|DTS_E_CHECKPOINTFILELOCKED|Der Prüfpunktdatei "%1" wird von einem anderen Prozess gesperrt. Dieser Fehler tritt auf, wenn eine andere Instanz dieses Pakets zurzeit ausgeführt wird.|  
|0xC001604C|-1073651636|DTS_E_OPENCHECKPOINTFILE|Fehler beim Öffnen der Prüfpunktdatei "%1" aufgrund des Fehlers 0x%2!8.8X! „%3“.|  
|0xC001604D|-1073651635|DTS_E_CREATECHECKPOINTFILE|Fehler beim Erstellen der Prüfpunktdatei „%1“ aufgrund des Fehlers „0x%2!8.8X!“ „%3“.|  
|0xC0016050|-1073651632|DTS_E_FTPINVALIDPORT|Der FTP-Port enthält einen ungültigen Wert. Der FTP-Port-Wert sollte eine ganze Zahl zwischen %1!d! und %2!d! liegen.|  
|0xC00160AA|-1073651542|DTS_E_CONNECTTOSERVERFAILED|Fehler beim Herstellen einer Verbindung mit dem SSIS-Dienst auf dem Computer "%1":<br /><br /> %2.|  
|0xC0017002|-1073647614|DTS_E_PROPERTYEXPRESSIONSDISABLEDONVARIABLES|Die Expression-Eigenschaft wird in Variable-Objekten nicht unterstützt. Verwenden Sie stattdessen die EvaluateAsExpression-Eigenschaft.|  
|0xC0017003|-1073647613|DTS_E_PROPERTYEXPRESSIONEVAL|Der Ausdruck "%1" in der "%2"-Eigenschaft wurde nicht ausgewertet. Ändern Sie den Ausdruck so, dass er gültig ist.|  
|0xC0017004|-1073647612|DTS_E_PROPERTYEXPRESSIONSET|Das Ergebnis des Ausdrucks "%1" in der "%2"-Eigenschaft kann nicht in die Eigenschaft geschrieben werden. Der Ausdruck wurde ausgewertet, kann jedoch in der Eigenschaft nicht festgelegt werden.|  
|0xC0017005|-1073647611|DTS_E_FORLOOPEVALEXPRESSIONINVALID|Der Auswertungsausdruck für die Schleife ist ungültig. Der Ausdruck muss geändert werden. Zusätzliche Fehlermeldungen sollten vorhanden sein.|  
|0xC0017006|-1073647610|DTS_E_EXPRESSIONNOTBOOLEAN|Der Ausdruck "%1" muss zu True oder False ausgewertet werden. Ändern Sie den Ausdruck, sodass er zu einem booleschen Wert ausgewertet wird.|  
|0xC0017007|-1073647609|DTS_E_FORLOOPHASNOEXPRESSION|Für die Schleife ist kein Ausdruck zum Auswerten vorhanden. Dieser Fehler tritt auf, wenn der Ausdruck in der For-Schleife leer ist. Fügen Sie einen Ausdruck hinzu.|  
|0xC0017008|-1073647608|DTS_E_FORLOOPASSIGNEXPRESSIONINVALID|Der Zuweisungsausdruck für die Schleife ist ungültig und muss geändert werden. Zusätzliche Fehlermeldungen sollten vorhanden sein.|  
|0xC0017009|-1073647607|DTS_E_FORLOOPINITEXPRESSIONINVALID|Der Initalisierungsausdruck für die Schleife ist ungültig und muss geändert werden. Zusätzliche Fehlermeldungen sollten vorhanden sein.|  
|0xC001700A|-1073647606|DTS_E_INVALIDVERSIONNUMBER|Die Versionsnummer im Paket ist ungültig. Die Versionsnummer kann nicht größer als die aktuelle Versionsnummer sein.|  
|0xC001700C|-1073647604|DTS_E_INVALIDVERNUMCANTBENEGATIVE|Die Versionsnummer im Paket ist ungültig. Die Versionsnummer ist negativ.|  
|0xC001700D|-1073647603|DTS_E_PACKAGEUPDATEDISABLED|Das Paket weist eine ältere Formatversion auf, aber das automatische Paketformatupgrade ist deaktiviert.|  
|0xC001700E|-1073647602|DTS_E_EXPREVALTRUNCATIONASERROR|Beim Auswerten des Ausdrucks wurden Daten abgeschnitten.|  
|0xC0019001|-1073639423|DTS_E_FAILEDSETEXECVALVARIABLE|Der Wrapper konnte den Wert der in der ExecutionValueVariable-Eigenschaft angegebenen Variablen nicht festlegen.|  
|0xC0019004|-1073639420|DTS_E_VARIABLEEXPRESSIONERROR|Fehler beim Auswerten des "%1"-Variablenausdrucks. Im Ausdruck ist ein Fehler aufgetreten.|  
|0xC0019305|-1073638651|DTS_E_UNSUPPORTEDSQLVERSION|Der Vorgang wird von dieser Datenbankversion nicht unterstützt.|  
|0xC001A003|-1073635325|DTS_E_TXNSPECINVALID|Die Transaktion kann nicht angegeben werden, wenn eine beibehaltene Verbindung verwendet wird. Dieser Fehler tritt auf, wenn Retain für den Verbindungs-Manager auf TRUE festgelegt ist, aber AcquireConnection mit einem Transaktionsparameter ungleich NULL aufgerufen wurde.|  
|0xC001A004|-1073635324|DTS_E_INCOMPATIBLETRANSACTIONCONTEXT|Für eine beibehaltene Verbindung wurde ein inkompatibler Transaktionskontext angegeben. Die Verbindung wurde unter einem anderen Transaktionskontext eingerichtet. Beibehaltene Verbindungen können unter genau einem Transaktionskontext verwendet werden.|  
|0xC001B001|-1073631231|DTS_E_NOTSUSPENDED|Fehler beim Aufrufen des Befehls zum Fortsetzen, weil das Paket nicht angehalten ist. Dieser Fehler tritt auf, wenn der Client den Befehl zum Fortsetzen aufruft, aber das Paket nicht angehalten ist.|  
|0xC001B002|-1073631230|DTS_E_ALREADYEXECUTING|Fehler beim Aufrufen des Befehls zum Ausführen, weil die ausführbare Datei bereits ausgeführt wird. Dieser Fehler tritt auf, wenn der Client den Befehl zum Ausführen in einem Container aufruft, der noch vom letzten Aufruf des Befehls zum Ausführen ausgeführt wird.|  
|0xC001B003|-1073631229|DTS_E_NOTEXECUTING|Fehler beim Aufrufen des Befehls zum Anhalten oder Fortsetzen, weil die ausführbare Datei nicht ausgeführt wird oder weil sie nicht die ausführbare Datei der obersten Ebene ist. Dieser Fehler tritt auf, wenn der Client den Befehl zum Anhalten oder Fortsetzen in einer ausführbaren Datei aufruft, die zurzeit keinen Aufruf des Befehls zum Ausführen verarbeitet.|  
|0xC001C002|-1073627134|DTS_E_INVALIDFILE|Die im For Each File-Enumerator angegebene Datei ist ungültig. Überprüfen Sie, ob die im For Each File-Enumerator angegebene Datei vorhanden ist.|  
|0xC001C010|-1073627120|DTS_E_VALUEINDEXNOTINTEGER|Der Werteindex ist keine ganze Zahl. Die ForEach-Variable-Zahl „%1!d!“ wird der %2-Variablen zugeordnet.|  
|0xC001C011|-1073627119|DTS_E_VALUEINDEXNEGATIVE|Der Wertindex ist negativ. Die ForEach Variable-Zahl %1!d! wird der Variable „%2“ zugeordnet.|  
|0xC001C012|-1073627118|DTS_E_FOREACHVARIABLEMAPPING|Die Zuordnung der ForEach Variable-Zahl %1!d! zur %2-Variablen ist nicht möglich.|  
|0xC001C013|-1073627117|DTS_E_OBJECTNOTINFOREACHLOOP|Fehler beim Hinzufügen eines Objekts zu einem ForEachPropertyMapping-Objekt, das kein direkt untergeordnetes Element des ForEachLoop-Containers ist.|  
|0xC001F001|-1073614847|DTS_E_FAILEDSYSTEMVARIABLEREMOVE|Fehler beim Entfernen einer Systemvariablen. Dieser Fehler tritt auf, wenn eine erforderliche Variable entfernt wird.  Erforderliche Variablen werden von der Laufzeitumgebung für die Kommunikation zwischen Tasks und der Laufzeitumgebung erstellt.|  
|0xC001F002|-1073614846|DTS_E_CHANGESYSTEMVARIABLEREADONLYFAILED|Fehler beim Ändern der Eigenschaft einer Variablen, weil es sich um eine Systemvariable handelt. Systemvariablen sind schreibgeschützt.|  
|0xC001F003|-1073614845|DTS_E_CHANGESYSTEMVARIABLENAMEFAILED|Fehler beim Ändern des Namens einer Variablen, weil es sich um eine Systemvariable handelt. Systemvariablen sind schreibgeschützt.|  
|0xC001F004|-1073614844|DTS_E_CHANGESYSTEMVARIABLENAMESPACEFAILED|Fehler beim Ändern des Namespaces einer Variablen, weil es sich um eine Systemvariable handelt. Systemvariablen sind schreibgeschützt.|  
|0xC001F006|-1073614842|DTS_E_EVENTHANDLERNAMEREADONLY|Fehler beim Ändern des Ereignishandlernamens. Ereignishandlernamen sind schreibgeschützt.|  
|0xC001F008|-1073614840|DTS_E_PATHUNKNOWN|Der Pfad zum Objekt kann nicht abgerufen werden. Dies ist ein Systemfehler.|  
|0xC001F009|-1073614839|DTS_E_RUNTIMEVARIABLETYPECHANGE|Der Typ des Werts, der der "%1"-Variablen zugewiesen wird, weicht vom aktuellen Variablentyp ab. Für Variablen kann während der Ausführung der Typ nicht geändert werden. Variablentypen sind festgelegt, außer für Variablen vom Typ Object.|  
|0xC001F010|-1073614832|DTS_E_INVALIDSTRING|Ungültige Zeichen in der Zeichenfolge "%1". Dieser Fehler tritt auf, wenn eine für einen Eigenschaftswert eingegebene Zeichenfolge nicht druckbare Zeichen enthält.|  
|0xC001F011|-1073614831|DTS_E_INVALIDOBJECTNAME|Ungültiger SSIS-Objektname. Genauere Fehlermeldungen wurden angezeigt, die das Benennungsproblem genau beschreiben.|  
|0xC001F021|-1073614815|DTS_E_PROPERTYREADONLY|Die "%1"-Eigenschaft ist schreibgeschützt. Dieser Fehler tritt beim Versuch auf, eine schreibgeschützte Eigenschaft zu ändern.|  
|0xC001F022|-1073614814|DTS_E_FAILEDGETTYPEINFO|Das Objekt unterstützt keine Typinformationen. Dieser Fehler tritt auf, wenn die Laufzeitumgebung versucht, die Typinformationen von einem Objekt abzurufen und die Properties-Auflistung damit aufzufüllen.  Das Objekt muss Typinformationen unterstützen.|  
|0xC001F023|-1073614813|DTS_E_FAILEDPROPERTYGET|Fehler beim Abrufen des Werts der %1-Eigenschaft. Fehlercode: 0x%2!8.8X!.|  
|0xC001F024|-1073614812|DTS_E_FAILEDPROPERTYGET_ERRORINFO|Fehler beim Abrufen des Werts der %1-Eigenschaft. Fehlercode: „0x%2!8.8X!“ „%3“.|  
|0xC001F025|-1073614811|DTS_E_FAILEDPROPERTYSET|Fehler beim Festlegen des Werts der "%1"-Eigenschaft. Zurückgegebener Fehler: 0x%2!8.8X!.|  
|0xC001F026|-1073614810|DTS_E_FAILEDPROPERTYSET_ERRORINFO|Fehler beim Festlegen des Werts der "%1"-Eigenschaft. Zurückgegebener Fehler: 0x%2!8.8X! „%3“.|  
|0xC001F027|-1073614809|DTS_E_PROPERTYWRITEONLY|Die "%1"-Eigenschaft weist nur Schreibzugriff auf. Dieser Fehler tritt auf, wenn der Wert einer Eigenschaft über ein Eigenschaftenobjekt abgerufen wird, die Eigenschaft aber nur Schreibzugriff aufweist.|  
|0xC001F028|-1073614808|DTS_E_NODISPATCH|Das Objekt implementiert IDispatch nicht. Dieser Fehler tritt auf, wenn ein Eigenschaftenobjekt oder eine Properties-Auflistung auf eine IDispatch-Schnittstelle in einem Objekt zugreift.|  
|0xC001F029|-1073614807|DTS_E_NOCONTAININGTYPELIB|Die Typbibliothek des Objekts kann nicht abgerufen werden. Dieser Fehler tritt auf, wenn die Properties-Auflistung die Typbibliothek für ein Objekt über die IDispatch-Schnittstelle abruft.|  
|0xC001F02A|-1073614806|DTS_E_INVALIDTASKMONIKER|Ein Task vom XML-Element für Task "%1!s!" vom Typ "%2!s!" aufgrund des Fehlers 0x%3!8.8X! „%4! s!“ nicht erstellt werden.|  
|0xC001F02C|-1073614804|DTS_E_FAILEDCREATEXMLDOCUMENT|Fehler beim Erstellen des XML-Dokuments "%1".|  
|0xC001F02D|-1073614803|DTS_E_PMVARPROPTYPESDIFFERENT|Fehler, weil eine Eigenschaftszuordnung einer Variable zu einer Eigenschaft mit einem anderen Typ vorhanden ist. Der Eigenschaftentyp muss mit dem Variablentyp übereinstimmen.|  
|0xC001F02E|-1073614802|DTS_E_PMINVALIDPROPMAPTARGET|Fehler beim Festlegen der Eigenschaftenzuordnung auf einen nicht unterstützten Zielobjekttyp. Dieser Fehler tritt auf, wenn ein nicht unterstützter Objekttyp an eine Eigenschaftenzuordnung übergeben wird.|  
|0xC001F02F|-1073614801|DTS_E_COULDNOTRESOLVEPACKAGEPATH|Ein Paketpfad zu einem Objekt im Paket "%1" kann nicht aufgelöst werden.  Überprüfen Sie, ob der Paketpfad gültig ist.|  
|0xC001F030|-1073614800|DTS_E_PMNODESTPROPERTY|Die Zieleigenschaft für die Eigenschaftenzuordnung ist leer. Legen Sie den Zieleigenschaftsnamen fest.|  
|0xC001F031|-1073614799|DTS_E_INVALIDPROPERTYMAPPINGSFOUND|Fehler beim Wiederherstellen von mindestens einer Eigenschaftenzuordnung durch das Paket.|  
|0xC001F032|-1073614798|DTS_E_AMBIGUOUSVARIABLENAME|Der Variablenname ist mehrdeutig, weil mehrere Variablen mit diesem Namen in verschiedenen Namespaces vorhanden sind. Geben Sie einen mit einem Namespace qualifizierten Namen an, um Mehrdeutigkeit zu vermeiden.|  
|0xC001F033|-1073614797|DTS_E_DESTINATIONOBJECTPARENTLESS|Das Zielobjekt in einer Eigenschaftenzuordnung weist kein übergeordnetes Element auf. Das Zielobjekt ist kein untergeordnetes Objekt eines Sequenzcontainers. Möglicherweise wurde es aus dem Paket entfernt.|  
|0xC001F036|-1073614794|DTS_E_INVALIDPROPERTYMAPPING|Die Eigenschaftenzuordnung ist ungültig. Die Zuordnung wird ignoriert.|  
|0xC001F038|-1073614792|DTS_E_PMFAILALERTREMOVE|Fehler beim Warnen von Eigenschaftenzuordnungen, dass ein Ziel entfernt wird.|  
|0xC001F03A|-1073614790|DTS_E_INVALIDFOREACHPROPERTYMAPPING|In der For Each-Schleife wurde eine ungültige Eigenschaftenzuordnung gefunden. Dieser Fehler tritt auf, wenn die ForEach-Eigenschaftenzuordnung nicht wiederhergestellt werden kann.|  
|0xC001F040|-1073614784|DTS_E_PMPROPERTYINVALID|In einer Eigenschaftenzuordnung wurde eine ungültige Zieleigenschaft angegeben. Dieser Fehler tritt auf, wenn in einem Zielobjekt eine Eigenschaft angegeben wird, die in diesem Objekt nicht gefunden wird.|  
|0xC001F041|-1073614783|DTS_E_INVALIDTASKMONIKERNOPARAM|Ein Task kann nicht aus dem XML-Code erstellt werden. Dieser Fehler tritt auf, wenn die Laufzeitumgebung den Namen nicht auflösen kann, um einen Task zu erstellen. Überprüfen Sie, ob der Name richtig ist.|  
|0xC001F080|-1073614720|DTS_E_COULDNOTREPLACECHECKPOINTFILE|Die vorhandene Prüfpunktdatei kann nicht durch die aktualisierte Prüfpunktdatei ersetzt werden. Der Prüfpunkt wurde in einer temporären Datei erfolgreich erstellt, aber die vorhandene Datei konnte nicht mit der neuen Datei überschrieben werden.|  
|0xC001F081|-1073614719|DTS_E_CHECKPOINTFILENOTSPECIFIED|Das Paket ist so konfiguriert, dass es immer an einem Prüfpunkt neu gestartet wird. Die Prüfpunktdatei ist jedoch nicht angegeben.|  
|0xC001F082|-1073614718|DTS_E_CHECKPOINTLOADXML|Fehler beim Laden der XML-Prüfpunktdatei „%1“ (Fehlercode: 0x%2!8.8X!) „%3“. Überprüfen Sie, ob der angegebene Dateiname richtig ist und die Datei vorhanden ist.|  
|0xC001F083|-1073614717|DTS_E_LOADCHECKPOINT|Fehler beim Ausführen des Pakets, weil die Prüfpunktdatei nicht geladen werden kann. Für die weitere Ausführung des Pakets ist eine Prüfpunktdatei erforderlich. Dieser Fehler tritt gewöhnlich auf, wenn die CheckpointUsage-Eigenschaft auf ALWAYS festgelegt ist, wodurch das Paket immer neu gestartet wird.|  
|0xC001F185|-1073614459|DTS_E_NOEVALEXPRESSION|Der Auswertungsbedingungsausdruck in der For-Schleife "%1" ist leer. In der For-Schleife ist ein boolescher Auswertungsausdruck erforderlich.|  
|0xC001F186|-1073614458|DTS_E_EXPREVALASSIGNMENTTYPEMISMATCH|Das Ergebnis des "%1"-Zuweisungsausdrucks kann nicht in einen Typ konvertiert werden, der mit der Variablen kompatibel ist, der er zugewiesen wurde.|  
|0xC001F187|-1073614457|DTS_E_EXPREVALASSIGNMENTTOREADONLYVARIABLE|Fehler bei der Verwendung der schreibgeschützten "%1"-Variablen in einem Zuweisungsausdruck. Das Ausdrucksergebnis kann nicht der Variablen zugewiesen werden, weil die Variable schreibgeschützt ist. Wählen Sie eine Variable aus, in die geschrieben werden kann, oder entfernen Sie den Ausdruck aus dieser Variablen.|  
|0xC001F188|-1073614456|DTS_E_EXPREVALASSIGNMENTVARIABLELOCKFORWRITEFAILED|Der Ausdruck "%1" kann nicht ausgewertet werden, weil die "%2"-Variable nicht vorhanden ist oder weil es nicht möglich ist, in die Variable zu schreiben. Das Ausdrucksergebnis kann der Variablen nicht zugewiesen werden, weil die Variable nicht gefunden wurde oder weil sie nicht für den Schreibzugriff gesperrt werden konnte.|  
|0xC001F189|-1073614455|DTS_E_EXPREVALRESULTTYPENOTSUPPORTED|Der Ausdruck "%1" weist den Ergebnistyp "%2" auf, der nicht in einen unterstützten Typ konvertiert werden kann.|  
|0xC001F18A|-1073614454|DTS_E_EXPREVALRESULTTYPECONVERSIONFAILED|Fehler beim Konvertieren des Ergebnisses für den Ausdruck "%1" vom Typ "%1" in einen unterstützten Typ (Fehlercode: 0x%3!8.8X!). Beim Konvertieren des Ausdrucksergebnisses in einen vom Laufzeitmodul unterstützten Typ ist ein unerwarteter Fehler aufgetreten, obwohl die Typkonvertierung unterstützt wird.|  
|0xC001F200|-1073614336|DTS_E_DTSNAME_NOTNULL|Der Objektname ist ungültig. Der Name kann nicht auf NULL festgelegt werden.|  
|0xC001F201|-1073614335|DTS_E_DTSNAME_NOTEMPTY|Der Objektname ist ungültig. Der Name darf nicht leer sein.|  
|0xC001F202|-1073614334|DTS_E_DTSNAME_LEGAL|Der Objektname "%1" ist ungültig. Der Name darf keines der folgenden Zeichen enthalten: / \ : [ ] . =|  
|0xC001F203|-1073614333|DTS_E_DTSNAME_PRINTABLE|Der Objektname „%1“ ist ungültig. Der Name kann keine Steuerzeichen enthalten, durch die er nicht mehr gedruckt werden kann.|  
|0xC001F204|-1073614332|DTS_E_DTSNAME_NOLEADWHITESP|Der Objektname „%1“ ist ungültig. Der Name darf nicht mit einem Leerzeichen beginnen.|  
|0xC001F205|-1073614331|DTS_E_DTSNAME_NOTRAILWHITESP|Der Objektname „%1“ ist ungültig. Der Name darf nicht mit einem Leerzeichen enden.|  
|0xC001F206|-1073614330|DTS_E_DTSNAME_BEGINSWITHALPHA|Der Objektname „%1“ ist ungültig. Der Name muss mit einem Buchstaben beginnen.|  
|0xC001F207|-1073614329|DTS_E_DTSNAME_BEGINSWITHALPHAUNDERBAR|Der Objektname „%1“ ist ungültig. Der Name muss mit einem Buchstaben oder einem Unterstrich "_" beginnen.|  
|0xC001F208|-1073614328|DTS_E_DTSNAME_ALPHADIGITUNDERBAR|Der Objektname „%1“ ist ungültig. Der Name darf nur alphanumerische Zeichen und Unterstriche "_" enthalten.|  
|0xC001F209|-1073614327|DTS_E_DTSNAME_VALIDFILENAME|Der Objektname „%1“ ist ungültig. Der Name darf keines der folgenden Zeichen enthalten: / \ : ? " < > &#124;|  
|0xC001F420|-1073613792|DTS_E_FAILLOADINGPROPERTY|Fehler beim Laden der Werteigenschaft "%1" mit Standardpersistenz.|  
|0xC001F422|-1073613790|DTS_E_NODELISTENUM_INVALIDCONNMGRTYPE|Der Verbindungs-Manager „%1“ ist nicht vom Typ „%2“.|  
|0xC001F423|-1073613789|DTS_E_NODELISTENUM_XPATHISEMPTY|"%1" ist ohne Eintrag|  
|0xC001F424|-1073613788|DTS_E_NODELISTENUM_INVALIDDATANODE|Ungültiger Datenknoten im Abschnitt NodeList-Enumerator.|  
|0xC001F425|-1073613787|DTS_E_NODELISTENUM_NOENUMERATORCREATED|Es kann kein Enumerator erstellt werden.|  
|0xC001F427|-1073613785|DTS_E_OPERATIONFAILCACHEINUSE|Fehler bei dem Vorgang, da der Cache verwendet wird.|  
|0xC001F428|-1073613784|DTS_E_PROPERTYCANNOTBEMODIFIED|Die Eigenschaft kann nicht geändert werden.|  
|0xC001F429|-1073613783|DTS_E_PACKAGEUPGRADEFAILED|Fehler beim Paketupgrade.|  
|0xC00220DE|-1073602338|DTS_E_TKEXECPACKAGE_UNABLETOLOADFILE|Fehler 0x%1!8.8X! beim Laden der Paketdatei "%3". %2.|  
|0xC00220DF|-1073602337|DTS_E_TKEXECPACKAGE_UNSPECIFIEDPACKAGE|Das Paket ist nicht angegeben.|  
|0xC00220E0|-1073602336|DTS_E_TKEXECPACKAGE_UNSPECIFIEDCONNECTION|Die Verbindung ist nicht angegeben.|  
|0xC00220E2|-1073602334|DTS_E_TKEXECPACKAGE_INCORRECTCONNECTIONMANAGERTYPE|Der Verbindungs-Manager "%1" weist den nicht unterstützten Typ "%2" auf. Nur Verbindungs-Manager vom Typ "FILE" und "OLEDB" werden unterstützt.|  
|0xC00220E3|-1073602333|DTS_E_TKEXECPACKAGE_UNABLETOLOADXML|Fehler 0x%1!8.8X! beim Laden der Paketdatei "%3" in ein XML-Dokument. %2.|  
|0xC00220E4|-1073602332|DTS_E_TKEXECPACKAGE_UNABLETOLOAD|Fehler 0x%1!8.8X! beim Vorbereiten zum Laden des Pakets. %2.|  
|0xC0024102|-1073594110|DTS_E_TASKVALIDATIONFAILED|Fehler bei der Validate-Methode für den Task. Der Fehlercode 0x%1!8.8X! (%2) wurde zurückgegeben. Die Validate-Methode muss erfolgreich sein und das Ergebnis mithilfe eines Ausgabeparameters anzeigen.|  
|0xC0024104|-1073594108|DTS_E_TASKEXECUTEFAILED|Die Execute-Methode für den Task hat den Fehlercode 0x%1!8.8X! (%2) wurde zurückgegeben. Die Execute-Methode muss erfolgreich sein und das Ergebnis mithilfe eines Ausgabeparameters anzeigen.|  
|0xC0024105|-1073594107|DTS_E_RETRIEVINGDEPENDENCIES|Fehler beim Task "%1": 0x%2!8.8X! beim Abrufen von Abhängigkeiten. Die Laufzeitumgebung hat Abhängigkeiten von der Abhängigkeitsauflistung des Tasks abgerufen, als der Fehler auftrat. Möglicherweise hat der Task eine der Abhängigkeitsschnittstellen falsch implementiert.|  
|0xC0024107|-1073594105|DTS_E_TASKVALIDATIONERROR|Fehler bei der Tasküberprüfung.|  
|0xC0024108|-1073594104|DTS_E_CONNECTIONSTRINGFORMAT|Ungültiges Format der Verbindungszeichenfolge. Sie muss aus mindestens einer Komponente im Format X=Y bestehen, getrennt durch Semikolons. Dieser Fehler tritt auf, wenn im Datenbankverbindungs-Manager eine Verbindungszeichenfolge mit 0 (null) Komponenten festgelegt wird.|  
|0xC0024109|-1073594103|DTS_E_UNQUOTEDSEMICOLON|Die Komponenten der Verbindungszeichenfolge dürfen keine Semikolons ohne Anführungszeichen enthalten. Falls für den Wert ein Semikolon erforderlich ist, schließen Sie den gesamten Wert in Anführungszeichen ein. Dieser Fehler tritt auf, wenn Werte in der Verbindungszeichenfolge Semikolons ohne Anführungszeichen enthalten, z. B. die InitialCatalog-Eigenschaft.|  
|0xC002410A|-1073594102|DTS_E_LOGPROVIDERVALIDATIONFAILED|Fehler beim Überprüfen von mindestens einem Protokollanbieter. Das Paket kann nicht ausgeführt werden. Das Paket wird nicht ausgeführt, wenn ein Protokollanbieter nicht überprüft werden kann.|  
|0xC002410B|-1073594101|DTS_E_INVALIDVALUEINARRAY|Ungültiger Wert im Array.|  
|0xC002410C|-1073594100|DTS_E_ENUMERATIONELEMENTNOTENUMERABLE|Ein vom ForEach-Enumerator zurückgegebenes Enumeratorelement implementiert IEnumerator nicht. Dies steht im Widerspruch zu der CollectionEnumerator-Eigenschaft des ForEach-Enumerators.|  
|0xC002410D|-1073594099|DTS_E_INVALIDENUMERATORINDEX|Fehler vom Enumerator beim Erhalt eines Elements vom Index '%1!d!'.|  
|0xC0029100|-1073573632|DTS_E_AXTASK_MISSING_ENTRY_METHOD_NAME|Die Funktion wurde nicht gefunden.|  
|0xC0029101|-1073573631|DTS_E_AXTASK_EMPTY_SCRIPT|Die Funktion wurde nicht gefunden.|  
|0xC0029102|-1073573630|DTS_E_AXTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Der ActiveX-Skripttask wurde mit einem falschen XML-Element initiiert.|  
|0xC0029105|-1073573627|DTS_E_AXTASK_HANDLER_NOT_FOUND|Der Handler wurde nicht gefunden.|  
|0xC0029106|-1073573626|DTS_E_AXTASKUTIL_ENUMERATE_LANGUAGES_FAILED|Fehler beim Abrufen der auf dem System installierten Skriptsprachen.|  
|0xC0029107|-1073573625|DTS_E_AXTASKUTIL_SCRIPTHOST_CREATE_FAILED|Fehler beim Erstellen des ActiveX-Skripthosts. Überprüfen Sie, ob der Skripthost ordnungsgemäß installiert ist.|  
|0xC0029108|-1073573624|DTS_E_AXTASKUTIL_SCRIPTHOSTINIT_FAILED|Fehler beim Instanziieren des Skripthosts für die ausgewählte Skriptsprache. Überprüfen Sie, ob die ausgewählte Skriptsprache auf dem System installiert ist.|  
|0xC0029109|-1073573623|DTS_E_AXTASKUTIL_ADDVARIABLES_FAILED|Fehler beim Hinzufügen der SSIS-Variablen zum Skripthostnamespace. Dadurch können möglicherweise keine SSIS-Variablen im Taskskript verwendet werden.|  
|0xC002910A|-1073573622|DTS_E_AXTASKUTIL_SCRIPT_PARSING_FAILED|Schwerwiegender Fehler beim Analysieren des Skripttexts. Überprüfen Sie, ob das Skriptmodul für die ausgewählte Sprache ordnungsgemäß installiert ist.|  
|0xC002910B|-1073573621|DTS_E_AXTASKUTIL_MSG_BAD_FUNCTION|Der eingegebene Funktionsname ist ungültig. Überprüfen Sie, ob ein gültiger Funktionsname angegeben wurde.|  
|0xC002910C|-1073573620|DTS_E_AXTASKUTIL_EXECUTION_FAILED|Fehler beim Ausführen des Skripts. Überprüfen Sie, ob das Skriptmodul für die ausgewählte Sprache ordnungsgemäß installiert ist.|  
|0xC002910D|-1073573619|DTS_E_AXTASKUTIL_ADDTYPELIB_FAILED|Fehler beim Hinzufügen der Bibliothek für verwaltete Typen zum Skripthost. Überprüfen Sie, ob DTS 2000 Runtime installiert ist.|  
|0xC002910E|-1073573618|DTS_E_BITASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Der Masseneinfügungstask wurde mit einem falschen XML-Element initiiert.|  
|0xC002910F|-1073573617|DTS_E_BITASK_DATA_FILE_NOT_SPECIFIED|Der Datendateiname ist nicht angegeben.|  
|0xC0029110|-1073573616|DTS_E_BITASK_HANDLER_NOT_FOUND|Der Handler wurde nicht gefunden.|  
|0xC0029111|-1073573615|DTS_E_BITASK_CANNOT_ACQUIRE_CONNECTION|Fehler beim Abrufen der angegebenen Verbindung: "%1".|  
|0xC0029112|-1073573614|DTS_E_BITASK_NO_CONNECTION_MANAGER_SPECIFIED|Fehler beim Abrufen des Verbindungs-Managers.|  
|0xC0029113|-1073573613|DTS_E_BITASK_INVALID_CONNECTION|Die Verbindung ist ungültig.|  
|0xC0029114|-1073573612|DTS_E_BITASK_NULL_CONNECTION|Die Verbindung ist NULL.|  
|0xC0029115|-1073573611|DTS_E_BITASK_EXECUTE_FAILED|Fehler bei der Ausführung.|  
|0xC0029116|-1073573610|DTS_E_BITASK_CANNOT_RETRIEVE_TABLES|Fehler beim Abrufen der Tabellen aus der Datenbank.|  
|0xC0029117|-1073573609|DTS_E_BITASK_CANNOT_RETRIEVE_COLUMN_INFO|Fehler beim Abrufen der Spalten aus der Tabelle.|  
|0xC0029118|-1073573608|DTS_E_BITASK_ERROR_IN_DB_OPERATION|Fehler beim Datenbankvorgang.|  
|0xC0029119|-1073573607|DTS_E_BITASK_INVALIDSOURCECONNECTIONNAME|Die angegebene Verbindung "%1" ist ungültig oder zeigt auf ein ungültiges Objekt. Geben Sie eine gültige Verbindung an, um den Vorgang fortzusetzen.|  
|0xC002911A|-1073573606|DTS_E_BITASK_INVALIDDESTCONNECTIONNAME|Die angegebene Zielverbindung ist ungültig. Geben Sie eine gültige Verbindung an, um den Vorgang fortzusetzen.|  
|0xC002911B|-1073573605|DTS_E_BITASK_DESTINATION_TABLE_NOT_SPECIFIED|Sie müssen einen Tabellennamen angeben, um den Vorgang fortzusetzen.|  
|0xC002911C|-1073573604|DTS_E_BITASK_ERROR_IN_LOAD_FROM_XML|Fehler in LoadFromXML beim "%1"-Tag.|  
|0xC002911D|-1073573603|DTS_E_BITASK_ERROR_IN_SAVE_TO_XML|Fehler in SaveToXML beim "%1"-Tag.|  
|0xC002911E|-1073573602|DTS_E_BITASKUNMANCONNECTION_INVALID_CONNECTION|Die Verbindung ist ungültig.|  
|0xC002911F|-1073573601|DTS_E_BITASKUNMANCONNECTION_EXECUTE_FAILED|Fehler bei der Ausführung.|  
|0xC0029120|-1073573600|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_TABLES|Fehler beim Abrufen der Tabellen aus der Datenbank.|  
|0xC0029121|-1073573599|DTS_E_BITASKUNMANCONNECTION_CANNOT_RETRIEVE_COLUMN_INFO|Fehler beim Abrufen der Spalten aus der Tabelle.|  
|0xC0029122|-1073573598|DTS_E_BITASKUNMANCONNECTION_CANNOT_OPEN_FILE|Fehler beim Öffnen der Datendatei.|  
|0xC0029123|-1073573597|DTS_E_BITASKUNMANCONNECTION_OEM_CONVERSION_FAILED|Die OEM-Eingabedatei kann nicht in das angegebene Format konvertiert werden.|  
|0xC0029124|-1073573596|DTS_E_BITASKUNMANCONNECTION_ERROR_IN_DB_OPERATION|Fehler beim Datenbankvorgang.|  
|0xC0029125|-1073573595|DTS_E_DTSPROCTASK_NOCONNECTIONSPECIFIED|Es ist kein Verbindungs-Manager angegeben.|  
|0xC0029126|-1073573594|DTS_E_DTSPROCTASK_CONNECTIONMANAGERNOTOLAP|Die "%1"-Verbindung ist keine Analysis Services-Verbindung.|  
|0xC0029127|-1073573593|DTS_E_DTSPROCTASK_UNABLETOLOCATECONNECTIONMANAGER|Die „%1“-Verbindung wurde nicht gefunden.|  
|0xC0029128|-1073573592|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEEXE|Vom Analysis Services-Task DDL ausführen wurde ein ungültiger Taskdatenknoten empfangen.|  
|0xC0029129|-1073573591|DTS_E_DTSPROCTASK_INVALIDTASKDATANODEPROC|Vom Analysis Services-Verarbeitungstask wurde ein ungültiger Taskdatenknoten empfangen.|  
|0xC002912A|-1073573590|DTS_E_DTSPROCTASK_INVALIDDDL|Der DDL-Code ist ungültig.|  
|0xC002912B|-1073573589|DTS_E_DTSPROCTASK_INVALIDDDLPROCESSINGCOMMANDS|Der in ProcessingCommands gefundene DDL-Code ist ungültig.|  
|0xC002912C|-1073573588|DTS_E_DTSPROCTASK_CANNOTWRITEINAREADONLYVARIABLE|Das Ausführungsergebnis kann nicht in einer schreibgeschützten Variablen gespeichert werden.|  
|0xC002912D|-1073573587|DTS_E_DTSPROCTASK_INVALIDVARIABLE|Die "%1"-Variable ist nicht definiert.|  
|0xC002912E|-1073573586|DTS_E_DTSPROCTASK_CONNECTIONNOTFOUND|Der Verbindungs-Manager "%1" ist nicht definiert.|  
|0xC002912F|-1073573585|DTS_E_DTSPROCTASK_INVALIDCONNECTION|Der Verbindungs-Manager "%1" ist kein Dateiverbindungs-Manager.|  
|0xC0029130|-1073573584|DTS_E_DTSPROCTASK_NONEXISTENTATTRIBUTE|"%1" wurde beim Deserialisieren nicht gefunden.|  
|0xC0029131|-1073573583|DTS_E_DTSPROCTASK_TRACEHASBEENSTOPPED|Die Ablaufverfolgung wurde aufgrund einer Ausnahme beendet.|  
|0xC0029132|-1073573582|DTS_E_DTSPROCTASK_DDLEXECUTIONFAILED|Fehler bei der Ausführung von DDL.|  
|0xC0029133|-1073573581|DTS_E_DTSPROCTASK_FILEDOESNOTEXIST|Der "%1"-Verbindung ist keine Datei zugeordnet.|  
|0xC0029134|-1073573580|DTS_E_DTSPROCTASK_VARIABLENOTDEFINED|Die Variable „%1“ ist nicht definiert.|  
|0xC0029135|-1073573579|DTS_E_DTSPROCTASK_FILECONNECTIONNOTDEFINED|Die "%1"-Dateiverbindung ist nicht definiert.|  
|0xC0029136|-1073573578|DTS_E_EXEC2000PKGTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Der Task DTS 2000-Paket ausführen wird mit einem falschen XML-Element initiiert.|  
|0xC0029137|-1073573577|DTS_E_EXEC2000PKGTASK_HANDLER_NOT_FOUND|Der Handler wurde nicht gefunden.|  
|0xC0029138|-1073573576|DTS_E_EXEC2000PKGTASK_PACKAGE_NAME_NOT_SPECIFIED|Der Paketname ist nicht angegeben.|  
|0xC0029139|-1073573575|DTS_E_EXEC2000PKGTASK_PACKAGE_ID_NOT_SPECIFIED|Die Paket-ID ist nicht angegeben.|  
|0xC002913A|-1073573574|DTS_E_EXEC2000PKGTASK_PACKAGE_VERSIONGUID_NOT_SPECIFIED|Der Paketversions-GUID ist nicht angegeben.|  
|0xC002913B|-1073573573|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_SPECIFIED|SQL Server ist nicht angegeben.|  
|0xC002913C|-1073573572|DTS_E_EXEC2000PKGTASK_SQL_USERNAME_NOT_SPECIFIED|Der SQL Server-Benutzername ist nicht angegeben.|  
|0xC002913D|-1073573571|DTS_E_EXEC2000PKGTASK_FILE_NAME_NOT_SPECIFIED|Der Speicherdateiname ist nicht angegeben.|  
|0xC002913E|-1073573570|DTS_E_EXEC2000PKGTASK_DTS2000CANTBEEMPTY|Die DTS 2000-Paketeigenschaft ist leer.|  
|0xC002913F|-1073573569|DTS_E_EXEC2000PKGTASK_ERROR_IN_PACKAGE_EXECUTE|Fehler beim Ausführen des DTS 2000-Pakets.|  
|0xC0029140|-1073573568|DTS_E_EXEC2000PKGTASK_SQLSERVER_NOT_AVAILABLE_NETWORK|Die verfügbaren SQL Server können nicht vom Netzwerk geladen werden. Überprüfen Sie die Netzwerkverbindung.|  
|0xC0029141|-1073573567|DTS_E_EXEC2000PKGTASK_DATATYPE_NULL|Der Datentyp darf nicht NULL sein. Geben Sie den richtigen Datentyp zum Überprüfen des Werts an.|  
|0xC0029142|-1073573566|DTS_E_EXEC2000PKGTASK_NULL_VALUE|Ein NULL-Wert kann nicht mit einem beliebigen Datentyp überprüft werden.|  
|0xC0029143|-1073573565|DTS_E_EXEC2000PKGTASK_NULL_VALUE_ARGUMENT|Ein erforderliches Argument ist NULL.|  
|0xC0029144|-1073573564|DTS_E_EXEC2000PKGTASK_CLS_NOT_REGISTRED_EXCEPTION|Starten Sie zum Ausführen des DTS 2000-Pakettasks SQL Server-Setup, und wählen Sie mithilfe der Schaltfläche Erweitert im Dialogfeld Zu installierende Komponenten die Option Legacykomponente aus.|  
|0xC0029145|-1073573563|DTS_E_EXEC2000PKGTASK_NOT_PRIMITIVE_TYPE|"%1" ist kein Werttyp.|  
|0xC0029146|-1073573562|DTS_E_EXEC2000PKGTASK_CONVERT_FAILED|"%1" konnte nicht in "%2" konvertiert werden.|  
|0xC0029147|-1073573561|DTS_E_EXEC2000PKGTASK_ERROR_IN_VALIDATE|"%1" konnte nicht mit "%2" überprüft werden.|  
|0xC0029148|-1073573560|DTS_E_EXEC2000PKGTASK_ERROR_IN_LOAD_FROM_XML|Fehler in LoadFromXML beim "%1"-Tag.|  
|0xC0029149|-1073573559|DTS_E_EXEC2000PKGTASK_ERROR_IN_SAVE_TO_XML|Fehler in SaveToXML beim "%1"-Tag.|  
|0xC002914A|-1073573558|DTS_E_EXECPROCTASK_INVALIDTIMEOUT|Der eingegebene Timeoutwert ist ungültig. Geben Sie an, wie viele Sekunden der Prozess ausgeführt werden darf. Der minimale Timeout ist 0 (null). In diesem Fall wird kein Timeoutwert verwendet, und der Prozess wird so lange ausgeführt, bis er abgeschlossen ist oder bis ein Fehler auftritt. Der maximale Timeoutwert ist 2147483 (((2^31) - 1)/1000).|  
|0xC002914B|-1073573557|DTS_E_EXECPROCTASK_CANTREDIRECTIO|Datenströme können nicht umgeleitet werden, wenn der Prozess nach Ablauf der Lebensdauer des Tasks weiter ausgeführt werden kann.|  
|0xC002914C|-1073573556|DTS_E_EXECPROCTASK_PROCESSHASTIMEDOUT|Timeout des Prozesses.|  
|0xC002914D|-1073573555|DTS_E_EXECPROCTASK_EXECUTABLENOTSPECIFIED|Die ausführbare Datei ist nicht angegeben.|  
|0xC002914E|-1073573554|DTS_E_EXECPROCTASK_STDOUTVARREADONLY|Die Standardausgabevariable ist schreibgeschützt.|  
|0xC002914F|-1073573553|DTS_E_EXECPROCTASK_STDERRVARREADONLY|Die Standardfehlervariable ist schreibgeschützt.|  
|0xC0029150|-1073573552|DTS_E_EXECPROCTASK_RECEIVEDINVALIDTASKDATANODE|Vom Task Prozess ausführen wurde ein ungültiger Taskdatenknoten empfangen.|  
|0xC0029151|-1073573551|DTS_E_EXECPROCTASK_PROCESSEXITCODEEXCEEDS|Beim Ausführen von "%2" "%3" auf "%1" war der Prozessexitcode "%4", der erwartete Code war jedoch "%5".|  
|0xC0029152|-1073573550|DTS_E_EXECPROCTASK_WORKINGDIRDOESNOTEXIST|Das Verzeichnis "%1" ist nicht vorhanden.|  
|0xC0029153|-1073573549|DTS_E_EXECPROCTASK_FILEDOESNOTEXIST|Die Datei/der Prozess "%1" ist im Verzeichnis "%2" nicht vorhanden.|  
|0xC0029154|-1073573548|DTS_E_EXECPROCTASK_FILENOTINPATH|Die Datei/der Prozess "%1" ist nicht im Pfad vorhanden.|  
|0xC0029156|-1073573546|DTS_E_EXECPROCTASK_WORKINGDIRECTORYDOESNOTEXIST|Das Arbeitsverzeichnis "%1" ist nicht vorhanden.|  
|0xC0029157|-1073573545|DTS_E_EXECPROCTASK_ERROREXECUTIONVALUE|Der Prozess wurde mit dem Rückgabecode "%1" beendet. Es wurde jedoch der Code "%2" erwartet.|  
|0xC0029158|-1073573544|DTS_E_FSTASK_SYNCFAILED|Fehler beim Synchronisierungsobjekt.|  
|0xC0029159|-1073573543|DTS_E_FSTASK_INVALIDDATA|Vom Task Dateisystem wurde ein ungültiger Taskdatenknoten empfangen.|  
|0xC002915A|-1073573542|DTS_E_FSTASK_DIRECTORYEXISTS|Das Verzeichnis ist bereits vorhanden.|  
|0xC002915B|-1073573541|DTS_E_FSTASK_PATHNOTVALID|"%1" ist für den "%2"-Vorgangstyp ungültig.|  
|0xC002915C|-1073573540|DTS_E_FSTASK_DESTINATIONNOTSET|Die Destination-Eigenschaft des "%1"-Vorgangs ist nicht festgelegt.|  
|0xC002915D|-1073573539|DTS_E_FSTASK_SOURCENOTSET|Die Source-Eigenschaft des "%1"-Vorgangs ist nicht festgelegt.|  
|0xC002915E|-1073573538|DTS_E_FSTASK_CONNECTIONTYPENOTFILE|Der "%1"-Verbindungstyp ist keine Datei.|  
|0xC002915F|-1073573537|DTS_E_FSTASK_VARIABLEDOESNTEXIST|Die "%1"-Variable ist nicht vorhanden.|  
|0xC0029160|-1073573536|DTS_E_FSTASK_VARIABLENOTASTRING|Die "%1"-Variable ist keine Zeichenfolge.|  
|0xC0029163|-1073573533|DTS_E_FSTASK_FILEDOESNOTEXIST|Die Datei oder das Verzeichnis "%1", die bzw. das durch die "%2"-Verbindung dargestellt ist, ist nicht vorhanden.|  
|0xC0029165|-1073573531|DTS_E_FSTASK_DESTCONNUSAGETYPEINVALID|Der Zieldateiverbindungs-Manager "%1" besitzt einen ungültigen Verwendungstyp: "%2".|  
|0xC0029166|-1073573530|DTS_E_FSTASK_SRCCONNUSAGETYPEINVALID|Der Quelldateiverbindungs-Manager "%1" besitzt einen ungültigen Verwendungstyp: "%2".|  
|0xC0029167|-1073573529|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATION|FileSystemOperation|  
|0xC0029168|-1073573528|DTS_E_FSTASK_LOGENTRYGETTINGFILEOPERATIONDESC|Stellt Informationen zu Dateisystemvorgängen bereit.|  
|0xC0029169|-1073573527|DTS_E_FSTASK_TASKDISPLAYNAME|Task Dateisystem|  
|0xC002916A|-1073573526|DTS_E_FSTASK_TASKDESCRIPTION|Ausführen von Dateisystemvorgängen wie dem Kopieren und Löschen von Dateien.|  
|0xC002916B|-1073573525|DTS_E_FTPTASK_SYNCOBJFAILED|Fehler beim Synchronisierungsobjekt.|  
|0xC002916C|-1073573524|DTS_E_FTPTASK_UNABLETOOBTAINFILELIST|Die Dateiliste kann nicht abgerufen werden.|  
|0xC002916D|-1073573523|DTS_E_FTPTASK_LOCALPATHEMPTY|Der lokale Pfad ist leer.|  
|0xC002916E|-1073573522|DTS_E_FTPTASK_REMOTEPATHEMPTY|Der Remotepfad ist leer.|  
|0xC002916F|-1073573521|DTS_E_FTPTASK_LOCALVARIBALEEMPTY|Die lokale Variable ist leer.|  
|0xC0029170|-1073573520|DTS_E_FTPTASK_REMOTEVARIBALEEMPTY|Die Remotevariable ist leer.|  
|0xC0029171|-1073573519|DTS_E_FTPTASK_FTPRCVDINVLDDATANODE|Vom FTP-Task wurde ein ungültiger Taskdatenknoten empfangen.|  
|0xC0029172|-1073573518|DTS_E_FTPTASK_CONNECTION_NAME_NULL|Die Verbindung ist leer. Überprüfen Sie, ob eine gültige FTP-Verbindung bereitgestellt ist.|  
|0xC0029173|-1073573517|DTS_E_FTPTASK_CONNECTION_NOT_FTP|Die angegebene Verbindung ist keine FTP-Verbindung. Überprüfen Sie, ob eine gültige FTP-Verbindung bereitgestellt ist.|  
|0xC0029175|-1073573515|DTS_E_FTPTASK__INITIALIZATION_WITH_NULL_XML_ELEMENT|Der Task kann nicht mit einem NULL-XML-Element initialisiert werden.|  
|0xC0029176|-1073573514|DTS_E_FTPTASK_SAVE_TO_NULL_XML_ELEMENT|Der Task kann nicht in einem NULL-XML-Dokument gespeichert werden.|  
|0xC0029177|-1073573513|DTS_E_FTPTASK_ERROR_IN_LOAD_FROM_XML|Fehler in LoadFromXML beim "%1"-Tag.|  
|0xC0029178|-1073573512|DTS_E_FTPTASK_NOFILESATLOCATION|Es sind keine Dateien in "%1" vorhanden.|  
|0xC0029179|-1073573511|DTS_E_FTPTASK_LOCALVARIABLEISEMPTY|Die "%1"-Variable ist leer.|  
|0xC002917A|-1073573510|DTS_E_FTPTASK_REMOTEVARIABLEISEMPTY|Die "%1"-Variable ist leer.|  
|0xC002917B|-1073573509|DTS_E_FTPTASK_NOFILESINCONNMGR|Der Datei "%1" enthält keine(n) Dateipfad(e).|  
|0xC002917C|-1073573508|DTS_E_FTPTASK_NOFILEPATHSINLOCALVAR|Die Variable "%1" enthält keine(n) Dateipfad(e).|  
|0xC002917D|-1073573507|DTS_E_FTPTASK_VARIABLENOTASTRING|Die "%1"-Variable ist keine Zeichenfolge.|  
|0xC002917E|-1073573506|DTS_E_FTPTASK_VARIABLENOTFOUND|Die "%1"-Variable ist nicht vorhanden.|  
|0xC002917F|-1073573505|DTS_E_FTPTASK_INVALIDPATHONOPERATION|Ungültiger Pfad für den "%1"-Vorgang.|  
|0xC0029180|-1073573504|DTS_E_FTPTASK_DIRECTORYEXISTS|"%1" ist bereits vorhanden.|  
|0xC0029182|-1073573502|DTS_E_FTPTASK_CONNECTIONTYPENOTFILE|Der "%1"-Verbindungstyp ist keine Datei.|  
|0xC0029183|-1073573501|DTS_E_FTPTASK_FILEDOESNOTEXIST|Die durch "%1" dargestellte Datei ist nicht vorhanden.|  
|0xC0029184|-1073573500|DTS_E_FTPTASK_INVALIDDIRECTORY|Das Verzeichnis ist in der "%1"-Variablen nicht angegeben.|  
|0xC0029185|-1073573499|DTS_E_FTPTASK_NOFILESFOUND|In "%1" wurden keine Dateien gefunden.|  
|0xC0029186|-1073573498|DTS_E_FTPTASK_NODIRECTORYPATHINCONMGR|Das Verzeichnis ist im Dateiverbindungs-Manager "%1" nicht angegeben.|  
|0xC0029187|-1073573497|DTS_E_FTPTASK_UNABLETODELETELOCALEFILE|Die lokale Datei "%1" kann nicht gelöscht werden.|  
|0xC0029188|-1073573496|DTS_E_FTPTASK_UNABLETOREMOVELOCALDIRECTORY|Das lokale Verzeichnis "%1" kann nicht entfernt werden.|  
|0xC0029189|-1073573495|DTS_E_FTPTASK_UNABLETOCREATELOCALDIRECTORY|Das lokale Verzeichnis "%1" kann nicht erstellt werden.|  
|0xC002918A|-1073573494|DTS_E_FTPTASK_UNABLETORECEIVEFILES|Dateien können nicht mithilfe von "%1" empfangen werden.|  
|0xC002918B|-1073573493|DTS_E_FTPTASK_UNABLETOSENDFILES|Dateien können nicht mithilfe von "%1" gesendet werden.|  
|0xC002918C|-1073573492|DTS_E_FTPTASK_UNABLETOMAKEDIRREMOTE|Mithilfe von "%1" kann kein Remoteverzeichnis erstellt werden.|  
|0xC002918D|-1073573491|DTS_E_FTPTASK_UNABLETOREMOVEDIRREMOTE|Mithilfe von "%1" kann kein Remoteverzeichnis entfernt werden.|  
|0xC002918E|-1073573490|DTS_E_FTPTASK_UNABLETODELETEREMOTEFILES|Remotedateien können nicht mithilfe von "%1" gelöscht werden.|  
|0xC002918F|-1073573489|DTS_E_FTPTASK_UNABLETOCONNECTTOSERVER|Mithilfe von "%1" kann keine Verbindung mit dem FTP-Server hergestellt werden.|  
|0xC0029190|-1073573488|DTS_E_FTPTASK_INVALIDVARIABLEVALUE|Die "%1"-Variable beginnt nicht mit dem Zeichen "/".|  
|0xC0029191|-1073573487|DTS_E_FTPTASK_INVALIDREMOTEPATH|Der Remotepfad "%1" beginnt nicht mit dem Zeichen "/".|  
|0xC0029192|-1073573486|DTS_E_DTS_E_FTPTASK_CANNOT_ACQUIRE_CONNECTION|Fehler beim Abrufen der FTP-Verbindung. Überprüfen Sie, ob ein gültiger "%1"-Verbindungstyp angegeben wurde.|  
|0xC0029193|-1073573485|DTS_E_MSGQTASKUTIL_CERT_OPEN_STORE_FAILED|Fehler beim Öffnen des Zertifikatspeichers.|  
|0xC0029194|-1073573484|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_DISPLAY_NAME|Fehler beim Abrufen des Anzeigenamens des Zertifikats.|  
|0xC0029195|-1073573483|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_ISSUER_NAME|Fehler beim Abrufen des Ausstellernamens des Zertifikats.|  
|0xC0029196|-1073573482|DTS_E_MSGQTASKUTIL_CERT_FAILED_GETTING_FRIENDLY_NAME|Fehler beim Abrufen des Anzeigenamens des Zertifikats.|  
|0xC0029197|-1073573481|DTS_E_MSMQTASK_NO_CONNECTION|Der MSMQ-Verbindungsname ist nicht festgelegt.|  
|0xC0029198|-1073573480|DTS_E_MSMQTASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Der Task wurde mit dem falschen XML-Element initialisiert.|  
|0xC0029199|-1073573479|DTS_E_MSMQTASK_DATA_FILE_NAME_EMPTY|Der Datendateiname ist leer.|  
|0xC002919A|-1073573478|DTS_E_MSMQTASK_DATA_FILE_SAVE_NAME_EMPTY|Der zum Speichern der Datendatei angegebene Name ist leer.|  
|0xC002919B|-1073573477|DTS_E_MSMQTASK_DATA_FILE_SIZE_ERROR|Die Dateigröße sollte kleiner als 4 MB. sein.|  
|0xC002919C|-1073573476|DTS_E_MSMQTASK_DATA_FILE_SAVE_FAILED|Fehler beim Speichern der Datendatei.|  
|0xC002919D|-1073573475|DTS_E_MSMQTASK_STRING_COMPARE_VALUE_MISSING|Der Zeichenfolgen-Filterwert ist leer.|  
|0xC002919E|-1073573474|DTS_E_MSMQTASK_INVALID_QUEUE_PATH|Ungültiger Warteschlangenpfad.|  
|0xC002919F|-1073573473|DTS_E_MSMQTASK_NOT_TRANSACTIONAL|Der Task Nachrichtenwarteschlange unterstützt das Eintragen in verteilte Transaktionen nicht.|  
|0xC00291A0|-1073573472|DTS_E_MSMQTASK_INVALID_MESSAGE_TYPE|Ungültiger Nachrichtentyp.|  
|0xC00291A1|-1073573471|DTS_E_MSMQTASK_TASK_TIMEOUT|Timeout der Nachrichtenwarteschlange. Es wurde keine Nachricht empfangen.|  
|0xC00291A2|-1073573470|DTS_E_MSMQTASK_INVALID_PROPERTY_VALUE|Die angegebene Eigenschaft ist ungültig. Überprüfen Sie, ob der Argumenttyp richtig ist.|  
|0xC00291A3|-1073573469|DTS_E_MSMQTASK_MESSAGE_NON_AUTHENTICATED|Die Nachricht ist nicht authentifiziert.|  
|0xC00291A4|-1073573468|DTS_E_MSMQTASK_INVALID_ENCRYPTION_ALGO_WRAPPER|Sie versuchen, den Wert für den Verschlüsselungsalgorithmus mit einem ungültigen Objekt festzulegen.|  
|0xC00291A5|-1073573467|DTS_E_MSMQTASK_VARIABLE_TO_RECEIVE_STRING_MSG_EMPTY|Die Variable zum Empfangen der Zeichenfolgennachricht ist leer.|  
|0xC00291A6|-1073573466|DTS_E_MSMQTASK_RECEIVE_VARIABLE_EMPTY|Die Variable zum Empfangen der Variablennachricht ist leer.|  
|0xC00291A7|-1073573465|DTS_E_MSMQTASK_CONNECTIONTYPENOTMSMQ|Die "%1"-Verbindung ist nicht vom Typ "MSMQ".|  
|0xC00291A8|-1073573464|DTS_E_MSMQTASK_DATAFILE_ALREADY_EXISTS|Die Datendatei "%1" ist im angegebenen Speicherort bereits vorhanden. Die Datei kann nicht überschrieben werden, da die Option für das Überschreiben auf False festgelegt ist.|  
|0xC00291A9|-1073573463|DTS_E_MSMQTASK_STRING_MSG_TO_VARIABLE_NOT_FOUND|Die angegebene "%1"-Variable zum Empfangen der Zeichenfolgennachricht wurde in der Auflistung der Paketvariablen nicht gefunden.|  
|0xC00291AA|-1073573462|DTS_E_MSMQTASK_CONNMNGRNULL|Der Verbindungs-Manager "%1" ist leer.|  
|0xC00291AB|-1073573461|DTS_E_MSMQTASK_CONNMNGRDOESNOTEXIST|Der Verbindungs-Manager "%1" ist nicht vorhanden.|  
|0xC00291AC|-1073573460|DTS_E_SCRIPTTASK_COMPILEERRORMSG|Fehler "% 1": "% 2 "\r\nLine "% 3"   Spalte "% 4" durch "% 5."|  
|0xC00291AD|-1073573459|DTS_E_SCRIPTTASK_COMPILEERRORMSG2|Fehler beim Kompilieren des Skripts: "%1".|  
|0xC00291AE|-1073573458|DTS_E_SCRIPTTASK_COMPILEERRORMSG3|Fehler "%1": "%2"\r\nZeile "%3" Spalten "%4"-"%5"\r\nZeilentext: "%6".|  
|0xC00291AF|-1073573457|DTS_E_SCRIPTTASK_SCRIPTREPORTEDFAILURE|Vom Benutzerskript wurde ein Fehlerergebnis zurückgegeben.|  
|0xC00291B0|-1073573456|DTS_E_SCRIPTTASK_SCRIPTFILESFAILEDTOLOAD|Fehler beim Laden der Benutzerskriptdateien.|  
|0xC00291B1|-1073573455|DTS_E_SCRIPTTASK_SCRIPTTHREWEXCEPTION|Vom Benutzerskript wurde eine Ausnahme zurückgegeben: "%1".|  
|0xC00291B2|-1073573454|DTS_E_SCRIPTTASK_COULDNOTCREATEENTRYPOINTCLASS|Eine Instanz der Einstiegspunktklasse "%1" konnte nicht erstellt werden.|  
|0xC00291B3|-1073573453|DTS_E_SCRIPTTASK_LOADFROMXMLEXCEPTION|Ausnahme beim Laden des Skripttasks aus dem XML-Code: "%1".|  
|0xC00291B4|-1073573452|DTS_E_SCRIPTTASK_SOURCEITEMNOTFOUNDEXCEPTION|Das "%1"-Quellelement wurde im Paket nicht gefunden.|  
|0xC00291B5|-1073573451|DTS_E_SCRIPTTASK_BINARYITEMNOTFOUNDEXCEPTION|Das "%1"-Binärelement wurde im Paket nicht gefunden.|  
|0xC00291B6|-1073573450|DTS_E_SCRIPTTASK_UNRECOGNIZEDSCRIPTLANGUAGEEXCEPTION|"%1" wurde nicht als gültige Skriptsprache erkannt.|  
|0xC00291B7|-1073573449|DTS_E_SCRIPTTASK_ILLEGALSCRIPTNAME|Der Skriptname ist ungültig. Er darf keine Leerzeichen, Schrägstriche oder Sonderzeichen enthalten und nicht mit einer Zahl beginnen.|  
|0xC00291B8|-1073573448|DTS_E_SCRIPTTASK_INVALIDSCRIPTLANGUAGE|Die angegebene Skriptsprache ist ungültig.|  
|0xC00291B9|-1073573447|DTS_E_SCRIPTTASK_CANTINITNULLTASK|Mit einem NULL-Task kann nicht initialisiert werden.|  
|0xC00291BA|-1073573446|DTS_E_SCRIPTTASK_MUSTINITWITHRIGHTTASK|Die Skripttask-Benutzeroberfläche muss mit einem Skripttask initialisiert werden.|  
|0xC00291BB|-1073573445|DTS_E_SCRIPTTASK_WASNOTINITED|Die Skripttask-Benutzeroberfläche ist nicht initialisiert.|  
|0xC00291BC|-1073573444|DTS_E_SCRIPTTASK_HOST_NAME_CANT_EMPTY|Der Name darf nicht leer sein.|  
|0xC00291BD|-1073573443|DTS_E_SCRIPTTASK_INVALID_SCRIPT_NAME|Der Projektname ist ungültig. Er darf keine Leerzeichen, Schrägstriche oder Sonderzeichen enthalten und nicht mit einer Zahl beginnen.|  
|0xC00291BE|-1073573442|DTS_E_SCRIPTTASK_INVALID_SCRIPT_LANGUAGE|Die angegebene Skriptsprache ist ungültig.|  
|0xC00291BF|-1073573441|DTS_E_SCRIPTTASK_INVALID_ENTRY_POINT|Der Einstiegspunkt wurde nicht gefunden.|  
|0xC00291C0|-1073573440|DTS_E_SCRIPTTASK_LANGUAGE_EMPTY|Die Skriptsprache ist nicht angegeben. Überprüfen Sie, ob eine gültige Skriptsprache angegeben wurde.|  
|0xC00291C1|-1073573439|DTS_E_SCRIPTTASK_INITIALIZATION_WITH_NULL_TASK|Initialisierung der Benutzeroberfläche: Der Task ist NULL.|  
|0xC00291C2|-1073573438|DTS_E_SCRIPTTASK_UI_INITIALIZATION_WITH_WRONG_TASK|Die Skripttask-Benutzeroberfläche ist mit einem falschen Task initialisiert.|  
|0xC00291C3|-1073573437|DTS_E_SENDMAILTASK_RECIPIENT_EMPTY|Ein Empfänger wurde nicht angegeben.|  
|0xC00291C4|-1073573436|DTS_E_SENDMAILTASK_SMTP_SERVER_NOT_SPECIFIED|Der SMTP (Simple Mail Transfer Protocol)-Server ist nicht angegeben. Stellen Sie einen gültigen Namen oder eine gültige IP-Adresse für den SMTP-Server bereit.|  
|0xC00291C5|-1073573435|DTS_E_SENDMAILTASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Der Task „Mail senden“ ist mit einem falschen XML-Element initialisiert.|  
|0xC00291CB|-1073573429|DTS_E_SENDMAILTASK_INVALIDATTACHMENT|Die Datei "%1" ist nicht vorhanden, oder Sie haben keine Zugriffsberechtigungen für die Datei.|  
|0xC00291CD|-1073573427|DTS_E_SENDMAILTASK_CHECK_VALID_SMTP_SERVER|Überprüfen Sie, ob der angegebene SMTP (Simple Mail Transfer Protocol)-Server gültig ist.|  
|0xC00291CE|-1073573426|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTFILE|Die „%1“-Verbindung ist nicht vom Typ „File“.|  
|0xC00291CF|-1073573425|DTS_E_SENDMAILTASK_FILEDOESNOTEXIST|Für den "%1"-Vorgang ist die Datei "%2" nicht vorhanden.|  
|0xC00291D0|-1073573424|DTS_E_SENDMAILTASK_VARIABLETYPEISNOTSTRING|Die "%1"-Variable ist nicht vom Typ "String".|  
|0xC00291D1|-1073573423|DTS_E_SENDMAILTASK_CONNECTIONTYPENOTSMTP|Die "%1"-Verbindung ist nicht vom Typ "SMTP".|  
|0xC00291D2|-1073573422|DTS_E_SENDMAILTASK_CONNMNGRNULL|Die "%1"-Verbindung ist leer.|  
|0xC00291D3|-1073573421|DTS_E_SENDMAILTASK_NOCONNMNGR|Die angegebene "%1"-Verbindung ist nicht vorhanden.|  
|0xC00291D4|-1073573420|DTS_E_SQLTASK_NOSTATEMENTSPECIFIED|Eine Transact-SQL-Anweisung wurde nicht angegeben.|  
|0xC00291D5|-1073573419|DTS_E_SQLTASK_NOXMLSUPPORT|Die Verbindung unterstützt keine XML-Resultsets.|  
|0xC00291D6|-1073573418|DTS_E_SQLTASK_NOHANDLERFORCONNECTION|Für den angegebenen Verbindungstyp kann kein Handler gefunden werden.|  
|0xC00291D7|-1073573417|DTS_E_SQLTASK_NOCONNECTIONMANAGER|Es ist kein Verbindungs-Manager angegeben.|  
|0xC00291D8|-1073573416|DTS_E_SQLTASK_CANNOTACQUIRECONNMANAGER|Es konnte keine Verbindung aus dem Verbindungs-Manager abgerufen werden.|  
|0xC00291D9|-1073573415|DTS_E_SQLTASK_NULLPARAMETERNAME|Ein NULL-Parametername ist unzulässig.|  
|0xC00291DA|-1073573414|DTS_E_SQLTASK_INVALIDPARAMETERNAME|Der Parametername ist ungültig.|  
|0xC00291DB|-1073573413|DTS_E_SQLTASK_VALIDPARAMETERTYPES|Gültige Parameternamen sind vom Typ Int oder String.|  
|0xC00291DC|-1073573412|DTS_E_SQLTASK_READONLYVARIABLE|Die "%1"-Variable kann in einer Ergebnisbindung nicht verwendet werden, da sie schreibgeschützt ist.|  
|0xC00291DD|-1073573411|DTS_E_SQLTASK_INDESNOTINCOLLECTION|In dieser Auflistung ist der Index nicht zugewiesen.|  
|0xC00291DE|-1073573410|DTS_E_SQLTASK_ROVARINOUTPARAMETER|Die "%1"-Variable kann nicht als Ausgabeparameter oder Rückgabewert in einer Parameterbindung verwendet werden, da sie schreibgeschützt ist.|  
|0xC00291DF|-1073573409|DTS_E_SQLTASK_OBJECTNOTINCOLLECTION|Das Objekt ist in dieser Auflistung nicht vorhanden.|  
|0xC00291E0|-1073573408|DTS_E_SQLTASK_UNABLETOACQUIREMANAGEDCONN|Eine verwaltete Verbindung kann nicht abgerufen werden.|  
|0xC00291E1|-1073573407|DTS_E_UNABLETOPOPRESULT|Die Ergebnisspalten für den Ergebnistyp mit einzelnen Zeilen konnten nicht aufgefüllt werden. Die Abfrage gab ein leeres Resultset zurück.|  
|0xC00291E2|-1073573406|DTS_E_SQLTASK_INVALIDNUMOFRESULTBINDINGS|Die zurückgegebene Anzahl von Ergebnisbindungen ist für ResultSetType ungültig: "%1".|  
|0xC00291E3|-1073573405|DTS_E_SQLTASK_RESULTBINDTYPEFORROWSETXML|Der Name der Ergebnisbindung muss für vollständige Resultset- und XML-Ergebnisse auf 0 (null) festgelegt sein.|  
|0xC00291E4|-1073573404|DTS_E_SQLTASK_INVALIDEPARAMDIRECTIONFALG|Das Richtungsflag des Parameters ist ungültig.|  
|0xC00291E5|-1073573403|DTS_E_SQLTASK_NOSQLTASKDATAINXMLFRAGMENT|Das XML-Fragment enthält keine Daten für den SQL-Task.|  
|0xC00291E6|-1073573402|DTS_E_SQLTASK_MULTIPLERETURNVALUEPARAM|Es wird kein Parameter vom Typ Rückgabewert als erster Parameter verwendet, oder es sind mehrere Parameter vom Typ Rückgabewert vorhanden.|  
|0xC00291E7|-1073573401|DTS_E_SQLTASK_CONNECTIONTYPENOTFILE|Die "%1"-Verbindung ist kein Dateiverbindungs-Manager.|  
|0xC00291E8|-1073573400|DTS_E_SQLTASK_FILEDOESNOTEXIST|Die durch "%1" dargestellte Datei ist nicht vorhanden.|  
|0xC00291E9|-1073573399|DTS_E_SQLTASK_VARIABLETYPEISNOTSTRING|Die Variable „%1“ ist nicht vom Typ „String“.|  
|0xC00291EA|-1073573398|DTS_E_SQLTASK_VARIABLENOTFOUND|Die "%1"-Variable ist nicht vorhanden oder konnte nicht gesperrt werden.|  
|0xC00291EB|-1073573397|DTS_E_SQLTASK_CANNOTLOCATECONNMANAGER|Der Verbindungs-Manager "%1" ist nicht vorhanden.|  
|0xC00291EC|-1073573396|DTS_E_SQLTASK_FAILEDTOACQUIRECONNECTION|Fehler beim Abrufen der "%1"-Verbindung. Die Verbindung ist möglicherweise nicht ordnungsgemäß konfiguriert, oder Sie verfügen nicht über die erforderlichen Berechtigungen für die Verbindung.|  
|0xC00291ED|-1073573395|DTS_E_SQLTASK_RESULTBYNAMENOTSUPPORTED|Die Ergebnisbindung anhand des Namens "%1" wird für diesen Verbindungstyp nicht unterstützt.|  
|0xC00291EE|-1073573394|DTS_E_SQLTASKCONN_ERR_NO_ROWS|Der Resultsettyp Einzelne Zeile ist angegeben, aber es wurden keine Zeilen zurückgegeben.|  
|0xC00291EF|-1073573393|DTS_E_SQLTASKCONN_ERR_NO_DISCONNECTED_RS|Für die Transact-SQL-Anweisung ist kein getrenntes Recordset verfügbar.|  
|0xC00291F0|-1073573392|DTS_E_SQLTASKCONN_ERR_UNSUPPORTED_TYPE|Nicht unterstützter Typ.|  
|0xC00291F1|-1073573391|DTS_E_SQLTASKCONN_ERR_UNKNOWN_TYPE|Unbekannter Typ.|  
|0xC00291F2|-1073573390|DTS_E_SQLTASKCONN_ERR_PARAM_DATA_TYPE|Nicht unterstützter Datentyp in der Parameterbindung \\"%s\\".|  
|0xC00291F3|-1073573389|DTS_E_SQLTASKCONN_ERR_PARAM_NAME_MIX|Parameternamen dürfen nicht aus einer Mischung von Ordnungszahlen und Namen bestehen.|  
|0xC00291F4|-1073573388|DTS_E_SQLTASKCONN_ERR_PARAM_DIR|Ungültige Parameterrichtung in der Parameterbindung \\"%s\\".|  
|0xC00291F5|-1073573387|DTS_E_SQLTASKCONN_ERR_RESULT_DATA_TYPE|Nicht unterstützter Datentyp in der Resultsetbindung \\"%s\\".|  
|0xC00291F6|-1073573386|DTS_E_SQLTASKCONN_ERR_RESULT_COL_INDEX|Ungültiger Ergebnisspaltenindex %d.|  
|0xC00291F7|-1073573385|DTS_E_SQLTASKCONN_ERR_UNKNOWN_RESULT_COL|Die \\"%s\\"-Spalte wurde im Resultset nicht gefunden.|  
|0xC00291F9|-1073573383|DTS_E_SQLTASKCONN_ERR_NOROWSET|Der Ausführung dieser Abfrage ist kein Ergebnisrowset zugeordnet.|  
|0xC00291FA|-1073573382|DTS_E_SQLTASKCONN_ERR_ODBC_DISCONNECTED|Getrennte Recordsets sind bei ODBC-Verbindungen nicht verfügbar.|  
|0xC00291FB|-1073573381|DTS_E_SQLTASKCONN_ERR_RESULT_SET_DATA_TYPE|Der Datentyp im Resultset, Spalte '%hd', wird nicht unterstützt.|  
|0xC00291FC|-1073573380|DTS_E_SQLTASKCONN_ERR_CANT_LOAD_XML|XML kann nicht mit dem Abfrageergebnis geladen werden.|  
|0xC00291FD|-1073573379|DTS_E_TTGENTASK_NOCONNORVARIABLE|Für das Paket muss ein Verbindungsname oder Variablenname angegeben sein.|  
|0xC00291FE|-1073573378|DTS_E_TTGENTASK_FAILEDCREATE|Das Paket konnte nicht erstellt werden.|  
|0xC00291FF|-1073573377|DTS_E_TTGENTASK_BADTABLEMETADATA|Das TableMetaDataNode-Objekt ist kein XMLNode-Objekt.|  
|0xC0029200|-1073573376|DTS_E_TTGENTASK_FAILEDCREATEPIPELINE|Die Pipeline konnte nicht erstellt werden.|  
|0xC0029201|-1073573375|DTS_E_TTGENTASK_BADVARIABLETYPE|Die Variable ist nicht vom richtigen Typ.|  
|0xC0029202|-1073573374|DTS_E_TTGENTASK_NOTFILECONNECTION|Der angegebene Verbindungs-Manager ist kein Dateiverbindungs-Manager.|  
|0xC0029203|-1073573373|DTS_E_TTGENTASK_BADFILENAME|Für den Verbindungs-Manager "%1" ist ein ungültiger Dateiname angegeben.|  
|0xC0029204|-1073573372|DTS_E_WEBSERVICETASK_CONNECTION_NAME_NULL|Die Verbindung ist leer. Überprüfen Sie, ob eine gültige HTTP-Verbindung angegeben ist.|  
|0xC0029205|-1073573371|DTS_E_WEBSERVICETASK_CONNECTION_NOT_FOUND|Die Verbindung ist nicht vorhanden. Überprüfen Sie, ob eine gültige, vorhandene HTTP-Verbindung angegeben ist.|  
|0xC0029206|-1073573370|DTS_E_WEBSERVICETASK_CONNECTION_NOT_HTTP|Die angegebene Verbindung ist keine HTTP-Verbindung. Überprüfen Sie, ob eine gültige HTTP-Verbindung angegeben ist.|  
|0xC0029207|-1073573369|DTS_E_WEBSERVICETASK_SERVICE_NULL|Der Webdienstname ist leer. Überprüfen Sie, ob ein gültiger Webdienstname angegeben ist.|  
|0xC0029208|-1073573368|DTS_E_WEBSERVICETASK_METHODNAME_NULL|Der Name der Webmethode ist leer. Überprüfen Sie, ob eine gültige Webmethode angegeben ist.|  
|0xC0029209|-1073573367|DTS_E_WEBSERVICETASK_WEBMETHODINFO_NULL|Die Webmethode ist leer oder ist möglicherweise nicht vorhanden. Überprüfen Sie, ob eine vorhandene Webmethode angegeben werden kann.|  
|0xC002920A|-1073573366|DTS_E_WEBSERVICETASK_OUTPUTLOC_NULL|Der Ausgabespeicherort ist leer. Überprüfen Sie, ob eine vorhandene Dateiverbindung oder Variable angegeben ist.|  
|0xC002920B|-1073573365|DTS_E_WEBSERVICETASK_VARIABLE_NOT_FOUND|Die Variable wurde nicht gefunden. Überprüfen Sie, ob die Variable im Paket vorhanden ist.|  
|0xC002920C|-1073573364|DTS_E_WEBSERVICETASK_VARIABLE_READONLY|Das Ergebnis kann nicht gespeichert werden. Überprüfen Sie, ob die Variable schreibgeschützt ist.|  
|0xC002920D|-1073573363|DTS_E_WEBSERVICETASK_ERROR_IN_LOAD_FROM_XML|Fehler in LoadFromXML beim "%1"-Tag.|  
|0xC002920E|-1073573362|DTS_E_WEBSERVICETASK_ERROR_IN_SAVE_TO_XML|Fehler in SaveToXML beim "%1"-Tag.|  
|0xC002920F|-1073573361|DTS_E_WEBSERVICETASK_TASK_SAVE_TO_NULL_XML_ELEMENT|Der Task kann nicht in einem NULL-XML-Dokument gespeichert werden.|  
|0xC0029210|-1073573360|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_NULL_XML_ELEMENT|Der Task kann nicht mit einem NULL-XML-Element initialisiert werden.|  
|0xC0029211|-1073573359|DTS_E_WEBSERVICETASK_TASK_INITIALIZATION_WITH_WRONG_XML_ELEMENT|Der Task Webdienst wurde mit einem falschen XML-Element initiiert.|  
|0xC0029212|-1073573358|DTS_E_WEBSERVICETASK_UNEXPECTED_XML_ELEMENT|Ein unerwartetes XML-Element wurde gefunden.|  
|0xC0029213|-1073573357|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_CONNECTION|Fehler beim Abrufen der HTTP-Verbindung. Überprüfen Sie, ob ein gültiger Verbindungstyp angegeben ist.|  
|0xC0029214|-1073573356|DTS_E_WEBSERVICETASK_FILE_CONN_NOT_FOUND|Das Ergebnis kann nicht gespeichert werden. Überprüfen Sie, ob eine Dateiverbindung vorhanden ist.|  
|0xC0029215|-1073573355|DTS_E_WEBSERVICETASK_FILE_NOT_FOUND|Das Ergebnis kann nicht gespeichert werden. Überprüfen Sie, ob die Datei vorhanden ist.|  
|0xC0029216|-1073573354|DTS_E_WEBSERVICETASK_FILE_NULL|Das Ergebnis kann nicht gespeichert werden. Der Dateiname ist leer, oder die Datei wird von einem anderen Prozess verwendet.|  
|0xC0029217|-1073573353|DTS_E_WEBSERVICETASK_CANNOT_ACQUIRE_FILE_CONNECTION|Fehler beim Anfordern der Dateiverbindung. Überprüfen Sie, ob eine gültige Dateiverbindung angegeben ist.|  
|0xC0029218|-1073573352|DTS_E_WEBSERVICETASK_DATATYPE_NOT_SUPPORTED|Es werden nur Complex-Typen mit Werten vom Primitive-Typ, Arrays vom Primitive-Typ und Enumerationen unterstützt.|  
|0xC0029219|-1073573351|DTS_E_WEBSERVICETASK_PARAMTYPE_NOT_SUPPORTED|Es werden nur die Typen Primitive, Enum, Complex, PrimitiveArray und ComplexArray unterstützt.|  
|0xC002921A|-1073573350|DTS_E_WEBSERVICETASK_WSDL_VERSION_NOT_SUPPORTED|Diese WSDL-Version wird nicht unterstützt.|  
|0xC002921B|-1073573349|DTS_E_WEBSERVICETASK_WRONG_XML_ELEMENT|Initialisiert mit einem falschen XML-Element.|  
|0xC002921C|-1073573348|DTS_E_WEBSERVICETASK_XML_ATTRIBUTE_NOT_FOUND|Ein verbindliches Attribut wurde nicht gefunden.|  
|0xC002921D|-1073573347|DTS_E_WEBSERVICETASK_ENUM_NO_VALUES|Die "%1"-Enumeration weist keine Werte auf. Die WSDL-Datei ist beschädigt.|  
|0xC002921E|-1073573346|DTS_E_WEBSERVICETASK_CONNECTIONNOTFOUND|Die Verbindung wurde nicht gefunden.|  
|0xC002921F|-1073573345|DTS_E_WEBSERVICETASK_CONNECTION_ALREADY_EXISTS|Eine Verbindung mit diesem Namen ist bereits vorhanden.|  
|0xC0029220|-1073573344|DTS_E_WEBSERVICETASK_NULL_CONNECTION|Die Verbindung darf nicht NULL oder leer sein.|  
|0xC0029221|-1073573343|DTS_E_WEBSERVICETASK_NOT_HTTP_CONNECTION|Die angegebene Verbindung ist keine HTTP-Verbindung. Überprüfen Sie, ob eine gültige HTTP-Verbindung angegeben ist.|  
|0xC0029222|-1073573342|DTS_E_WEBSERVICETASK_WSDL_NOT_FOUND|Der angegebene URI (Uniform Resource Identifier) weist keine gültige WSDL auf.|  
|0xC0029223|-1073573341|DTS_E_WEBSERVICETASK_ERROR_IN_DOWNLOAD|Die WSDL-Datei konnte nicht gelesen werden. Die WSDL-Eingabedatei ist ungültig. Der folgende Fehler trat beim Leser auf: "%1".|  
|0xC0029224|-1073573340|DTS_E_WEBSERVICETASK_SERVICE_DESC_NULL|Die Dienstbeschreibung darf nicht NULL sein.|  
|0xC0029225|-1073573339|DTS_E_WEBSERVICETASK_SERVICENULL|Der Dienstname darf nicht NULL sein.|  
|0xC0029226|-1073573338|DTS_E_WEBSERVICETASK_WSDL_NULL|Die URL darf nicht NULL sein.|  
|0xC0029227|-1073573337|DTS_E_WEBSERVICETASK_SERVICE_NOT_FOUND|Der Dienst ist zurzeit nicht verfügbar.|  
|0xC0029228|-1073573336|DTS_E_WEBSERVICETASK_SOAPPORT_NOT_FOUND|Der Dienst ist am SOAP-Port nicht verfügbar.|  
|0xC0029229|-1073573335|DTS_E_WEBSERVICETASK_SOAPBINDING_NOT_FOUND|Fehler beim Analysieren der Web Services Description Language (WSDL). Die dem SOAP-Port entsprechende Bindung wurde nicht gefunden.|  
|0xC002922A|-1073573334|DTS_E_WEBSERVICETASK_SOAPPORTTYPE_NOT_FOUND|Fehler beim Analysieren der Web Services Description Language (WSDL). Ein dem SOAP-Port entsprechendes PortType-Objekt wurde nicht gefunden.|  
|0xC002922B|-1073573333|DTS_E_WEBSERVICETASK_MSG_NOT_FOUND|Die Meldung, die der angegebenen Methode entspricht, wurde nicht gefunden.|  
|0xC002922C|-1073573332|DTS_E_WEBSERVICETASK_CANNOT_GEN_PROXY|Der Proxy für den angegebenen Webdienst konnte nicht generiert werden. Folgende Fehler traten beim Generieren des Proxys auf: "%1".|  
|0xC002922D|-1073573331|DTS_E_WEBSERVICETASK_CANNOT_LOAD_PROXY|Der Proxy für den angegebenen Webdienst konnte nicht geladen werden. Der genaue Fehler: "%1".|  
|0xC002922E|-1073573330|DTS_E_WEBSERVICETASK_INVALID_SERVICE|Der angegebene Dienst wurde nicht gefunden. Der genaue Fehler: "%1".|  
|0xC002922F|-1073573329|DTS_E_WEBSERVICETASK_WEBMETHOD_INVOKE_FAILED|Fehler beim Webdienst beim Ausführen der Methode: "%1".|  
|0xC0029230|-1073573328|DTS_E_WEBSERVICETASK_INVOKE_ERR|Die Webmethode konnte nicht ausgeführt werden. Der genaue Fehler: "%1".|  
|0xC0029231|-1073573327|DTS_E_WEBSERVICETASK_METHODINFO_NULL|MethodInfo darf nicht NULL sein.|  
|0xC0029232|-1073573326|DTS_E_WEBSERVICETASK_VALUE_NOT_PRIMITIVE|Das angegebene WebMethodInfo-Objekt ist falsch. Das angegebene ParamValue-Objekt stimmt nicht mit dem ParamType-Objekt überein. Das DTSParamValue-Objekt ist nicht vom Typ PrimitiveValue.|  
|0xC0029233|-1073573325|DTS_E_WEBSERVICETASK_VALUE_NOT_ENUM|Das angegebene WebMethodInfo-Objekt ist falsch. Das angegebene ParamValue-Objekt stimmt nicht mit dem ParamType-Objekt überein. Das gefundene DTSParamValue-Objekt ist nicht vom Typ EnumValue.|  
|0xC0029234|-1073573324|DTS_E_VALUE_WEBSERVICETASK_NOT_COMPLEX|Das angegebene WebMethodInfo-Objekt ist falsch. Das angegebene ParamValue-Objekt stimmt nicht mit dem ParamType-Objekt überein. Das gefundene DTSParamValue-Objekt ist nicht vom Typ ComplexValue.|  
|0xC0029235|-1073573323|DTS_E_WEBSERVICETASK_VALUE_NOT_ARRAY|Das angegebene WebMethodInfo-Objekt ist falsch. Das angegebene ParamValue-Objekt stimmt nicht mit dem ParamType-Objekt überein. Das gefundene DTSParamValue-Objekt ist nicht vom Typ ArrayValue.|  
|0xC0029236|-1073573322|DTS_E_WEBSERVICETASK_TYPE_NOT_PRIMITIVE|Das angegebene WebMethodInfo-Objekt ist falsch. "%1" ist nicht vom Typ "Primitive".|  
|0xC0029237|-1073573321|DTS_E_WEBSERVICETASK_ARRAY_VALUE_INVALID|Ungültiges Format des ArrayValue-Objekts. Im Array muss mindestens ein Element vorhanden sein.|  
|0xC0029238|-1073573320|DTS_E_WEBSERVICETASK_SELECTED_VALUE_NULL|Der Wert der Enumeration darf nicht NULL sein. Wählen Sie einen Standardwert für die Enumeration aus.|  
|0xC0029239|-1073573319|DTS_E_WEBSERVICETASK_NULL_VALUE|Ein NULL-Wert kann nicht mit einem beliebigen Datentyp überprüft werden.|  
|0xC002923A|-1073573318|DTS_E_WEBSERVICETASK_ENUM_VALUE_NOT_FOUND|Ungültiger Enumerationswert.|  
|0xC002923B|-1073573317|DTS_E_WEBSERVICETASK_PROP_NOT_EXISTS|Die angegebene Klasse enthält keine öffentliche Eigenschaft mit dem Namen "%1".|  
|0xC002923C|-1073573316|DTS_E_WEBSERVICETASK_CONVERT_FAILED|"%1" konnte nicht in "%2" konvertiert werden.|  
|0xC002923D|-1073573315|DTS_E_WEBSERVICETASK_CLEANUP_FAILED|Fehler beim Cleanup. Der für den Webdienst erstellte Proxy wurde möglicherweise nicht gelöscht.|  
|0xC002923E|-1073573314|DTS_E_WEBSERVICETASK_CREATE_INSTANCE_FAILED|Ein Objekt vom Typ "%1" konnte nicht erstellt werden. Überprüfen Sie, ob der Standardkonstruktor vorhanden ist.|  
|0xC002923F|-1073573313|DTS_E_WEBSERVICETASK_NOT_PRIMITIVE_TYPE|"%1" ist kein Werttyp.|  
|0xC0029240|-1073573312|DTS_E_WEBSERVICETASK_ERROR_IN_VALIDATE|"%1" konnte nicht mit "%1" überprüft werden.|  
|0xC0029241|-1073573311|DTS_E_WEBSERVICETASK_DATATYPE_NULL|Der Datentyp darf nicht NULL sein. Geben Sie den Wert des zu überprüfenden Datentyps an.|  
|0xC0029242|-1073573310|DTS_E_WEBSERVICETASK_INDEX_OUT_OF_BOUNDS|Das ParamValue-Objekt kann an dieser Position nicht eingefügt werden. Der angegebene Index ist möglicherweise kleiner als 0 (null) oder größer als die Länge.|  
|0xC0029243|-1073573309|DTS_E_WEBSERVICETASK_WRONG_WSDL|Die WSDL-Eingabedatei ist ungültig.|  
|0xC0029244|-1073573308|DTS_E_WMIDRTASK_SYNCOBJECTFAILED|Fehler beim Synchronisierungsobjekt.|  
|0xC0029245|-1073573307|DTS_E_WMIDRTASK_MISSINGWQLQUERY|Die WQL-Abfrage fehlt.|  
|0xC0029246|-1073573306|DTS_E_WMIDRTASK_DESTINATIONMUSTBESET|Das Ziel muss festgelegt sein.|  
|0xC0029247|-1073573305|DTS_E_WMIDRTASK_MISSINGCONNECTION|Eine WMI-Verbindung wurde nicht festgelegt.|  
|0xC0029248|-1073573304|DTS_E_WMIDRTASK_INVALIDDATANODE|Vom Task WMI-Datenleser wurde ein ungültiger Taskdatenknoten empfangen.|  
|0xC0029249|-1073573303|DTS_E_WMIDRTASK_FAILEDVALIDATION|Fehler bei der Überprüfung des Tasks.|  
|0xC002924A|-1073573302|DTS_E_WMIDRTASK_FILEDOESNOTEXIST|Die Datei "%1" ist nicht vorhanden.|  
|0xC002924B|-1073573301|DTS_E_WMIDRTASK_CONNECTIONMNGRDOESNTEXIST|Der Verbindungs-Manager "%1" ist nicht vorhanden.|  
|0xC002924C|-1073573300|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRINGOROBJECT|Die "%1"-Variable ist nicht vom Typ "String" oder "Object".|  
|0xC002924D|-1073573299|DTS_E_WMIDRTASK_CONNECTIONTYPENOTFILE|Die "%1"-Verbindung ist nicht vom Typ "FILE".|  
|0xC002924E|-1073573298|DTS_E_WMIDRTASK_CONNECTIONTYPENOTWMI|Die "%1"-Verbindung ist nicht vom Typ "WMI".|  
|0xC002924F|-1073573297|DTS_E_WMIDRTASK_FILEALREADYEXISTS|Die Datei "%1" ist bereits vorhanden.|  
|0xC0029250|-1073573296|DTS_E_WMIDRTASK_CONNECTIONMANAGEREMPTY|Der Verbindungs-Manager "%1" ist leer.|  
|0xC0029251|-1073573295|DTS_E_WMIDRTASK_VARNOTOBJECT|Die „%1“-Variable muss vom Typ „Object“ sein, damit ihr eine Datentabelle zugewiesen werden kann.|  
|0xC0029252|-1073573294|DTS_E_WMIDRTASK_TASKFAILURE|Fehler beim Task aufgrund einer ungültigen WMI-Abfrage: "%1".|  
|0xC0029253|-1073573293|DTS_E_WMIDRTASK_CANTWRITETOVAR|Die "%1"-Variable kann nicht geschrieben werden, da festgelegt ist, dass der ursprüngliche Wert der Variablen erhalten bleiben soll.|  
|0xC0029254|-1073573292|DTS_E_WMIEWTASK_SYNCOBJECTFAILED|Fehler beim Synchronisierungsobjekt.|  
|0xC0029255|-1073573291|DTS_E_WMIEWTASK_MISSINGWQLQUERY|Die WQL-Abfrage fehlt.|  
|0xC0029256|-1073573290|DTS_E_WMIEWTASK_MISSINGCONNECTION|Die WMI-Verbindung fehlt.|  
|0xC0029257|-1073573289|DTS_E_WMIEWTASK_QUERYFAILURE|Fehler beim Ausführen der WMI-Abfrage durch den Task.|  
|0xC0029258|-1073573288|DTS_E_WMIEWTASK_INVALIDDATANODE|Vom Task WMI-Ereignisüberwachung wurde ein ungültiger Taskdatenknoten empfangen.|  
|0xC0029259|-1073573287|DTS_E_WMIEWTASK_CONNECTIONMNGRDOESNTEXIST|Der Verbindungs-Manager "%1" ist nicht vorhanden.|  
|0xC002925A|-1073573286|DTS_E_WMIEWTASK_FILEDOESNOTEXIST|Die Datei "%1" ist nicht vorhanden.|  
|0xC002925B|-1073573285|DTS_E_WMIEWTASK_VARIABLETYPEISNOTSTRING|Die "%1"-Variable ist nicht vom Typ "String".|  
|0xC002925C|-1073573284|DTS_E_WMIEWTASK_CONNECTIONTYPENOTFILE|Die "%1"-Verbindung ist nicht vom Typ "FILE".|  
|0xC002925D|-1073573283|DTS_E_WMIEWTASK_CONNECTIONTYPENOTWMI|Die "%1"-Verbindung ist nicht vom Typ "WMI".|  
|0xC002925E|-1073573282|DTS_E_WMIEWTASK_FILEALREADYEXISTS|Die Datei "%1" ist bereits vorhanden.|  
|0xC002925F|-1073573281|DTS_E_WMIEWTASK_CONNECTIONMANAGEREMPTY|Der Verbindungs-Manager "%1" ist leer.|  
|0xC0029260|-1073573280|DTS_E_WMIEWTASK_TIMEOUTOCCURRED|Ein Timeout von "%1" Sekunde(n) ist vor dem durch "%2" dargestellten Ereignis aufgetreten.|  
|0xC0029261|-1073573279|DTS_E_WMIEWTASK_ERRMESSAGE|Beim Überwachen der WQL-Abfrage wurde die folgende Systemausnahme verursacht: "%1". Überprüfen Sie die Abfrage auf Fehler, oder überprüfen Sie die Zugriffsrechte und Berechtigungen der WMI-Verbindung.|  
|0xC0029262|-1073573278|DTS_E_XMLTASK_NODEFAULTOPERTION|Das angegebene Operations-Objekt ist nicht definiert.|  
|0xC0029263|-1073573277|DTS_E_XMLTASK_CONNECTIONTYPENOTFILE|Der Verbindungstyp ist nicht File.|  
|0xC0029264|-1073573276|DTS_E_XMLTASK_CANTGETREADERFROMSOURCE|Aus dem XML-Quelldokument kann kein XmlReader-Objekt abgerufen werden.|  
|0xC0029265|-1073573275|DTS_E_XMLTASK_CANTGETREADERFROMDEST|Aus dem geänderten XML-Dokument kann kein XmlReader-Objekt abgerufen werden.|  
|0xC0029266|-1073573274|DTS_E_XMLTASK_CANTGETREADERFROMDIFFGRAM|Der XDL-DiffGram-Leser kann aus dem XML-Code für das XDL-DiffGram-Objekt nicht abgerufen werden.|  
|0xC0029268|-1073573272|DTS_E_XMLTASK_EMPTYNODELIST|Die Knotenliste ist leer.|  
|0xC0029269|-1073573271|DTS_E_XMLTASK_NOELEMENTFOUND|Das Element wurde nicht gefunden.|  
|0xC002926A|-1073573270|DTS_E_XMLTASK_UNDEFINEDOPERATION|Das angegebene Operations-Objekt ist nicht definiert.|  
|0xC002926B|-1073573269|DTS_E_XMLTASK_XPATHNAVERROR|Unerwartetes Inhaltselement in XPathNavigator.|  
|0xC002926C|-1073573268|DTS_E_XMLTASK_NOSCHEMAFOUND|Ein Schema für die Überprüfung wurde nicht gefunden.|  
|0xC002926D|-1073573267|DTS_E_XMLTASK_VALIDATIONERROR|Überprüfungsfehler beim Überprüfen des Instanzdokuments.|  
|0xC002926E|-1073573266|DTS_E_XMLTASK_SYNCOBJECTFAILED|Fehler beim Synchronisierungsobjekt.|  
|0xC002926F|-1073573265|DTS_E_XMLTASK_ROOTNOODESNOTMATCHED|Die Stammknoten stimmen nicht überein.|  
|0xC0029270|-1073573264|DTS_E_XMLTASK_INVALIDEDITSCRIPT|Der Typ zum Bearbeiten von Skriptvorgängen im endgültigen Bearbeitungsskript ist ungültig.|  
|0xC0029271|-1073573263|DTS_E_XMLTASK_CDATANODESISSUE|CDATA-Knoten sollten mit der DiffgramAddSubtrees-Klasse hinzugefügt werden.|  
|0xC0029272|-1073573262|DTS_E_XMLTASK_COMMENTSNODEISSUE|Kommentarknoten sollten mit der DiffgramAddSubtrees-Klasse hinzugefügt werden.|  
|0xC0029273|-1073573261|DTS_E_XMLTASK_TEXTNODEISSUES|Textknoten sollten mit der DiffgramAddSubtrees-Klasse hinzugefügt werden.|  
|0xC0029274|-1073573260|DTS_E_XMLTASK_WHITESPACEISSUE|Knoten mit wichtigen Leerzeichen sollten mit der DiffgramAddSubtrees-Klasse hinzugefügt werden.|  
|0xC0029275|-1073573259|DTS_E_XMLTASK_DIFFENUMISSUE|Korrigieren Sie das OperationCost-Array, sodass es die XmlDiffOperation-Enumeration widerspiegelt.|  
|0xC0029276|-1073573258|DTS_E_XMLTASK_TASKISEMPTY|Es sind keine Vorgänge im Task vorhanden.|  
|0xC0029277|-1073573257|DTS_E_XMLTASK_DOCUMENTHASDATA|Das Dokument enthält bereits Daten und darf nicht erneut verwendet werden.|  
|0xC0029278|-1073573256|DTS_E_XMLTASK_INVALIDENODETYPE|Ungültiger Knotentyp.|  
|0xC0029279|-1073573255|DTS_E_XMLTASK_INVALIDDATANODE|Vom XML-Task wurde ein ungültiger Taskdatenknoten empfangen.|  
|0xC002927B|-1073573253|DTS_E_XMLTASK_VARIABLETYPEISNOTSTRING|Der Datentyp der Variablen ist nicht String.|  
|0xC002927C|-1073573252|DTS_E_XMLTASK_COULDNOTGETENCODINGFROMDOCUMENT|Die Codierung kann nicht aus dem XML-Code abgerufen werden.|  
|0xC002927D|-1073573251|DTS_E_XMLTASK_MISSINGSOURCE|Die Quelle ist nicht angegeben.|  
|0xC002927E|-1073573250|DTS_E_XMLTASK_MISSINGSECONDOPERAND|Der zweite Operand ist nicht angegeben.|  
|0xC002927F|-1073573249|DTS_E_XMLTASK_INVALIDPATHDESCRIPTOR|Ungültiges XDL-DiffGram-Objekt. "%1" ist ein ungültiger Pfaddeskriptor.|  
|0xC0029280|-1073573248|DTS_E_XMLTASK_NOMATCHINGNODE|Ungültiges XDL-DiffGram-Objekt. Kein Knoten stimmt mit dem "%1"-Pfaddeskriptor überein.|  
|0xC0029281|-1073573247|DTS_E_XMLTASK_EXPECTINGDIFFGRAMELEMENT|Ungültiges XDL-DiffGram-Objekt. xd:xmldiff als Stammelement mit dem Namespace-URI "%1" wird erwartet.|  
|0xC0029282|-1073573246|DTS_E_XMLTASK_MISSINGSRCDOCATTRIBUTE|Ungültiges XDL-DiffgGram-Objekt. Es fehlt ein srcDocHash-Attribut im xd:xmldiff-Element.|  
|0xC0029283|-1073573245|DTS_E_XMLTASK_MISSINGOPTIONSATTRIBUTE|Ungültiges XDL-DiffgGram-Objekt. Es fehlt ein Options-Attribut im xd:xmldiff-Element.|  
|0xC0029284|-1073573244|DTS_E_XMLTASK_INVALIDSRCDOCATTRIBUTE|Ungültiges XDL-DiffgGram-Objekt. Das srcDocHash-Attribut weist einen ungültigen Wert auf.|  
|0xC0029285|-1073573243|DTS_E_XMLTASK_INVALIDOPTIONSATTRIBUTE|Ungültiges XDL-DiffgGram-Objekt. Das Options-Attribut weist einen ungültigen Wert auf.|  
|0xC0029286|-1073573242|DTS_E_XMLTASK_SRCDOCMISMATCH|Das XDL-DiffGram-Objekt ist für dieses XML-Dokument ungültig. Der rcDocHash-Wert stimmt nicht überein.|  
|0xC0029287|-1073573241|DTS_E_XMLTASK_MORETHANONENODEMATCHED|Ungültiges XDL-DiffGram-Objekt. Es stimmen mehrere Knoten mit dem "%1"-Pfaddeskriptor im xd:node- oder xd:change-Element überein.|  
|0xC0029288|-1073573240|DTS_E_XMLTASK_XMLDECLMISMATCH|Das XDL-DiffGram-Objekt ist für dieses XML-Dokument ungültig. Eine neue XML-Deklaration kann nicht hinzugefügt werden.|  
|0xC0029289|-1073573239|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODEINLIST|Interner Fehler. In XmlDiffPathSingleNodeList kann nur ein Knoten enthalten sein.|  
|0xC002928A|-1073573238|DTS_E_XMLTASK_INTERNALERRORMORETHANONENODELEFT|Interner Fehler. "%1" Knoten sind nach dem Patchen übrig, erwartet wurde 1.|  
|0xC002928B|-1073573237|DTS_E_XMLTASK_XSLTRESULTFILEISNOTXML|Die Datei/der Text, die bzw. der von XSLT erstellt wurde, ist kein gültiges XmlDocument-Objekt und kann deshalb nicht als Ergebnis des Vorgangs festgelegt werden: „%1“.|  
|0xC002928E|-1073573234|DTS_E_XMLTASK_FILEDOESNOTEXIST|Der "%1"-Verbindung ist keine Datei zugeordnet.|  
|0xC002928F|-1073573233|DTS_E_XMLTASK_XMLTEXTEMPTY|Die "%1"-Eigenschaft weist keinen XML-Quelltext auf. Der XML-Text ist ungültig, NULL oder eine leere Zeichenfolge.|  
|0xC0029290|-1073573232|DTS_E_XMLTASK_FILEALREADYEXISTS|Die Datei "%1" ist bereits vorhanden.|  
|0xC0029293|-1073573229|DTS_E_TRANSFERTASKS_SRCCONNECTIONREQUIRED|Eine Quellverbindung muss angegeben werden.|  
|0xC0029294|-1073573228|DTS_E_TRANSFERTASKS_DESTCONNECTIONREQUIRED|Eine Zielverbindung muss angegeben werden.|  
|0xC0029295|-1073573227|DTS_E_TRANSFERTASKS_CONNECTIONNOTFOUND|Die Verbindung "%1" wurde im Paket nicht gefunden.|  
|0xC0029296|-1073573226|DTS_E_TRANSFERTASKS_SERVERVERSIONNOTALLOWED|Die Verbindung "%1" gibt einen Computer mit SQL Server-Instanz an, deren Version für die Übertragung nicht unterstützt wird.  Nur Version 7, 2000 und 2005 werden unterstützt.|  
|0xC0029297|-1073573225|DTS_E_TRANSFERTASKS_SRCSERVERLESSEQUALDESTSERVER|Für die Quellverbindung "%1" muss ein Computer mit einer SQL Server-Instanz angegeben werden, deren Version älter oder gleich der Version der Zielverbindung "%2" ist.|  
|0xC0029298|-1073573224|DTS_E_TRANSFERTASKS_SRCDBREQUIRED|Eine Quelldatenbank muss angegeben werden.|  
|0xC0029299|-1073573223|DTS_E_TRANSFERTASKS_SRCDBMUSTEXIST|Die "%1"-Quelldatenbank muss auf dem Quellserver vorhanden sein.|  
|0xC002929A|-1073573222|DTS_E_TRANSFERTASKS_DESTDBREQUIRED|Eine Zieldatenbank muss angegeben werden.|  
|0xC002929B|-1073573221|DTS_E_TRANSFERTASKS_SRCDBANDDESTDBTHESAME|Die Quell- und Zieldatenbank dürfen nicht identisch sein.|  
|0xC002929C|-1073573220|DTS_E_TRANSFERDBTASK_FILENAMEREQUIRED|In den Übertragungsdateiinformationen %1 fehlt der Dateiname.|  
|0xC002929D|-1073573219|DTS_E_TRANSFERDBTASK_FOLDERREQUIRED|In den Übertragungsdateiinformationen %1 fehlt die Ordnerkomponente.|  
|0xC002929E|-1073573218|DTS_E_TRANSFERTASKS_NETSHAREREQUIRED|In den Übertragungsdateiinformationen %1 fehlt die Netzwerkfreigabekomponente.|  
|0xC002929F|-1073573217|DTS_E_TRANSFERTASKS_FILELISTSCOUNTMISMATCH|Die Anzahl von Quell- und Zielübertragungsdateien muss identisch sein.|  
|0xC00292A0|-1073573216|DTS_E_DOESNOTSUPPORTTRANSACTIONS|Das Eintragen in Transaktionen wird nicht unterstützt.|  
|0xC00292A1|-1073573215|DTS_E_TRANSFERDBTASK_OFFLINEERROR|Ausnahme während einer Offlinedatenbankübertragung: %1.|  
|0xC00292A2|-1073573214|DTS_E_TRANSFERDBTASK_NETSHAREDOESNOTEXIST|Die Netzwerkfreigabe "%1" wurde nicht gefunden.|  
|0xC00292A3|-1073573213|DTS_E_TRANSFERDBTASK_NETSHARENOACCESS|Der Zugriff auf die Netzwerkfreigabe "%1" war nicht möglich.  Fehler: %2.|  
|0xC00292A4|-1073573212|DTS_E_TRANSFERDBTASK_USERMUSTBEDBOORSYSADMIN|Der Benutzer "%1" muss Datenbankbesitzer oder Mitglied der Rolle Sysadmin für "%2" sein, um eine Onlinedatenbankübertragung auszuführen.|  
|0xC00292A5|-1073573211|DTS_E_TRANSFERDBTASK_USERMUSTBESYSADMIN|Der Benutzer "%1" muss Mitglied der Rolle Sysadmin für "%2" sein, um eine Offlinedatenbankübertragung auszuführen.|  
|0xC00292A6|-1073573210|DTS_E_TRANSFERDBTASK_FTCATALOGSOFFLINEYUKONONLY|Volltextkataloge können nur für eine Offlinedatenbankübertragung zwischen zwei Servern mit SQL Server 2005 eingeschlossen werden.|  
|0xC00292A7|-1073573209|DTS_E_TRANSFERDBTASK_NOOVERWRITEDB|Die "%1"-Datenbank ist bereits auf dem Zielserver "%2" vorhanden.|  
|0xC00292A8|-1073573208|DTS_E_TRANSFERDBTASK_MUSTHAVESOURCEFILES|Mindestens eine Quelldatei muss angegeben werden.|  
|0xC00292A9|-1073573207|DTS_E_TRANSFERDBTASKS_SRCFILENOTFOUND|Die Datei "%1" wurde in der "%2"-Quelldatenbank nicht gefunden.|  
|0xC00292B3|-1073573197|DTS_E_MSMQTASK_FIPS1402COMPLIANCE|Der angeforderte Vorgang ist in mit U.S. FIPS 140-2 kompatiblen Systemen unzulässig.|  
|0xC002F210|-1073548784|DTS_E_SQLTASK_ERROREXECUTINGTHEQUERY|Fehler beim Ausführen der Abfrage "%1": "%2". Mögliche Ursachen sind folgende: Probleme bei der Abfrage, nicht richtig festgelegte ResultSet-Eigenschaft, nicht richtig festgelegte Parameter oder nicht richtig hergestellte Verbindung.|  
|0xC002F300|-1073548544|DTS_E_TRANSFERSPTASK_ERRORREADINGSPNAMES|Fehler beim Lesen der Namen gespeicherter Prozeduren aus der XML-Datei.|  
|0xC002F301|-1073548543|DTS_E_TRANSFERSPTASK_INVALIDDATANODE|Ungültiger Datenknoten für den Task Gespeicherte Prozeduren übertragen.|  
|0xC002F302|-1073548542|DTS_E_TRANSFERTASKS_CONNECTIONTYPEISNOTSMOSERVER|Die Verbindung "%1" ist nicht vom Typ "SMOServer".|  
|0xC002F303|-1073548541|DTS_E_TRANSFERSPTASK_EXECUTIONFAILED|Fehler bei der Ausführung: "%1".|  
|0xC002F304|-1073548540|DTS_E_ERROROCCURREDWITHFOLLOWINGMESSAGE|Fehler mit folgender Fehlermeldung: "%1".|  
|0xC002F305|-1073548539|DTS_E_BITASK_EXECUTION_FAILED|Fehler beim Ausführen der Masseneinfügung.|  
|0xC002F306|-1073548538|DTS_E_FSTASK_INVALIDDESTPATH|Ungültiger Zielpfad.|  
|0xC002F307|-1073548537|DTS_E_FSTASK_CANTCREATEDIR|Das Verzeichnis kann nicht erstellt werden. Der Benutzer hat das Fehlschlagen des Tasks bei vorhandenem Verzeichnis festgelegt.|  
|0xC002F308|-1073548536|DTS_E_SQLTASK_ODBCNOSUPPORTTRANSACTION|Der Task weist die Transaktionsoption "Required" auf, und die "%1"-Verbindung ist vom Typ "ODBC". ODBC-Verbindungen unterstützen keine Transaktionen.|  
|0xC002F309|-1073548535|DTS_E_SQLTASK_ERRORASSIGINGVALUETOVAR|Fehler beim Zuweisen eines Werts zur "%1"-Variablen: "%2".|  
|0xC002F30A|-1073548534|DTS_E_FSTASK_SOURCEISEMPTY|Die Quelle ist leer.|  
|0xC002F30B|-1073548533|DTS_E_FSTASK_DESTINATIONISEMPTY|Das Ziel ist leer.|  
|0xC002F30C|-1073548532|DTS_E_FSTASK_FILEDIRNOTFOUND|Die Datei oder das Verzeichnis "%1" ist nicht vorhanden.|  
|0xC002F30D|-1073548531|DTS_E_FSTASK_VARSRCORDESTISEMPTY|Die "%1"-Variable wird als Quelle oder Ziel verwendet und ist leer.|  
|0xC002F30E|-1073548530|DTS_E_FSTASK_FILEDELETED|Die Datei oder das Verzeichnis "%1" wurde gelöscht.|  
|0xC002F30F|-1073548529|DTS_E_FSTASK_DIRECTORYDELETED|Das Verzeichnis "%1" wurde gelöscht.|  
|0xC002F310|-1073548528|DTS_E_WMIDRTASK_VARIABLETYPEISNOTOBJECT|Die "%1"-Variable muss vom Typ "Object" sein, damit ihr eine Datentabelle zugewiesen werden kann.|  
|0xC002F311|-1073548527|DTS_E_WMIDRTASK_VARIABLETYPEISNOTSTRING|Die "%1"-Variable weist nicht den String-Datentyp auf.|  
|0xC002F312|-1073548526|DTS_E_FTPTASK_CANNOTACQUIRECONNECTION|Fehler beim Abrufen der FTP-Verbindung. Überprüfen Sie, ob ein gültiger Verbindungstyp in "%1" angegeben ist.|  
|0xC002F313|-1073548525|DTS_E_FTPTASK_CONNECTIONNOTFOUND|Der FTP-Verbindungs-Manager "%1" wurde nicht gefunden.|  
|0xC002F314|-1073548524|DTS_E_FTPTASK_FILEUSAGETYPEERROR|Der Dateiverwendungstyp der "%1"-Verbindung muss für den "%3"-Vorgang "%2" lauten.|  
|0xC002F315|-1073548523|DTS_E_TRANSFERTASKS_SOURCECANTBESAMEASDESTINATION|Der Quellserver kann nicht mit dem Zielserver identisch sein.|  
|0xC002F316|-1073548522|DTS_E_ERRMSGTASK_EMPTYSOURCELIST|Es sind keine zu übertragenden Fehlermeldungen vorhanden.|  
|0xC002F317|-1073548521|DTS_E_ERRMSGTASK_DIFFERENTMESSAGEANDLANGUAGESIZES|Die Listen der Fehlermeldungen und der entsprechenden Sprachen sind unterschiedlich lang.|  
|0xC002F318|-1073548520|DTS_E_ERRMSGTASK_ERRORMESSAGEOUTOFRANGE|Die Fehlermeldungs-ID "%1" liegt außerhalb des zulässigen Bereichs für benutzerdefinierte Fehlermeldungen. IDs für benutzerdefinierte Fehlermeldungen liegen zwischen 50000 und 2147483647.|  
|0xC002F319|-1073548519|DTS_E_TRANSFERTASKS_NOTRANSACTIONSUPPORT|Dieser Task kann nicht an einer Transaktion teilnehmen.|  
|0xC002F320|-1073548512|DTS_E_ERRMSGTASK_FAILEDTOTRANSFERERRORMESSAGES|Fehler beim Übertragen einiger oder aller Fehlermeldungen.|  
|0xC002F321|-1073548511|DTS_E_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|Die Fehlermeldung "%1" ist bereits auf dem Zielserver vorhanden.|  
|0xC002F324|-1073548508|DTS_E_ERRMSGTASK_ERRORMESSAGECANTBEFOUND|Die Fehlermeldung „%1“ wurde nicht auf dem Quellserver gefunden.|  
|0xC002F325|-1073548507|DTS_E_TRANSFERTASKS_EXECUTIONFAILED|Fehler bei der Ausführung: „%1“.|  
|0xC002F327|-1073548505|DTS_E_JOBSTASK_FAILEDTOTRANSFERJOBS|Fehler beim Übertragen der Aufträge.|  
|0xC002F330|-1073548496|DTS_E_JOBSTASK_EMPTYSOURCELIST|Es sind keine zu übertragenden Aufträge vorhanden.|  
|0xC002F331|-1073548495|DTS_E_JOBSTASK_JOBEXISTSATDEST|Der Auftrag "%1" ist bereits auf dem Zielserver vorhanden.|  
|0xC002F334|-1073548492|DTS_E_JOBSTASK_JOBCANTBEFOUND|Der "%1"-Auftrag wurde nicht auf dem Quellserver gefunden.|  
|0xC002F337|-1073548489|DTS_E_LOGINSTASK_EMPTYLIST|Die Liste der zu übertragenden Anmeldenamen ist leer.|  
|0xC002F338|-1073548488|DTS_E_LOGINSTASK_CANTGETLOGINSNAMELIST|Die Liste der Anmeldenamen kann nicht vom Quellserver abgerufen werden.|  
|0xC002F340|-1073548480|DTS_E_LOGINSTASK_ERRORLOGINEXISTS|Der Anmeldename "%1" ist bereits auf dem Zielserver vorhanden.|  
|0xC002F342|-1073548478|DTS_E_LOGINSTASK_LOGINNOTFOUND|Der Anmeldename "%1" ist nicht an der Quelle vorhanden.|  
|0xC002F344|-1073548476|DTS_E_LOGINSTASK_FAILEDTOTRANSFERLOGINS|Fehler beim Übertragen einiger oder aller Anmeldenamen.|  
|0xC002F345|-1073548475|DTS_E_STOREDPROCSTASK_FAILEDTOTRANSFERSPS|Fehler beim Übertragen der gespeicherten Prozedur(en). Eine ausführlichere Fehlermeldung sollte ausgelöst worden sein.|  
|0xC002F346|-1073548474|DTS_E_STOREDPROCSTASK_STOREDPROCNOTFOUND|Die gespeicherte Prozedur "%1" wurde nicht an der Quelle gefunden.|  
|0xC002F349|-1073548471|DTS_E_STOREDPROCSTASK_ERRORSTOREDPROCEDUREEXISTS|Die gespeicherte Prozedur "%1" ist bereits auf dem Zielserver vorhanden.|  
|0xC002F350|-1073548464|DTS_E_STOREDPROCSTASK_EMPTYSOURCELIST|Es sind keine zu übertragenden gespeicherten Prozeduren vorhanden.|  
|0xC002F353|-1073548461|DTS_E_TRANSOBJECTSTASK_FAILEDTOTRANSFEROBJECTS|Fehler beim Übertragen der Objekte.|  
|0xC002F354|-1073548460|DTS_E_TRANSOBJECTSTASK_EMPTYLIST|Die Liste der zu übertragenden Objekte ist leer.|  
|0xC002F355|-1073548459|DTS_E_TRANSOBJECTSTASK_NOSPATSOURCE|Die gespeicherte Prozedur "%1" ist nicht an der Quelle vorhanden.|  
|0xC002F356|-1073548458|DTS_E_TRANSOBJECTSTASK_SPALREADYATDEST|Die gespeicherte Prozedur "%1" ist am Ziel bereits vorhanden.|  
|0xC002F357|-1073548457|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSPS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender gespeicherter Prozeduren: "%1".|  
|0xC002F359|-1073548455|DTS_E_TRANSOBJECTSTASK_NORULEATSOURCE|Die "%1"-Regel ist an der Quelle nicht vorhanden.|  
|0xC002F360|-1073548448|DTS_E_TRANSOBJECTSTASK_RULEALREADYATDEST|Die Regel "%1" ist bereits am Ziel vorhanden.|  
|0xC002F361|-1073548447|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGRULES|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Regeln: "%1".|  
|0xC002F363|-1073548445|DTS_E_TRANSOBJECTSTASK_NOTABLEATSOURCE|Die "%1"-Tabelle ist an der Quelle nicht vorhanden.|  
|0xC002F364|-1073548444|DTS_E_TRANSOBJECTSTASK_TABLEALREADYATDEST|Die Tabelle "%1" ist bereits am Ziel vorhanden.|  
|0xC002F365|-1073548443|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTABLES|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Tabellen: "%1".|  
|0xC002F367|-1073548441|DTS_E_TRANSOBJECTSTASK_NOVIEWATSOURCE|Die "%1"-Sicht ist an der Quelle nicht vorhanden.|  
|0xC002F368|-1073548440|DTS_E_TRANSOBJECTSTASK_VIEWALREADYATDEST|Die Sicht "%1" ist bereits am Ziel vorhanden.|  
|0xC002F369|-1073548439|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGVIEWS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Sichten: "%1".|  
|0xC002F371|-1073548431|DTS_E_TRANSOBJECTSTASK_NOUDFATSOURCE|Die benutzerdefinierte Funktion "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F372|-1073548430|DTS_E_TRANSOBJECTSTASK_UDFALREADYATDEST|Die benutzerdefinierte Funktion "%1" ist bereits am Ziel vorhanden.|  
|0xC002F373|-1073548429|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDFS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender benutzerdefinierter Funktionen: "%1".|  
|0xC002F375|-1073548427|DTS_E_TRANSOBJECTSTASK_NODEFAULTATSOURCE|Der Standardwert "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F376|-1073548426|DTS_E_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Der Standardwert "%1" ist bereits am Ziel vorhanden.|  
|0xC002F377|-1073548425|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGDEFAULTS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Standardwerte: "%1".|  
|0xC002F379|-1073548423|DTS_E_TRANSOBJECTSTASK_NOUDDTATSOURCE|Der benutzerdefinierte Datentyp "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F380|-1073548416|DTS_E_TRANSOBJECTSTASK_UDDTALREADYATDEST|Der benutzerdefinierte Datentyp "%1" ist bereits am Ziel vorhanden.|  
|0xC002F381|-1073548415|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUDDTS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender benutzerdefinierter Datentypen: "%1".|  
|0xC002F383|-1073548413|DTS_E_TRANSOBJECTSTASK_NOPFATSOURCE|Die "%1"-Partitionsfunktion ist an der Quelle nicht vorhanden.|  
|0xC002F384|-1073548412|DTS_E_TRANSOBJECTSTASK_PFALREADYATDEST|Die Partitionsfunktion "%1" ist bereits am Ziel vorhanden.|  
|0xC002F385|-1073548411|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPFS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Partitionsfunktionen: "%1".|  
|0xC002F387|-1073548409|DTS_E_TRANSOBJECTSTASK_NOPSATSOURCE|Das "%1"-Partitionsschema ist an der Quelle nicht vorhanden.|  
|0xC002F388|-1073548408|DTS_E_TRANSOBJECTSTASK_PSALREADYATDEST|Das Partitionsschema "%1" ist bereits am Ziel vorhanden.|  
|0xC002F389|-1073548407|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGPSS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Partitionsschemas: "%1".|  
|0xC002F391|-1073548399|DTS_E_TRANSOBJECTSTASK_NOSCHEMAATSOURCE|Das "%1"-Schema ist an der Quelle nicht vorhanden.|  
|0xC002F392|-1073548398|DTS_E_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Das Schema "%1" ist bereits am Ziel vorhanden.|  
|0xC002F393|-1073548397|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSCHEMAS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Schemas: "%1".|  
|0xC002F395|-1073548395|DTS_E_TRANSOBJECTSTASK_NOSQLASSEMBLYATSOURCE|Das SqlAssembly-Objekt "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F396|-1073548394|DTS_E_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|Das SqlAssembly-Objekt "%1" ist bereits am Ziel vorhanden.|  
|0xC002F397|-1073548393|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGSQLASSEMBLIES|Fehler beim Abrufen oder Festlegen der Liste zu übertragender SqlAssemblys-Objekte: "%1".|  
|0xC002F399|-1073548391|DTS_E_TRANSOBJECTSTASK_NOAGGREGATEATSOURCE|Das benutzerdefinierte Aggregat "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F400|-1073548288|DTS_E_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|Das benutzerdefinierte Aggregat "%1" ist bereits am Ziel vorhanden.|  
|0xC002F401|-1073548287|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGAGGREGATES|Fehler beim Abrufen oder Festlegen der Liste zu übertragender benutzerdefinierter Aggregate: "%1".|  
|0xC002F403|-1073548285|DTS_E_TRANSOBJECTSTASK_NOTYPEATSOURCE|Der benutzerdefinierte Typ "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F404|-1073548284|DTS_E_TRANSOBJECTSTASK_TYPEALREADYATDEST|Der benutzerdefinierte Typ "%1" ist bereits am Ziel vorhanden.|  
|0xC002F405|-1073548283|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGTYPES|Fehler beim Abrufen oder Festlegen der Liste zu übertragender benutzerdefinierter Typen: "%1".|  
|0xC002F407|-1073548281|DTS_E_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONATSOURCE|Das XmlSchemaCollection-Objekt "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F408|-1073548280|DTS_E_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|Das XmlSchemaCollection-Objekt "%1" ist bereits am Ziel vorhanden.|  
|0xC002F409|-1073548279|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGXMLSCHEMACOLLECTIONS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender XmlSchemaCollections-Objekte: "%1".|  
|0xC002F411|-1073548271|DTS_E_TRANSOBJECTSTASK_SUPPORTEDONYUKONONLY|Objekte vom Typ "%1" werden nur zwischen Servern mit SQL Server 2005 oder neueren Servern unterstützt.|  
|0xC002F413|-1073548269|DTS_E_LOGINSTASK_EMPTYDATABASELIST|Die Datenbankliste ist leer.|  
|0xC002F414|-1073548268|DTS_E_TRANSOBJECTSTASK_NOLOGINATSOURCE|Der Anmeldename "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F416|-1073548266|DTS_E_TRANSOBJECTSTASK_LOGINALREADYATDEST|Der Anmeldename "%1" ist bereits am Ziel vorhanden.|  
|0xC002F417|-1073548265|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGLOGINS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Anmeldenamen: "%1".|  
|0xC002F419|-1073548263|DTS_E_TRANSOBJECTSTASK_NOUSERATSOURCE|Der Benutzer "%1" ist an der Quelle nicht vorhanden.|  
|0xC002F41B|-1073548261|DTS_E_TRANSOBJECTSTASK_USERALREADYATDEST|Der Benutzer "%1" ist bereits am Ziel vorhanden.|  
|0xC002F41C|-1073548260|DTS_E_TRANSOBJECTSTASK_ERRORHANDLINGUSERS|Fehler beim Abrufen oder Festlegen der Liste zu übertragender Benutzer: "%1".|  
|0xC002F41F|-1073548257|DTS_E_BITASK_CANNOTRETAINCONNINTRANSACTION|Dieser Task kann keinen beibehaltenen Verbindungs-Manager in einer Transaktion aufweisen.|  
|0xC002F421|-1073548255|DTS_E_SQLTASKOUTPUTENCODINGNOTSUPPORTED|XML-Daten können aus SQL Server nicht als Unicode abgerufen werden, da der Anbieter die OUTPUTENCODING-Eigenschaft nicht unterstützt.|  
|0xC002F426|-1073548250|DTS_E_FTPTASK_FILECONNECTIONNOTFOUND|Der Dateiverbindungs-Manager "%2" für den FTP-Vorgang "%1" wurde nicht gefunden.|  
|0xC002F428|-1073548248|DTS_E_TRANSOBJECTSTASK_CANNOTDROPOBJECTS|Anmeldungen sind Objekte auf Serverebene und können nicht zuerst gelöscht werden, da der Quell- und Zielserver identisch sind. Wenn Objekte zuerst gelöscht werden, werden die Anmeldungen auch aus der Quelle entfernt.|  
|0xC002F429|-1073548247|DTS_E_SQLTASK_PARAMSIZEERROR|Der "%1"-Parameter darf nicht negativ sein. (-1) wird als Standardwert verwendet.|  
|0xC0040019|-1073479655|DTS_E_UNREGISTEREDPIPELINEXML_LOAD|Datenflussobjekte können nicht geladen werden. Stellen Sie sicher, dass Microsoft.SqlServer.PipelineXml.dll ordnungsgemäß registriert ist.|  
|0xC0040020|-1073479648|DTS_E_UNREGISTEREDPIPELINEXML_SAVE|Datenflussobjekte können nicht gespeichert werden. Stellen Sie sicher, dass Microsoft.SqlServer.PipelineXml.dll ordnungsgemäß registriert ist.|  
|0xC0040040|-1073479616|DTS_E_PIPELINE_SAVE|Fehler beim Speichern von Datenflussobjekten.|  
|0xC0040041|-1073479615|DTS_E_PIPELINE_LOAD|Fehler beim Laden von Datenflussobjekten.|  
|0xC0040042|-1073479614|DTS_E_SAVE_PERSTFORMAT|Fehler beim Speichern von Datenflussobjekten. Das angegebene Format wird nicht unterstützt.|  
|0xC0040043|-1073479613|DTS_E_LOAD_PERSTFORMAT|Fehler beim Laden von Datenflussobjekten. Das angegebene Format wird nicht unterstützt.|  
|0xC0040044|-1073479612|DTS_E_SETPERSIST_PROPEVENTS|Fehler beim Festlegen der XML-Persistenzereigniseigenschaft für die Datenflussobjekte.|  
|0xC0040045|-1073479611|DTS_E_SETPERSIST_XMLDOM|Fehler beim Festlegen der XML-DOM-Persistenzeigenschaft für die Datenflussobjekte.|  
|0xC0040046|-1073479610|DTS_E_SETPERSIST_XMLNODE|Fehler beim Festlegen der XML-ELEMENT-Persistenzeigenschaft für die Datenflussobjekte.|  
|0xC0040047|-1073479609|DTS_E_SETPERSISTPROP_FAILED|Fehler beim Festlegen der XML-Persistenzeigenschaften für die Datenflussobjekte.|  
|0xC0040048|-1073479608|DTS_E_NOCUSTOMPROPCOL|Fehler beim Abrufen der benutzerdefinierten Eigenschaftsauflistung für Datenflusskomponenten.|  
|0xC0047000|-1073451008|DTS_E_CYCLEINEXECUTIONTREE|Eine Ausführungsstruktur enthält eine Schleife.|  
|0xC0047001|-1073451007|DTS_E_DISCONNECTEDOBJECT|Das %1-Objekt "%2" (%3!d!) ist vom Layout getrennt.|  
|0xC0047002|-1073451006|DTS_E_INVALIDOBJECTID|Ungültige ID für das Layoutobjekt.|  
|0xC0047003|-1073451005|DTS_E_INPUTWITHOUTPATHS|Ein erforderliches Eingabeobjekt ist nicht mit einem Pfadobjekt verbunden.|  
|0xC0047005|-1073451003|DTS_E_INVALIDSYNCHRONOUSINPUT|%1 weist die ungültige synchrone Eingabe-ID %2!d! auf.|  
|0xC0047006|-1073451002|DTS_E_INVALIDOUTPUTLINEAGEID|%1 weist die Herkunfts-ID %2!d! anstelle von %3!d! auf.|  
|0xC0047008|-1073451000|DTS_E_DUPLICATENAMESINCOLLECTION|Das Paket enthält zwei Objekte mit den doppelten Namen "%1" und "%2".|  
|0xC0047009|-1073450999|DTS_E_INVALIDEXCLUSIONGROUP|"%1" und "%2" befinden sich in derselben Ausschlussgruppe, besitzen jedoch nicht dieselbe synchrone Eingabe.|  
|0xC004700A|-1073450998|DTS_E_DUPLICATELINEAGEIDSINCOLLECTION|Zwei Objekte in derselben Auflistung weisen die doppelte Herkunfts-ID %1!d! auf. Bei den Objekten handelt es sich um %2 und %3.|  
|0xC004700B|-1073450997|DTS_E_VALIDATIONFAILEDONLAYOUT|Fehler beim Überprüfen des Layouts.|  
|0xC004700C|-1073450996|DTS_E_VALIDATIONFAILEDONCOMPONENTS|Fehler beim Überprüfen von mindestens einer Komponente.|  
|0xC004700D|-1073450995|DTS_E_VALIDATIONFAILED|Fehler beim Überprüfen des Layouts und mindestens einer Komponente.|  
|0xC004700E|-1073450994|DTS_E_THREADSTARTUPFAILED|Fehler beim Starten des Datenflusstask-Moduls, weil mindestens ein erforderlicher Thread nicht erstellt werden konnte.|  
|0xC004700F|-1073450993|DTS_E_CANTGETMUTEX|Fehler beim Erstellen des Mutex durch einen Thread bei der Initialisierung.|  
|0xC0047010|-1073450992|DTS_E_CANTGETSEMAPHORE|Fehler beim Erstellen der Semaphore durch einen Thread bei der Initialisierung.|  
|0xC0047011|-1073450991|DTS_E_BUFFERFAILUREDETAILS|Das System meldet eine Arbeitsspeicherbelastung von %1!d!. Es sind %2 Bytes physischer Arbeitsspeicher mit %3 freien Bytes verfügbar. Es sind %4 Bytes virtueller Arbeitsspeicher mit %5 freien Bytes verfügbar. Die Auslagerungsdatei verfügt über %6 Bytes, davon %7 freie Bytes.|  
|0xC0047012|-1073450990|DTS_E_BUFFERALLOCFAILED|Fehler bei einem Puffer beim Zuordnen von %1!d! Bytes ist.|  
|0xC0047013|-1073450989|DTS_E_CANTCREATEBUFFERMANAGER|Der Puffer-Manager konnte nicht erstellt werden.|  
|0xC0047015|-1073450987|DTS_E_BUFFERBADSIZE|Der Puffertyp %1!d! weist eine Größe von %2!I64d Bytes ist.|  
|0xC0047016|-1073450986|DTS_E_DANGLINGWITHPATH|%1 ist als verbleibend gekennzeichnet, weist jedoch einen angefügten Pfad auf.|  
|0xC0047017|-1073450985|DTS_E_INDIVIDUALVALIDATIONFAILED|Fehler beim Überprüfen von %1. Fehlercode: 0x%2!8.8X!.|  
|0xC0047018|-1073450984|DTS_E_INDIVIDUALPOSTEXECUTEFAILED|Fehler in der Phase nach der Ausführung für %1. Fehlercode: 0x%2!8.8X!.|  
|0xC0047019|-1073450983|DTS_E_INDIVIDUALPREPAREFAILED|Fehler in der Vorbereitungsphase für %1. Fehlercode: 0x%2!8.8X!.|  
|0xC004701A|-1073450982|DTS_E_INDIVIDUALPREEXECUTEFAILED|Fehler in der Phase vor der Ausführung für %1. Fehlercode: 0x%2!8.8X!.|  
|0xC004701B|-1073450981|DTS_E_INDIVIDUALCLEANUPFAILED|Fehler in der Cleanupphase für %1. Fehlercode: 0x%2!8.8X!.|  
|0xC004701C|-1073450980|DTS_E_INVALIDINPUTLINEAGEID|%1 weist die Herkunfts-ID% 2! d! auf, die noch nicht im Datenflusstask verwendet wurde.|  
|0xC004701E|-1073450978|DTS_E_EXECUTIONTREECYCLE|%1 kann nicht mit %2 verbunden werden, weil eine Schleife erstellt würde.|  
|0xC004701F|-1073450977|DTS_E_CANTCOMPARE|Der Datentyp "%1" kann nicht verglichen werden. Das Vergleichen dieses Datentyps wird nicht unterstützt. Er kann deshalb nicht sortiert oder als Schlüssel verwendet werden.|  
|0xC0047020|-1073450976|DTS_E_REFUSEDFORSHUTDOWN|Dieser Thread wurde beendet und nimmt keine Puffer für die Eingabe an.|  
|0xC0047021|-1073450975|DTS_E_THREADFAILED|SSIS-Fehlercode DTS_E_THREADFAILED.  Der Thread "%1" wurde mit dem Fehlercode 0x%2!8.8X! beendet.  Möglicherweise wurden bereits Fehlermeldungen veröffentlicht, die weitere Informationen zum Beenden des Threads beinhalten.|  
|0xC0047022|-1073450974|DTS_E_PROCESSINPUTFAILED|SSIS-Fehlercode DTS_E_PROCESSINPUTFAILED.  Fehler bei der ProcessInput-Methode in der Komponente "%1" (%2!d!) mit dem Fehlercode 0x%3!8.8X! beim Verarbeiten der Eingabe "% 4" (% 5! d!). Die identifizierte Komponente hat einen Fehler von der ProcessInput-Methode zurückgegeben. Der Fehler ist komponentenspezifisch. Es handelt sich jedoch um einen schwerwiegenden Fehler, sodass die Ausführung des Datenflusstasks unterbrochen wird.  Möglicherweise wurden bereits Fehlermeldungen veröffentlicht, die weitere Fehlerinformationen beinhalten.|  
|0xC0047023|-1073450973|DTS_E_CANTREALIZEVIRTUALBUFFERS|Eine Gruppe von virtuellen Puffern wurde nicht gefunden.|  
|0xC0047024|-1073450972|DTS_E_PIPELINETOOCOMPLEX|Für die Pipeline sind %1!d! Threads erforderlich. Der Wert überschreitet die Systemgrenze von %2!d!. Die Pipeline benötigt in dieser Konfiguration zu viele Threads. Es sind zu viele asynchrone Ausgaben vorhanden, oder für die EngineThreads-Eigenschaft ist ein zu hoher Wert festgelegt. Teilen Sie die Pipeline in mehrere Pakete auf, oder reduzieren Sie den Wert der EngineThreads-Eigenschaft.|  
|0xC0047028|-1073450968|DTS_E_SCHEDULERCOULDNOTCOUNTSOURCES|Die Datenfluss-Modulplanung kann die Anzahl von Quellen im Layout nicht abrufen.|  
|0xC0047029|-1073450967|DTS_E_SCHEDULERCOULDNOTCOUNTDESTINATIONS|Die Datenfluss-Modulplanung kann die Anzahl von Zielen im Layout nicht abrufen.|  
|0xC004702A|-1073450966|DTS_E_COMPONENTVIEWISUNAVAILABLE|Die Komponentensicht ist nicht verfügbar. Stellen Sie sicher, dass die Komponentensicht erstellt wurde.|  
|0xC004702B|-1073450965|DTS_E_INCORRECTCOMPONENTVIEWID|Die Komponentensicht-ID ist falsch. Die Komponentensicht ist möglicherweise nicht mehr synchronisiert. Geben Sie die Komponentensicht frei, und erstellen Sie sie neu.|  
|0xC004702C|-1073450964|DTS_E_BUFFERNOTLOCKED|Dieser Puffer ist nicht gesperrt und kann nicht manipuliert werden.|  
|0xC004702D|-1073450963|DTS_E_CANTBUILDBUFFERTYPE|Der Datenflusstask kann keinen Arbeitsspeicher belegen, um eine Pufferdefinition zu erstellen. Die Pufferdefinition wies %1!d! Spalten auf.|  
|0xC004702E|-1073450962|DTS_E_CANTREGISTERBUFFERTYPE|Der Datenflusstask kann einen Puffertyp nicht registrieren. Der Typ wies %1!d! Spalten auf und war für die Ausführungsstruktur %2!d! bestimmt.|  
|0xC004702F|-1073450961|DTS_E_INVALIDUSESDISPOSITIONSVALUE|Der ursprüngliche Wert der UsesDispositions-Eigenschaft kann nicht geändert werden. Dieses Problem tritt auf, wenn der XML-Code bearbeitet und der UsesDispositions-Wert geändert wird. Dieser Wert wird von der Komponente festgelegt, wenn diese dem Paket hinzugefügt wird, und darf nicht geändert werden.|  
|0xC0047030|-1073450960|DTS_E_THREADFAILEDINITIALIZE|Der Datenflusstask konnte einen erforderlichen Thread nicht initialisieren und kann nicht mit der Ausführung beginnen. Der Thread hatte zuvor einen speziellen Fehler gemeldet.|  
|0xC0047031|-1073450959|DTS_E_THREADFAILEDCREATE|Der Datenflusstask konnte einen erforderlichen Thread nicht erstellen und kann nicht ausgeführt werden. Dieser Fehler tritt gewöhnlich auf, wenn nicht genügend Arbeitsspeicher verfügbar ist.|  
|0xC0047032|-1073450958|DTS_E_EXECUTIONTREECYCLEADDINGSYNCHRONOUSINPUT|Die synchrone Eingabe von "%1" kann nicht auf "%2" festgelegt werden, weil dadurch eine Schleife erstellt würde.|  
|0xC0047033|-1073450957|DTS_E_INVALIDCUSTOMPROPERTYNAME|Die benutzerdefinierte Eigenschaft "%1" ist ungültig, weil eine Systemeigenschaft mit diesem Namen vorhanden ist. Eine benutzerdefinierte Eigenschaft kann im gleichen Objekt nicht denselben Namen wie eine Systemeigenschaft aufweisen.|  
|0xC0047035|-1073450955|DTS_E_BUFFERLOCKUNDERFLOW|Die Sperre des Puffers war bereits aufgehoben.|  
|0xC0047036|-1073450954|DTS_E_INDIVIDUALCACHEINTERFACESFAILED|Fehler beim Initialisieren von %1 (Fehlercode: 0x%2!8.8X!).|  
|0xC0047037|-1073450953|DTS_E_INDIVIDUALRELEASEINTERFACESFAILED|Fehler bei %1 beim Herunterfahren (Fehlercode: 0x%2!8.8X!). Die Schnittstellen einer Komponente konnten nicht freigegeben werden.|  
|0xC0047038|-1073450952|DTS_E_PRIMEOUTPUTFAILED|SSIS-Fehlercode DTS_E_PRIMEOUTPUTFAILED.  Die PrimeOutput-Methode in %1 hat den Fehlercode 0x%2!8.8X! zurückgegeben.  Die Komponente gab einen Fehlercode zurück, als das Pipelinemodul PrimeOutput() aufgerufen hat. Die Bedeutung des Fehlercodes wird von der Komponente definiert. Der Fehler ist jedoch schwerwiegend, und die Ausführung der Pipeline wurde beendet.  Möglicherweise wurden bereits Fehlermeldungen veröffentlicht, die weitere Fehlerinformationen beinhalten.|  
|0xC0047039|-1073450951|DTS_E_THREADCANCELLED|SSIS-Fehlercode DTS_E_THREADCANCELLED.  Der Thread "%1" hat ein Signal zum Herunterfahren erhalten und wird beendet. Der Benutzer hat das Herunterfahren angefordert, oder ein Fehler in einem anderen Thread hat dazu geführt, dass die Pipeline heruntergefahren wird.  Möglicherweise wurden bereits Fehlermeldungen veröffentlicht, die weitere Informationen zum Abbruch des Threads beinhalten.|  
|0xC004703A|-1073450950|DTS_E_DISTRIBUTORCANTSETPROPERTY|Der Verteiler für den Thread "%1" konnte die "%2"-Eigenschaft in der "%3"-Komponente aufgrund des Fehlers 0x%8.8X nicht initialisieren. Der Verteiler konnte die Eigenschaft der Komponente nicht initialisieren und kann nicht weiter ausgeführt werden.|  
|0xC004703B|-1073450949|DTS_E_CANTREGISTERVIEWBUFFERTYPE|Der Datenflusstask kann einen Sichtpuffertyp nicht registrieren. Der Typ wies %1!d! Spalten auf und war für die Eingabe-ID %2!d! bestimmt.|  
|0xC004703F|-1073450945|DTS_E_CANTCREATEEXECUTIONTREE|Zum Erstellen einer Ausführungsstruktur ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0047040|-1073450944|DTS_E_CANTINSERTINTOHASHTABLE|Zum Einfügen eines Objekts in die Hashtabelle ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0047041|-1073450943|DTS_E_OBJECTNOTINHASHTABLE|Das Objekt ist nicht in der Hashtabelle enthalten.|  
|0xC0047043|-1073450941|DTS_E_CANTCREATECOMPONENTVIEW|Eine Komponentensicht kann nicht erstellt werden, weil bereits eine andere Komponentensicht vorhanden ist. Es kann jeweils nur eine Komponentensicht vorhanden sein.|  
|0xC0047046|-1073450938|DTS_E_LAYOUTCANTSETUSAGETYPE|An der Eingabe "%1" (%2!d!) enthält die Auflistung für die virtuelle Eingabespalte keine virtuelle Eingabespalte mit der Herkunfts-ID %3!d!.|  
|0xC0047047|-1073450937|DTS_E_WRONGOBJECTTYPE|Das angeforderte Objekt weist den falschen Objekttyp auf.|  
|0xC0047048|-1073450936|DTS_E_CANTCREATESPOOLFILE|Der Puffer-Manager kann in keinem Pfad der BufferTempStoragePath-Eigenschaft eine temporäre Speicherdatei erstellen. Der Dateiename ist falsch, oder die entsprechende Berechtigung fehlt, oder der Speicherplatz an den Pfaden ist voll.|  
|0xC0047049|-1073450935|DTS_E_SEEKFAILED|Der Puffer-Manager konnte nicht bis zum Offset %1!d! in der Datei "%2" suchen. Die Datei ist beschädigt.|  
|0xC004704A|-1073450934|DTS_E_EXTENDFAILED|Der Puffer-Manager kann die Datei "%1" nicht auf die Länge von %2!lu! Bytes ist.  Es war nicht genügend Speicherplatz vorhanden.|  
|0xC004704B|-1073450933|DTS_E_FILEWRITEFAILED|The buffer manager cannot write %1!d! Bytes können nicht in die Datei "%2" geschrieben werden. Der Speicherplatz oder das Kontingent ist nicht ausreichend.|  
|0xC004704C|-1073450932|DTS_E_FILEREADFAILED|Der Puffer-Manager kann %1!d! aus der Datei "%2". Die Datei ist beschädigt.|  
|0xC004704D|-1073450931|DTS_E_VIRTUALNOTSEQUENTIAL|Die Puffer-ID %1!d! unterstützt andere virtuelle Puffer und kann nicht in den sequenziellen Modus versetzt werden. IDTSBuffer100.SetSequentialMode in einem Puffer aufgerufen, der virtuelle Puffer unterstützt.|  
|0xC004704E|-1073450930|DTS_E_BUFFERISREADONLY|Dieser Vorgang konnte nicht ausgeführt werden, weil sich der Puffer im schreibgeschützten Modus befindet. Ein schreibgeschützter Puffer kann nicht geändert werden.|  
|0xC004704F|-1073450929|DTS_E_EXECUTIONTREECYCLESETTINGID|Die ID %1 kann nicht auf %2!d! festgelegt werden, weil dadurch eine Schleife erstellt würde.|  
|0xC0047050|-1073450928|DTS_E_NOMOREBUFFERTYPES|Der Puffer-Manager konnte die Tabelle mit den Puffertypen nicht erweitern, weil nicht genügend Arbeitsspeicher verfügbar war. Dieser Fehler tritt auf, weil nicht genügend Speicherplatz vorhanden ist.|  
|0xC0047051|-1073450927|DTS_E_CANTCREATENEWTYPE|Fehler beim Erstellen eines neuen Puffertyps durch den Puffer-Manager.|  
|0xC0047053|-1073450925|DTS_E_SCHEDULERBADTREE|Fehler beim Abrufen der Ausführungsstruktur mit dem Index %1!d! aus dem Layout nicht aus dem Layout abrufen. Die Planung hat mehr Ausführungsstrukturen erhalten, als tatsächlich vorhanden sind.|  
|0xC0047056|-1073450922|DTS_E_CANTCREATEPRIMEOUTPUTBUFFER|Fehler beim Erstellen des Puffers zum Abrufen von PrimeOutput für die Ausgabe "%3" (%4!d!) in der Komponente "%1" (%2!d!) durch den Datenflusstask. Dieser Fehler tritt gewöhnlich auf, wenn nicht genügend Arbeitsspeicher verfügbar ist.|  
|0xC0047057|-1073450921|DTS_E_SCHEDULERTHREADMEMORY|Fehler beim Erstellen eines Threadobjekts durch die Datenfluss-Modulplanung. Dieser Fehler tritt auf, weil nicht genügend Speicherplatz vorhanden ist.|  
|0xC004705A|-1073450918|DTS_E_SCHEDULEROBJECT|Die Datenfluss-Modulplanung kann das Objekt mit der ID %1!d! nicht aus dem Layout abrufen. Die Datenfluss-Modulplanung fand zuvor ein Objekt, das nun nicht mehr verfügbar ist.|  
|0xC004705B|-1073450917|DTS_E_PREPARETREENODEFAILED|Fehler beim Vorbereiten des Puffers für den Ausführungsstrukturknoten beginnend an der Ausgabe "%1" (%2!d!).|  
|0xC004705C|-1073450916|DTS_E_CANTCREATEVIRTUALBUFFER|Der Datenflusstask kann einen virtuellen Puffer nicht zur Vorbereitung für die Ausführung erstellen.|  
|0xC004705E|-1073450914|DTS_E_NOMOREIDS|Die maximale Anzahl an IDs wurde erreicht. Es sind keine weiteren IDs verfügbar, die Objekten zugewiesen werden können.|  
|0xC004705F|-1073450913|DTS_E_ALREADYATTACHED|%1 ist bereits angefügt und kann nicht erneut angefügt werden.  Trennen Sie das Objekt, und versuchen Sie es noch einmal.|  
|0xC0047060|-1073450912|DTS_E_OUTPUTCOLUMNNAMECONFLICT|Der Spaltenname "%1" in der Ausgabe "%2" kann nicht verwendet werden, weil er in Konflikt mit einer gleichnamigen Spalte in der synchronen Eingabe "%3" steht.|  
|0xC0047061|-1073450911|DTS_E_EOFANNOUNCEMENTFAILED|Der Datenflusstask kann keinen Puffer erstellen, um das Ende des Rowsets zu kennzeichnen.|  
|0xC0047062|-1073450910|DTS_E_USERCOMPONENTEXCEPTION|Eine verwaltete Benutzerkomponente hat die Ausnahme "%1" zurückgegeben.|  
|0xC0047063|-1073450909|DTS_E_SCHEDULERMEMORY|Die Datenfluss-Modulplanung kann den Ausführungsstrukturen nicht genügend Arbeitsspeicher zuordnen. Schon vor Ausführungsbeginn war auf dem System wenig Arbeitsspeicher verfügbar.|  
|0xC0047064|-1073450908|DTS_E_BUFFERNOOBJECTMEMORY|Das Pufferobjekt konnte nicht erstellt werden, weil nicht genügend Arbeitsspeicher verfügbar war.|  
|0xC0047065|-1073450907|DTS_E_BUFFERNOMAPMEMORY|Die Herkunfts-IDs eines Puffers können nicht DTP_HCOL-Indizes zugeordnet werden, weil nicht genügend Arbeitsspeicher verfügbar ist.|  
|0xC0047066|-1073450906|DTS_E_INDIVIDUALPUTVARIABLESFAILED|„%1! s!“ kann die Variablenauflistung nicht zwischenspeichern und gab den Fehlercode „0x%2!8.8X“ zurück.|  
|0xC0047067|-1073450905|DTS_E_INDIVIDUALPUTCOMPONENTMETADATAFAILED|Fehler beim Zwischenspeichern des Komponentenmetadatenobjekts durch "%1". Fehlercode: 0x%2!8.8X!.|  
|0xC0047068|-1073450904|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITION|"%1" weist ein SortKeyPosition-Objekt ungleich 0 auf, dessen Wert (%2!ld!) aber zu hoch ist. Es muss kleiner oder gleich der Spaltenanzahl sein.|  
|0xC004706A|-1073450902|DTS_E_SORTEDOUTPUTHASINVALIDSORTKEYPOSITIONS|Die IsSorted-Eigenschaft von %1 ist auf TRUE festgelegt, aber die absoluten Werte der SortKeyPositions-Ausgabespalte ungleich 0 (null) bilden keine monoton ansteigende Sequenz, die bei 1 beginnt.|  
|0xC004706B|-1073450901|DTS_E_INDIVIDUALVALIDATIONSTATUSFAILED|Fehler beim Überprüfen von "%1". Überprüfungsstatus: "%2".|  
|0xC004706C|-1073450900|DTS_E_CANTCREATECOMPONENT|Die Komponente „%1!s!“ konnte nicht erstellt werden. Fehlercode: 0x%2!8.8X! „%3!s!“. Stellen Sie sicher, dass die Komponente ordnungsgemäß registriert ist.|  
|0xC004706D|-1073450899|DTS_E_COMPONENTNOTREGISTERED|Das Modul, das "%1" enthält, ist nicht registriert oder nicht ordnungsgemäß installiert.|  
|0xC004706E|-1073450898|DTS_E_COMPONENTNOTFOUND|Das Modul, das "%1" enthält, wurde nicht gefunden, obwohl es registriert ist.|  
|0xC004706F|-1073450897|DTS_E_BINARYCODENOTFOUND|Für die Skriptkomponente ist die Vorkompilierung des Skripts konfiguriert, aber es wurde kein binärer Code gefunden. Öffnen Sie die IDE im Skriptkomponenten-Editor, indem Sie auf die Schaltfläche 'Skript entwerfen' klicken, um binären Code zu generieren.|  
|0xC0047070|-1073450896|DTS_E_CANTCREATEBLOBFILE|Der Puffer-Manager kann keine Datei zum Spoolen eines umfangreichen Objekts in den Verzeichnissen erstellen, die in der BLOBTempStoragePath-Eigenschaft genannt werden.  Ein falscher Dateiname wurde angegeben, oder die entsprechenden Berechtigungen fehlen, oder der Speicherplatz an den Pfaden ist voll.|  
|0xC0047071|-1073450895|DTS_E_SYNCHRONOUSIDMISMATCH|Die SynchronousInputID-Eigenschaft in "%1" lautete "%2!d!", aber "%3!d!" wurde erwartet.|  
|0xC0047072|-1073450894|DTS_E_OBJECTIDNOTFOUND|Ein Objekt mit der ID %1!d! ist nicht vorhanden.|  
|0xC0047073|-1073450893|DTS_E_OBJECTIDLOOKUPFAILED|Ein Objekt mit der ID %1!d! wurde aufgrund des Fehlercodes 0x%2!8.8X! nicht gefunden.|  
|0xC0047074|-1073450892|DTS_E_INVALIDCODEPAGE|Die Codepage %1!d!, die in der Ausgabespalte „%2“ (%3!d!) angegeben ist, ist ungültig. Wählen Sie eine andere Codepage für die "%2"-Ausgabespalte aus.|  
|0xC0047075|-1073450891|DTS_E_INDIVIDUALPUTEVENTINFOSFAILED|Die EventInfos-Auflistung konnte von "%1" nicht zwischengespeichert werden. Fehlercode: 0x%2!8.8X!.|  
|0xC0047077|-1073450889|DTS_E_DUPLICATEOUTPUTCOLUMNNAMES|Der Name für "%1" ist bereits vorhanden.  Alle Namen müssen eindeutig sein.|  
|0xC0047078|-1073450888|DTS_E_NOOUTPUTCOLUMNFORINPUTCOLUMN|Der "%1"-Eingabespalte (%2!d!) ist keine Ausgabespalte zugeordnet.|  
|0xC0047079|-1073450887|DTS_E_EXCLGRPNOSYNCINP|"%1" weist einen virtuellen Puffer auf, der von einer Stammquelle ausgeht. Eine Ausschlussgruppe ungleich 0 (null) mit einer synchronen Eingabe gleich 0 (null) ist vorhanden.|  
|0xC004707A|-1073450886|DTS_E_ERROROUTCANTBEONSYNCNONEXCLUSIVEOUTPUT|"%1" kann keine Fehlerausgabe sein, weil Fehlerausgaben in synchronen, nichtexklusiven Ausgaben unzulässig sind.|  
|0xC004707B|-1073450885|DTS_E_EXPREVALDIVBYZERO|Fehler aufgrund einer Division durch 0 (null). Der rechte Operand im Ausdruck "%1" ergibt 0 (null).|  
|0xC004707C|-1073450884|DTS_E_EXPREVALLITERALOVERFLOW|Das Literal "%1" ist zu groß für den Typ %2. Das Literal führt zu einem Überlauf der zulässigen Größe für diesen Typ.|  
|0xC004707D|-1073450883|DTS_E_EXPREVALBINARYOPNUMERICOVERFLOW|Das Ergebnis der binären Operation "%1" für die Datentypen %2 und %3 überschreitet die maximal zulässige Größe für numerische Datentypen. Eine implizite Typumwandlung der Operandentypen in ein numerisches (DT_NUMERIC) Ergebnis war ohne Verlust der Genauigkeit oder der Dezimalstellen nicht möglich. Für diesen Vorgang müssen einer oder beide der Operanden explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC004707E|-1073450882|DTS_E_EXPREVALBINARYOPOVERFLOW|Das Ergebnis der binären Operation "%1" führt zu einem Überlauf der maximal zulässigen Größe für den Ergebnisdatentyp "%2". Das Ergebnis der Operation führt zu einem Überlauf der zulässigen Größe für diesen Ergebnistyp.|  
|0xC004707F|-1073450881|DTS_E_EXPREVALFUNCTIONOVERFLOW|Das Ergebnis des Funktionsaufrufs "%1" ist für den Typ "%2" zu groß. Das Ergebnis des Funktionsaufrufs führt zu einem Überlauf der zulässigen Größe für diesen Operandentyp. Möglicherweise ist eine explizite Umwandlung in einen größeren Typ erforderlich.|  
|0xC0047080|-1073450880|DTS_E_EXPREVALBINARYTYPEMISMATCH|Der Datentypen "%1" und "%2" sind für den binären Operator "%3" inkompatibel. Die Operandentypen konnten nicht implizit in für den Vorgang kompatible Typen umgewandelt werden. Für diesen Vorgang müssen einer oder beide der Operanden explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC0047081|-1073450879|DTS_E_EXPREVALUNSUPPORTEDBINARYTYPE|Der "%1"-Datentyp kann nicht mit dem binären Operator "%2" verwendet werden. Der Datentyp eines oder beider Operanden wird für den Vorgang nicht unterstützt. Für diesen Vorgang müssen einer oder beide der Operanden explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC0047082|-1073450878|DTS_E_EXPREVALBINARYSIGNMISMATCH|Nicht übereinstimmende Vorzeichen beim bitweisen binären Operator "%1" bei der Operation "%2". Beide Operanden für diesen Operator müssen entweder positiv oder negativ sein.|  
|0xC0047083|-1073450877|DTS_E_EXPREVALBINARYOPERATIONFAILED|Fehler bei der binären Operation "%1" (Fehlercode: 0x%2!8.8X!). Ein interner Fehler ist aufgetreten, oder es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0047084|-1073450876|DTS_E_EXPREVALBINARYOPERATIONSETTYPEFAILED|Fehler beim Festlegen des Ergebnistyps der binären Operation "%1" (Fehlercode: 0x%2!8.8X!).|  
|0xC0047085|-1073450875|DTS_E_EXPREVALSTRINGCOMPARISONFAILED|Fehler beim Vergleichen von "%1" mit der Zeichenfolge "%2".|  
|0xC0047086|-1073450874|DTS_E_EXPREVALUNSUPPORTEDUNNARYTYPE|Der "%1"-Datentyp kann nicht mit dem unären Operator "%2" verwendet werden. Dieser Operandentyp wird für diesen Vorgang nicht unterstützt. Für diesen Vorgang muss der Operand explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC0047087|-1073450873|DTS_E_EXPREVALUNARYOPERATIONFAILED|Fehler bei der unären Operation "%1" (Fehlercode: 0x%2!8.8X!). Ein interner Fehler ist aufgetreten, oder es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0047088|-1073450872|DTS_E_EXPREVALUNARYOPERATIONSETTYPEFAILED|Fehler beim Festlegen des Ergebnistyps der unären Operation "%1" (Fehlercode: 0x%2!8.8X!).|  
|0xC0047089|-1073450871|DTS_E_EXPREVALPARAMTYPEMISMATCH|Der "%2"-Datentyp wird von der "%1"-Funktion für den Parameter mit der Nummer %3!d! nicht unterstützt. Der Parametertyp konnte nicht implizit in einen für die Funktion kompatiblen Datentyp umgewandelt werden. Für diesen Vorgang muss der Operand explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC004708A|-1073450870|DTS_E_EXPREVALINVALIDFUNCTION|Die "%1"-Funktion wurde nicht erkannt. Der Funktionsname ist falsch oder nicht vorhanden.|  
|0xC004708B|-1073450869|DTS_E_EXPREVALFNSUBSTRINGINVALIDLENGTH|Die für die Funktion ist für die %2-Funktion ungültig. Der length-Parameter darf nicht negativ sein. Ändern Sie den Wert für den length-Parameter in 0 (null) oder einen positiven Wert.|  
|0xC004708C|-1073450868|DTS_E_EXPREVALFNSUBSTRINGINVALIDSTARTINDEX|Der Startindex "%1!d!" ist für die %2-Funktion ungültig. Der Startindexwert muss eine ganze Zahl größer als 0 (null) sein. Der Startindex ist einsbasiert, nicht nullbasiert.|  
|0xC004708E|-1073450866|DTS_E_EXPREVALCHARMAPPINGFAILED|Die "%1"-Funktion kann die Zeichenzuordnung für die Zeichenfolge "%2" nicht ausführen.|  
|0xC004708F|-1073450865|DTS_E_EXPREVALINVALIDDATEPART|"%1" ist kein gültiger Datumsteil für die "%2"-Funktion.|  
|0xC0047090|-1073450864|DTS_E_EXPREVALINVALIDNULLPARAM|Der Parameter mit der Nummer %1!d! der NULL-Funktion mit dem %2-Datentyp ist ungültig. Die Parameter von NULL() müssen statisch sein und dürfen keine dynamischen Elemente, wie z. B. Eingabespalten, enthalten.|  
|0xC0047091|-1073450863|DTS_E_EXPREVALINVALIDNULLPARAMTYPE|Der Parameter mit der Nummer %1!d! der NULL-Funktion mit dem %2-Datentyp ist keine ganze Zahl. Parameter von NULL() müssen eine ganze Zahl oder von einem Datentyp sein, der in eine ganze Zahl konvertiert werden kann.|  
|0xC0047092|-1073450862|DTS_E_EXPREVALFUNCTIONPARAMNOTSTATIC|Der Parameter mit der Nummer %1!d! der %2-Funktion ist nicht statisch. Dieser Parameter muss statisch sein und darf keine dynamischen Elemente, wie z. B. Eingabespalten, enthalten.|  
|0xC0047093|-1073450861|DTS_E_EXPREVALINVALIDCASTPARAM|Der Parameter mit der Nummer %1!d! der Umwandlung in den %2-Datentyp ist ungültig. Die Parameter von Umwandlungsoperatoren müssen statisch sein und dürfen keine dynamischen Elemente, wie z. B. Eingabespalten, enthalten.|  
|0xC0047094|-1073450860|DTS_E_EXPREVALINVALIDCASTPARAMTYPE|Der Parameter mit der Nummer %1!d! der Umwandlung in den %2-Datentyp ist keine ganze Zahl. Parameter von Umwandlungsoperatoren müssen einer ganzen Zahl entsprechen oder einen Datentyp aufweisen, der in eine ganze Zahl konvertiert werden kann.|  
|0xC0047095|-1073450859|DTS_E_EXPREVALINVALIDCAST|Der Ausdruck "%1" kann nicht vom "%2"-Datentyp in den "%3"-Datentyp umgewandelt werden. Die angeforderte Umwandlung wird nicht unterstützt.|  
|0xC0047096|-1073450858|DTS_E_EXPREVALINVALIDTOKEN|Fehler beim Analysieren des Ausdrucks "%1".  Das "%2"-Token in Zeile Nummer "%3", Zeichen Nummer "%4", wurde nicht erkannt. Der Ausdruck kann nicht analysiert werden, weil er an der angegebenen Position ungültige Elemente enthält.|  
|0xC0047097|-1073450857|DTS_E_EXPREVALUNEXPECTEDPARSEERROR|Fehler beim Analysieren des Ausdrucks "%1". Der Ausdruck konnte aus einem unbekannten Grund nicht analysiert werden.|  
|0xC0047098|-1073450856|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONWITHHR|Fehler beim Analysieren des Ausdrucks "%1" (Fehlercode: 0x%2!8.8X!). Der Ausdruck kann nicht analysiert werden. Er enthält möglicherweise ungültige Elemente oder ist fehlerhaft. Möglicherweise ist auch nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0047099|-1073450855|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSION|Der Ausdruck "%1" ist ungültig und kann nicht analysiert werden. Der Ausdruck enthält möglicherweise ungültige Elemente oder ist fehlerhaft.|  
|0xC004709A|-1073450854|DTS_E_EXPREVALEXPRESSIONEMPTY|Ein Ausdruck zum Berechnen war nicht vorhanden. Es wurde versucht, einen leeren Ausdruck zu berechnen oder eine Zeichenfolge dafür abzurufen.|  
|0xC004709B|-1073450853|DTS_E_EXPREVALCOMPUTEFAILED|Fehler beim Berechnen des Ausdrucks "%1" (Fehlercode: 0x%2!8.8X!).|  
|0xC004709C|-1073450852|DTS_E_EXPREVALBUILDSTRINGFAILED|Fehler beim Generieren einer Zeichenfolgendarstellung des Ausdrucks (Fehlercode: 0x%1!8.8X!). Fehler beim Generieren einer darstellbaren Zeichenfolge, die den Ausdruck darstellt.|  
|0xC004709D|-1073450851|DTS_E_EXPREVALCANNOTCONVERTRESULT|Der "%1"-Ergebnisdatentyp des Ausdrucks kann nicht in den "%2"-Spaltendatentyp konvertiert werden. Das Ergebnis des Ausdrucks sollte in eine Eingabe-/Ausgabespalte geschrieben werden, aber der Datentyp des Ausdrucks kann nicht in den Datentyp der Spalte konvertiert werden.|  
|0xC004709E|-1073450850|DTS_E_EXPREVALCONDITIONALOPINVALIDCONDITIONTYPE|Der bedingte Ausdruck "%1" des Bedingungsoperators weist den ungültigen "%2"-Datentyp auf. Der bedingte Ausdruck des Bedingungsoperators muss einen booleschen Wert zurückgeben, also den DT_BOOL-Datentyp.|  
|0xC004709F|-1073450849|DTS_E_EXPREVALCONDITIONALOPTYPEMISMATCH|Der Datentypen "%1" und "%2" sind für den Bedingungsoperator inkompatibel. Die Operandentypen können nicht implizit in für den Bedingungsvorgang kompatible Datentypen umgewandelt werden. Für diesen Vorgang müssen einer oder beide der Operanden explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC00470A0|-1073450848|DTS_E_EXPREVALCONDITIONALOPSETTYPEFAILED|Fehler beim Festlegen des Ergebnistyps des Bedingungsvorgangs "%1" (Fehlercode: 0x%2!8.8X!).|  
|0xC00470A1|-1073450847|DTS_E_BUFFERORPHANED|Dieser Puffer ist verwaist. Der Puffer-Manager wurde heruntergefahren, wodurch ein Puffer aussteht und für den Puffer kein Cleanup ausgeführt wird. Es besteht die Gefahr von Speicherlecks und anderen Problemen.|  
|0xC00470A2|-1073450846|DTS_E_EXPREVALINPUTCOLUMNNAMENOTFOUND|Fehler beim Suchen der "%1"-Eingabespalte (Fehlercode: 0x%2!8.8X!). Die angegebene Eingabespalte wurde in der Eingabespaltenauflistung nicht gefunden.|  
|0xC00470A3|-1073450845|DTS_E_EXPREVALINPUTCOLUMNIDNOTFOUND|Fehler beim Suchen der Eingabespalte mit der Herkunfts-ID "%1!d!" (Fehlercode: 0x%2!8.8X!). Die Eingabespalte wurde in der Eingabespaltenauflistung nicht gefunden.|  
|0xC00470A4|-1073450844|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNNAME|Der Ausdruck enthält das unbekannte Token "%1". Falls "%1" eine Variable ist, sollte das Format "@%1" dafür verwendet werden. Das angegebene Token ist ungültig. Falls das Token ein Variablenname sein soll, sollte das Symbol @ vorangestellt werden.|  
|0xC00470A5|-1073450843|DTS_E_EXPREVALNOINPUTCOLUMNCOLLECTIONFORCOLUMNID|Der Ausdruck enthält das unbekannte Token "#%1!d!".|  
|0xC00470A6|-1073450842|DTS_E_EXPREVALVARIABLENOTFOUND|Die "%1"-Variable wurde in der Variables-Auflistung nicht gefunden. Möglicherweise ist die Variable nicht im richtigen Bereich vorhanden.|  
|0xC00470A7|-1073450841|DTS_E_EXPREVALINVALIDTOKENSTATE|Fehler beim Analysieren des Ausdrucks "%1". Der Ausdruck enthält möglicherweise ein ungültiges Token, ein unvollständiges Token oder ein ungültiges Element. Er ist möglicherweise fehlerhaft, oder es fehlt ein Teil eines erforderlichen Elements, wie z. B. eine Klammer.|  
|0xC00470A8|-1073450840|DTS_E_BLANKOUTPUTCOLUMNNAME|Der Name für "%1" ist leer. Namen dürfen jedoch nicht leer sein.|  
|0xC00470A9|-1073450839|DTS_E_HASSIDEEFFECTSWITHSYNCINP|Für "%1"' ist die HasSideEffects-Eigenschaft auf TRUE festgelegt, aber "%1" ist synchron, weshalb dies nicht zulässig ist. Legen Sie die HasSideEffects-Eigenschaft auf FALSE fest.|  
|0xC00470AA|-1073450838|DTS_E_EXPREVALINVALIDCASTCODEPAGE|Der Wert %1!d!, der für den Codepageparameter der Umwandlung in den "%2"-Datentyp angegeben ist, ist ungültig. Die Codepage ist auf dem Computer nicht installiert.|  
|0xC00470AB|-1073450837|DTS_E_EXPREVALINVALIDCASTPRECISION|Der Wert %1!d! , der für den precision-Parameter der Umwandlung in den %2-Datentyp angegeben ist, ist ungültig. Der Wert für die Genauigkeit muss zwischen %3!d! und %4!d! liegen , und der Wert für die Genauigkeit liegt für die Typumwandlung außerhalb des zulässigen Bereichs.|  
|0xC00470AC|-1073450836|DTS_E_EXPREVALINVALIDCASTSCALE|Der Wert %1!d! , der für den scale-Parameter der Umwandlung in den %2-Datentyp angegeben ist, ist ungültig. Die Dezimalstellen müssen zwischen %3!d! und %4!d! liegen , und der Wert für die Dezimalstellen liegt für die Typumwandlung außerhalb des zulässigen Bereichs. Der Wert für die Dezimalstellen darf die Genauigkeit nicht überschreiten und muss positiv sein.|  
|0xC00470AD|-1073450835|DTS_E_NONSORTEDOUTPUTHASSORTKEYPOSITIONS|Die IsSorted-Eigenschaft für "% 1" ist ungültig, aber %2!lu! SortKeyPositions-Objekte der Ausgabespalten sind ungleich 0.|  
|0xC00470AF|-1073450833|DTS_E_EXPREVALCONDITIONALOPCODEPAGEMISMATCH|Die Codepages müssen für Operanden des Bedingungsvorgangs "%1" für den %2-Typ übereinstimmen. Die Codepage des linken Operanden stimmt nicht mit der Codepage des rechten Operanden überein. Für den Bedingungsoperator des angegebenen Typs müssen die Codepages identisch sein.|  
|0xC00470B1|-1073450831|DTS_E_REFERENCEDMETADATABADCOUNT|Die Eingabe "%1" (%2!d!) verweist auf die Eingabe "%3" (%4!d!). Sie weisen jedoch nicht die gleiche Spaltenanzahl auf. Die Eingabe %5!d! weist „%6!d!“ Spalten auf, die Eingabe %7!d! weist dagegen %8!d! Spalten auf.|  
|0xC00470B2|-1073450830|DTS_E_OBJECTLINEAGEIDNOTFOUND|Ein Objekt mit der Herkunfts-ID %1!d! ist nicht vorhanden.|  
|0xC00470B3|-1073450829|DTS_E_FILENAMEOUTPUTCOLUMNOTFOUND|Die Ausgabespalte für den Dateinamen wurde nicht gefunden.|  
|0xC00470B4|-1073450828|DTS_E_FILENAMEOUTPUTCOLUMNINVALIDDATATYPE|Die Ausgabespalte für den Dateiname ist keine NULL-terminierte Unicode-Zeichenfolge, also der DT_WSTR-Datentyp.|  
|0xC00470B5|-1073450827|DTS_E_DISTRIBUTORADDFAILED|Fehler beim Vergeben eines Puffers an den Thread "%1" durch einen Verteiler aufgrund des Fehlers 0x%2!8.8X!. Der Zielthread wird wahrscheinlich heruntergefahren.|  
|0xC00470B6|-1073450826|DTS_E_LOCALENOTINSTALLED|Der LocaleID-Wert "%1!ld!" ist auf diesem Computer nicht installiert.|  
|0xC00470B7|-1073450825|DTS_E_EXPREVALILLEGALHEXESCAPEINSTRINGLITERAL|Das Zeichenfolgenliteral "%1" enthält die ungültige hexadezimale Escapesequenz "\x%2". Diese Escapesequenz wird bei Zeichenfolgenliteralen in der Ausdrucksauswertung nicht unterstützt. Für hexadezimale Escapesequenzen ist das Format \xhhhh erforderlich, wobei h für eine gültige Hexadezimalzahl steht.|  
|0xC00470B8|-1073450824|DTS_E_EXPREVALILLEGALESCAPEINSTRINGLITERAL|Das Zeichenfolgenliteral „%1“ enthält die ungültige Escapesequenz „\\%2!c!“. Diese Escapesequenz wird bei Zeichenfolgenliteralen in der Ausdrucksauswertung nicht unterstützt. Falls in der Zeichenfolge ein umgekehrter Schrägstrich erforderlich ist, verwenden Sie einen doppelten umgekehrten Schrägstrich, „\\\\“.|  
|0xC00470B9|-1073450823|DTS_E_NOOUTPUTCOLUMNS|"%1" enthält keine Ausgabespalten. Eine asynchrone Ausgabe muss Ausgabespalten enthalten.|  
|0xC00470BA|-1073450822|DTS_E_LOBDATATYPENOTSUPPORTED|"%1" weist den Long-Objektdatentyp DT_TEXT, DT_NTEXT oder DT_IMAGE auf. Diese Datentypen werden nicht unterstützt.|  
|0xC00470BB|-1073450821|DTS_E_OUTPUTWITHMULTIPLEERRORS|Fehler beim Einfügen von Ausgabe-ID %1!d! wurden mehrere Fehlerausgabekonfigurationen zugewiesen: zunächst %2!d! und %3!d!, anschließend %4!d! und %5!d!.|  
|0xC00470BC|-1073450820|DTS_E_FAILEDDURINGOLEDBDATATYPECONVERSIONCHECK|Fehler beim OLE DB-Anbieter beim Überprüfen der Datentypkonvertierung für "%1".|  
|0xC00470BD|-1073450819|DTS_E_BUFFERISEOR|Dieser Puffer stellt das Ende des Rowsets dar, und die Zeilenanzahl kann nicht geändert werden.  Es wurde versucht, AddRow oder RemoveRow für einen Puffer aufzurufen, in dem sich das Flag für das Ende des Rowsets befindet.|  
|0xC00470BE|-1073450818|DTS_E_EXPREVALUNSUPPORTEDTYPE|Der "%1"-Datentyp wird in einem Ausdruck nicht unterstützt. Der angegebene Typ wird nicht unterstützt oder ist ungültig.|  
|0xC00470BF|-1073450817|DTS_E_PRIMEOUTPUTNOEOR|Die PrimeOutput-Methode in "%1" wurde erfolgreich ausgeführt, aber das Ende des Rowsets wurde nicht gemeldet. In der Komponente liegt ein Fehler vor. Das Ende des Rowsets hätte gemeldet werden sollen. Die Pipeline beendet die Ausführung, um unvorhersehbare Ergebnisse zu vermeiden.|  
|0xC00470C0|-1073450816|DTS_E_EXPREVALDATACONVERSIONOVERFLOW|Überlauf beim Konvertieren des "%1"-Datentyps in den "%2"-Datentyp. Der Quelltyp ist für den Zieltyp zu groß.|  
|0xC00470C1|-1073450815|DTS_E_EXPREVALDATACONVERSIONNOTSUPPORTED|Die Konvertierung vom "%1"-Datentyp in den "%2"-Datentyp wird nicht unterstützt. Der Quelltyp kann nicht in den Zieltyp konvertiert werden.|  
|0xC00470C2|-1073450814|DTS_E_EXPREVALDATACONVERSIONFAILED|Fehlercode: 0x%1!8.8X! beim Konvertieren vom %2-Datentyp in den %3-Datentyp (Fehlercode: 0x%1!8.8X!).|  
|0xC00470C3|-1073450813|DTS_E_EXPREVALCONDITIONALOPERATIONFAILED|Fehler beim Bedingungsvorgang "%1" (Fehlercode: 0x%2!8.8X!). Ein interner Fehler ist aufgetreten, oder es war nicht genügend Arbeitsspeicher verfügbar.|  
|0xC00470C4|-1073450812|DTS_E_EXPREVALCASTFAILED|Fehler beim Umwandeln des Ausdrucks "%1" vom "%2"-Datentyp in den "%3"-Datentyp (Fehlercode: 0x%4!8.8X!).|  
|0xC00470C5|-1073450811|DTS_E_EXPREVALFUNCTIONCOMPUTEFAILED|Fehler beim Auswerten der "%1"-Funktion (Fehlercode: 0x%2!8.8X!).|  
|0xC00470C6|-1073450810|DTS_E_EXPREVALFUNCTIONCONVERTPARAMTOMEMBERFAILED|Der Parameter mit der Nummer %1!d! der %2-Funktion kann nicht in einen statischen Wert konvertiert werden.|  
|0xC00470C7|-1073450809|DTS_E_REDIRECTROWUNAVAILABLEWITHFASTLOADANDZEROMAXINSERTCOMMITSIZE|Die Fehlerzeilendisposition in "%1" kann nicht so festgelegt werden, dass die Zeile umgeleitet wird, wenn die Option "Schnelles Laden" aktiviert und die maximale Einfügungscommitgröße auf den Wert 0 (null) festgelegt ist.|  
|0xC00470CE|-1073450802|DTS_E_EXPREVALBINARYOPERATORCODEPAGEMISMATCH|Die Codepages für Operanden des binären Operators "%1" für den "%2"-Typ müssen übereinstimmen. Derzeit stimmt die Codepage des linken Operanden nicht mit der Codepage des rechten Operanden überein. Für den angegebenen binären Operator des angegebenen Typs müssen die Codepages identisch sein.|  
|0xC00470CF|-1073450801|DTS_E_EXPREVALVARIABLECOMPUTEFAILED|Fehler beim Abrufen des Werts der "%1"-Variablen (Fehlercode: 0x%2!8.8X!).|  
|0xC00470D0|-1073450800|DTS_E_EXPREVALVARIABLETYPENOTSUPPORTED|Der Datentyp der "%1"-Variablen wird in einem Ausdruck nicht unterstützt.|  
|0xC00470D1|-1073450799|DTS_E_EXPREVALCASTCODEPAGEMISMATCH|Der Ausdruck "%1" kann nicht vom "%2"-Datentyp in den "%3"-Datentyp umgewandelt werden, weil die Codepage des umzuwandelnden Werts (%4!d!) nicht mit der angeforderten Ergebniscodepage (%5!d!) übereinstimmt. Die Codepage der Quelle muss mit der für das Ziel angeforderten Codepage übereinstimmen.|  
|0xC00470D2|-1073450798|DTS_E_BUFFERSIZEOUTOFRANGE|Die Standardpuffergröße muss zwischen %1!d! und %2!d! Bytes ist. Es wurde versucht, die DefaultBufferSize-Eigenschaft auf einen zu kleinen oder zu großen Wert festzulegen.|  
|0xC00470D3|-1073450797|DTS_E_BUFFERMAXROWSIZEOUTOFRANGE|Die maximale Zeilenanzahl für den Standardpuffer muss mindestens %1!d! Zeilen zwischengespeichert. Es wurde versucht, die DefaultBufferMaxRows-Eigenschaft auf einen zu kleinen Wert festzulegen.|  
|0xC00470D4|-1073450796|DTS_E_EXTERNALCOLUMNMETADATACODEPAGEMISMATCH|Die Codepage in %1 ist %2!d!, muss jedoch %3!d! sein.|  
|0xC00470D5|-1073450795|DTS_E_THREADCOUNTOUTOFRANGE|Fehler beim Zuweisen von %3!d! zur EngineThreads-Eigenschaft der Datenflusstask. Der Wert muss zwischen %1!d! und %2!d! liegen.|  
|0xC00470D6|-1073450794|DTS_E_EXPREVALINVALIDTOKENSINGLEQUOTE|Fehler beim Analysieren des Ausdrucks „%1“. Das einfache Anführungszeichen in Zeile Nummer "%2", Zeichen Nummer "%3", wurde nicht erwartet.|  
|0xC00470D7|-1073450793|DTS_E_EXPREVALINVALIDTOKENSINGLEEQUAL|Fehler beim Analysieren des Ausdrucks „%1“. Das Gleichheitszeichen (=) in Zeile Nummer "%2", Zeichen Nummer "%3", wurde nicht erwartet. An der angegebenen Position ist möglicherweise ein doppeltes Gleichheitszeichen (==) erforderlich.|  
|0xC00470DA|-1073450790|DTS_E_INDIVIDUALPUTREFTRACKERFAILED|Die Komponente "%1" konnte die Auflistung für die Laufzeitobjekt-Verweisnachverfolgung nicht zwischenspeichern und hat den Fehlercode 0x%2!8.8X! zurückgegeben.|  
|0xC00470DB|-1073450789|DTS_E_EXPREVALAMBIGUOUSINPUTCOLUMNNAME|Es sind mehrere Eingabespalten mit dem Namen "%1" vorhanden. Die gewünschte Eingabespalte muss eindeutig im Format [Komponentenname].[%2] oder mithilfe der Herkunfts-ID angegeben werden. Derzeit ist die angegebene Eingabespalte in mehreren Komponenten vorhanden.|  
|0xC00470DC|-1073450788|DTS_E_EXPREVALDOTTEDINPUTCOLUMNNAMENOTFOUND|Fehler beim Suchen der Eingabespalte "[%1].[%2]" (Fehlercode: 0x%3!8.8X!). Die Eingabespalte wurde in der Eingabespaltenauflistung nicht gefunden.|  
|0xC00470DD|-1073450787|DTS_E_EXPREVALAMBIGUOUSVARIABLENNAME|Es sind mehrere Variablen mit dem Namen "%1" vorhanden. Die gewünschte Variable muss eindeutig im Format @[Namespace::%2] angegeben werden. Die Variable ist in mehreren Namespaces vorhanden.|  
|0xC00470DE|-1073450786|DTS_E_REDUCTIONFAILED|Die Datenfluss-Modulplanung konnte den Ausführungsplan für die Pipeline nicht reduzieren. Legen Sie die OptimizedMode-Eigenschaft auf False fest.|  
|0xC00470DF|-1073450785|DTS_E_EXPREVALSQRTINVALIDPARAM|Die SQRT-Funktion kann nicht für negative Werte verwendet werden. Ein negativer Wert wurde jedoch an die SQRT-Funktion übergeben.|  
|0xC00470E0|-1073450784|DTS_E_EXPREVALLNINVALIDPARAM|Die LN-Funktion kann nicht für NULL-Werte oder negative Werte verwendet werden. Ein NULL-Wert oder negativer Wert wurde jedoch an die LN-Funktion übergeben.|  
|0xC00470E1|-1073450783|DTS_E_EXPREVALLOGINVALIDPARAM|Die LOG-Funktion kann nicht für NULL-Werte oder negative Werte verwendet werden. Ein NULL-Wert oder negativer Wert wurde jedoch an die LOG-Funktion übergeben.|  
|0xC00470E2|-1073450782|DTS_E_EXPREVALPOWERINVALIDPARAM|Die an die POWER-Funktion übergebenen Parameter können nicht ausgewertet werden und führen zu einem unbestimmten Ergebnis.|  
|0xC00470E3|-1073450781|DTS_E_NOCANCELEVENT|Die Laufzeitumgebung kann aufgrund des Fehlers 0x%1!8.8X! kein Abbruchereignis bereitstellen.|  
|0xC00470E4|-1073450780|DTS_E_CANCELRECEIVED|Die Pipeline erhielt eine Abbruchanforderung und wird heruntergefahren.|  
|0xC00470E5|-1073450779|DTS_E_EXPREVALUNARYOPOVERFLOW|Das Ergebnis der unären Minusoperation (Negation) "%1" führt zu einem Überlauf der maximal zulässigen Größe für den Ergebnisdatentyp "%2". Das Ergebnis der Operation führt zu einem Überlauf der zulässigen Größe für diesen Ergebnistyp.|  
|0xC00470E6|-1073450778|DTS_E_EXPREVALPLACEHOLDERINEXPRESSION|Der Platzhalter "%1" wurde in einem Ausdruck gefunden. Dieser Platzhalter muss durch einen tatsächlichen Parameter oder Operanden ersetzt werden.|  
|0xC00470E7|-1073450777|DTS_E_EXPREVALFNRIGHTINVALIDLENGTH|Die für die Funktion angegebene Länge von %1!d! ist negativ und deshalb ungültig. Der length-Parameter muss ein positiver Wert sein.|  
|0xC00470E8|-1073450776|DTS_E_EXPREVALFNREPLICATEINVALIDREPEATCOUNT|Die Wiederholungsanzahl %1!d! für die %2-Funktion ist negativ und daher ungültig. Der Parameter für die Wiederholungsanzahl darf nicht negativ sein.|  
|0xC00470EA|-1073450774|DTS_E_EXPREVALVARIABLECOULDNOTBEREAD|Fehler beim Lesen der %1-Variablen (Fehlercode: 0x%2!8.8X!).|  
|0xC00470EC|-1073450772|DTS_E_EXPREVALBINARYOPDTSTRNOTSUPPORTED|Für Operanden einer binären Operation wird der DT_STR-Datentyp nur für Eingabespalten und Umwandlungsvorgänge unterstützt. Der Ausdruck "%1" weist einen DT_STR-Operanden auf, der keine Eingabespalte und nicht das Ergebnis einer Typumwandlung ist und nicht in einer binären Operation verwendet werden kann. Für diesen Vorgang muss der Operand explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC00470ED|-1073450771|DTS_E_EXPREVALCONDITIONALOPDTSTRNOTSUPPORTED|Für Operanden des Bedingungsoperators wird der DT_STR-Datentyp nur für Eingabespalten und Umwandlungsvorgänge unterstützt. Der Ausdruck "%1" weist einen DT_STR-Operanden auf, der keine Eingabespalte und nicht das Ergebnis einer Typumwandlung ist und daher nicht im Bedingungsvorgang verwendet werden kann. Für diesen Vorgang muss der Operand explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC00470EE|-1073450770|DTS_E_EXPREVALFNFINDSTRINGINVALIDOCCURRENCECOUNT|Die Anzahl der Vorkommen von %1!d! ist für die %2-Funktion ungültig. Dieser Parameter muss größer als 0 (null) sein.|  
|0xC00470EF|-1073450769|DTS_E_INDIVIDUALPUTLOGENTRYINFOS|"%1" konnte die LogEntryInfos-Auflistung nicht zwischenspeichern und gab den Fehlercode 0x%2!8.8X! zurück.|  
|0xC00470F0|-1073450768|DTS_E_EXPREVALINVALIDDATEPARTNODE|Der für die %1-Funktion angegebene date part-Parameter ist ungültig. Es muss eine statische Zeichenfolge sein.  Der date part-Parameter darf keine dynamischen Elemente enthalten, wie z. B. Eingabespalten, und muss vom Typ DT_WSTR sein.|  
|0xC00470F1|-1073450767|DTS_E_EXPREVALINVALIDCASTLENGTH|Der Wert %1!d! , der für den length-Parameter der Umwandlung in den %2-Datentyp angegeben ist, ist negativ und daher ungültig. Der Wert für die Länge muss positiv sein.|  
|0xC00470F2|-1073450766|DTS_E_EXPREVALINVALIDNULLCODEPAGE|Der Wert %1!d! , der für den Codepageparameter der NULL-Funktion mit dem %2-Datentyp angegeben ist, ist ungültig. Die Codepage ist nicht auf dem Computer installiert.|  
|0xC00470F3|-1073450765|DTS_E_EXPREVALINVALIDNULLPRECISION|Der Wert %1!d! , der für den precision-Parameter der NULL-Funktion mit dem %2-Datentyp angegeben ist, liegt außerhalb des zulässigen Bereichs. Der Wert für die Genauigkeit muss zwischen %3!d! und „%4!d!“ liegen.|  
|0xC00470F4|-1073450764|DTS_E_EXPREVALINVALIDNULLSCALE|Der Wert %1!d! , der für den scale-Parameter der NULL-Funktion mit dem %2-Datentyp angegeben ist, liegt außerhalb des zulässigen Bereichs. Der Wert für die Dezimalstellen muss zwischen %3!d! und „%4!d!“ liegen. Der Wert für die Dezimalstellen darf die Genauigkeit nicht überschreiten und darf nicht negativ sein.|  
|0xC00470F5|-1073450763|DTS_E_EXPREVALINVALIDNULLLENGTH|Der Wert %1!d! , der für den length-Parameter der NULL-Funktion mit dem %2-Datentyp angegeben ist, ist negativ und deshalb ungültig. Der Wert für die Länge muss positiv sein.|  
|0xC00470F6|-1073450762|DTS_E_NEGATIVESNOTALLOWED|%1 kann kein negativer Wert zugewiesen werden.|  
|0xC00470F7|-1073450761|DTS_E_FASTPARSENOTALLOWED|Die benutzerdefinierte Eigenschaft "%1" für "%2" darf nicht auf True festgelegt werden.  Folgende Spaltendatentypen sind möglich: DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4, DT_UI8, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAMPOFFSET, DT_DATE, DT_DBDATE, DT_DBTIME, DT_DBTIME2 oder DT_FILETIME.|  
|0xC00470F8|-1073450760|DTS_E_CANNOTREATTACHPATH|"%1" kann nicht erneut angefügt werden. Löschen Sie den Pfad, fügen Sie einen neuen Pfad hinzu, und fügen Sie das Objekt an.|  
|0xC00470F9|-1073450759|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALSINGULAR|Die %1-Funktion erfordert %2!d!-Parameter, nicht %3!d!-Parameter . Der Funktionsname wurde erkannt, aber die Parameteranzahl ist ungültig.|  
|0xC00470FA|-1073450758|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSSINGULARPLURAL|Die %1-Funktion erfordert %2!d!-Parameter, Parameter, und nicht %3!d! Parameter auf. Der Funktionsname wurde erkannt, aber die Parameteranzahl ist ungültig.|  
|0xC00470FB|-1073450757|DTS_E_EXPREVALINVALIDNUMBEROFPARAMSPLURALPLURAL|Die %1-Funktion erfordert %2!d!-Parameter, nicht %3!d!-Parameter Parameter auf. Der Funktionsname wurde erkannt, aber die Parameteranzahl ist ungültig.|  
|0xC00470FC|-1073450756|DTS_E_EXPREVALFAILEDTOPARSEEXPRESSIONOUTOFMEMORY|Fehler beim Analysieren des Ausdrucks "%1", weil nicht genügend Arbeitsspeicher verfügbar war.|  
|0xC00470FD|-1073450755|DTS_E_INDIVIDUALCHECKPRODUCTLEVELFAILED|%1 konnte die erforderliche Produktebenenüberprüfung nicht ausführen und gab den Fehlercode 0x%2!8.8X! zurück.|  
|0xC00470FE|-1073450754|DTS_E_PRODUCTLEVELTOLOW|SSIS-Fehlercode DTS_E_PRODUCTLEVELTOLOW.  %1 kann in Integration Services %2 nicht ausgeführt werden. Hierfür ist %3 oder höher erforderlich.|  
|0xC00470FF|-1073450753|DTS_E_EXPREVALSTRINGLITERALTOOLONG|Ein Zeichenfolgenliteral im Ausdruck überschreitet die maximal zulässige Länge von %1!d! Zeichen ist.|  
|0xC0047100|-1073450752|DTS_E_EXPREVALSTRINGVARIABLETOOLONG|Die %1-Variable enthält eine Zeichenfolge, die die maximal zulässige Länge von %2!d! Zeichen ist.|  
|0xC0047101|-1073450751|DTS_E_COMPONENT_NOINTERFACE|% 1 wurde gefunden, aber es unterstützt keine erforderliche Integration Services-Schnittstelle (IDTSRuntimeComponent100).  Eine aktualisierte Version dieser Komponente erhalten Sie von Ihrem Komponentenanbieter.|  
|0xC0048000|-1073446912|DTS_E_CANNOTOPENREGISTRYKEY|Der Registrierungsschlüssel "%1" kann nicht geöffnet werden.|  
|0xC0048001|-1073446911|DTS_E_INVALIDCOMPONENTFILENAME|Der Dateiname für die Komponente mit der CLSID "%1" kann nicht abgerufen werden. Überprüfen Sie, ob die Komponente ordnungsgemäß registriert ist oder ob die bereitgestellte CLSID richtig ist.|  
|0xC0048002|-1073446910|DTS_E_UNKNOWNCOMPONENTHASINVALIDCLSID|Die CLSID für eine der Komponenten ist ungültig. Überprüfen Sie, ob alle Komponenten in der Pipeline gültige CLSIDs aufweisen.|  
|0xC0048003|-1073446909|DTS_E_COMPONENTHASINVALIDCLSID|Die CLSID für eine der Komponenten mit der ID %1!d! ist ungültig.|  
|0xC0048004|-1073446908|DTS_E_INVALIDINDEX|Ungültiger Index.|  
|0xC0048005|-1073446907|DTS_E_CANNOTACCESSDTSAPPLICATIONOBJECT|Der Zugriff auf das Anwendungsobjekt ist nicht möglich. Überprüfen Sie, ob SSIS ordnungsgemäß installiert ist.|  
|0xC0048006|-1073446906|DTS_E_ERROROCCURREDWHILERETRIEVINGFILENAME|Fehler beim Abrufen des Dateinamens für eine Komponente (Fehlercode: 0x%1!8.8X!).|  
|0xC0048007|-1073446905|DTS_E_CANNOTRETRIEVEPROPERTYFORCOMPONENT|Die "%1"-Eigenschaft kann nicht aus der Komponente mit der ID %2!d! abgerufen werden.|  
|0xC0048008|-1073446904|DTS_E_DUPLICATEIDFOUND|Es wurde versucht, die ID %1!d! mehrmals im Datenflusstask zu verwenden.|  
|0xC0048009|-1073446903|DTS_E_CANNOTRETRIEVEBYLINEAGE|Ein Element kann nicht anhand der Herkunfts-ID aus einer Auflistung abgerufen werden, die keine Spalten enthält.|  
|0xC004800B|-1073446901|DTS_E_CANNOTMAPRUNTIMECONNECTIONMANAGER|Der Verbindungs-Manager mit der ID "%1" wurde aufgrund des Fehlercodes 0x%2!8.8X! nicht in der Verbindungs-Manager-Auflistung gefunden. Dieser Verbindungs-Manager wird von "%3" in der Verbindungs-Manager-Auflistung von "%4" benötigt. Überprüfen Sie, ob in der Verbindungs-Manager-Auflistung Connections ein Verbindungs-Manager mit dieser ID erstellt wurde.|  
|0xC004800E|-1073446898|DTS_E_INPUTNOTKNOWN|Der Thread "%1" hat einen Puffer für die Eingabe %2!d! erhalten, aber der Thread ist nicht für die Eingabe zuständig. Ein Fehler bewirkte, dass die Datenfluss-Modulplanung einen fehlerhaften Ausführungsplan erstellt hat.|  
|0xC004800F|-1073446897|DTS_E_GETRTINTERFACEFAILED|Die Komponente "%1" (%2!d!) kann keine IDTSRuntimeComponent100-Schnittstelle bereitstellen.|  
|0xC0048011|-1073446895|DTS_E_CANTGIVEAWAYBUFFER|Fehler beim Kopieren eines Puffers durch das Datenflusstask-Modul, um einen anderen Thread zuzuweisen.|  
|0xC0048012|-1073446894|DTS_E_CANTCREATEVIEWBUFFER|Das Datenflusstask-Modul konnte keinen Sichtpuffer vom Typ %1!d! basierend auf dem Typ %2!d! für den Puffer %3!d erstellen.|  
|0xC0048013|-1073446893|DTS_E_UNUSABLETEMPORARYPATH|Der Puffer-Manager konnte eine temporäre Datei im Pfad "%1" nicht erstellen. Der Pfad wird nicht mehr für den temporären Speicher berücksichtigt.|  
|0xC0048014|-1073446892|DTS_E_DIRECTTONONERROROUTPUT|Der Puffer-Manager versuchte, eine Fehlerzeile in eine Ausgabe zu übertragen, die nicht als Fehlerausgabe registriert war. DirectErrorRow wurde in einer Ausgabe aufgerufen, für die die IsErrorOut-Eigenschaft nicht auf TRUE festgelegt ist.|  
|0xC0048015|-1073446891|DTS_E_BUFFERISPRIVATE|Eine Puffermethode wurde in einem privaten Puffer aufgerufen. Dieser Vorgang wird jedoch von privaten Puffern nicht unterstützt.|  
|0xC0048016|-1073446890|DTS_E_BUFFERISFLAT|Dieser Vorgang wird von Puffern im privaten Modus nicht unterstützt.|  
|0xC0048017|-1073446889|DTS_E_BUFFERISPRIMEOUTPUT|Dieser Vorgang kann in einem Puffer, der an PrimeOutput übergeben wurde, nicht aufgerufen werden. Eine Puffermethode wurde während PrimeOutput aufgerufen, aber dieser Aufruf ist während PrimeOutput nicht zulässig.|  
|0xC0048018|-1073446888|DTS_E_BUFFERISPROCESSINPUT|Dieser Vorgang kann in einem Puffer, der an ProcessInput übergeben wurde, nicht aufgerufen werden. Eine Puffermethode wurde während ProcessInput aufgerufen, aber dieser Aufruf ist während ProcessInput nicht zulässig.|  
|0xC0048019|-1073446887|DTS_E_BUFFERGETTEMPFILENAME|Der Puffer-Manager konnte einen temporären Dateinamen nicht abrufen.|  
|0xC004801A|-1073446886|DTS_E_REFERENCECOLUMNTOOWIDE|Im Code wurde eine zu breite Spalte gefunden.|  
|0xC004801B|-1073446885|DTS_E_CANNOTGETRUNTIMECONNECTIONMANAGERID|Die ID des Laufzeitverbindungs-Managers, die von "%1" in der Verbindungs-Manager-Auflistung Connections von "%2" angegeben ist, konnte aufgrund des Fehlercodes "0x%3!8.8X!" nicht abgerufen werden. Überprüfen Sie, ob die ConnectionManager.ID-Eigenschaft des Laufzeitverbindungsobjekts für die Komponente festgelegt wurde.|  
|0xC004801C|-1073446884|DTS_E_EMPTYRUNTIMECONNECTIONMANAGERID|"%1" in der Verbindungs-Manager-Auflistung Connections von "%2" weist keinen Wert für die ID-Eigenschaft auf. Überprüfen Sie, ob die ConnectionManagerID-Eigenschaft des Laufzeitverbindungsobjekts für die Komponente festgelegt wurde.|  
|0xC004801D|-1073446883|DTS_E_METADATAREADONLY|Metadaten können während der Ausführung nicht geändert werden.|  
|0xC004801F|-1073446881|DTS_E_UPGRADEFAILED|Die Komponentenmetadaten für "%1" konnten nicht auf die neuere Version der Komponente aktualisiert werden. Fehler bei der PerformUpgrade-Methode.|  
|0xC0048020|-1073446880|DTS_E_COMPONENTVERSIONMISMATCH|Die Version von %1 ist nicht mit dieser DataFlow-Version kompatibel.|  
|0xC0048021|-1073446879|DTS_E_ERRORCOMPONENT|Die Komponente fehlt, ist nicht registriert, nicht aktualisierbar, oder es fehlen erforderliche Schnittstellen. Die Kontaktinformationen für diese Komponente lauten "%1".|  
|0xC0048022|-1073446878|DTS_E_BUFFERISNOTPRIMEOUTPUT|Die Methode wurde im falschen Puffer aufgerufen. Dieser Vorgang wird von Puffern, die nicht für die Komponentenausgabe verwendet werden, nicht unterstützt.|  
|0xC0049014|-1073442796|DTS_E_EXPREVALSTATIC_COMPUTATIONFAILED|Fehler beim Berechnen des Ausdrucks.|  
|0xC0049030|-1073442768|DTS_E_EXPREVALSTATIC_DIVBYZERO|Der Ausdruck weist eine Division durch 0 (null) auf.|  
|0xC0049031|-1073442767|DTS_E_EXPREVALSTATIC_LITERALOVERFLOW|Der Literalwert war für diesen Datentyp zu groß.|  
|0xC0049032|-1073442766|DTS_E_EXPREVALSTATIC_BINARYOPNUMERICOVERFLOW|Das Ergebnis einer binären Operation hat die maximal zulässige Größe für numerische Datentypen überschritten. Eine implizite Typumwandlung der Operandentypen in ein numerisches (DT_NUMERIC) Ergebnis war ohne Verlust der Genauigkeit oder der Dezimalstellen nicht möglich. Für diesen Vorgang müssen einer oder beide der Operanden explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC0049033|-1073442765|DTS_E_EXPREVALSTATIC_BINARYOPOVERFLOW|Das Ergebnis einer binären Operation führt zu einem Überlauf der maximal zulässigen Größe für diesen Ergebnisdatentyp.|  
|0xC0049034|-1073442764|DTS_E_EXPREVALSTATIC_FUNCTIONOVERFLOW|Das Ergebnis eines Funktionsaufrufs war für den Ergebnistyp zu groß und führte zu einem Überlauf der maximal zulässigen Größe des Operandentyps. Möglicherweise ist eine explizite Umwandlung in einen größeren Typ erforderlich.|  
|0xC0049035|-1073442763|DTS_E_EXPREVALSTATIC_BINARYTYPEMISMATCH|Für einen binären Operator wurden inkompatible Datentypen verwendet. Die Operandentypen konnten nicht implizit in für den Vorgang kompatible Typen umgewandelt werden. Für diesen Vorgang müssen einer oder beide der Operanden explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC0049036|-1073442762|DTS_E_EXPREVALSTATIC_UNSUPPORTEDBINARYTYPE|Für einen binären Operator wurde ein nicht unterstützter Datentyp verwendet. Der Datentyp eines oder beider Operanden wird für den Vorgang nicht unterstützt. Für diesen Vorgang müssen einer oder beide der Operanden explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC0049037|-1073442761|DTS_E_EXPREVALSTATIC_BINARYSIGNMISMATCH|Die Vorzeichen für den bitweisen binären Operator stimmen nicht überein. Die Operanden für diesen Operator müssen entweder beide positiv oder negativ sein.|  
|0xC0049038|-1073442760|DTS_E_EXPREVALSTATIC_BINARYOPERATIONFAILED|Fehler bei einer binären Operation. Es ist nicht genügend Arbeitsspeicher verfügbar, oder ein interner Fehler ist aufgetreten.|  
|0xC0049039|-1073442759|DTS_E_EXPREVALSTATIC_BINARYOPERATIONSETTYPEFAILED|Fehler beim Festlegen des Ergebnistyps einer binären Operation.|  
|0xC004903A|-1073442758|DTS_E_EXPREVALSTATIC_STRINGCOMPARISONFAILED|Zwei Zeichenfolgen können nicht verglichen werden.|  
|0xC004903B|-1073442757|DTS_E_EXPREVALSTATIC_UNSUPPORTEDUNNARYTYPE|Für einen unären Operator wird ein nicht unterstützter Datentyp verwendet. Der Operandentyp wird für den Vorgang nicht unterstützt. Für diesen Vorgang muss der Operand explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC004903C|-1073442756|DTS_E_EXPREVALSTATIC_UNARYOPERATIONFAILED|Fehler bei einer unären Operation. Es ist nicht genügend Arbeitsspeicher verfügbar, oder ein interner Fehler ist aufgetreten.|  
|0xC004903D|-1073442755|DTS_E_EXPREVALSTATIC_UNARYOPERATIONSETTYPEFAILED|Fehler beim Festlegen des Ergebnistyps einer unären Operation.|  
|0xC004903E|-1073442754|DTS_E_EXPREVALSTATIC_PARAMTYPEMISMATCH|Eine Funktion weist einen Parameter mit einem nicht unterstützten Datentyp auf. Der Parametertyp kann nicht implizit in einen für die Funktion kompatiblen Datentyp umgewandelt werden. Für diesen Vorgang muss der Operand explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC004903F|-1073442753|DTS_E_EXPREVALSTATIC_INVALIDFUNCTION|In dem Ausdruck ist ein ungültiger Funktionsname vorhanden. Überprüfen Sie, ob der Funktionsname richtig und vorhanden ist.|  
|0xC0049040|-1073442752|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDLENGTH|Der length-Parameter war für die SUBSTRING-Funktion ungültig. Der length-Parameter darf nicht negativ sein.|  
|0xC0049041|-1073442751|DTS_E_EXPREVALSTATIC_FNSUBSTRINGINVALIDSTARTINDEX|Der Startindex war für die SUBSTRING-Funktion ungültig. Der Startindexwert muss eine ganze Zahl größer als 0 (null) sein. Der Startindex ist einsbasiert, nicht nullbasiert.|  
|0xC0049042|-1073442750|DTS_E_EXPREVALSTATIC_INVALIDNUMBEROFPARAMS|An eine Funktion wurde eine falsche Parameteranzahl übergeben. Der Funktionsname wurde erkannt, aber die Parameteranzahl war nicht richtig.|  
|0xC0049043|-1073442749|DTS_E_EXPREVALSTATIC_CHARMAPPINGFAILED|Fehler bei einer Zeichenzuordnungsfunktion.|  
|0xC0049044|-1073442748|DTS_E_EXPREVALSTATIC_INVALIDDATEPART|Für eine Datumsfunktion wurde ein unbekannter date part-Parameter angegeben.|  
|0xC0049045|-1073442747|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAM|Für die NULL-Funktion wurde ein ungültiger Parameter angegeben. Die Parameter von NULL müssen statisch sein und dürfen keine dynamischen Elemente, wie z. B. Eingabespalten, enthalten.|  
|0xC0049046|-1073442746|DTS_E_EXPREVALSTATIC_INVALIDNULLPARAMTYPE|Für die NULL-Funktion wurde ein ungültiger Parameter angegeben. Parameter von NULL müssen eine ganze Zahl oder von einem Datentyp sein, der in eine ganze Zahl konvertiert werden kann.|  
|0xC0049047|-1073442745|DTS_E_EXPREVALSTATIC_FUNCTIONPARAMNOTSTATIC|Für eine Funktion wurde ein ungültiger Parameter angegeben. Dieser Parameter muss statisch sein und darf keine dynamischen Elemente, wie z. B. Eingabespalten, enthalten.|  
|0xC0049048|-1073442744|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAM|Für einen Umwandlungsvorgang wurde ein ungültiger Parameter angegeben. Parameter von Umwandlungsoperatoren müssen statisch sein und dürfen keine dynamischen Elemente, wie z. B. Eingabespalten, enthalten.|  
|0xC0049049|-1073442743|DTS_E_EXPREVALSTATIC_INVALIDCASTPARAMTYPE|Für einen Umwandlungsvorgang wurde ein ungültiger Parameter angegeben. Parameter von Umwandlungsoperatoren müssen einer ganzen Zahl entsprechen oder einen Datentyp aufweisen, der in eine ganze Zahl konvertiert werden kann.|  
|0xC004904A|-1073442742|DTS_E_EXPREVALSTATIC_INVALIDCAST|Der Ausdruck enthielt eine nicht unterstützte Typumwandlung.|  
|0xC004904B|-1073442741|DTS_E_EXPREVALSTATIC_INVALIDTOKEN|Der Ausdruck enthielt ein unbekanntes Token. Der Ausdruck konnte nicht analysiert werden, weil er ungültige Elemente enthält.|  
|0xC004904C|-1073442740|DTS_E_EXPREVALSTATIC_FAILEDTOPARSEEXPRESSION|Der Ausdruck ist ungültig und konnte nicht analysiert werden. Er enthält möglicherweise ungültige Elemente oder ist fehlerhaft.|  
|0xC004904D|-1073442739|DTS_E_EXPREVALSTATIC_UNARYOPOVERFLOW|Das Ergebnis einer unären Minusoperation (Negation) führte zu einem Überlauf der maximal zulässigen Größe für den Ergebnisdatentyp. Das Ergebnis der Operation führt zu einem Überlauf der zulässigen Größe für diesen Ergebnistyp.|  
|0xC004904E|-1073442738|DTS_E_EXPREVALSTATIC_COMPUTEFAILED|Fehler beim Berechnen des Ausdrucks.|  
|0xC004904F|-1073442737|DTS_E_EXPREVALSTATIC_BUILDSTRINGFAILED|Fehler beim Generieren einer Zeichenfolgendarstellung des Ausdrucks.|  
|0xC0049050|-1073442736|DTS_E_EXPREVALSTATIC_CANNOTCONVERTRESULT|Der Ergebnisdatentyp Ausdrucks kann nicht in den Spaltendatentyp konvertiert werden. Das Ergebnis des Ausdrucks sollte in eine Eingabe-/Ausgabespalte geschrieben werden, aber der Datentyp des Ausdrucks kann nicht in den Datentyp der Spalte konvertiert werden.|  
|0xC0049051|-1073442735|DTS_E_EXPREVALSTATIC_CONDITIONALOPINVALIDCONDITIONTYPE|Der bedingte Ausdruck des Bedingungsoperators weist einen ungültigen Datentyp auf. Für den bedingten Ausdruck ist der DT_BOOL-Datentyp erforderlich.|  
|0xC0049052|-1073442734|DTS_E_EXPREVALSTATIC_CONDITIONALOPTYPEMISMATCH|Der Datentypen der Operanden des Bedingungsoperator waren inkompatibel. Die Operandentypen konnten nicht implizit in für den Bedingungsvorgang kompatible Typen umgewandelt werden. Für diesen Vorgang müssen einer oder beide der Operanden explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC0049053|-1073442733|DTS_E_EXPREVALSTATIC_CONDITIONALOPSETTYPEFAILED|Fehler beim Festlegen des Ergebnistyps eines Bedingungsvorgangs.|  
|0xC0049054|-1073442732|DTS_E_EXPREVALSTATIC_INPUTCOLUMNNAMENOTFOUND|Die angegebene Eingabespalte wurde in der Eingabespaltenauflistung nicht gefunden.|  
|0xC0049055|-1073442731|DTS_E_EXPREVALSTATIC_INPUTCOLUMNIDNOTFOUND|Fehler beim Suchen einer Eingabespalte anhand der Herkunfts-ID. Die Eingabespalte wurde in der Eingabespaltenauflistung nicht gefunden.|  
|0xC0049056|-1073442730|DTS_E_EXPREVALSTATIC_NOINPUTCOLUMNCOLLECTION|Der Ausdruck enthält ein unbekanntes Token, das ein Eingabespaltenverweis zu sein scheint, aber die Eingabespaltenauflistung steht nicht zur Verarbeitung von Eingabespalten zur Verfügung. Die Eingabespaltenauflistung wurde der Ausdrucksauswertung nicht bereitgestellt, aber eine Eingabespalte wurde in den Ausdruck eingeschlossen.|  
|0xC0049057|-1073442729|DTS_E_EXPREVALSTATIC_VARIABLENOTFOUND|Eine angegebene Variable wurde in der Auflistung nicht gefunden. Möglicherweise ist sie nicht im richtigen Bereich vorhanden. Überprüfen Sie, ob die Variable vorhanden und der Bereich richtig ist.|  
|0xC0049058|-1073442728|DTS_E_EXPREVALSTATIC_INVALIDTOKENSTATE|Fehler beim Analysieren des Ausdrucks. Der Ausdruck enthält ein ungültiges oder unvollständiges Token. Es ist möglich, dass er ungültige Elemente enthält, dass ein Teil eines erforderlichen Elements, wie z. B. schließende Klammern fehlen, oder dass der Ausdruck fehlerhaft ist.|  
|0xC0049059|-1073442727|DTS_E_EXPREVALSTATIC_INVALIDCASTCODEPAGE|Der für den Codepageparameter der Umwandlung in den Datentyp DT_STR oder DT_TEXT angegebene Wert ist ungültig. Die angegebene Codepage ist nicht auf dem Computer installiert.|  
|0xC004905A|-1073442726|DTS_E_EXPREVALSTATIC_INVALIDCASTPRECISION|Der für den precision-Parameter des Umwandlungsvorgangs angegebene Wert liegt für die Typumwandlung außerhalb des zulässigen Bereichs.|  
|0xC004905B|-1073442725|DTS_E_EXPREVALSTATIC_INVALIDCASTSCALE|Der für den scale-Parameter eines Umwandlungsvorgangs angegebene Wert liegt für die Typumwandlung außerhalb des zulässigen Bereichs. Der Wert für die Dezimalstellen darf die Genauigkeit nicht überschreiten und darf nicht negativ sein.|  
|0xC004905C|-1073442724|DTS_E_EXPREVALSTATIC_CONDITIONALOPCODEPAGEMISMATCH|Die Codepages stimmen in einem Bedingungsvorgang nicht überein. Die Codepage des linken Operanden stimmt nicht mit der Codepage des rechten Operanden überein. Für den Bedingungsoperator dieses Typs müssen die Codepages identisch sein.|  
|0xC004905D|-1073442723|DTS_E_EXPREVALSTATIC_ILLEGALHEXESCAPEINSTRINGLITERAL|Ein Zeichenfolgenliteral enthält eine ungültige hexadezimale Escapesequenz. Diese Escapesequenz wird bei Zeichenfolgenliteralen in der Ausdrucksauswertung nicht unterstützt. Für hexadezimale Escapesequenzen ist das Format \xhhhh erforderlich, wobei h für eine gültige Hexadezimalzahl steht.|  
|0xC004905E|-1073442722|DTS_E_EXPREVALSTATIC_ILLEGALESCAPEINSTRINGLITERAL|Das Zeichenfolgenliteral enthält eine ungültige Escapesequenz. Diese Escapesequenz wird bei Zeichenfolgenliteralen in der Ausdrucksauswertung nicht unterstützt. Falls in der Zeichenfolge ein umgekehrter Schrägstrich erforderlich ist, formatieren Sie ihn als einen doppelten umgekehrten Schrägstrich, „\\\\“.|  
|0xC004905F|-1073442721|DTS_E_EXPREVALSTATIC_UNSUPPORTEDTYPE|Ein nicht unterstützter oder unbekannter Datentyp wurde im Ausdruck verwendet.|  
|0xC0049060|-1073442720|DTS_E_EXPREVALSTATIC_DATACONVERSIONOVERFLOW|Überlauf beim Konvertieren von Datentypen. Der Quelltyp ist für den Zieltyp zu groß.|  
|0xC0049061|-1073442719|DTS_E_EXPREVALSTATIC_DATACONVERSIONNOTSUPPORTED|Der Ausdruck enthält eine nicht unterstützte Datentypkonvertierung. Der Quelltyp kann nicht in den Zieltyp konvertiert werden.|  
|0xC0049062|-1073442718|DTS_E_EXPREVALSTATIC_DATACONVERSIONFAILED|Fehler beim Ausführen der Datenkonvertierung. Der Quelltyp konnte nicht in den Zieltyp konvertiert werden.|  
|0xC0049063|-1073442717|DTS_E_EXPREVALSTATIC_CONDITIONALOPERATIONFAILED|Fehler beim Bedingungsvorgang.|  
|0xC0049064|-1073442716|DTS_E_EXPREVALSTATIC_CASTFAILED|Fehler beim Ausführen einer Typumwandlung.|  
|0xC0049065|-1073442715|DTS_E_EXPREVALFAILEDTOCONVERTSTRCOLUMNTOWSTR|Fehler beim Konvertieren von "%1" vom DT_STR-Datentyp in den DT_WSTR-Datentyp (Fehlercode: 0x%2!8.8X!). Fehler bei der impliziten Konvertierung für die Eingabespalte.|  
|0xC0049066|-1073442714|DTS_E_EXPREVALSTATIC_FAILEDTOCONVERTSTRCOLUMNTOWSTR|Fehler beim Konvertieren einer Eingabespalte vom DT_STR-Datentyp in den DT_WSTR-Datentyp. Fehler bei der impliziten Konvertierung für die Eingabespalte.|  
|0xC0049067|-1073442713|DTS_E_EXPREVALSTATIC_FUNCTIONCOMPUTEFAILED|Fehler beim Auswerten der Funktion.|  
|0xC0049068|-1073442712|DTS_E_EXPREVALSTATIC_FUNCTIONCONVERTPARAMTOMEMBERFAILED|Ein Funktionsparameter kann nicht in einen statischen Wert konvertiert werden. Der Parameter muss statisch sein und darf keine dynamischen Elemente, wie z. B. Eingabespalten, enthalten.|  
|0xC0049088|-1073442680|DTS_E_EXPREVALSTATIC_FNRIGHTINVALIDLENGTH|Der length-Parameter ist für die RIGHT-Funktion ungültig. Der length-Parameter darf nicht negativ sein.|  
|0xC0049089|-1073442679|DTS_E_EXPREVALSTATIC_FNREPLICATEINVALIDREPEATCOUNT|Der repeat count-Parameter für die REPLICATE-Funktion ist ungültig. Dieser Parameter darf nicht negativ sein.|  
|0xC0049096|-1073442666|DTS_E_EXPREVALSTATIC_BINARYOPERATORCODEPAGEMISMATCH|Die Codepages stimmen in einer binären Operation nicht überein. Die Codepage des linken Operanden stimmt nicht mit der Codepage des rechten Operanden überein. Für diese binäre Operation müssen die Codepages identisch sein.|  
|0xC0049097|-1073442665|DTS_E_EXPREVALSTATIC_VARIABLECOMPUTEFAILED|Fehler beim Abrufen des Werts für eine Variable.|  
|0xC0049098|-1073442664|DTS_E_EXPREVALSTATIC_VARIABLETYPENOTSUPPORTED|Der Ausdruck enthält eine Variable mit einem nicht unterstützten Datentyp.|  
|0xC004909B|-1073442661|DTS_E_EXPREVALSTATIC_CASTCODEPAGEMISMATCH|Der Ausdruck kann nicht umgewandelt werden, weil die Codepage des umzuwandelnden Werts nicht mit der angeforderten Ergebniscodepage übereinstimmt. Die Codepage der Quelle muss mit der für das Ziel angeforderten Codepage übereinstimmen.|  
|0xC004909C|-1073442660|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEQUOTE|Der Ausdruck enthält ein unerwartetes einfaches Anführungszeichen. Möglicherweise ist ein doppeltes Anführungszeichen erforderlich.|  
|0xC004909D|-1073442659|DTS_E_EXPREVALSTATIC_INVALIDTOKENSINGLEEQUAL|Der Ausdruck enthält ein unerwartetes Gleichheitszeichen (=). Dieser Fehler tritt gewöhnlich auf, wenn ein doppeltes Gleichheitszeichen (==) erforderlich ist.|  
|0xC00490AA|-1073442646|DTS_E_EXPREVALSTATIC_AMBIGUOUSINPUTCOLUMNNAME|Ein mehrdeutiger Eingabespaltenname wurde angegeben.  Die Spalte muss im Format [Komponentenname].[Spaltenname] oder mithilfe der Herkunfts-ID angegeben werden. Dieser Fehler tritt auf, wenn die Eingabespalte in mehreren Komponenten vorhanden ist. Zur Unterscheidung müssen Sie den Komponentennamen oder die Herkunfts-ID hinzufügen.|  
|0xC00490AB|-1073442645|DTS_E_EXPREVALSTATIC_PLACEHOLDERINEXPRESSION|In einem Ausdruck wurde ein Platzhalterfunktionsparameter oder -operand gefunden. Dieser sollte durch einen tatsächlichen Parameter oder Operanden ersetzt werden.|  
|0xC00490AC|-1073442644|DTS_E_EXPREVALSTATIC_AMBIGUOUSVARIABLENNAME|Es wurde ein mehrdeutiger Variablenname angegeben. Die gewünschte Variable muss im Format @[Namespace::Variable] angegeben werden. Dieser Fehler tritt auf, wenn die Variable in mehreren Namespaces vorhanden ist.|  
|0xC00490D3|-1073442605|DTS_E_EXPREVALSTATIC_BINARYOPDTSTRNOTSUPPORTED|Für Operanden einer binären Operation wird der DT_STR-Datentyp nur für Eingabespalten und Umwandlungsvorgänge unterstützt. Ein DT_STR-Operand, der keine Eingabespalte und nicht das Ergebnis einer Typumwandlung ist, kann nicht in einer binären Operation verwendet werden. Für diesen Vorgang muss der Operand explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC00490D4|-1073442604|DTS_E_EXPREVALSTATIC_CONDITIONALOPDTSTRNOTSUPPORTED|Für Operanden des Bedingungsoperators wird der DT_STR-Datentyp nur für Eingabespalten und Umwandlungsvorgänge unterstützt. Ein DT_STR-Operand, der keine Eingabespalte und nicht das Ergebnis einer Typumwandlung ist, kann nicht in einem Bedingungsvorgang verwendet werden. Für diesen Vorgang muss der Operand explizit mit einem Umwandlungsoperator umgewandelt werden.|  
|0xC00490D5|-1073442603|DTS_E_EXPREVALSTATIC_FNFINDSTRINGINVALIDOCCURRENCECOUNT|Der occurrence count-Parameter für die FINDSTRING-Funktion ist ungültig. Dieser Parameter muss größer als 0 (null) sein.|  
|0xC00490DD|-1073442595|DTS_E_EXPREVALSTATIC_INVALIDDATEPARTNODE|Der für eine Datumsfunktion angegebene date part-Parameter ist ungültig. Die date part-Parameter müssen statische Zeichenfolgen sein und dürfen keine dynamischen Elemente, wie z. B. Eingabespalten, enthalten. Sie müssen vom Typ DT_WSTR sein.|  
|0xC00490DE|-1073442594|DTS_E_EXPREVALSTATIC_INVALIDCASTLENGTH|Der für den length-Parameter eines Umwandlungsvorgangs angegebene Wert ist ungültig. Der Wert für die Länge muss positiv sein. Die für die Typumwandlung angegebene Länge ist negativ. Ändern Sie die Länge in einen positiven Wert.|  
|0xC00490DF|-1073442593|DTS_E_EXPREVALSTATIC_INVALIDNULLLENGTH|Der für den length-Parameter einer NULL-Funktion angegebene Wert ist ungültig. Der Wert für die Länge muss positiv sein. Die für die NULL-Funktion angegebene Länge ist negativ. Ändern Sie die Länge in einen positiven Wert.|  
|0xC00490E0|-1073442592|DTS_E_EXPREVALSTATIC_INVALIDNULLCODEPAGE|Der für den Codepageparameter der NULL-Funktion mit dem Datentyp DT_STR oder DT_TEXT angegebene Wert ist ungültig. Die angegebene Codepage ist nicht auf dem Computer installiert. Ändern Sie die angegebene Codepage, oder installieren Sie die Codepage auf dem Computer.|  
|0xC00490E1|-1073442591|DTS_E_EXPREVALSTATIC_INVALIDNULLPRECISION|Der für den precision-Parameter einer NULL-Funktion angegebene Wert ist ungültig. Der angegebene Wert liegt für die NULL-Funktion außerhalb des zulässigen Bereichs.|  
|0xC00490E2|-1073442590|DTS_E_EXPREVALSTATIC_INVALIDNULLSCALE|Der für den scale-Parameter einer NULL-Funktion angegebene Wert ist ungültig. Der angegebene Wert liegt für die NULL-Funktion außerhalb des zulässigen Bereichs. Der Wert für die Dezimalstellen darf die Genauigkeit nicht überschreiten und muss positiv sein.|  
|0xC00490E8|-1073442584|DTS_E_XMLSRCERRORSETTINGERROROUTPUTCOLUMNDATA|%1 konnte keine Daten auf %2 in %3 schreiben. %4|  
|0xC00490F5|-1073442571|DTS_E_TXLOOKUP_CANCEL_REQUESTED|Die Transformation für Suche hat eine Abbruchanforderung vom Benutzer erhalten.|  
|0xC00490F6|-1073442570|DTS_E_LOBLENGTHLIMITEXCEEDED|Die Verarbeitung von Zeichen oder BLOB-Daten (Binary Large Object) wurde beendet, da das Limit von 4 GB erreicht wurde.|  
|0xC00490F7|-1073442569|DTS_E_CANNOTLOADCOMPONENT|Die verwaltete Pipelinekomponente "%1" konnte nicht geladen werden.  Die Ausnahme war: %2.|  
|0xC00F9304|-1072721148|DTS_E_OLEDB_EXCEL_NOT_SUPPORTED|SSIS-Fehlercode DTS_E_OLEDB_EXCEL_NOT_SUPPORTED: Der Excel-Verbindungs-Manager wird in der 64-Bit-Version von SSIS nicht unterstützt, da kein OLE DB-Anbieter verfügbar ist.|  
|0xC00F9310|-1072721136|DTS_E_CACHEBADHEADER|Die Cachedatei ist beschädigt, oder die Datei wurde nicht mithilfe des Cacheverbindungs-Managers erstellt.  Stellen Sie eine gültige Cachedatei bereit.|  
|0xC0202001|-1071636479|DTS_E_MISSINGSQLCOMMAND|Der SQL-Befehl wurde nicht richtig festgelegt. Überprüfen Sie die SQLCommand-Eigenschaft.|  
|0xC0202002|-1071636478|DTS_E_COMERROR|Informationen zum COM-Fehlerobjekt sind verfügbar.  Quelle: "%1" Fehlercode: 0x%2!8.8X!  Beschreibung: "%3".|  
|0xC0202003|-1071636477|DTS_E_ACQUIREDCONNECTIONUNAVAILABLE|Auf die erforderlichen Verbindungen kann nicht zugegriffen werden.|  
|0xC0202004|-1071636476|DTS_E_INCORRECTCOLUMNCOUNT|Die Spaltenanzahl ist falsch.|  
|0xC0202005|-1071636475|DTS_E_COLUMNNOTFOUND|Die Spalte "%1" wurde in der Datenquelle nicht gefunden.|  
|0xC0202007|-1071636473|DTS_E_OLEDBRECORD|Ein OLE DB-Datensatz ist verfügbar.  Quelle: "%1" HRESULT: 0x%2!8.8X!  Beschreibung: "%3".|  
|0xC0202009|-1071636471|DTS_E_OLEDBERROR|SSIS-Fehlercode DTS_E_OLEDBERROR.  OLE DB-Fehler. Fehlercode: 0x%1!8.8X!.|  
|0xC020200A|-1071636470|DTS_E_ALREADYCONNECTED|Die Komponente ist bereits verbunden. Die Komponente muss getrennt werden, bevor eine Verbindung mit dieser Komponente hergestellt werden kann.|  
|0xC020200B|-1071636469|DTS_E_INCORRECTSTOCKPROPERTYVALUE|Der Wert der Eigenschaft "%1" ist falsch.|  
|0xC020200E|-1071636466|DTS_E_CANNOTOPENDATAFILE|Die Datendatei "%1" kann nicht geöffnet werden.|  
|0xC0202010|-1071636464|DTS_E_DESTINATIONFLATFILEREQUIRED|Ein Name für die Zielflatfile wurde nicht bereitgestellt. Stellen Sie sicher, dass für den Verbindungs-Manager für Flatfiles eine Verbindungszeichenfolge konfiguriert ist. Falls der Verbindungs-Manager für Flatfiles von mehreren Komponenten verwendet wird, achten Sie darauf, dass die Verbindungszeichenfolge genügend Dateinamen aufweist.|  
|0xC0202011|-1071636463|DTS_E_TEXTQUALIFIERNOTFOUND|Der Textqualifizierer für die Spalte "%1" wurde nicht gefunden.|  
|0xC0202014|-1071636460|DTS_E_CANNOTCONVERTTYPES|Die Konvertierung von "%1" in "%2" wird nicht unterstützt.|  
|0xC0202015|-1071636459|DTS_E_PROBLEMDETECTINGTYPECOMPATIBILITY|Der Fehlercode 0x%1!8.8X! wurde beim Überprüfen der Typkonvertierung von %2 in %3 zurückgegeben.|  
|0xC0202016|-1071636458|DTS_E_CANNOTMAPINPUTCOLUMNTOOUTPUTCOLUMN|Die Eingabespalte mit der Herkunfts-ID „%1!d!“, die von „%2“ benötigt wird. Überprüfen Sie die benutzerdefinierte Eigenschaft SourceInputColumnLineageID der Ausgabespalte.|  
|0xC0202017|-1071636457|DTS_E_INCORRECTMINIMUMNUMBEROFOUTPUTS|Die Anzahl von Ausgaben ist falsch. Es müssen mindestens %1!d! Ausgaben vorhanden sein.|  
|0xC0202018|-1071636456|DTS_E_INCORRECTEXACTNUMBEROFOUTPUTS|Die Anzahl von Ausgaben ist falsch. Es müssen genau %1!d! Eingaben vorhanden sein.|  
|0xC0202019|-1071636455|DTS_E_STRINGCONVERSIONTOOLONG|Eine Zeichenfolge konnte nicht konvertiert werden, weil sie zu lang ist.|  
|0xC020201A|-1071636454|DTS_E_INCORRECTEXACTNUMBEROFINPUTS|Die Anzahl von Eingaben ist falsch. Es müssen genau %1!d! Eingaben vorhanden auf.|  
|0xC020201B|-1071636453|DTS_E_CANNOTHAVEZEROINPUTCOLUMNS|Die Anzahl von Eingabespalten für %1 darf nicht 0 (null) lauten.|  
|0xC020201C|-1071636452|DTS_E_CANNOTHAVEINPUTS|Diese Komponente weist %1!d! Eingaben auf.  Für die Komponente ist keine Eingabe zulässig.|  
|0xC020201D|-1071636451|DTS_E_PROCESSINPUTCALLEDWITHINVALIDINPUTID|ProcessInput wurde mit der ungültigen Eingabe-ID %1!d! aufgerufen.|  
|0xC020201F|-1071636449|DTS_E_INCORRECTCUSTOMPROPERTYTYPE|Für die benutzerdefinierte Eigenschaft "%1" ist der %2-Datentyp erforderlich.|  
|0xC0202020|-1071636448|DTS_E_INVALIDBUFFERTYPE|Ungültiger Puffertyp. Stellen Sie sicher, dass das Pipelinelayout und alle Komponenten nach der Überprüfung keine Fehler aufweisen.|  
|0xC0202021|-1071636447|DTS_E_INCORRECTCUSTOMPROPERTYVALUE|Der Wert für die benutzerdefinierte Eigenschaft "%1" ist falsch.|  
|0xC0202022|-1071636446|DTS_E_CONNECTIONREQUIREDFORMETADATA|Ein Fehler ist aufgetreten, weil keine Verbindung besteht. Zum Anfordern von Metadaten ist eine Verbindung erforderlich. Deaktivieren Sie im Offlinemodus das Kontrollkästchen Offline arbeiten im SSIS-Menü, um die Verbindung zu aktivieren.|  
|0xC0202023|-1071636445|DTS_E_CANTCREATECUSTOMPROPERTY|Der benutzerdefinierte Eigenschaft "%1" kann nicht erstellt werden.|  
|0xC0202024|-1071636444|DTS_E_CANTGETCUSTOMPROPERTYCOLLECTION|Die Auflistung mit den benutzerdefinierten Eigenschaften kann für die Initialisierung nicht abgerufen werden.|  
|0xC0202025|-1071636443|DTS_E_CANNOTCREATEACCESSOR|Fehler beim Erstellen eines OLE DB-Accessors. Überprüfen Sie, ob die Spaltenmetadaten gültig sind.|  
|0xC0202026|-1071636442|DTS_E_PRIMEOUTPUTCALLEDWITHINVALIDOUTPUTID|PrimeOutput wurde mit der ungültigen Ausgabe-ID %1!d! aufgerufen.|  
|0xC0202027|-1071636441|DTS_E_INCORRECTSTOCKPROPERTY|Der Wert für die Eigenschaft "%1" in "%2" ist ungültig.|  
|0xC0202028|-1071636440|DTS_E_CONNECTIONREQUIREDFORREAD|Zum Lesen von Daten ist eine Verbindung erforderlich.|  
|0xC020202C|-1071636436|DTS_E_ERRORWHILEREADINGHEADERROWS|Fehler beim Lesen des Headers.|  
|0xC020202D|-1071636435|DTS_E_DUPLICATECOLUMNNAME|Doppelter Spaltenname "%1".|  
|0xC0202030|-1071636432|DTS_E_CANNOTGETCOLUMNNAME|Der Name der Spalte mit der ID %1!d! kann nicht abgerufen werden.|  
|0xC0202031|-1071636431|DTS_E_CANTDIRECTROW|Fehler beim Umleiten der Zeile in die Ausgabe "%1" (%2!d!).|  
|0xC020203A|-1071636422|DTS_E_CANNOTCREATEBULKINSERTHREAD|Der Masseneinfügungsthread kann aufgrund des Fehlers "%1" nicht erstellt werden.|  
|0xC020203B|-1071636421|DTS_E_BULKINSERTHREADINITIALIZATIONFAILED|Fehler beim Initialisieren des Threads für den Masseneinfügungstask von SSIS.|  
|0xC020203E|-1071636418|DTS_E_BULKINSERTTHREADALREADYRUNNING|Der Thread für den Masseneinfügungstask von SSIS wird bereits ausgeführt.|  
|0xC020203F|-1071636417|DTS_E_BULKINSERTTHREADABNORMALCOMPLETION|Der Thread für den Masseneinfügungstask von SSIS wurde mit Fehlern oder Warnungen beendet.|  
|0xC0202040|-1071636416|DTS_E_CANNOTGETIROWSETFASTLOAD|Fehler beim Öffnen eines FastLoad-Rowsets für "%1". Überprüfen Sie, ob das Objekt in der Datenbank vorhanden ist.|  
|0xC0202041|-1071636415|DTS_E_CONNECTREQUIREDFORMETADATAVALIDATION|Fehler, weil keine Verbindung besteht. Eine Verbindung ist erforderlich, bevor Metadaten überprüft werden können.|  
|0xC0202042|-1071636414|DTS_E_DESTINATIONTABLENAMENOTPROVIDED|Ein Zieltabellenname wurde nicht angegeben.|  
|0xC0202043|-1071636413|DTS_E_ICONVERTTYPEUNAVAILABLE|IConvertType wird vom OLE DB-Anbieter, den der OLE DB-Adapter verwendet, nicht unterstützt. Legen Sie die ValidateColumnMetaData-Eigenschaft des Adapters auf FALSE fest.|  
|0xC0202044|-1071636412|DTS_E_OLEDBPROVIDERDATATYPECONVERSIONUNSUPPORTED|Der vom OLE DB-Adapter verwendete OLE DB-Anbieter kann für "%3" nicht zwischen den Typen "%1" und "%2" konvertieren.|  
|0xC0202045|-1071636411|DTS_E_VALIDATECOLUMNMETADATAFAILED|Fehler beim Überprüfen der Spaltenmetadaten.|  
|0xC0202047|-1071636409|DTS_E_ATTEMPTINGTOINSERTINTOAROWIDCOLUMN|"%1" ist eine Zeilen-ID-Spalte und kann nicht in einem Vorgang zum Einfügen von Daten verwendet werden.|  
|0xC0202048|-1071636408|DTS_E_ATTEMPTINGTOINSERTINTOAROWVERCOLUMN|Es wird versucht, Daten in die Zeilenversionsspalte "%1" einzufügen. Das Einfügen in eine Zeilenversionsspalte ist nicht möglich.|  
|0xC0202049|-1071636407|DTS_E_ATTEMPTINGTOINSERTINTOAREADONLYCOLUMN|Fehler beim Einfügen in die schreibgeschützte Spalte "%1".|  
|0xC020204A|-1071636406|DTS_E_UNABLETORETRIEVECOLUMNINFO|Spalteninformationen können nicht von der Datenquelle abgerufen werden. Stellen Sie sicher, dass die Zieltabelle in der Datenbank verfügbar ist.|  
|0xC020204B|-1071636405|DTS_E_CANTLOCKBUFFER|Ein Puffer konnte nicht gesperrt werden. Es ist nicht genügend Arbeitsspeicher verfügbar, oder das Kontingent des Puffer-Managers ist erreicht.|  
|0xC020204C|-1071636404|DTS_E_INVALIDCOMPARISONFLAGS|%1 weist eine ComparisonFlags-Eigenschaft auf, die zusätzliche Flags mit dem Wert %2!d! enthält.|  
|0xC020204D|-1071636403|DTS_E_COLUMNMETADATAUNAVAILABLEFORVALIDATION|Die Spaltenmetadaten waren für die Überprüfung nicht verfügbar.|  
|0xC0202053|-1071636397|DTS_E_CANNOTWRITETODATAFILE|In die Datendatei kann nicht geschrieben werden.|  
|0xC0202055|-1071636395|DTS_E_COLUMNDELIMITERNOTFOUND|Das Spaltentrennzeichen für die Spalte "%1" wurde nicht gefunden.|  
|0xC0202058|-1071636392|DTS_E_COLUMNPARSEFAILED|Fehler beim Analysieren der Spalte "%1" in der Datendatei.|  
|0xC020205A|-1071636390|DTS_E_RAWFILENAMEREQUIRED|Der Dateiname wurde nicht ordnungsgemäß angegeben.  Geben Sie den Pfad und den Namen für die Rohdatendatei direkt in der FileName-Eigenschaft oder mithilfe einer Variablen in der FileNameVariable-Eigenschaft ein.|  
|0xC020205B|-1071636389|DTS_E_RAWFILECANTOPEN|Die Datei "%1" kann nicht zum Schreiben geöffnet werden. Dieser Fehler tritt auf, wenn keine Dateiprivilegien vorhanden sind oder der Datenträger voll ist.|  
|0xC020205C|-1071636388|DTS_E_RAWFILECANTBUFFER|Für die Ausgabedatei kann kein E/A-Puffer erstellt werden. Dieser Fehler tritt auf, wenn keine Dateiprivilegien vorhanden sind oder der Datenträger voll ist.|  
|0xC020205D|-1071636387|DTS_E_RAWCANTWRITE|%1! d! Bytes können nicht in die Datei "%2" geschrieben werden. Weitere Informationen finden Sie in den vorherigen Fehlermeldungen.|  
|0xC020205E|-1071636386|DTS_E_RAWBADHEADER|Im Dateiheader wurden fehlerhafte Metadaten gefunden. Die Datei ist beschädigt oder keine von SSIS erstellte Rohdatendatei.|  
|0xC020205F|-1071636385|DTS_E_RAWEXISTSCREATEONCE|Fehler, weil die Ausgabedatei bereits vorhanden ist und die WriteOption-Eigenschaft auf Create Once festgelegt ist. Legen Sie die WriteOption-Eigenschaft auf Create Always fest, oder löschen Sie die Datei.|  
|0xC0202060|-1071636384|DTS_E_RAWCANTAPPENDTRUNCATE|Der Fehler wird durch miteinander in Konflikt stehende Eigenschaftseinstellungen verursacht. Die AllowAppend-Eigenschaft und die ForceTruncate-Eigenschaft sind auf TRUE festgelegt. Beide Eigenschaften dürfen nicht auf TRUE festgelegt sein. Legen Sie eine der beiden Eigenschaften auf FALSE fest.|  
|0xC0202061|-1071636383|DTS_E_RAWBADVERSION|Die Datei weist fehlerhafte Versions- und Flaginformationen auf. Die Datei ist beschädigt oder keine von SSIS erstellte Rohdatendatei.|  
|0xC0202062|-1071636382|DTS_E_RAWVERSIONINCOMPATIBLEAPPEND|Die Ausgabedatei wurde von einer inkompatiblen Version geschrieben und kann nicht angefügt werden. Möglicherweise weist die Datei ein älteres Dateiformat auf, das nicht mehr verwendet werden kann.|  
|0xC0202064|-1071636380|DTS_E_RAWMETADATAMISMATCH|Die Ausgabedatei kann nicht angefügt werden, weil in der vorhandenen Datei keine Spalte mit der Spalte "%1" aus der Eingabe übereinstimmt. Die alte Datei stimmt nicht mit den Metadaten überein.|  
|0xC0202065|-1071636379|DTS_E_RAWMETADATACOUNTMISMATCH|Die Ausgabedatei kann nicht angefügt werden, weil die Spaltenanzahl in der Ausgabedatei nicht mit der Spaltenanzahl in diesem Ziel übereinstimmt. Die alte Datei stimmt nicht mit den Metadaten überein.|  
|0xC0202067|-1071636377|DTS_E_ERRORRETRIEVINGCOLUMNCODEPAGE|Fehler beim Abrufen der Codepageinformationen für Spalten.|  
|0xC0202068|-1071636376|DTS_E_RAWCANTREAD|Fehler beim Lesen der %1! d! Bytes aus der Datei "%2". Die Ursache für diesen Fehler sollte vorher angezeigt worden sein.|  
|0xC0202069|-1071636375|DTS_E_RAWUNEXPECTEDEOF|Unerwartetes Dateiende beim Lesen von %1!d! Bytes aus der Datei "%2". Die Datei endete aufgrund eines ungültigen Dateiformats vorzeitig.|  
|0xC020206A|-1071636374|DTS_E_RAWNOLONGTYPES|Die Spalte %1 kann nicht verwendet werden. Daten vom Typ image, text oder ntext werden von den Rohdatenadaptern nicht unterstützt.|  
|0xC020206B|-1071636373|DTS_E_RAWUNEXPECTEDTYPE|Der Adapter hat den unbekannten Datentyp %1!d! gefunden. Dieses Problem kann auf eine beschädigte Eingabedatei (Quelle) oder einen ungültigen Puffertyp (Ziel) zurückzuführen sein.|  
|0xC020206C|-1071636372|DTS_E_RAWSTRINGTOOLONG|Die Zeichenfolge ist zu lang. Der Adapter hat eine Zeichenfolge gelesen, die %1!d! Bytes lang war, erwartet wurde jedoch eine Zeichenfolge mit maximal %2!d! Bytes und einem Offset von %3!d!. Dies kann ein Hinweis auf eine beschädigte Eingabedatei sein. Die Datei weist eine für die Pufferspalte zu lange Zeichenfolge auf.|  
|0xC020206E|-1071636370|DTS_E_RAWSKIPFAILED|Der Rohdatenadapter hat versucht, %1!d! Bytes in der Eingabedatei für die unreferenzierte Spalte "%2" mit der Herkunfts-ID %3!d! auszulassen. Es wurde jedoch ein Fehler gemeldet. Der vom Betriebssystem zurückgegebene Fehler sollte vorher angezeigt worden sein.|  
|0xC020206F|-1071636369|DTS_E_RAWREADFAILED|Der Rohdatenadapter hat versucht, %1!d! Bytes in der Eingabedatei für die Spalte "%2" mit der Herkunfts-ID %3!d! zu lesen. Es wurde jedoch ein Fehler gemeldet. Der vom Betriebssystem zurückgegebene Fehler sollte vorher angezeigt worden sein.|  
|0xC0202070|-1071636368|DTS_E_RAWFILENAMEINVALID|Die Dateinameneigenschaft ist ungültig. Der Dateiname ist ein Gerät oder enthält ungültige Zeichen.|  
|0xC0202071|-1071636367|DTS_E_BULKINSERTAPIPREPARATIONFAILED|Die SSIS-Masseneinfügung kann zum Einfügen von Daten nicht vorbereitet werden.|  
|0xC0202072|-1071636366|DTS_E_INVALIDDATABASEOBJECTNAME|Der Datenbank-Objektname "%1" ist ungültig.|  
|0xC0202073|-1071636365|DTS_E_INVALIDORDERCLAUSE|Die ORDER-Klausel ist ungültig.|  
|0xC0202074|-1071636364|DTS_E_RAWFILECANTOPENREAD|Die Datei "%1" kann nicht zum Lesen geöffnet werden. Dieser Fehler tritt auf, wenn keine Privilegien vorhanden sind oder die Datei nicht gefunden wird. Die genaue Ursache wurde in der vorherigen Fehlermeldung angezeigt.|  
|0xC0202075|-1071636363|DTS_E_TIMEGENCANTCREATE|Microsoft.AnalysisServices.TimeDimGenerator.TimeDimGenerator kann nicht erstellt werden.|  
|0xC0202076|-1071636362|DTS_E_TIMEGENCANTCONFIGURE|Microsoft.AnalysisServices.TimeDimGenerator kann nicht konfiguriert werden.|  
|0xC0202077|-1071636361|DTS_E_TIMEGENCANTCONVERT|Dieser Datentyp wird von der Spalte %1!d! nicht unterstützt.|  
|0xC0202079|-1071636359|DTS_E_TIMEGENCANTREAD|Fehler beim Lesen aus Microsoft.AnalysisServices.TimeDimGenerator (Fehlercode: 0x%1!8.8X!).|  
|0xC020207A|-1071636358|DTS_E_TIMEGENCANTREADCOLUMN|Fehler beim Lesen der Daten aus Spalte „%2!d!“ aus Microsoft.AnalysisServices.TimeDimGenerator (Fehlercode: 0x%2!8.8X!).|  
|0xC020207B|-1071636357|DTS_E_RSTDESTBADVARIABLENAME|Für die VariableName-Eigenschaft ist kein Name einer gültigen Variablen festgelegt. Der Name einer Laufzeitvariablen, in die geschrieben werden kann, ist erforderlich.|  
|0xC020207C|-1071636356|DTS_E_RSTDESTRSTCONFIGPROBLEM|Das ADODB.Recordset-Objekt kann nicht erstellt oder konfiguriert werden.|  
|0xC020207D|-1071636355|DTS_E_RSTDESTRSTWRITEPROBLEM|Fehler beim Schreiben in das ADODB.Recordset-Objekt.|  
|0xC020207E|-1071636354|DTS_E_FILENAMEINVALID|Der Dateiname ist ungültig. Der Dateiname ist ein Gerät oder enthält ungültige Zeichen.|  
|0xC020207F|-1071636353|DTS_E_FILENAMEINVALIDWITHPARAM|Der Dateiname "%1" ist ungültig. Der Dateiname ist ein Gerät oder enthält ungültige Zeichen.|  
|0xC0202080|-1071636352|DTS_E_CMDDESTNOPARAMS|Zielspaltenbeschreibungen können nicht aus den Parametern des SQL-Befehls abgerufen werden.|  
|0xC0202081|-1071636351|DTS_E_CMDDESTNOTBOUND|Die Parameter sind nicht gebunden. Alle Parameter im SQL-Befehl müssen an Eingabespalten gebunden sein.|  
|0xC0202082|-1071636350|DTS_E_TXPIVOTBADUSAGE|Der PivotUsage-Wert für die Eingabespalte "%1" (%2!d!) ist ungültig.|  
|0xC0202083|-1071636349|DTS_E_TXPIVOTTOOMANYPIVOTKEYS|Zu viele Pivotschlüssel wurden gefunden. Nur eine Eingabespalte kann als Pivotschlüssel verwendet werden.|  
|0xC0202084|-1071636348|DTS_E_TXPIVOTNOPIVOTKEY|Ein Pivotschlüssel wurde nicht gefunden. Eine Eingabespalte muss als Pivotschlüssel verwendet werden.|  
|0xC0202085|-1071636347|DTS_E_TXPIVOTINPUTALREADYMAPPED|Mehrere Ausgabespalten (z. B. "%1" (%2!d!)) sind der Eingabespalte "%3" (%4!d!) zugeordnet.|  
|0xC0202086|-1071636346|DTS_E_TXPIVOTCANTMAPPIVOTKEY|Die Ausgabespalte "%1" (%2!d!) darf nicht der PivotKey-Eingabespalte zugeordnet werden.|  
|0xC0202087|-1071636345|DTS_E_TXPIVOTCANTMAPPINGNOTFOUND|Die Ausgabespalte "%1" (%2!d!) weist den SourceColumn-Wert %3!d! auf, der keine gültige Eingabespalten-Herkunfts-ID darstellt.|  
|0xC0202088|-1071636344|DTS_E_TXPIVOTEMPTYPIVOTKEYVALUE|Die Ausgabespalte "%1" (%2!d!) ist der Eingabespalte vom Typ Pivotierter Wert zugeordnet, aber ihr PivotKeyValue-Eigenschaftswert fehlt.|  
|0xC0202089|-1071636343|DTS_E_TXPIVOTDUPLICATEPIVOTKEYVALUE|Die Ausgabespalte "%1" (%2!d!) ist der Eingabespalte vom Typ Pivotierter Wert mit einem nicht eindeutigen PivotKeyValue-Eigenschaftswert zugeordnet.|  
|0xC020208A|-1071636342|DTS_E_TXPIVOTOUTPUTNOTMAPPED|Die Eingabespalte "%1" (%2!d!) ist keiner Ausgabespalte zugeordnet.|  
|0xC020208B|-1071636341|DTS_E_TXPIVOTCANTCOMPARESETKEYS|Fehler beim Vergleichen von Werten für die festgelegten Schlüssel.|  
|0xC020208D|-1071636339|DTS_E_TXPIVOTNOBLOB|Die Eingabespalte "%1" (%2!d!) kann nicht als Spalte des Typs Schlüssel festlegen, Pivotschlüssel oder Pivotierter Wert verwendet werden, weil sie Long-Daten enthält|  
|0xC020208E|-1071636338|DTS_E_TXPIVOTBADOUTPUTTYPE|Falscher Ausgabetyp. Die Ausgabespalte "%1" (%2!d!) erfordert denselben Datentyp und dieselben Metadaten wie die Eingabespalte, der sie zugeordnet ist.|  
|0xC020208F|-1071636337|DTS_E_TXPIVOTPROCESSERROR|Fehler beim Pivotieren der Quelldatensätze.|  
|0xC0202090|-1071636336|DTS_E_TXPIVOTBADPIVOTKEYVALUE|Der Pivotschlüsselwert "%1" ist ungültig.|  
|0xC0202091|-1071636335|DTS_E_ERRORWHILESKIPPINGDATAROWS|Fehler beim Auslassen von Datenzeilen.|  
|0xC0202092|-1071636334|DTS_E_ERRORWHILEREADINGDATAROWS|Fehler beim Verarbeiten der Datei "%1" in der Datenzeile %2!I64d!.|  
|0xC0202093|-1071636333|DTS_E_FAILEDTOINITIALIZEFLATFILEPARSER|Fehler beim Initialisieren des Flatfileparsers.|  
|0xC0202094|-1071636332|DTS_E_UNABLETORETRIEVECOLUMNINFOFROMFLATFILECONNECTIONMANAGER|Spalteninformationen konnten nicht aus dem Verbindungs-Manager für Flatfiles abgerufen werden.|  
|0xC0202095|-1071636331|DTS_E_FAILEDTOWRITEOUTCOLUMNNAME|Fehler beim Schreiben des Spaltennamens für die Spalte "%1".|  
|0xC0202096|-1071636330|DTS_E_INVALIDFLATFILECOLUMNTYPE|Falscher Spaltentyp für die Spalte "%1". Der Spaltentyp lautet "%2". Zulässig sind jedoch nur "%3" oder "%4".|  
|0xC0202097|-1071636329|DTS_E_DISKIOBUFFEROVERFLOW|Fehler beim Versuch, Daten mit %1!d! Bytes in den Datenträger-E/A zu schreiben. Der Datenträger-E/A-Puffer weist %2!d! freie Bytes auf.|  
|0xC0202098|-1071636328|DTS_E_FAILEDTOWRITEOUTHEADER|Fehler beim Schreiben des Dateiheaders.|  
|0xC0202099|-1071636327|DTS_E_FAILEDTOGETFILESIZE|Fehler beim Abrufen der Dateigröße für die Datei "%1".|  
|0xC020209A|-1071636326|DTS_E_FAILEDTOSETFILEPOINTER|Fehler beim Festlegen des Dateizeigers für die Datei "%1".|  
|0xC020209B|-1071636325|DTS_E_UNABLETOSETUPDISKIOBUFFER|Fehler beim Einrichten des Datenträger-E-A-Puffers.|  
|0xC020209C|-1071636324|DTS_E_COLUMNDATAOVERFLOWDISKIOBUFFER|Überlauf der Spaltendaten für die Spalte "%1" im Datenträger-E/A-Puffer.|  
|0xC020209D|-1071636323|DTS_E_DISKIOFAILED|Unerwarteter Datenträger-E/A-Fehler beim Lesen der Datei.|  
|0xC020209E|-1071636322|DTS_E_DISKIOTIMEDOUT|Datenträger-E/A-Timeout beim Lesen der Datei.|  
|0xC020209F|-1071636321|DTS_E_INPUTSNOTREADONLY|Der für die Eingabespalten angegebene Verwendungstyp für die Transformation kann nicht gelesen/geschrieben werden. Ändern Sie den Verwendungstyp, sodass er schreibgeschützt ist.|  
|0xC02020A0|-1071636320|DTS_E_CANNOTCOPYORCONVERTFLATFILEDATA|Flatfiledaten für die Spalte "%1" können nicht kopiert oder konvertiert werden.|  
|0xC02020A1|-1071636319|DTS_E_FAILEDCOLUMNDATACONVERSIONSTATUS|Fehler bei der Datenkonvertierung. Die Datenkonvertierung für die Spalte "%1" hat den Statuswert %2!d! und den Statustext "%3" zurückgegeben.|  
|0xC02020A2|-1071636318|DTS_E_VARIABLESCOLLECTIONUNAVAILABLE|Die Variables-Auflistung ist nicht verfügbar.|  
|0xC02020A3|-1071636317|DTS_E_TXUNPIVOTDUPLICATEPIVOTKEYVALUE|Das PivotKeyValue-Objekt ist doppelt vorhanden. Die Eingabespalte "%1" (%2!d!) ist der Ausgabespalte vom Typ Pivotierter Wert zugeordnet und weist ein nicht eindeutiges PivotKeyValue-Objekt auf.|  
|0xC02020A4|-1071636316|DTS_E_TXUNPIVOTNOUNPIVOTDESTINATION|Ein Entpivotierungsziel wurde nicht gefunden. Mindestens eine Eingabespalte muss mit einem PivotKeyValue-Objekt einem DestinationColumn-Objekt in der Ausgabe zugeordnet werden.|  
|0xC02020A5|-1071636315|DTS_E_TXUNPIVOTBADKEYLIST|Ungültiges PivotKeyValue-Objekt. Bei einer UnPivot-Transformation mit mehreren entpivotierten DestinationColumn-Objekten müssen die PivotKeyValues-Objekte pro Ziel genau übereinstimmen.|  
|0xC02020A6|-1071636314|DTS_E_TXUNPIVOTBADUNPIVOTMETADATA|Falsche UnPivot-Metadaten. Bei einer UnPivot-Transformation müssen für alle Eingabespalten mit einem festgelegten PivotKeyValue-Objekt, die auf dasselbe DestinationColumn-Objekt zeigen, die Metadaten genau mit dem DestinationColumn-Objekt übereinstimmen.|  
|0xC02020A7|-1071636313|DTS_E_TXPIVOTBADPIVOTKEYCONVERT|Der Pivotschlüsselwert "%1" kann nicht in den Datentyp der Pivotschlüsselspalte konvertiert werden.|  
|0xC02020A8|-1071636312|DTS_E_TXUNPIVOTTOOMANYPIVOTKEYS|Es sind zu viele Pivotschlüssel angegeben. Nur eine Ausgabespalte kann als Pivotschlüssel verwendet werden.|  
|0xC02020A9|-1071636311|DTS_E_TXUNPIVOTUNMAPPEDOUTPUT|Die Ausgabespalte "%1" (%2!d!) weist keine Zuordnung durch eine DestinationColumn-Eigenschaft für Eingabespalten auf.|  
|0xC02020AA|-1071636310|DTS_E_TXUNPIVOTNOPIVOT|Keine Ausgabespalte ist als PivotKey gekennzeichnet.|  
|0xC02020AB|-1071636309|DTS_E_TXUNPIVOTNOTINPUTMAP|Die Eingabespalte "%1" (%2!d!) weist einen DestinationColumn-Eigenschaftswert auf, der nicht auf einen gültigen LineageID-Wert einer Ausgabespalte verweist.|  
|0xC02020AC|-1071636308|DTS_E_TXUNPIVOTDUPLICATEDESTINATION|Fehler aufgrund von doppeltem Ziel. Mehrere nicht pivotierte Eingabespalten sind derselben Zielausgabespalte zugeordnet.|  
|0xC02020AD|-1071636307|DTS_E_TOTALINPUTCOLSCANNOTBEZERO|Es wurden keine Eingabespalten gefunden. Mindestens eine Eingabespalte muss einer Ausgabespalte zugeordnet werden.|  
|0xC02020AE|-1071636306|DTS_E_TXMERGEJOINMUSTHAVESAMENUMBEROFINPUTANDOUTPUTCOLS|Die Anzahl von Eingabe- und Ausgabespalten ist nicht identisch. Die Gesamtanzahl von Eingabespalten in allen Eingaben muss mit der Gesamtanzahl von Ausgabespalten identisch sein.|  
|0xC02020AF|-1071636305|DTS_E_INPUTMUSTBESORTED|Die Eingabe ist nicht sortiert. "%1" muss sortiert werden.|  
|0xC02020B0|-1071636304|DTS_E_TXMERGEJOININVALIDJOINTYPE|Die benutzerdefinierte Eigenschaft JoinType für %l enthält den ungültigen Wert %2!ld!. Gültige Werte sind 0 (vollständiger Join), 1 (linker Join) und 2 (innerer Join).|  
|0xC02020B1|-1071636303|DTS_E_TXMERGEJOININVALIDNUMKEYCOLS|Der NumKeyColumns-Wert ist ungültig. In %1 muss der Wert für die benutzerdefinierte Eigenschaft NumKeyColumns zwischen 1 und %2!lu! liegen.|  
|0xC02020B2|-1071636302|DTS_E_NOKEYCOLS|Es wurden keine Schlüsselspalten gefunden. %1 erfordert mindestens eine Spalte mit einem SortKeyPosition-Wert, der ungleich 0 (null) ist.|  
|0xC02020B3|-1071636301|DTS_E_TXMERGEJOINNOTENOUGHKEYCOLS|Nicht genügend Schlüsselspalten. % 1 muss mindestens %2!ld! Spalten mit SortKeyPosition-Werten ungleich 0 (null) aufweisen.|  
|0xC02020B4|-1071636300|DTS_E_TXMERGEJOINDATATYPEMISMATCH|Nichtübereinstimmung beim Datentyp. Die Datentypen für die Spalten mit dem SortKeyPosition-Wert %1!ld! stimmen nicht überein.|  
|0xC02020B5|-1071636299|DTS_E_TXMERGEJOININVALIDSORTKEYPOS|Die Spalte mit dem SortKeyPosition-Wert %1!ld! ist ungültig. Der Wert muss %2!ld! betragen.|  
|0xC02020B6|-1071636298|DTS_E_TXMERGEJOINSORTDIRECTIONMISMATCH|Nichtübereinstimmung bei der Sortierrichtung. Die Sortierrichtungen für die Spalten mit dem SortKeyPosition-Wert %1!ld! stimmen nicht überein.|  
|0xC02020B7|-1071636297|DTS_E_TXMERGEJOINOUTPUTCOLMUSTHAVEASSOCIATEDINPUTCOL|Eine Spalte fehlt. %1 muss eine Eingabespalte zugeordnet sein.|  
|0xC02020B8|-1071636296|DTS_E_TXMERGEJOINREADONLYINPUTCOLSWITHNOOUTPUTCOL|Eingabespalten erfordern Ausgabespalten. Es gibt Eingabespalten, die laut Verwendungstyp schreibgeschützt sind und denen keine Ausgabespalten zugeordnet sind.|  
|0xC02020B9|-1071636295|DTS_E_TXMERGEJOINNONSTRINGCOMPARISONFLAGSNOTZERO|Die Vergleichsflags sind ungleich 0 (null). Die Vergleichsflags für andere als Zeichenfolgenspalten müssen gleich 0 (null) sein.|  
|0xC02020BA|-1071636294|DTS_E_TXMERGEJOINCOMPARISONFLAGSMISMATCH|Die Vergleichsflags für die Spalten mit dem SortKeyPosition-Wert %1!ld! stimmen nicht überein.|  
|0xC02020BB|-1071636293|DTS_E_TXPIVOTBADPIVOTKEYVALUENOSTRING|Unbekannter Pivotschlüsselwert.|  
|0xC02020BC|-1071636292|DTS_E_TXLINEAGEINVALIDLINEAGEITEM|Der Herkunftselementwert %1!ld! ist ungültig. Der gültige Bereich liegt zwischen %2!ld! und %3!ld! liegen.|  
|0xC02020BD|-1071636291|DTS_E_CANNOTHAVEANYINPUTCOLUMNS|Eingabespalten sind nicht zulässig. Die Anzahl von Eingabespalten muss 0 (null) sein.|  
|0xC02020BE|-1071636290|DTS_E_TXLINEAGEDATATYPEMISMATCH|Der Datentyp für "%1" ist für das angegebene Herkunftselement ungültig.|  
|0xC02020BF|-1071636289|DTS_E_TXLINEAGEINVALIDLENGTH|Die Länge für "%1" ist für das angegebene Herkunftselement ungültig.|  
|0xC02020C1|-1071636287|DTS_E_METADATAMISMATCHWITHOUTPUTCOLUMN|Die Metadaten für "%1" stimmen nicht mit den Metadaten für die zugehörige Ausgabespalte überein.|  
|0xC02020C3|-1071636285|DTS_E_TXMERGESORTKEYPOSMISMATCH|Es sind Ausgabespalten mit SortKeyPosition-Werten vorhanden, die nicht mit den SortKeyPosition-Werten der zugehörigen Eingabespalten übereinstimmen.|  
|0xC02020C4|-1071636284|DTS_E_ADDROWTOBUFFERFAILED|Fehler beim Hinzufügen einer Zeile zum Datenflusstask-Puffer (Fehlercode: 0x%1!8.8X!).|  
|0xC02020C5|-1071636283|DTS_E_DATACONVERSIONFAILED|Datenkonvertierungsfehler beim Konvertieren der Spalte "%1" (%2!d!) in die Spalte "%3" (%4!d!).  Die Konvertierung hat den Statuswert %5!d! und den Statustext "%6" zurückgegeben.|  
|0xC02020C6|-1071636282|DTS_E_FAILEDTOALLOCATEROWHANDLEBUFFER|Fehler beim Zuordnen eines Zeilenhandlepuffers (Fehlercode: 0x%1!8.8X!).|  
|0xC02020C7|-1071636281|DTS_E_FAILEDTOSENDROWTOSQLSERVER|Fehler beim Senden einer Zeile an SQL Server (Fehlercode: 0x%1!8.8X!).|  
|0xC02020C8|-1071636280|DTS_E_FAILEDTOPREPAREBUFFERSTATUS|Fehler beim Vorbereiten des Pufferstatus (Fehlercode: 0x%1!8.8X!).|  
|0xC02020C9|-1071636279|DTS_E_FAILEDTOBUFFERROWSTARTS|Fehler beim Abrufen des Beginns der Pufferzeile (Fehlercode: 0x%1!8.8X!).|  
|0xC02020CA|-1071636278|DTS_E_BULKINSERTTHREADTERMINATED|Der Thread für den Masseneinfügungstask von SSIS wird nicht mehr ausgeführt.  Es können keine Zeilen mehr eingefügt werden. Erhöhen Sie den Timeout für den Masseneinfügungsthread.|  
|0xC02020CB|-1071636277|DTS_E_RAWTOOMANYCOLUMNS|Die Quelldatei ist ungültig. Die Quelldatei gibt mehr als 131.072 Spalten zurück. Dieser Fehler tritt gewöhnlich auf, wenn die Quelldatei nicht vom Rohdatendateiziel erstellt wird.|  
|0xC02020CC|-1071636276|DTS_E_TXUNIONALL_EXTRADANGLINGINPUT|%1 ist eine zusätzliche, nicht angefügte Eingabe und wird entfernt.|  
|0xC02020CD|-1071636275|DTS_E_TXUNIONALL_NONDANGLINGUNATTACHEDINPUT|%1 ist nicht angefügt, aber auch nicht als verbleibend gekennzeichnet.  Die Kennzeichnung als verbleibend erfolgt.|  
|0xC02020CF|-1071636273|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUE|Doppelter Pivotschlüsselwert "%1".|  
|0xC02020D0|-1071636272|DTS_E_TXPIVOTRUNTIMEDUPLICATEPIVOTKEYVALUENOSTRING|Doppelter Pivotschlüsselwert.|  
|0xC02020D1|-1071636271|DTS_E_FAILEDTOGETCOMPONENTLOCALEID|Fehler beim Abrufen der Gebietsschema-ID der Komponente. Fehlercode: 0x%1!8.8X!.|  
|0xC02020D2|-1071636270|DTS_E_MISMATCHCOMPONENTCONNECTIONMANAGERLOCALEID|Nichtübereinstimmung bei den Gebietsschema-IDs. Die Gebietsschema-ID der Komponente (%1!d!) stimmt nicht mit der Gebietsschema-ID des Verbindungs-Managers (%2!d!) überein.|  
|0xC02020D3|-1071636269|DTS_E_LOCALEIDNOTSET|Die Gebietsschema-ID der Komponente wurde nicht festgelegt. Für Flatfileadapter muss die Gebietsschema-ID im Verbindungs-Manager für Flatfiles festgelegt sein.|  
|0xC02020D4|-1071636268|DTS_E_RAWBYTESTOOLONG|Das binäre Feld ist zu groß. Der Adapter hat versucht, ein binäres Feld zu lesen, das %1!d! Bytes lang war, erwartet wurde jedoch ein Feld mit maximal %2!d! Bytes und einem Offset von %3!d!. Dieser Fehler tritt gewöhnlich auf, wenn die Eingabedatei ungültig ist. Die Datei weist eine für die Pufferspalte zu lange Zeichenfolge auf.|  
|0xC02020D5|-1071636267|DTS_E_TXSAMPLINGINVALIDPCT|Der Prozentsatz %2!ld! ist für die Eigenschaft "%1" ungültig. Der Wert muss zwischen „0“ und „100“ liegen.|  
|0xC02020D6|-1071636266|DTS_E_TXSAMPLINGINVALIDROWS|Die Anzahl von %2!ld! Zeilen ist für die Eigenschaft "%1" ungültig. Dieser Wert muss größer als 0 (null) sein.|  
|0xC02020D7|-1071636265|DTS_E_RAWSTRINGINPUTTOOLONG|Der Adapter wurde aufgefordert, eine Zeichenfolge zu schreiben, die %1!I64d! Bytes lang war, alle Daten zusammen dürfen jedoch maximal 4.294.967.294 Bytes aufweisen.|  
|0xC02020D9|-1071636263|DTS_E_ATLEASTONEINPUTMUSTBEMAPPEDTOOUTPUT|Der Ausgabe wurden keine Eingaben zugeordnet. Für "%1" muss mindestens eine Eingabespalte einer Ausgabespalte zugeordnet sein.|  
|0xC02020DB|-1071636261|DTS_E_CANNOTCONVERTDATATYPESWITHDIFFERENTCODEPAGES|Konvertierung von "% 1" mit Codepage %2!d! in "%3" mit Codepage %4!d! wird nicht unterstützt.|  
|0xC02020DC|-1071636260|DTS_E_COLUMNNOTMAPPEDTOEXTERNALMETADATACOLUMN|Die Zuordnung der externen Metadatenspalte für %1 ist ungültig.  Die externe Metadatenspalten-ID darf nicht gleich 0 (null) sein.|  
|0xC02020DD|-1071636259|DTS_E_COLUMNMAPPEDTONONEXISTENTEXTERNALMETADATACOLUMN|%1 ist einer externen Metadatenspalte zugeordnet, die nicht vorhanden ist.|  
|0xC02020E5|-1071636251|DTS_E_UNABLETOWRITELOBDATATOBUFFER|Fehler beim Schreiben der Long-Objektdaten vom Typ DT_TEXT, DT_NTEXT oder DT_IMAGE in den Datenflusstask-Puffer der Spalte "%1".|  
|0xC02020E8|-1071636248|DTS_E_CANNOTGETIROWSET|Fehler beim Öffnen eines Rowsets für "%1". Überprüfen Sie, ob das Objekt in der Datenbank vorhanden ist.|  
|0xC02020E9|-1071636247|DTS_E_VARIABLEACCESSFAILED|Fehler beim Zugriff auf die Variable "%1" (Fehlercode: 0x%2!8.8X!).|  
|0xC02020EA|-1071636246|DTS_E_CONNECTIONMANAGERNOTFOUND|Der Verbindungs-Manager "%1" wurde nicht gefunden. Eine Komponente konnte den Verbindungs-Manager nicht in der Connections-Auflistung finden.|  
|0xC02020EB|-1071636245|DTS_E_VERSIONUPGRADEFAILED|Fehler beim Aktualisieren von Version "%1" auf Version %2!d! .|  
|0xC02020EC|-1071636244|DTS_E_RSTDESTBIGBLOB|Ein Wert in einer Eingabespalte ist für das Speichern im ADODB.Recordset-Objekt zu groß.|  
|0xC02020ED|-1071636243|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Die Spalten "%1" und "%2" können nicht zwischen Unicode- und Nicht-Unicode-Zeichenfolgendatentypen konvertiert werden.|  
|0xC02020EE|-1071636242|DTS_E_ROWCOUNTBADVARIABLENAME|Die von der VariableName-Eigenschaft angegebene Variable "%1" ist ungültig. Der Name einer Variablen ist erforderlich, in die geschrieben werden kann.|  
|0xC02020EF|-1071636241|DTS_E_ROWCOUNTBADVARIABLETYPE|Die von der VariableName-Eigenschaft angegebene Variable "%1" ist keine ganze Zahl. Ändern Sie die Variable in den Datentyp VT_I4, VT_UI4, VT_I8 oder VT_UI8.|  
|0xC02020F0|-1071636240|DTS_E_NOCOLUMNADVANCETHROUGHFILE|Für die Komponente wurde keine Spalte zum Fortsetzen der Verarbeitung in der Datei angegeben.|  
|0xC02020F1|-1071636239|DTS_E_MERGEJOINSORTEDOUTPUTHASNOSORTKEYPOSITIONS|Für "%1" ist die IsSorted-Eigenschaft auf TRUE festgelegt, aber die SortKeyPosition-Eigenschaft ist in allen Ausgabespalten gleich 0 (null). Legen Sie die IsSorted-Eigenschaft auf FALSE fest, oder wählen Sie mindestens eine Ausgabespalte aus, die eine SortKeyPosition-Eigenschaft ungleich 0 (null) enthalten soll.|  
|0xC02020F2|-1071636238|DTS_E_METADATAMISMATCHWITHINPUTCOLUMN|Die "%1"-Metadaten stimmen nicht mit den Metadaten der Eingabespalte überein.|  
|0xC02020F3|-1071636237|DTS_E_RSTDESTBADVARIABLE|Der Wert der angegebenen Variablen kann nicht gefunden, gesperrt oder festgelegt werden.|  
|0xC02020F4|-1071636236|DTS_E_CANTPROCESSCOLUMNTYPECODEPAGE|Die Spalte "%1" kann nicht verarbeitet werden, weil mehrere Codepages (%2!d! und %3!d!) dafür angegeben wurden.|  
|0xC02020F5|-1071636235|DTS_E_CANTINSERTCOLUMNTYPE|Die Spalte "%1" kann nicht eingefügt werden, weil die Konvertierung zwischen den Typen %2 und %3 nicht unterstützt wird.|  
|0xC02020F6|-1071636234|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Die Spalte "%1" kann nicht zwischen Unicode- und Nicht-Unicode-Zeichenfolgendatentypen konvertiert werden.|  
|0xC02020F8|-1071636232|DTS_E_COULDNOTFINDINPUTBUFFERCOLUMNBYLINEAGE|%1 kann die Spalte mit dem LineageID-Wert %2!ld! im Eingabepuffer nicht finden.|  
|0xC02020F9|-1071636231|DTS_E_COULDNOTGETCOLUMNINFOFORINPUTBUFFER|%1 kann die Spalteninformationen für die Spalte %2!lu! nicht aus dem Eingabepuffer abrufen.|  
|0xC02020FA|-1071636230|DTS_E_COULDNOTGETCOLUMNINFOFORCOPYBUFFER|„%1“ kann die Spalteninformationen für die Spalte „%2!lu!“ nicht aus dem Kopierpuffer erhalten.|  
|0xC02020FB|-1071636229|DTS_E_COULDNOTREGISTERCOPYBUFFER|%1 kann einen Puffertyp nicht für den Kopierpuffer registrieren.|  
|0xC02020FC|-1071636228|DTS_E_COULDNOTCREATECOPYBUFFER|%1 kann keinen Puffer erstellen, um die Daten zum Sortieren zu kopieren.|  
|0xC02020FD|-1071636227|DTS_E_DATAREADERDESTREADFAILED|Fehler vom DataReader-Client beim Aufrufen von Read, oder das DataReader-Objekt wurde geschlossen.|  
|0xC02020FE|-1071636226|DTS_E_NOSCHEMAINFOFOUND|Der SQL-Befehl hat keine Spalteninformationen zurückgegeben.|  
|0xC02020FF|-1071636225|DTS_E_GETSCHEMATABLEFAILED|%1 konnte keine Spalteninformationen für den SQL-Befehl abrufen. Folgender Fehler ist aufgetreten: %2|  
|0xC0202100|-1071636224|DTS_E_SOURCETABLENAMENOTPROVIDED|Es wurde kein Quelltabellenname angegeben.|  
|0xC0203110|-1071632112|DTS_E_CACHE_INVALID_INDEXPOS|Die Cacheindexposition %1!d! ist ungültig. Die Indexposition für Nicht-Indexspalten sollte 0 sein. Bei Indexspalten sollte die Indexposition eine sequenzielle, positive Zahl sein.|  
|0xC0203111|-1071632111|DTS_E_CACHE_DUPLICATE_INDEXPOS|Die Indexposition %1!d! ist bereits vorhanden. Die Indexposition für Nicht-Indexspalten sollte 0 sein. Bei Indexspalten sollte die Indexposition eine sequenzielle, positive Zahl sein.|  
|0xC0203112|-1071632110|DTS_E_CACHE_TOO_FEW_INDEX_COLUMNS|Es sollte mindestens eine Indexspalte für den Cacheverbindungs-Manager angegeben werden. Legen Sie die Indexpositionseigenschaft der Cachespalte fest, um eine Indexspalte anzugeben.|  
|0xC0203113|-1071632109|DTS_E_CACHE_INDEXPOS_NOT_CONTINUOUS|Cacheindexpositionen müssen zusammenhängend sein. Die Indexposition für Nicht-Indexspalten sollte 0 sein. Bei Indexspalten sollte die Indexposition eine sequenzielle, positive Zahl sein.|  
|0xC0204000|-1071628288|DTS_E_PROPERTYNOTSUPPORTED|Die Eigenschaft "%1" kann in "%2" nicht festgelegt werden. Die festgelegte Eigenschaft wird in dem angegebenen Objekt nicht unterstützt. Überprüfen Sie den Eigenschaftsnamen, die Groß- und Kleinschreibung sowie die Rechtschreibung.|  
|0xC0204002|-1071628286|DTS_E_CANTCHANGEPROPERTYTYPE|Der von der Komponente festgelegte Eigenschaftentyp kann nicht geändert werden.|  
|0xC0204003|-1071628285|DTS_E_CANTADDOUTPUTID|Fehler beim Einfügen von Ausgabe-ID %1!d! . Die neue Ausgabe wurde nicht erstellt.|  
|0xC0204004|-1071628284|DTS_E_CANTDELETEOUTPUTID|Ausgabe-ID %1!d! kann nicht aus der output-Auflistung gelöscht werden.  Möglicherweise ist die ID ungültig, oder die ID ist die Standard- oder Fehlerausgabe.|  
|0xC0204006|-1071628282|DTS_E_FAILEDTOSETPROPERTY|Fehler beim Festlegen der Eigenschaft "%1" für "%2".|  
|0xC0204007|-1071628281|DTS_E_FAILEDTOSETOUTPUTCOLUMNTYPE|Fehler beim Festlegen des Typs „%1“ auf Typ: „%2“, Länge: %3!d!, Genauigkeit: %4!d!, Dezimalstellen: %5!d!, Codepage: %6!d!.|  
|0xC0204008|-1071628280|DTS_E_MORETHANONEERROROUTPUTFOUND|In der Komponente wurden mehrere Fehlerausgaben gefunden, aber nur eine Fehlerausgabe ist zulässig.|  
|0xC020400A|-1071628278|DTS_E_CANTSETOUTPUTCOLUMNPROPERTY|Die Eigenschaft in einer Ausgabespalte kann nicht festgelegt werden.|  
|0xC020400B|-1071628277|DTS_E_CANTMODIFYERROROUTPUTCOLUMNDATATYPE|Der Datentyp für "%1" kann im Fehler "%2" nicht geändert werden.|  
|0xC020400E|-1071628274|DTS_E_CANONLYSETISSORTEDONSOURCE|Für "%1" kann die IsSorted-Eigenschaft nicht auf TRUE festgelegt werden, weil es sich nicht um eine Quellausgabe handelt. Quellausgaben haben einen SynchronousInputID-Wert von 0 (null).|  
|0xC020400F|-1071628273|DTS_E_CANONLYSETSORTKEYONSOURCE|Für "%1" kann eine SortKeyPosition-Eigenschaft nicht auf einen Wert ungleich 0 (null) festgelegt werden, weil "%2" keine Quellausgabe ist. Für die Ausgabespalte colname (ID) kann die SortKeyPosition-Eigenschaft nicht auf einen Wert ungleich 0 (null) festgelegt werden, weil ihre Ausgabe outputname (ID) keine Quellausgabe ist.|  
|0xC0204010|-1071628272|DTS_E_CANONLYSETCOMPFLAGSONSOURCE|Die ComparisonFlags-Eigenschaft kann für "%1" nicht auf einen Wert ungleich 0 (null) festgelegt werden, weil "%2" keine Quellausgabe ist. Für die Ausgabespalte colname (ID) kann eine ComparisonFlags-Eigenschaft nicht auf einen Wert ungleich 0 (null) festgelegt werden, weil ihre Ausgabe outputname (ID) keine Quellausgabe ist.|  
|0xC0204011|-1071628271|DTS_E_NONSTRINGCOMPARISONFLAGSNOTZERO|Die Vergleichsflags für "%1" müssen 0 (null) lauten, weil es sich nicht um einen Zeichenfolgentyp handelt. ComparisonFlags darf nur für Spalten von einem Zeichenfolgentyp ungleich 0 (null) sein.|  
|0xC0204012|-1071628270|DTS_E_COMPFLAGSONLYONSORTCOL|Für "%1" kann eine ComparisonFlags-Eigenschaft nicht auf einen Wert ungleich 0 (null) festgelegt werden, weil die SortKeyPosition-Eigenschaft auf 0 (null) festgelegt ist. Die ComparisonFlags-Eigenschaft einer Ausgabespalte kann nur ungleich 0 (null) sein, wenn die SortKeyPosition-Eigenschaft ebenfalls ungleich 0 (null) ist.|  
|0xC0204013|-1071628269|DTS_E_READONLYSTOCKPROPERTY|Die Eigenschaft ist schreibgeschützt.|  
|0xC0204014|-1071628268|DTS_E_INVALIDDATATYPE|Für %l wurde ein ungültiger Datentypwert (%2!ld!) festgelegt.|  
|0xC0204015|-1071628267|DTS_E_CODEPAGEREQUIRED|Für "%1" muss eine Codepage festgelegt werden, aber der angegebene Wert lautete 0 (null).|  
|0xC0204016|-1071628266|DTS_E_INVALIDSTRINGLENGTH|"%1" weist eine ungültige Länge auf. Die Länge muss zwischen %2!ld! und %3!ld! liegen.|  
|0xC0204017|-1071628265|DTS_E_INVALIDSCALE|"%1" weist eine ungültige Dezimalstellenanzahl auf. Die Dezimalstellenanzahl muss zwischen %2!ld! und %3!ld! liegen.|  
|0xC0204018|-1071628264|DTS_E_INVALIDPRECISION|"%1" weist eine ungültige Genauigkeit auf. Die Genauigkeit muss zwischen %2!ld! und %3!ld! liegen.|  
|0xC0204019|-1071628263|DTS_E_PROPVALUEIGNORED|Für "%1" ist ein Wert für die Länge, Genauigkeit, Dezimalstellen oder Codepage festgelegt. Dieser Wert ist ungleich 0 (null), aber für den Datentyp ist der Wert 0 (null) erforderlich.|  
|0xC020401A|-1071628262|DTS_E_CANTSETOUTPUTCOLUMNDATATYPEPROPERTIES|%1 lässt kein Festlegen von Eigenschaften für Datentypen in Ausgabespalten zu.|  
|0xC020401B|-1071628261|DTS_E_INVALIDDATATYPEFORERRORCOLUMNS|"%1" enthält einen ungültigen Datentyp. "%1" ist eine spezielle Fehlerspalte, und nur DT_I4 ist ein gültiger Datentyp.|  
|0xC020401C|-1071628260|DTS_E_NOERRORDESCFORCOMPONENT|Die Komponente stellt keine Fehlercodebeschreibungen bereit.|  
|0xC020401D|-1071628259|DTS_E_UNRECOGNIZEDERRORCODE|Der angegebene Fehlercode ist nicht dieser Komponente zugeordnet.|  
|0xC020401F|-1071628257|DTS_E_TRUNCATIONTRIGGEREDREDIRECTION|Durch das Abschneiden wurde eine Zeile umgeleitet, basierend auf den Dispositionseinstellungen für das Abschneiden.|  
|0xC0204020|-1071628256|DTS_E_CANTSETUSAGETYPETOREADWRITE|"%1" konnte für die Spalte mit der Herkunfts-ID %2!d! keinen Lese-/Schreibzugriff festlegen, da dieser Verwendungstyp für die Spalte nicht zulässig ist. Es wurde versucht, den Verwendungstyp einer Eingabespalte in den UT_READWRITE-Datentyp zu ändern, der in dieser Komponente nicht unterstützt wird.|  
|0xC0204023|-1071628253|DTS_E_CANTSETUSAGETYPE|%1 hat die angeforderte Verwendung der Eingabespalte mit der Herkunfts-ID %2!d! untersagt.|  
|0xC0204024|-1071628252|DTS_E_FAILEDTOSETUSAGETYPE|"%1" konnte die angeforderte Änderung an der Eingabespalte mit der Herkunfts-ID %2!d! nicht vornehmen. Fehlercode bei der Anforderung: 0x%3!8.8X!. Der angegebene Fehler trat beim Festlegen des Verwendungstyps einer Eingabespalte auf.|  
|0xC0204025|-1071628251|DTS_E_FAILEDTOSETOUTPUTCOLUMNDATATYPEPROPERTIES|Fehler beim Festlegen der Datentypeigenschaften in "%1" (Fehlercode: 0x%2!8.8X!). Der Fehler trat beim Festlegen mindestens einer Datentypeigenschaft der Ausgabespalte auf.|  
|0xC0204026|-1071628250|DTS_E_UNABLETORETRIEVEMETADATA|Die Metadaten für "%1" können nicht abgerufen werden. Stellen Sie sicher, dass der Objektname richtig und das Objekt vorhanden ist.|  
|0xC0204027|-1071628249|DTS_E_CANNOTMAPOUTPUTCOLUMN|Die Ausgabespalte kann einer externen Metadatenspalte nicht zugeordnet werden.|  
|0xC0204028|-1071628248|DTS_E_UNSUPPORTEDVARIABLETYPE|Die Variable %1 muss den Typ "%2" aufweisen.|  
|0xC020402A|-1071628246|DTS_E_CANTSETEXTERNALMETADATACOLUMNDATATYPEPROPERTIES|%1 lässt das Festlegen von Datentypeigenschaften für die externe Metadatenspalte nicht zu.|  
|0xC020402B|-1071628245|DTS_E_IDNOTINPUTNOROUTPUT|Die ID %1!lu! ist weder eine Eingabe-ID noch eine Ausgabe-ID. Die angegebene ID muss die Eingabe- oder Ausgabe-ID sein, die der Auflistung mit den externen Metadaten zugeordnet ist.|  
|0xC020402C|-1071628244|DTS_E_METADATACOLLECTIONNOTUSED|Die Auflistung mit den externen Metadaten in "%1" ist als nicht verwendete Auflistung gekennzeichnet, weshalb dafür keine Vorgänge ausgeführt werden können.|  
|0xC020402D|-1071628243|DTS_E_NOBUFFERTYPEONSYNCOUTPUT|%1 ist eine synchrone Ausgabe; der Puffertyp kann für synchrone Ausgaben nicht abgerufen werden.|  
|0xC0207000|-1071616000|DTS_E_INPUTCOLUMNUSAGETYPENOTREADONLY|Die Eingabespalte "%1" muss schreibgeschützt sein. Die Eingabespalte weist einen anderen als den schreibgeschützten Verwendungstyp auf. Dies ist nicht zulässig.|  
|0xC0207001|-1071615999|DTS_E_MISSINGCUSTOMPROPERTY|Für "%1" fehlt die erforderliche Eigenschaft "%2". Für das Objekt ist die angegebene benutzerdefinierte Eigenschaft erforderlich.|  
|0xC0207002|-1071615998|DTS_E_ILLEGALCUSTOMOUTPUTPROPERTY|Für die Ausgabe %1 ist die Eigenschaft "%2" nicht zulässig. Momentan ist jedoch diese Eigenschaft zugewiesen.|  
|0xC0207003|-1071615997|DTS_E_INVALIDOUTPUTEXCLUSIONGROUP|%1 muss in der Ausschlussgruppe %2!d! vorhanden sein. Alle Ausgaben müssen in der angegebenen Ausschlussgruppe vorhanden sein.|  
|0xC0207004|-1071615996|DTS_E_PROPERTYISEMPTY|Die Eigenschaft "%1" ist leer. Die Eigenschaft darf nicht leer sein.|  
|0xC0207005|-1071615995|DTS_E_CREATEEXPRESSIONOBJECTFAILED|Für den Ausdruck "%1" kann kein Arbeitsspeicher zugeordnet werden. Beim Erstellen eines internen Objekts zum Speichern des Ausdrucks war nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0207006|-1071615994|DTS_E_EXPRESSIONPARSEFAILED|Der Ausdruck "%1" kann nicht analysiert werden. Der Ausdruck war ungültig, oder es war nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0207007|-1071615993|DTS_E_EXPRESSIONCOMPUTEFAILED|Fehler beim Berechnen des Ausdrucks "%1" (Fehlercode: 0x%2!8.8X!). Möglicherweise weist der Ausdruck Fehler auf (z. B. Division durch 0), die beim Analysieren nicht erkannt werden können, oder es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0207008|-1071615992|DTS_E_FAILEDTOCREATEEXPRESSIONARRAY|Den Expression-Objekten kann kein Arbeitsspeicher zugeordnet werden. Beim Erstellen des Arrays mit den Expression-Objektzeigern war nicht genügend Arbeitsspeicher verfügbar.|  
|0xC020700A|-1071615990|DTS_E_FAILEDTOCREATEEXPRESSIONMANANGER|Fehler bei %1 (Fehlercode: 0x%2!8.8X!) während der Erstellung des Ausdruck-Managers.|  
|0xC020700B|-1071615989|DTS_E_SPLITEXPRESSIONNOTBOOLEAN|Der Ausdruck "%1" ist kein boolescher Wert. Der Ergebnistyp des Ausdrucks muss ein boolescher Wert sein.|  
|0xC020700C|-1071615988|DTS_E_EXPRESSIONVALIDATIONFAILED|Der Ausdruck "%1" in "%2" ist ungültig.|  
|0xC020700E|-1071615986|DTS_E_COLUMNNOTMATCHED|Die Spalte "%1" (%2!d!) kann keiner Eingabedateispalte zugeordnet werden. Der Name der Ausgabe- oder Eingabespalte wurde in der Datei nicht gefunden.|  
|0xC020700F|-1071615985|DTS_E_SETRESULTCOLUMNFAILED|Fehler beim Festlegen der Ergebnisspalte für den Ausdruck "%1" in %2 (Fehlercode: 0x%3!8.8X!). Die Eingabe- oder Ausgabespalte, die das Ergebnis des Ausdrucks empfangen sollte, kann nicht bestimmt werden oder das Ausdrucksergebnis kann nicht in den Spaltentyp umgewandelt werden.|  
|0xC0207011|-1071615983|DTS_E_FAILEDTOGETLOCALEIDFROMPACKAGE|Fehler beim Abrufen der Gebietsschema-ID aus dem Paket durch %1.|  
|0xC0207012|-1071615982|DTS_E_INCORRECTPARAMETERMAPPINGFORMAT|Die Zeichenfolge für die Parameterzuordnung weist ein falsches Format auf.|  
|0xC0207013|-1071615981|DTS_E_NOTENOUGHPARAMETERSPROVIDED|Der SQL-Befehl erfordert %1!d! Parameter, aber die Parameterzuordnung weist nur %2!d! Parameter auf.|  
|0xC0207014|-1071615980|DTS_E_PARAMETERNOTFOUNDINMAPPING|Der SQL-Befehl erfordert einen Parameter namens "%1", der jedoch in der Parameterzuordnung nicht gefunden wurde.|  
|0xC0207015|-1071615979|DTS_E_DUPLICATEDATASOURCECOLUMNNAME|Es sind mehrere Datenquellspalten mit dem Namen "%1" vorhanden.  Die Namen von Datenquellspalten müssen eindeutig sein.|  
|0xC0207016|-1071615978|DTS_E_DATASOURCECOLUMNWITHNONAMEFOUND|Es ist eine Datenquellenspalte ohne Namen vorhanden.  Jede Datenquellenspalte muss einen Namen haben.|  
|0xC0208001|-1071611903|DTS_E_DISCONNECTEDCOMPONENT|Eine Komponente ist vom Layout getrennt.|  
|0xC0208002|-1071611902|DTS_E_INVALIDCOMPONENTID|Ungültige ID für eine Layoutkomponente.|  
|0xC0208003|-1071611901|DTS_E_INVALIDINPUTCOUNT|Eine Komponente weist eine ungültige Anzahl von Eingaben auf.|  
|0xC0208004|-1071611900|DTS_E_INVALIDOUTPUTCOUNT|Eine Komponente weist eine ungültige Anzahl von Ausgaben auf.|  
|0xC0208005|-1071611899|DTS_E_NOINPUTSOROUTPUTS|Eine Komponente weist keine Eingaben oder Ausgaben auf.|  
|0xC0208007|-1071611897|DTS_E_CANTALLOCATECOLUMNINFO|um Zuordnen einer Liste der Spalten, die von dieser Komponente bearbeitet werden, ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0208008|-1071611896|DTS_E_OUTPUTCOLUMNNOTININPUT|Die Ausgabespalte "%1" (%2!d!) verweist auf die Eingabespalte mit der Herkunfts-ID %3!d!, aber es wurde keine Eingabespalte mit dieser Herkunfts-ID gefunden.|  
|0xC0208009|-1071611895|DTS_E_SORTNEEDSONEKEY|Mindestens eine Eingabespalte muss als Sortierschlüssel gekennzeichnet sein. Es wurden jedoch keine Schlüssel gefunden.|  
|0xC020800A|-1071611894|DTS_E_SORTDUPLICATEKEYWEIGHT|Sowohl die Spalte "%1" (%2!d!) als auch die Spalte "%3" (%4!d!) waren mit der Sortierschlüsselgewichtung %5!d! gekennzeichnet.|  
|0xC020800D|-1071611891|DTS_E_CANTMODIFYINVALID|Die Komponente kann die angeforderte Metadatenänderung erst ausführen, nachdem das Überprüfungsproblem behoben wurde.|  
|0xC020800E|-1071611890|DTS_E_CANTADDINPUT|Der inputs-Auflistung kann keine Eingabe hinzugefügt werden.|  
|0xC020800F|-1071611889|DTS_E_CANTADDOUTPUT|Der outputs-Auflistung kann keine Ausgabe hinzugefügt werden.|  
|0xC0208010|-1071611888|DTS_E_CANTDELETEINPUT|Aus der inputs-Auflistung kann keine Eingabe gelöscht werden.|  
|0xC0208011|-1071611887|DTS_E_CANTDELETEOUTPUT|Aus der outputs-Auflistung kann keine Ausgabe entfernt werden.|  
|0xC0208014|-1071611884|DTS_E_CANTCHANGEUSAGETYPE|Der Verwendungstyp der Spalte kann nicht geändert werden.|  
|0xC0208016|-1071611882|DTS_E_INVALIDUSAGETYPEFORCUSTOMPROPERTY|%1 muss für die benutzerdefinierte Eigenschaft "%2" eine Lese-/Schreibberechtigung aufweisen. Die Eingabe- oder Ausgabespalte weist die angegebene benutzerdefinierte Eigenschaft, aber nicht den Lese-/Schreibmodus auf. Entfernen Sie die Eigenschaft, oder legen Sie für die Spalte den Lese-/Schreibmodus fest.|  
|0xC0208017|-1071611881|DTS_E_READWRITECOLUMNMISSINGREQUIREDCUSTOMPROPERTY|%1 weist den Lese-/Schreibmodus auf und erfordert die benutzerdefinierte Eigenschaft "%2". Fügen Sie die Eigenschaft hinzu, oder entfernen Sie das Lese-/Schreibattribut aus der Spalte.|  
|0xC0208018|-1071611880|DTS_E_CANTDELETECOLUMN|Die Spalte kann nicht gelöscht werden. Für die Komponente können in der Eingabe oder Ausgabe keine Spalten gelöscht werden.|  
|0xC0208019|-1071611879|DTS_E_CANTADDCOLUMN|Für die Komponente können der Eingabe oder Ausgabe keine Spalten hinzugefügt werden.|  
|0xC020801A|-1071611878|DTS_E_CANNOTTFINDRUNTIMECONNECTIONOBJECT|Die Verbindung "%1" wurde nicht gefunden. Überprüfen Sie, ob der Verbindungs-Manager eine Verbindung mit diesem Namen aufweist.|  
|0xC020801B|-1071611877|DTS_E_CANNOTFINDRUNTIMECONNECTIONMANAGER|Der Laufzeitverbindungs-Manager mit der ID "%1" wurde nicht gefunden. Überprüfen Sie, ob die Verbindungs-Manager-Auflistung einen Verbindungs-Manager mit dieser ID aufweist.|  
|0xC020801C|-1071611876|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|SSIS-Fehlercode DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  Fehler beim Aufrufen der AcquireConnection-Methode für den Verbindungs-Manager "%1" (Fehlercode: 0x%2!8.8X!).  Möglicherweise wurden bereits Fehlermeldungen veröffentlicht, die weitere Informationen zum Fehler beim Aufrufen der AcquireConnection-Methode beinhalten.|  
|0xC020801D|-1071611875|DTS_E_ACQUIREDCONNECTIONISINVALID|Die vom Verbindungs-Manager "%1" abgerufene Verbindung ist ungültig.|  
|0xC020801E|-1071611874|DTS_E_INCORRECTCONNECTIONMANAGERTYPE|Der Verbindungs-Manager "%1" weist einen falschen Typ auf.  Erforderlich ist der Typ "%2". Für die Komponente steht der Typ "%3" zur Verfügung.|  
|0xC020801F|-1071611873|DTS_E_CANNOTACQUIREMANAGEDCONNECTIONFROMCONNECTIONMANAGER|Eine verwaltete Verbindung kann aus dem Laufzeitverbindungs-Manager nicht abgerufen werden.|  
|0xC0208020|-1071611872|DTS_E_CANTINITINPUT|Eine Eingabe kann nicht erstellt werden, um die inputs-Auflistung zu initialisieren.|  
|0xC0208021|-1071611871|DTS_E_CANTINITOUTPUT|Eine Ausgabe kann nicht erstellt werden, um die outputs-Auflistung zu initialisieren.|  
|0xC0208023|-1071611869|DTS_E_EXTRACTORCANTWRITE|Fehler beim Schreiben in die Datei "%1" (Fehlercode: 0x%2!8.8X!).|  
|0xC0208024|-1071611868|DTS_E_INCORRECTCONNECTIONOBJECTTYPE|Der Verbindungs-Manager "%1" hat ein Objekt mit einem falschen Typ der AcquireConnection-Methode zurückgegeben.|  
|0xC0208025|-1071611867|DTS_E_INPUTCOLPROPERTYNOTFOUND|In der Eingabespalte "%1" (%2!d!) ist die Eigenschaft "%3" erforderlich, diese wurde jedoch nicht gefunden. Die fehlende Eigenschaft sollte hinzugefügt werden.|  
|0xC0208026|-1071611866|DTS_E_EXTRACTORUNREFERENCED|"%1" ist als schreibgeschützt gekennzeichnet. Es gibt jedoch keinen Verweis durch eine andere Spalte. Spalten, auf die nicht verwiesen wird, sind nicht zulässig.|  
|0xC0208027|-1071611865|DTS_E_EXTRACTORREFERENCEDCOLUMNNOTFOUND|"%1" verweist auf die Spalten-ID %2!d!. Diese Spalte wurde jedoch nicht in der Eingabe gefunden. Ein Verweis zeigt auf eine nicht vorhandene Spalte.|  
|0xC0208028|-1071611864|DTS_E_EXTRACTORDATACOLUMNNOTBLOB|"%1" verweist auf "%2", doch ist diese Spalte nicht vom Typ BLOB.|  
|0xC0208029|-1071611863|DTS_E_INSERTERREFERENCEDCOLUMNNOTFOUND|"%1" verweist auf die Ausgabespalten-ID %2!d!. Diese Spalte wurde jedoch nicht in der Ausgabe gefunden.|  
|0xC020802A|-1071611862|DTS_E_INSERTERCANTREAD|Fehler beim Lesen der Datei "%1" (Fehlercode: 0x%2!8.8X!).|  
|0xC020802B|-1071611861|DTS_E_TXSCD_NOTYPEDCOLUMNSATINPUT|Es muss mindestens eine feste, veränderliche oder Verlaufsspalte in der Eingabe einer Transformation für langsam veränderliche Dimensionen vorhanden sein. Überprüfen Sie, ob mindestens eine Spalte vom Typ FixedAttribute, ChangingAttribute oder HistoricalAttribute ist.|  
|0xC020802C|-1071611860|DTS_E_TXSCD_INVALIDINPUTCOLUMNTYPE|Die ColumnType-Eigenschaft "%1" ist ungültig. Der aktuelle Wert liegt außerhalb des Bereichs zulässiger Werte.|  
|0xC020802D|-1071611859|DTS_E_TXSCD_CANNOTMAPDIFFERENTTYPES|Die "%1"-Eingabespalte kann nicht der externen Spalte "%2" zugeordnet werden, weil sie unterschiedliche Datentypen aufweisen. Mit der Transformation für langsam veränderliche Dimensionen ist die Zuordnung zwischen Spalten mit unterschiedlichen Datentypen nicht möglich, mit Ausnahme von DT_STR und DT_WSTR.|  
|0xC020802E|-1071611858|DTS_E_NTEXTDATATYPENOTSUPPORTEDWITHANSIFILES|"%1" weist den Datentyp DT_NTEXT auf, der bei ANSI-Dateien nicht unterstützt wird. Verwenden Sie stattdessen DT_TEXT, und konvertieren Sie die Daten mithilfe der Datenkonvertierungskomponente in DT_NTEXT.|  
|0xC020802F|-1071611857|DTS_E_TEXTDATATYPENOTSUPPORTEDWITHUNICODEFILES|"%1" weist den Datentyp DT_TEXT auf, der bei Unicode-Dateien nicht unterstützt wird. Verwenden Sie stattdessen DT_NTEXT, und konvertieren Sie die Daten mithilfe der Datenkonvertierungskomponente in DT_TEXT.|  
|0xC0208030|-1071611856|DTS_E_IMAGEDATATYPENOTSUPPORTED|"%1" weist den Datentyp DT_IMAGE auf, der nicht unterstützt wird. Verwenden Sie stattdessen DT_TEXT oder DT_NTEXT, und konvertieren Sie die Daten mithilfe der Datenkonvertierungskomponente von bzw. nach DT_IMAGE.|  
|0xC0208031|-1071611855|DTS_E_FLATFILEFORMATNOTSUPPORTED|Das Format "%1" wird vom Verbindungs-Manager für Flatfiles nicht unterstützt. Die Formate Delimited, FixedWidth, RaggedRight und Mixed werden unterstützt.|  
|0xC0208032|-1071611854|DTS_E_EXTRACTORFILENAMECOLUMNNOTSTRING|"%1" sollte einen Dateinamen enthalten, gehört jedoch nicht zu einem Zeichenfolgentyp.|  
|0xC0208033|-1071611853|DTS_E_EXTRACTORCANTAPPENDTRUNCATE|Der Fehler wird durch miteinander in Konflikt stehende Eigenschaftseinstellungen verursacht. Für "%1" sind die AllowAppend-Eigenschaft und die ForceTruncate-Eigenschaft auf TRUE festgelegt. Beide Eigenschaften dürfen nicht auf TRUE festgelegt sein. Legen Sie eine der beiden Eigenschaften auf FALSE fest.|  
|0xC0208034|-1071611852|DTS_E_EXTRACTORCOLUMNALREADYREFERENCED|%1 verweist auf die Spalten-ID %2!d!, aber auf diese Spalte wird bereits von %3 verwiesen. Entfernen Sie einen der beiden Spaltenverweise.|  
|0xC0208035|-1071611851|DTS_E_CONNECTIONMANANGERNOTASSIGNED|%1 wurde kein Verbindungs-Manager zugewiesen.|  
|0xC0208036|-1071611850|DTS_E_INSERTERCOLUMNALREADYREFERENCED|%1 verweist auf die Ausgabespalte mit der ID %2!d!, aber auf diese Spalte wird bereits von %3 verwiesen.|  
|0xC0208037|-1071611849|DTS_E_INSERTERCOLUMNNOTREFERENCED|Auf "%1" wird von keiner Eingabespalte verwiesen. Auf jede Ausgabespalte muss von genau einer Eingabespalte verwiesen werden.|  
|0xC0208038|-1071611848|DTS_E_INSERTERDATACOLUMNNOTBLOB|"%1" verweist auf "%2", aber diese Spalte weist nicht den richtigen Datentyp auf. Sie muss vom Typ DT_TEXT, DT_NTEXT oder DT_IMAGE sein. Ein Verweis zeigt auf eine Spalte, die vom Typ BLOB sein muss.|  
|0xC0208039|-1071611847|DTS_E_INSERTERFILENAMECOLUMNNOTSTRING|"%1" sollte einen Dateinamen enthalten, gehört jedoch nicht zu einem Zeichenfolgentyp.|  
|0xC020803A|-1071611846|DTS_E_INSERTEREXPECTBOMINVALIDTYPE|Bei "%1" ist die ExpectBOM-Eigenschaft für %2 auf TRUE festgelegt, aber die Spalte ist nicht vom Typ NT_NTEXT. ExpectBOM gibt an, dass die Transformation für das Importieren von Spalten eine Bytereihenfolgemarke (Byte-Order Mark, BOM) erwartet. Legen Sie die ExpectBOM-Eigenschaft auf False fest, oder ändern Sie den Datentyp der Ausgabespalte in DT_NTEXT.|  
|0xC020803B|-1071611845|DTS_E_INSERTERINVALIDDATACOLUMNSETTYPE|Datenausgabespalten müssen vom Typ DT_TEXT, DT_NTEXT oder DT_IMAGE sein. Für die Datenausgabespalte kann nur ein BLOB-Typ festgelegt werden.|  
|0xC020803C|-1071611844|DTS_E_TXSCD_FIXEDATTRIBUTECHANGE|Falls die FailOnFixedAttributeChange-Eigenschaft auf TRUE festgelegt ist, kann die Transformation nicht ausgeführt werden, wenn eine Änderung des festen Attributs erkannt wird. Um Zeilen an die Ausgabe des festen Attributs zu senden, legen Sie die FailOnFixedAttributeChange-Eigenschaft auf FALSE fest.|  
|0xC020803D|-1071611843|DTS_E_TXSCD_LOOKUPFAILURE|Von der Transformation für Suche wurden keine Zeilen abgerufen. Die Transformation schlägt fehl, wenn die FailOnLookupFailure-Eigenschaft auf TRUE festgelegt ist und keine Zeilen abgerufen werden.|  
|0xC020803E|-1071611842|DTS_E_TXSCD_INVALIDNUMBERSOFPARAMETERS|Mindestens eine Spalte vom Typ Key muss in der Ausgabe einer Transformation für langsam veränderliche Dimensionen vorhanden sein. Legen Sie mindestens eine Spalte auf den Typ Key fest.|  
|0xC020803F|-1071611841|DTS_E_TXSCD_CANNOTFINDEXTERNALCOLUMN|Die externe Spalte mit dem Namen "%1" wurde nicht gefunden.|  
|0xC0208040|-1071611840|DTS_E_TXSCD_INFFEREDINDICATORNOTBOOL|Die abgeleitete Indikatorspalte "%1" muss vom Typ DT_BOOL sein.|  
|0xC0208107|-1071611641|DTS_E_ERRORROWDISPMUSTBENOTUSED|Bei %1 muss der Wert für die Fehlerzeilendisposition auf RD_NotUsed festgelegt werden.|  
|0xC0208108|-1071611640|DTS_E_TRUNCROWDISPMUSTBENOTUSED|Bei %1 muss der Wert für die Abschneidezeilendisposition auf RD_NotUsed festgelegt werden.|  
|0xC0208201|-1071611391|DTS_E_TXAGG_INPUTNOTFOUNDFOROUTPUT|Die Eingabespalte mit der Herkunfts-ID %1!d!, die von der Ausgabespalte mit ID %2!d! benötigt wird, wurde nicht gefunden.|  
|0xC0208202|-1071611390|DTS_E_TXAGG_INVALIDOUTPUTDATATYPEFORAGGREGATE|Ungültiger Ausgabedatentyp für den Aggregattyp, der in der Ausgabespalten-ID %1!d! angegeben ist.|  
|0xC0208203|-1071611389|DTS_E_TXAGG_INVALIDINPUTDATATYPEFORAGGREGATE|Der Eingabedatentyp für %1, der für das angegebene Aggregat in %2 verwendet wird, ist ungültig.|  
|0xC0208204|-1071611388|DTS_E_TXAGG_INPUTOUTPUTDATATYPEMISMATCH|Datentypen der Eingabespalte mit der Herkunfts-ID %1!d! und der Ausgabespalten-ID %2!d! stimmen nicht überein.|  
|0xC0208205|-1071611387|DTS_E_UNABLETOGETINPUTBUFFERHANDLE|Der Eingabepufferhandle für die Eingabe-ID %1!d! kann nicht abgerufen werden.|  
|0xC0208206|-1071611386|DTS_E_UNABLETOGETOUTPUTBUFFERHANDLE|Der Ausgabepufferhandle für die Ausgabe-ID %1!d! kann nicht abgerufen werden.|  
|0xC0208207|-1071611385|DTS_E_UNABLETOFINDCOLUMNHANDLEINOUTPUTBUFFER|Die Spalte mit der Herkunfts-ID %1!d! wurde im Ausgabepuffer nicht gefunden.|  
|0xC0208208|-1071611384|DTS_E_UNABLETOFINDCOLUMNHANDLEININPUTBUFFER|Die Spalte mit der Herkunfts-ID %1!d! wurde im Eingabepuffer nicht gefunden.|  
|0xC0208209|-1071611383|DTS_E_CANNOTHAVEZEROOUTPUTCOLUMNS|Die Anzahl der Ausgabespalten für %1 darf nicht 0 (null) lauten.|  
|0xC020820A|-1071611382|DTS_E_CONNECTIONMANAGERCOLUMNCOUNTMISMATCH|Die Spaltenanzahl im Verbindungs-Manager für Flatfiles muss mit der Spaltenanzahl im Flatfileadapter identisch sein. Die Spaltenanzahl beim Verbindungs-Manager für Flatfiles beträgt %1!d!, die Spaltenanzahl beim Flatfileadapter hingegen %2!d!.|  
|0xC020820B|-1071611381|DTS_E_MISMATCHCONNECTIONMANAGERCOLUMN|Die Spalte "%1" mit dem Index %2!d! des Verbindungs-Managers für Flatfiles wurde beim Index %3!d! in der Spaltenauflistung des Flatfileadapters nicht gefunden.|  
|0xC020820D|-1071611379|DTS_E_EXTERNALMETADATACOLUMNISALREADYMAPPED|Die externe Metadatenspalte mit der ID %1!d! wurde bereits %2 zugeordnet.|  
|0xC020820E|-1071611378|DTS_E_TXAGG_STRING_TOO_LONG|Die Transformation hat eine Schlüsselspalte gefunden, die länger als %1!u! Zeichen ist.|  
|0xC020820F|-1071611377|DTS_E_DERIVEDRESULT_TOO_LONG|Die Transformation hat einen Ergebniswert gefunden, der länger als %1!u! Bytes ist.|  
|0xC0208210|-1071611376|DTS_E_TXAGG_MEMALLOCERROUTPUTDESCRIPTORS|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0208211|-1071611375|DTS_E_TXAGG_MEMALLOCERRWORKSPACEDESCRIPTORS|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0208212|-1071611374|DTS_E_TXAGG_MEMALLOCERRSORTORDERDESCRIPTORS|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0208213|-1071611373|DTS_E_TXAGG_MEMALLOCERRNUMERICDESCRIPTORS|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0208214|-1071611372|DTS_E_TXAGG_MEMALLOCERRCOUNTDISTINCTDESCRIPTOR|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0208215|-1071611371|DTS_E_TXAGG_MEMALLOCERRWORKSPACESORTORDERDESCRIPTORS|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0208216|-1071611370|DTS_E_TXAGG_MEMALLOCERRWORKSPACENUMERICDESCRIPTORS|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0208217|-1071611369|DTS_E_TXAGG_MEMALLOCERRWORKSPACEBUFFCOLS|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0208218|-1071611368|DTS_E_UNREFERENCEDINPUTCOLUMN|Auf die Eingabespalte "%1" wird nicht verwiesen.|  
|0xC0208219|-1071611367|DTS_E_CANTBUILDTHREADPOOL|Die Transformation zum Sortieren konnte keinen Threadpool mit %1!d! Threads erstellen. Es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC020821A|-1071611366|DTS_E_QUEUEWORKITEMFAILED|Die Transformation für Sortieren kann ein Arbeitselement nicht in die Warteschlange des Threadpools einreihen. Es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC020821B|-1071611365|DTS_E_SORTTHREADSTOPPED|Ein Arbeitsthread in der Transformation für Sortieren wurde mit dem Fehlercode 0x%1!8.8X! beendet. Beim Sortieren eines Puffers wurde ein schwerwiegender Fehler gefunden.|  
|0xC020821E|-1071611362|DTS_E_SORTBADTHREADCOUNT|MaxThreads war %1!ld!, sollte aber einen Wert zwischen 1 und %2!ld! inkl. oder -1 aufweisen, um die Standard-CPU-Zahl zu verwenden.|  
|0xC020821F|-1071611361|DTS_E_DTPXMLLOADFAILURE|Aus XML kann nicht geladen werden.|  
|0xC0208220|-1071611360|DTS_E_DTPXMLSAVEFAILURE|In XML kann nicht gespeichert werden.|  
|0xC0208221|-1071611359|DTS_E_DTPXMLINT32CONVERTERR|Der Wert "%1" kann nicht in eine ganze Zahl konvertiert werden.|  
|0xC0208222|-1071611358|DTS_E_DTPXMLBOOLCONVERTERR|Der Wert "%1" kann nicht in einen booleschen Wert konvertiert werden.|  
|0xC0208223|-1071611357|DTS_E_DTPXMLPARSEERRORNEARID|Ladefehler beim Objekt mit der ID %1!d!.|  
|0xC0208226|-1071611354|DTS_E_DTPXMLPROPERTYTYPEERR|Der Wert "%1" ist für das Attribut "%2" ungültig.|  
|0xC0208228|-1071611352|DTS_E_DTPXMLSETUSAGETYPEERR|Der Wert "%1" ist für das Attribut "%2" ungültig.|  
|0xC0208229|-1071611351|DTS_E_DTPXMLDATATYPEERR|Der Wert "%1" ist für das Attribut "%2" ungültig.|  
|0xC020822A|-1071611350|DTS_E_UNMAPPEDINPUTCOLUMN|%1 ist keiner Ausgabespalte zugeordnet.|  
|0xC020822B|-1071611349|DTS_E_INPUTCOLUMNBADMAP|%1 weist eine ungültige Zuordnung auf.  Eine Ausgabespalte mit der ID %2!ld! ist in dieser Komponente nicht vorhanden.|  
|0xC020822D|-1071611347|DTS_E_MULTIPLYMAPPEDOUTCOL|%1 ist einer Ausgabespalte zugeordnet, die bereits eine Zuordnung in dieser Eingabe aufweist.|  
|0xC020822E|-1071611346|DTS_E_TXAGG_STRINGPROMOTIONFAILED|Die Eingabespalte mit der Herkunfts-ID %1!ld! kann aufgrund des Fehlers 0x%2!8.8X! nicht in DT_WSTR umgewandelt werden.|  
|0xC0208230|-1071611344|DTS_E_DTPXMLIDLOOKUPERR|Verwiesenes Objekt mit ID %1!d! wurde nicht in Paket gefunden.|  
|0xC0208231|-1071611343|DTS_E_DTPXMLINVALIDXMLPERSISTPROPERTY|Eine Persistenzeigenschaft, die für das Pipeline-XML-Modul erforderlich ist, kann nicht gelesen werden. Die Eigenschaft wurde von der Pipeline nicht bereitgestellt.|  
|0xC0208232|-1071611342|DTS_E_DTPXMLPROPERTYSTATEERR|Der Wert "%1" ist für das Attribut "%2" ungültig.|  
|0xC0208233|-1071611341|DTS_E_CANTGETCUSTOMPROPERTY|Die benutzerdefinierte Eigenschaft "%1" kann nicht abgerufen werden.|  
|0xC0208234|-1071611340|DTS_E_UNABLETOLOCATEINPUTCOLUMNID|In der Eingabespaltenauflistung wurde keine Eingabespalte mit der Herkunfts-ID %1!d! gefunden, auf die in der benutzerdefinierten ParameterMap-Eigenschaft mit dem Parameter an Positionsnummer %2!d! verwiesen wird.|  
|0xC0208235|-1071611339|DTS_E_TXLOOKUP_UNABLETOLOCATEREFCOLUMN|Die %1!s!-Verweisspalte wurde nicht gefunden.|  
|0xC0208236|-1071611338|DTS_E_TXLOOKUP_INCOMPATIBLEDATATYPES|%1 und die Verweisspalte "%2" weisen inkompatible Datentypen auf.|  
|0xC0208237|-1071611337|DTS_E_TXLOOKUP_PARAMMETADATAMISMATCH|Die parametrisierte SQL-Anweisung ergibt Metadaten, die nicht mit der SQL-Hauptanweisung übereinstimmen.|  
|0xC0208238|-1071611336|DTS_E_TXLOOKUP_INCORRECTNUMOFPARAMETERS|Die parametrisierte SQL-Anweisung enthält eine falsche Parameteranzahl. Erwartet wurden %1!d!, gefunden jedoch %2!d!.|  
|0xC0208239|-1071611335|DTS_E_TXLOOKUP_INVALIDJOINTYPE|%1 weist einen Datentyp auf, mit dem kein Join möglich ist.|  
|0xC020823A|-1071611334|DTS_E_TXLOOKUP_INVALIDCOPYTYPE|%1 weist einen Datentyp auf, der nicht kopiert werden kann.|  
|0xC020823B|-1071611333|DTS_E_INSERTERINVALIDCOLUMNDATATYPE|%1 weist einen nicht unterstützten Datentyp auf. Es muss DT_STR oder DT_WSTR lauten.|  
|0xC020823C|-1071611332|DTS_E_EXTRACTORINVALIDCOLUMNDATATYPE|%1 weist einen nicht unterstützten Datentyp auf. Er muss DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT oder DT_IMAGE lauten.|  
|0xC020823D|-1071611331|DTS_E_TXCHARMAPINVALIDCOLUMNDATATYPE|%1 weist einen nicht unterstützten Datentyp auf. Er muss DT_STR, DT_WSTR, DT_TEXT oder DT_NTEXT lauten.|  
|0xC020823E|-1071611330|DTS_E_SORTCANTCREATEEVENT|Ein Ereignis zum Kommunizieren mit den Arbeitsthreads kann von der Transformation zum Sortieren nicht erstellt werden. Für die Transformation für Sortieren sind nicht genügend Systemhandles verfügbar.|  
|0xC020823F|-1071611329|DTS_E_SORTCANTCREATETHREAD|Ein Arbeitsthread kann von der Transformation für Sortieren nicht erstellt werden. Für die Transformation für Sortieren ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0208240|-1071611328|DTS_E_SORTCANTCOMPARE|Die Transformation zum Sortieren konnte die Zeile %1!d! in der Puffer-ID %2!d! mit der Zeile %3!d! in der Puffer-ID %4!d! nicht vergleichen.|  
|0xC0208242|-1071611326|DTS_E_TXLOOKUP_TOOFEWREFERENCECOLUMNS|Die Verweismetadaten für die Transformation für Suche enthalten zu wenige Spalten. Überprüfen Sie die SQLCommand-Eigenschaft. Die SELECT-Anweisung muss mindestens eine Spalte zurückgeben.|  
|0xC0208243|-1071611325|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNINFO|Für ein Array mit ColumnInfo-Strukturen kann kein Arbeitsspeicher belegt werden.|  
|0xC0208244|-1071611324|DTS_E_TXLOOKUP_MALLOCERR_REFERENCECOLUMNPAIR|Für ein Array mit ColumnPair-Strukturen konnte kein Arbeitsspeicher belegt werden.|  
|0xC0208245|-1071611323|DTS_E_TXLOOKUP_MALLOCERR_BUFFCOL|Für ein Array mit BUFFCOL-Strukturen kann kein Arbeitsspeicher belegt werden, um einen Hauptarbeitsbereich zu erstellen.|  
|0xC0208246|-1071611322|DTS_E_TXLOOKUP_MAINWORKSPACE_CREATEERR|Hauptarbeitsbereichspuffer kann nicht erstellt werden.|  
|0xC0208247|-1071611321|DTS_E_TXLOOKUP_HASHTABLE_MALLOCERR|Für die Hashtabelle kann kein Arbeitsspeicher belegt werden.|  
|0xC0208248|-1071611320|DTS_E_TXLOOKUP_HASHNODEHEAP_CREATEERR|Zum Erstellen eines Heaps für Hashknoten kann kein Arbeitsspeicher belegt werden.|  
|0xC0208249|-1071611319|DTS_E_TXLOOKUP_HASHNODEHEAP_MALLOCERR|Für einen Hashknotenheap kann kein Arbeitsspeicher belegt werden.|  
|0xC020824A|-1071611318|DTS_E_TXLOOKUP_LRUNODEHEAP_CREATEERR|Ein Heap für LRU-Knoten kann nicht erstellt werden. Es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC020824B|-1071611317|DTS_E_TXLOOKUP_LRUNODEHEAP_MALLOCERR|Für den LRU-Knotenheap kann kein Arbeitsspeicher belegt werden. Es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC020824C|-1071611316|DTS_E_TXLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|OLE DB-Fehler beim Laden von Spaltenmetadaten. Überprüfen Sie die Eigenschaften SQLCommand und SqlCommandParam.|  
|0xC020824D|-1071611315|DTS_E_TXLOOKUP_OLEDBERR_GETIROWSET|OLE DB-Fehler beim Abrufen eines Rowsets. Überprüfen Sie die Eigenschaften SQLCommand und SqlCommandParam.|  
|0xC020824E|-1071611314|DTS_E_TXLOOKUP_OLEDBERR_FILLBUFFER|OLE DB-Fehler beim Auffüllen des internen Caches. Überprüfen Sie die Eigenschaften SQLCommand und SqlCommandParam.|  
|0xC020824F|-1071611313|DTS_E_TXLOOKUP_OLEDBERR_BINDPARAMETERS|OLE DB-Fehler beim Binden von Parametern. Überprüfen Sie die Eigenschaften SQLCommand und SqlCommandParam.|  
|0xC0208250|-1071611312|DTS_E_TXLOOKUP_OLEDBERR_CREATEBINDING|OLE DB-Fehler beim Erstellen von Bindungen. Überprüfen Sie die Eigenschaften SQLCommand und SqlCommandParam.|  
|0xC0208251|-1071611311|DTS_E_TXLOOKUP_INVALID_CASE|In einer switch-Anweisung wurde während der Laufzeit ein ungültiger Fall gefunden.|  
|0xC0208252|-1071611310|DTS_E_TXLOOKUP_MAINWORKSPACE_MALLOCERR|Für eine neue Zeile kann kein Arbeitsspeicher für den Hauptarbeitsbereichspuffer belegt werden. Es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0208253|-1071611309|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMIROWSET|OLE DB-Fehler beim Abrufen eines parametrisierten Rowsets. Überprüfen Sie die Eigenschaften SQLCommand und SqlCommandParam.|  
|0xC0208254|-1071611308|DTS_E_TXLOOKUP_OLEDBERR_GETPARAMSINGLEROW|OLE DB-Fehler beim Abrufen einer parametrisierten Zeile. Überprüfen Sie die Eigenschaften SQLCommand und SqlCommandParam.|  
|0xC0208255|-1071611307|DTS_E_TXAGG_MAINWORKSPACE_MALLOCERR|Für eine neue Zeile kann kein Arbeitsspeicher für den Hauptarbeitsbereichspuffer belegt werden. Es ist nicht genügend Arbeitsspeicher verfügbar.|  
|0xC0208256|-1071611306|DTS_E_TXAGG_MAINWORKSPACE_CREATEERR|Hauptarbeitsbereichspuffer kann nicht erstellt werden.|  
|0xC0208257|-1071611305|DTS_E_TXAGG_HASHTABLE_MALLOCERR|Für die Hashtabelle kann kein Arbeitsspeicher belegt werden.|  
|0xC0208258|-1071611304|DTS_E_TXAGG_HASHNODEHEAP_CREATEERR|Zum Erstellen eines Heaps für die Hashknoten kann kein Arbeitsspeicher belegt werden.|  
|0xC0208259|-1071611303|DTS_E_TXAGG_HASHNODEHEAP_MALLOCERR|Für den Hashknotenheap kann kein Arbeitsspeicher belegt werden.|  
|0xC020825A|-1071611302|DTS_E_TXAGG_CDNODEHEAP_CREATEERR|Zum Erstellen eines Heaps für CountDistinct-Knoten kann kein Arbeitsspeicher belegt werden.|  
|0xC020825B|-1071611301|DTS_E_TXAGG_CDNODEHEAP_MALLOCERR|Für den CountDistinct-Knotenheap kann kein Arbeitsspeicher belegt werden.|  
|0xC020825C|-1071611300|DTS_E_TXAGG_CDCHAINHEAP_CREATEERR|Zum Erstellen eines Heaps für CountDistinct-Ketten kann kein Arbeitsspeicher belegt werden.|  
|0xC020825D|-1071611299|DTS_E_TXAGG_CDHASHTABLE_CREATEERR|Für die CountDistinct-Hashtabelle kann kein Arbeitsspeicher belegt werden.|  
|0xC020825E|-1071611298|DTS_E_TXAGG_CDWORKSPACE_MALLOCERR|Für eine neue Zeile für den CountDistinct-Arbeitsbereichspuffer kann kein Arbeitsspeicher belegt werden.|  
|0xC020825F|-1071611297|DTS_E_TXAGG_CDWORKSPACE_CREATEERR|Ein CountDistinct-Arbeitsbereichspuffer kann nicht erstellt werden.|  
|0xC0208260|-1071611296|DTS_E_TXAGG_CDCOLLASSEARRAY_MALLOCERR|Für das CountDistinct Collapse-Array kann kein Arbeitsspeicher belegt werden.|  
|0xC0208261|-1071611295|DTS_E_TXAGG_CDCHAINHEAP_MALLOCERR|Für CountDistinct-Ketten kann kein Arbeitsspeicher belegt werden.|  
|0xC0208262|-1071611294|DTS_E_TXCOPYMAP_MISMATCHED_COLUMN_METADATA|Spalten mit den Herkunfts-IDs %1!d! und %2!d! weisen keine übereinstimmenden Metadaten auf. Die Eingabespalte, die einer Ausgabespalte zugeordnet ist, weist für die Transformation zum Kopieren von Zuordnungen nicht dieselben Metadaten auf (Datentyp, Genauigkeit, Dezimalstellen, Länge oder Codepage).|  
|0xC0208263|-1071611293|DTS_E_TXCOPYMAP_INCORRECT_OUTPUT_COLUMN_MAPPING|Die Ausgabespalte mit der Herkunfts-ID „%1! d!“ ist einer Eingabespalte falsch zugeordnet. Die CopyColumnId-Eigenschaft der Ausgabespalte ist nicht richtig.|  
|0xC0208265|-1071611291|DTS_E_CANTGETBLOBDATA|Fehler beim Abrufen von Long-Daten für die Spalte "%1".|  
|0xC0208266|-1071611290|DTS_E_CANTADDBLOBDATA|ong-Daten wurden für ein Spalte abgerufen, können jedoch nicht dem Datenflusstask-Puffer hinzugefügt werden.|  
|0xC0208267|-1071611289|DTS_E_MCASTOUTPUTCOLUMNS|Die Ausgabe "%1" (%2!d!) hat Spalten ausgegeben, Multicastausgaben deklarieren jedoch keine Spalten. Das Paket ist beschädigt.|  
|0xC0208273|-1071611277|DTS_E_UNABLETOGETLOCALIZEDRESOURCE|Die lokalisierte Ressourcen-ID %1!d! kann nicht geladen werden. Überprüfen Sie, ob die RLL-Datei vorhanden ist.|  
|0xC0208274|-1071611276|DTS_E_DTPXMLEVENTSCACHEERR|Der Zugriff auf die Ereignisschnittstelle konnte nicht erfolgen. Eine ungültige Ereignisschnittstelle wurde an das Datenflussmodul zur Weitergabe an XML übergeben.|  
|0xC0208275|-1071611275|DTS_E_DTPXMLPATHLOADERR|Fehler beim Festlegen eines Pfadobjekts beim Laden von XML.|  
|0xC0208276|-1071611274|DTS_E_DTPXMLINPUTLOADERR|Fehler beim Festlegen des Eingabeobjekts beim Laden von XML.|  
|0xC0208277|-1071611273|DTS_E_DTPXMLOUTPUTLOADERR|Fehler beim Festlegen des Ausgabeobjekts beim Laden von XML.|  
|0xC0208278|-1071611272|DTS_E_DTPXMLINPUTCOLUMNLOADERR|Fehler beim Festlegen des Eingabespaltenobjekts beim Laden von XML.|  
|0xC0208279|-1071611271|DTS_E_DTPXMLOUTPUTCOLUMNLOADERR|Fehler beim Festlegen des Ausgabespaltenobjekts beim Laden von XML.|  
|0xC0208280|-1071611264|DTS_E_DTPXMLPROPERTYLOADERR|Fehler beim Festlegen des Eigenschaftenobjekts beim Laden von XML.|  
|0xC0208281|-1071611263|DTS_E_DTPXMLCONNECTIONLOADERR|Fehler beim Festlegen des Verbindungsobjekts beim Laden von XML.|  
|0xC0208282|-1071611262|DTS_E_FG_MISSING_OUTPUT_COLUMNS|Spezielle transformationsspezifische Spalten fehlen oder weisen falsche Datentypen auf.|  
|0xC0208283|-1071611261|DTS_E_FG_PREPARE_TABLES_AND_ACCESSORS|Fehler beim Erstellen erforderlicher Tabellen und Accessoren durch die Transformation für Fuzzygruppierung.|  
|0xC0208284|-1071611260|DTS_E_FG_COPY_INPUT|Fehler beim Kopieren der Eingabe durch die Transformation für Fuzzygruppierung.|  
|0xC0208285|-1071611259|DTS_E_FG_GENERATE_GROUPS|Fehler beim Generieren von Gruppen durch die Transformation für Fuzzygruppierung.|  
|0xC0208286|-1071611258|DTS_E_FG_LEADING_TRAILING|Unerwarteter Fehler in der Fuzzygruppierung beim Anwenden der Einstellungen der Eigenschaft '%1'.|  
|0xC0208287|-1071611257|DTS_E_FG_PICK_CANONICAL|Die Fuzzygruppierung konnte eine kanonische Datenzeile nicht auswählen, die für die Standardisierung der Daten verwendet werden soll.|  
|0xC0208288|-1071611256|DTS_E_FG_NOBLOBS|Eingabespalten vom Typ IMAGE, TEXT oder NTEXT werden von der Fuzzygruppierung nicht unterstützt.|  
|0xC0208289|-1071611255|DTS_E_FG_FUZZY_MATCH_ON_NONSTRING|In der Spalte "%1" (%2!d!) ist eine Fuzzyübereinstimmung angegeben, die nicht den Datentypen DT_STR oder DT_WSTR entspricht.|  
|0xC020828A|-1071611254|DTS_E_FUZZYGROUPINGINTERNALPIPELINEERROR|Pipelinefehler bei der Transformation für Fuzzygruppierung (Fehlercode: 0x%1!8.8X!: "%2").|  
|0xC020828B|-1071611253|DTS_E_CODE_PAGE_NOT_SUPPORTED|Die Codepage %1!d!, die für die %2-Spalte (%3!d!) angegeben wurde, wird nicht unterstützt.  Sie müssen diese Spalte zuerst in DT_WSTR konvertieren, indem Sie davor eine Transformation für Datenkonvertierung einfügen.|  
|0xC0208294|-1071611244|DTS_E_SETEODFAILED|Fehler beim Festlegen des Datenendeflags für den Puffer, der die Ausgabe "%1" (%2!d!) steuert.|  
|0xC0208296|-1071611242|DTS_E_CANTCLONE|Der Eingabepuffer konnte nicht geklont werden. Es ist nicht genügend Arbeitsspeicher verfügbar, oder ein interner Fehler ist aufgetreten.|  
|0xC02082F9|-1071611143|DTS_E_TXCHARMAP_CANTKATAKANAHIRAGANA|Für die Spalte "%1" müssen gleichzeitig Katakana- und Hiragana-Zeichen erstellt werden.|  
|0xC02082FA|-1071611142|DTS_E_TXCHARMAP_CANTSIMPLECOMPLEX|Für die Spalte "%1" müssen gleichzeitig Zeichen in vereinfachtem und traditionellem Chinesisch erstellt werden.|  
|0xC02082FB|-1071611141|DTS_E_TXCHARMAP_CANTFULLHALF|Für die Spalte "%1" müssen für Vorgänge Zeichen mit voller und halber Breite generiert werden.|  
|0xC02082FC|-1071611140|DTS_E_TXCHARMAP_CANTCHINAJAPAN|In der Spalte "%1" werden Vorgänge mit japanischen Zeichen und Vorgänge mit chinesischen Zeichen miteinander kombiniert.|  
|0xC02082FD|-1071611139|DTS_E_TXCHARMAP_CANTCASECHINESE|In der Spalte "%1" werden Vorgänge mit chinesischen Zeichen und Vorgänge mit Groß- und Kleinbuchstaben miteinander kombiniert.|  
|0xC02082FE|-1071611138|DTS_E_TXCHARMAP_CANTCASEJAPANESE|In der Spalte "%1" werden Vorgänge mit japanischen Zeichen und Vorgänge mit Groß- und Kleinbuchstaben miteinander kombiniert.|  
|0xC02082FF|-1071611137|DTS_E_TXCHARMAP_CANTBOTHCASE|Die Spalte "%1" ordnet der Spalte Groß- und Kleinbuchstaben zu.|  
|0xC0208300|-1071611136|DTS_E_TXCHARMAP_CANTLINGUISTIC|In der Spalte "%1" werden andere Flags als die für Groß- und Kleinbuchstaben mit der linguistischen Schreibweise kombiniert.|  
|0xC0208301|-1071611135|DTS_E_TXCHARMAP_INVALIDMAPFLAGANDDATATYPE|Der Datentyp der Spalte "%1" kann nicht wie angegeben zugeordnet werden.|  
|0xC0208302|-1071611134|DTS_E_TXFUZZYLOOKUP_UNSUPPORTED_MATCH_INDEX_VERSION|Die Version (%1) des bereits vorhandenen Übereinstimmungsindex "%2" wird nicht unterstützt. Es wurde die Version "%3" erwartet. Dieser Fehler tritt auf, wenn die Version in den Indexmetadaten nicht mit der Version übereinstimmt, für die der aktuelle Code erstellt wurde. Beheben Sie den Fehler, indem Sie den Index mit der aktuellen Codeversion neu erstellen.|  
|0xC0208303|-1071611133|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX|Die Tabelle "%1" scheint kein gültiger vorgefertigter Übereinstimmungsindex zu sein. Dieser Fehler tritt auf, wenn der Metadatensatz nicht aus dem angegebenen vorgefertigten Index geladen werden kann.|  
|0xC0208304|-1071611132|DTS_E_TXFUZZYLOOKUP_UNABLE_TO_READ_MATCH_INDEX|Der angegebene vorgefertigte Übereinstimmungsindex "%1" kann nicht gelesen werden.  OLE DB-Fehlercode: 0x%2!8.8X!.|  
|0xC0208305|-1071611131|DTS_E_TXFUZZYLOOKUP_NO_JOIN_COLUMNS|Es waren keine Eingabespalten mit einem gültigen Join zu einer Verweistabellenspalte vorhanden.  Stellen Sie sicher, dass mindestens ein Join definiert ist, die die Eingabespalteneigenschaften JoinToReferenceColumn und JoinType verwendet.|  
|0xC0208306|-1071611130|DTS_E_TXFUZZYLOOKUP_INDEX_DOES_NOT_CONTAIN_COLUMN|Der angegebene bereits vorhandene Übereinstimmungsindex "%1" wurde ursprünglich nicht mit Fuzzyübereinstimmungsinformationen für die Spalte "%2" erstellt.  Es muss neu erstellt werden, um die Informationen aufzunehmen. Dieser Fehler tritt auf, wenn der Index erstellt wurde, ohne dass die Spalte eine Fuzzyjoinspalte ist.|  
|0xC0208307|-1071611129|DTS_E_TXFUZZYLOOKUP_IDENTIFIER_PROPERTY|Der Name "%1" für die Eigenschaft "%2" ist kein gültiger SQL-Bezeichnername. Dieser Fehler tritt auf, wenn der Name für die Eigenschaft nicht den Spezifikationen für gültige SQL-Bezeichnernamen entspricht.|  
|0xC0208309|-1071611127|DTS_E_TXFUZZYLOOKUP_MINSIMILARITY_INVALID|Die MinSimilarityThreshold-Eigenschaft in der Transformation für Fuzzysuche muss ein Wert zwischen 0,0 und 1,0 sein.|  
|0xC020830A|-1071611126|DTS_E_TXFUZZYLOOKUP_INVALID_PROPERTY_VALUE|Der Wert "%1" für die Eigenschaft "%2" ist ungültig.|  
|0xC020830B|-1071611125|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_FUZZY_JOIN_DATATYPES|Die zwischen der Eingabespalte "%1" und der Verweisspalte "%2" angegebene Fuzzysuche ist ungültig, weil Fuzzyjoins nur zwischen Zeichenfolgenspalten vom Typ DT_STR und DT_WSTR unterstützt werden.|  
|0xC020830C|-1071611124|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_EXACT_JOIN_DATATYPES|Die genauen Suchspalten "%1" und "%2" weisen keine identischen Datentypen auf oder sind nicht vergleichbare Zeichenfolgentypen. Genaue Joins werden zwischen Spalten mit identischen Datentypen oder einer Kombination aus DT_STR und DT_WSTR unterstützt.|  
|0xC020830D|-1071611123|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_COPYCOLUMN_DATATYPES|Die Kopierspalten "%1" und "%2" weisen keine identischen Datentypen auf oder sind keine einfach konvertierbaren Zeichenfolgentypen. Dieser Fehler tritt auf, weil das Kopieren vom Verweis zur Ausgabe zwischen Spalten mit identischen Datentypen bzw. einer Kombination aus DT_STR und DT_WSTR unterstützt wird, andere Datentypen jedoch nicht.|  
|0xC020830E|-1071611122|DTS_E_TXFUZZYLOOKUP_INCOMPATIBLE_PASSTHRUCOLUMN_DATATYPES|Die Pass-Through-Spalten "%1" und "%2" weisen keine identischen Datentypen auf. Nur Spalten mit identischen Datentypen werden als Pass-Through-Spalten von der Eingabe zur Ausgabe unterstützt.|  
|0xC020830F|-1071611121|DTS_E_TXFUZZYLOOKUP_UNABLETOLOCATEREFCOLUMN|Die Verweisspalte "%1" wurde nicht gefunden.|  
|0xC0208311|-1071611119|DTS_E_TXFUZZYLOOKUP_OUTPUT_COLUMN_MUST_BE_PASSTHRU_COLUMN_OR_A_COPY_COLUMN|Für eine Ausgabespalte muss genau eine CopyColumn-Eigenschaft oder PassThruColumn-Eigenschaft angegeben sein. Dieser Fehler tritt auf, wenn weder für die CopyColumn-Eigenschaft noch für die PassThruColumn-Eigenschaft oder sowohl für die CopyColumn-Eigenschaft als auch für die PassThruColumn-Eigenschaften nicht leere Werte festgelegt sind.|  
|0xC0208312|-1071611118|DTS_E_TXFUZZYLOOKUP_PASSTHRU_COLUMN_NOT_FOUND|Die Quellherkunfts-ID „'%1! d!“, die für die Eigenschaft „'%2'“ in der Ausgabespalte „'%3'“ angegeben ist, wurde in der Eingabespaltenauflistung nicht gefunden. Dieser Fehler tritt auf, wenn die für eine Ausgabespalte als Pass-Through-Spalte angegebene Eingabespalten-ID nicht in der Gruppe der Eingaben gefunden wird.|  
|0xC0208313|-1071611117|DTS_E_TXFUZZYLOOKUP_INDEXED_COLUMN_NOT_FOUND_IN_REF_TABLE|Die Spalte "%1" im vorgefertigten Index "%2" wurde in der Verweistabelle/Abfrage nicht gefunden. Dieser Fehler tritt auf, wenn das Schema bzw. die Abfrage der Verweistabelle seit dem Erstellen des bereits vorhandenen Übereinstimmungsindexes geändert wurde.|  
|0xC0208314|-1071611116|DTS_E_TXFUZZYLOOKUP_TOKEN_TOO_LONG|Die Komponente hat ein Token mit mehr als 2147483647 Zeichen gefunden.|  
|0xC0208315|-1071611115|DTS_E_RAWMETADATAMISMATCHTYPE|Die Ausgabedatei kann nicht angefügt werden. Die Spalte "%1" stimmt bezüglich des Namens überein, aber die Spalte in der Datei weist den Typ %2 und die Eingabespalte den Typ %3 auf. Die Metadaten für die Spalte stimmen bezüglich des Datentyps nicht überein.|  
|0xC0208316|-1071611114|DTS_E_RAWMETADATAMISMATCHSIZE|Die Ausgabedatei kann nicht angefügt werden. Die Spalte "%1" stimmt bezüglich des Namens überein, aber die Spalte in der Datei weist die maximale Länge %2!d! und die Eingabespalte die maximale Länge %3 d! auf. Die Metadaten für die Spalte stimmen bezüglich der Länge nicht überein.|  
|0xC0208317|-1071611113|DTS_E_RAWMETADATAMISMATCHCODEPAGE|Die Ausgabedatei kann nicht angefügt werden. Die Spalte "%1" stimmt bezüglich des Namens überein, aber die Spalte in der Datei weist die Codepage %2!d! und die Eingabespalte die Codepage %3!d! auf. Die Metadaten für die Spalte stimmen bezüglich der Codepage nicht überein.|  
|0xC0208318|-1071611112|DTS_E_RAWMETADATAMISMATCHPRECISION|Die Ausgabedatei kann nicht angefügt werden. Die Spalte "%1" stimmt bezüglich des Namens überein, aber die Spalte in der Datei weist die Genauigkeit %2!d! und die Eingabespalte die Genauigkeit %3!d! auf. Die Metadaten für die Spalte stimmen bezüglich der Genauigkeit nicht überein.|  
|0xC0208319|-1071611111|DTS_E_RAWMETADATAMISMATCHSCALE|Die Ausgabedatei kann nicht angefügt werden. Die Spalte "%1" stimmt bezüglich des Namens überein, aber die Spalte in der Datei weist die Dezimalstellen %2!d! und die Eingabespalte die Dezimalstellen %3!d! auf.  Die Metadaten für die Spalte stimmen bezüglich der Dezimalstellenanzahl nicht überein.|  
|0xC020831A|-1071611110|DTS_E_COULD_NOT_DETERMINE_DATASOURCE_DBMSNAME|Der DBMS-Name und die Version können für "%1" nicht bestimmt werden. Dieser Fehler tritt auf, wenn die IDBProperties-Schnittstelle für die Verbindung keine Informationen zurückgab, die zum Überprüfen des DBMS-Namens und der Version erforderlich sind.|  
|0xC020831B|-1071611109|DTS_E_INCORRECT_SQL_SERVER_VERSION|Der DBMS-Typ oder die Version von "%1" wird nicht unterstützt.  Eine Verbindung mit Microsoft SQL Server, Version 8.0 oder höher, ist erforderlich. Dieser Fehler tritt auf, wenn die IDBProperties-Schnittstelle für die Verbindung nicht die richtige Version zurückgab.|  
|0xC020831D|-1071611107|DTS_E_CANTDELETEERRORCOLUMNS|%1 ist eine spezielle Fehlerausgabespalte und kann nicht gelöscht werden.|  
|0xC020831E|-1071611106|DTS_E_UNEXPECTEDCOLUMNDATATYPE|Der für die Spalte "%1" angegebene Datentyp ist nicht der erwartete Typ "%2".|  
|0xC020831F|-1071611105|DTS_E_INPUTCOLUMNNOTFOUND|Die Herkunfts-ID "%1" der Eingabespalte, auf die die Eigenschaft "%2" der Ausgabespalte "%3" verweist, wurde in der Eingabespaltenauflistung nicht gefunden.|  
|0xC0208320|-1071611104|DTS_E_TXGROUPDUPS_INPUTCOLUMNNOTJOINED|Die Eingabespalte "%1", auf die die Eigenschaft "%2" der Ausgabespalte "%3" verweist, muss für die ToBeCleaned-Eigenschaft den Wert TRUE und für die ExactFuzzy-Eigenschaft einen gültigen Wert aufweisen.|  
|0xC0208322|-1071611102|DTS_E_TXFUZZYLOOKUP_REF_TABLE_MISSING_IDENTITY_INDEX|Die Verweistabelle '%1' weist keinen gruppierten Index für eine ganzzahlige Identitätsspalte auf. Dieser Index ist erforderlich, wenn die CopyRefTable-Eigenschaft auf FALSE festgelegt wird. Wenn die CopyRefTable-Eigenschaft auf FALSE festgelegt ist, benötigt die Verweistabelle einen gruppierten Index für eine ganzzahlige Identitätsspalte.|  
|0xC0208323|-1071611101|DTS_E_TXFUZZYLOOKUP_REF_CONTAINS_NON_INTEGER_IDENT_COLUMN|Die Verweistabelle '%1' enthält eine nicht ganzzahlige Identitätsspalte, die nicht unterstützt wird. Verwenden Sie eine Tabellensicht ohne die Spalte '%2'.  Dieser Fehler tritt auf, weil beim Erstellen einer Kopie der Verweistabelle eine ganzzahlige Identitätsspalte hinzugefügt wird, wobei aber nur eine Identitätsspalte pro Tabelle zulässig ist.|  
|0xC0208324|-1071611100|DTS_E_TXFUZZY_MATCHCONTRIBUTION_AND_HIERARCHY_SPECIFIED|MatchContribution und Informationen zur Hierarchie können nicht gleichzeitig angegeben werden. Dies ist nicht zulässig, weil diese Eigenschaften beide Gewichtungsfaktoren für die Bewertung sind.|  
|0xC0208325|-1071611099|DTS_E_TXFUZZY_HIERARCHY_INCORRECT|Hierarchieebenen müssen eindeutige Zahlen sein. Gültige Hierarchieebenenwerte sind ganze Zahlen größer oder gleich 1. Je kleiner die Zahl, desto niedriger ist die Spalte in der Hierarchie angesiedelt. Der Standardwert ist 0 (null), womit die Spalte zu keiner Hierarchie gehört. Überlappungen und Lücken sind nicht zulässig.|  
|0xC0208326|-1071611098|DTS_E_TXFUZZYGROUPING_INSUFFICIENT_FUZZY_JOIN_COLUMNS|Es wurden keine Spalten definiert, anhand derer eine Fuzzygruppierung ausgeführt werden kann.  Es muss mindestens eine Eingabespalte vorhanden sein, deren Spalteneigenschaften ToBeCleaned=true und ExactFuzzy=2 sind.|  
|0xC0208329|-1071611095|DTS_E_TXFUZZYLOOKUP_COLUMNINVALID|Die Spalte mit der ID „%1!d!“ war aus einem unbestimmten Grund ungültig.|  
|0xC020832A|-1071611094|DTS_E_TXFUZZYLOOKUP_UNSUPPORTEDDATATYPE|Der Datentyp der Spalte '%1' wird nicht unterstützt.|  
|0xC020832C|-1071611092|DTS_E_TXFUZZYLOOKUP_OUTPUTLENGTHMISMATCH|Die Ausgabespalte '%1' weist eine geringere Länge als die Quellspalte '%2' auf.|  
|0xC020832F|-1071611089|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFINPUTCOLUMNS|Es sollte nur eine Eingabespalte vorhanden sein.|  
|0xC0208330|-1071611088|DTS_E_TERMEXTRACTION_INCORRECTEXACTNUMBEROFOUTPUTCOLUMNS|Es sollte genau zwei Ausgabespalten geben.|  
|0xC0208331|-1071611087|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFINPUTCOLUMN|Für die Eingabespalte ist nur DT_WSTR oder DT_NTEXT als Datentyp zulässig.|  
|0xC0208332|-1071611086|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFOUTPUTCOLUMN|Für die Ausgabespalte [%1!d!] ist nur '%2' als Datentyp zulässig.|  
|0xC0208333|-1071611085|DTS_E_TERMEXTRACTION_INCORRECTDATATYPEOFREFERENCECOLUMN|Für die Verweisspalte ist nur DT_STR oder DT_WSTR als Datentyp zulässig.|  
|0xC0208334|-1071611084|DTS_E_TERMEXTRACTION_UNABLETOLOCATEREFCOLUMN|Fehler beim Suchen der Verweisspalte '%1'.|  
|0xC0208335|-1071611083|DTS_E_TERMEXTRACTION_INCORRECTTERMTYPE|Für den Ausdruckstyp der Transformation ist nur WordOnly, PhraseOnly oder WordPhrase zulässig.|  
|0xC0208336|-1071611082|DTS_E_TERMEXTRACTION_INCORRECTFREQUENCYTHRESHOLD|Der Schwellenwert für die Häufigkeit sollte nicht kleiner sein als '%1!d!'.|  
|0xC0208337|-1071611081|DTS_E_TERMEXTRACTION_INCORRECTMAXLENOFTERM|Die maximale Ausdruckslänge sollte nicht kleiner sein als '%1!d!'.|  
|0xC0208338|-1071611080|DTS_E_TERMEXTRACTION_TOOFEWREFERENCECOLUMNS|Die Verweismetadaten für die Ausdrucksextrahierung enthalten zu wenige Spalten.|  
|0xC0208339|-1071611079|DTS_E_TERMEXTRACTION_MALLOCERR_REFERENCECOLUMNINFO|Fehler beim Belegen von Arbeitsspeicher.|  
|0xC020833A|-1071611078|DTS_E_TERMEXTRACTION_MAINWORKSPACE_CREATEERR|Fehler beim Erstellen eines Arbeitsbereichspuffers.|  
|0xC020833B|-1071611077|DTS_E_TERMEXTRACTION_OLEDBERR_CREATEBINDING|OLE DB-Fehler beim Erstellen von Bindungen.|  
|0xC020833C|-1071611076|DTS_E_TERMEXTRACTION_OLEDBERR_GETIROWSET|OLE DB-Fehler beim Abrufen von Rowsets.|  
|0xC020833D|-1071611075|DTS_E_TERMEXTRACTION_OLEDBERR_FILLBUFFER|OLE DB-Fehler beim Auffüllen des internen Caches.|  
|0xC020833E|-1071611074|DTS_E_TERMEXTRACTION_PROCESSERR|Fehler beim Extrahieren von Ausdrücken in Zeile %1!ld!, Spalte %2!ld!. Der Fehlercode 0x%3!8.8X! wurde zurückgegeben. Um das Problem zu umgehen, entfernen Sie diese Elemente aus der Eingabe.|  
|0xC020833F|-1071611073|DTS_E_TERMEXTRACTIONORLOOKUP_PROCESSERR_DEPOSITFULL|Die Anzahl von Ausdruckskandidaten überschreitet die Grenze von 4G.|  
|0xC0208340|-1071611072|DTS_E_TERMEXTRACTION_INVALIDOUTTERMTABLEORCOLUMN|Die Verweistabelle, Sicht oder Spalte, die für Ausschlussausdrücke verwendet wird, ist ungültig.|  
|0xC0208341|-1071611071|DTS_E_TXFUZZYLOOKUP_STRINGCOLUMNTOOLONG|Die Länge der Zeichenfolgenspalte '%1' übersteigt 4.000 Zeichen.  Eine Konvertierung von DT_STR zu DT_WSTR ist notwendig. So käme es zu einem Abschneiden.  Reduzieren Sie entweder die Spaltenbreite oder verwenden Sie nur die DT_WSTR-Spaltentypen.|  
|0xC0208342|-1071611070|DTS_E_TERMEXTRACTION_OUTTERMTABLEANDCOLUMNNOTSET|Die Verweistabelle, Sicht oder Spalte, die für einen Ausschlussausdruck verwendet werden soll, wurde nicht festgelegt.|  
|0xC0208343|-1071611069|DTS_E_TERMLOOKUP_TOOFEWOUTPUTCOLUMNS|Die Ausdruckssuche enthält zu wenige Ausgabespalten.|  
|0xC0208344|-1071611068|DTS_E_TERMLOOKUP_INCORRECTDATATYPEOFREFERENCECOLUMN|Für die Verweisspalte ist nur DT_STR oder DT_WSTR als Datentyp zulässig.|  
|0xC0208345|-1071611067|DTS_E_TERMLOOKUP_UNABLETOLOCATEREFCOLUMN|Fehler beim Suchen der Verweisspalte '%1'.|  
|0xC0208346|-1071611066|DTS_E_TERMLOOKUP_TOOFEWREFERENCECOLUMNS|Die Verweismetadaten für die Ausdruckssuche enthalten zu wenige Spalten.|  
|0xC0208347|-1071611065|DTS_E_TERMEXTRACTIONORLOOKUP_TESTOFFSETERROR|Fehler beim Normalisieren von Wörtern.|  
|0xC0208348|-1071611064|DTS_E_TERMLOOKUP_MAINWORKSPACE_CREATEERR|Fehler beim Erstellen eines Arbeitsbereichspuffers.|  
|0xC0208349|-1071611063|DTS_E_TERMLOOKUP_OLEDBERR_CREATEBINDING|OLE DB-Fehler beim Erstellen von Bindungen.|  
|0xC020834A|-1071611062|DTS_E_TERMLOOKUP_OLEDBERR_GETIROWSET|OLE DB-Fehler beim Abrufen von Rowsets.|  
|0xC020834B|-1071611061|DTS_E_TERMLOOKUP_OLEDBERR_FILLBUFFER|OLE DB-Fehler beim Auffüllen des internen Caches.|  
|0xC020834C|-1071611060|DTS_E_TERMLOOKUP_PROCESSERR|Fehler beim Suchen nach Ausdrücken in Zeile %1!ld!, Spalte %2!ld!. Der Fehlercode 0x%3!8.8X! wurde zurückgegeben. Um das Problem zu umgehen, entfernen Sie diese Elemente aus der Eingabe.|  
|0xC020834D|-1071611059|DTS_E_TERMLOOKUP_TEXTIDINPUTCOLUMNNOTMAPPEDWITHOUTPUTCOLUMN|Mindestens eine Pass-Through-Spalte ist keiner Ausgabespalte zugeordnet.|  
|0xC020834E|-1071611058|DTS_E_TERMLOOKUP_INCORRECTEXACTNUMBEROFTEXTCOLUMNS|Es sollte genau eine Eingabespalte einer Verweisspalte zugeordnet sein.|  
|0xC020834F|-1071611057|DTS_E_TERMLOOKUP_TEXTINPUTCOLUMNHAVEINCORRECTDATATYPE|Für die Eingabespalte, die einer Verweisspalte zugeordnet ist, ist nur DT_NTXT oder DT_WSTR als Datentyp zulässig.|  
|0xC0208354|-1071611052|DTS_E_TXFUZZYLOOKUP_INVALID_MATCH_INDEX_NAME|Der Verweistabellenname "%1" ist kein gültiger SQL-Bezeichner. Dieser Fehler tritt auf, wenn der Tabellenname in der Eingabezeichenfolge nicht analysiert werden kann. Möglicherweise enthält der Name Leerzeichen ohne Anführungszeichen. Überprüfen Sie, ob Anführungszeichen für den Namen ordnungsgemäß verwendet sind.|  
|0xC0208355|-1071611051|DTS_E_TERMEXTRACTION_TERMFILTERSTARTITERATIONERROR|Fehler beim Starten der Iteration durch den Ausdrucksfilter.|  
|0xC0208356|-1071611050|DTS_E_TERMEXTRACTION_EMPTYTERMRESULTERROR|Fehler beim Freigeben des Puffers, der zum Zwischenspeichern von Ausdrücken verwendet wurde. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208357|-1071611049|DTS_E_TERMEXTRACTION_STDLENGTHERROR|std::length_error-Fehler in den STL-Containern.|  
|0xC0208358|-1071611048|DTS_E_TERMLOOKUP_SAVEWORDWITHPUNCTERROR|Fehler beim Speichern von Wörtern mit Satzzeichen. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208359|-1071611047|DTS_E_TERMLOOKUP_ADDREFERENCETERM|Fehler beim Verarbeiten des Verweisausdrucks %1!ld!th. Der Fehlercode 0x%2!8.8X! wurde zurückgegeben. Um das Problem zu umgehen, entfernen Sie den Verweisausdruck aus der Verweistabelle.|  
|0xC020835A|-1071611046|DTS_E_TERMLOOKUP_SORREFERENCETERM|Fehler beim Sortieren von Verweisausdrücken. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020835B|-1071611045|DTS_E_TERMLOOKUP_COUNTTERM|Fehler beim Zählen von Ausdruckskandidaten. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020835C|-1071611044|DTS_E_FUZZYLOOKUP_REFERENCECACHEFULL|Die Fuzzysuche konnte nicht die gesamte Verweistabelle in den Hauptspeicher laden, was bei aktivierter Exhaustive-Eigenschaft erforderlich ist.  Es war nicht genügend Systemarbeitsspeicher verfügbar, oder für 'MaxMemoryUsage' wurde eine Grenze angegeben, das zum Laden der Verweistabelle nicht ausreichend war.  Legen Sie MaxMemoryUsage auf 0 (null) fest, oder geben Sie einen deutlich höheren als den aktuellen Wert an.  Alternativ können Sie Exhaustive deaktivieren.|  
|0xC020835D|-1071611043|DTS_E_TERMLOOKUP_INITIALIZE|Fehler beim Initialisieren des Moduls für die Ausdruckssuche. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020835E|-1071611042|DTS_E_TERMLOOKUP_PROCESSSENTENCE|Fehler beim Verarbeiten von Sätzen. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020835F|-1071611041|DTS_E_TEXTMININGBASE_APPENDTOTEMPBUFFER|Fehler beim Hinzufügen von Zeichenfolgen zu einem internen Puffer. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208360|-1071611040|DTS_E_TERMEXTRACTION_SAVEPOSTAG|Fehler beim Speichern von Wortart-Tags in einem internen Puffer. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208361|-1071611039|DTS_E_TERMEXTRACTION_COUNTTERM|Fehler beim Zählen von Ausdruckskandidaten. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208362|-1071611038|DTS_E_TERMEXTRACTION_INITPOSPROCESSOR|Fehler beim Initialisieren des Wortart-Prozessors. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208363|-1071611037|DTS_E_TERMEXTRACTION_INITFSA|Fehler beim Laden des endlichen Automaten. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208364|-1071611036|DTS_E_TERMEXTRACTION_INITIALIZE|Fehler beim Initialisieren des Moduls für die Ausdrucksextrahierung. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208365|-1071611035|DTS_E_TERMEXTRACTION_PROCESSSENTENCE|Fehler beim Verarbeiten innerhalb eines Satzes. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208366|-1071611034|DTS_E_TERMEXTRACTION_INITPOSTAGVECTOR|Fehler beim Initialisieren des Wortart-Prozessors. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208367|-1071611033|DTS_E_TERMEXTRACTION_SAVEPTRSTRING|Fehler beim Hinzufügen von Zeichenfolgen zu einem internen Puffer. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208368|-1071611032|DTS_E_TERMEXTRACTION_ADDWORDTODECODER|Fehler beim Hinzufügen von Wörtern zu einem statistischen Decoder. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC0208369|-1071611031|DTS_E_TERMEXTRACTION_DECODE|Fehler beim Decodieren eines Satzes. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020836A|-1071611030|DTS_E_TERMEXTRACTION_SETEXCLUDEDTERM|Fehler beim Festlegen von Ausschlussausdrücken. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020836B|-1071611029|DTS_E_TERMEXTRACTION_PROCESSDOCUMENT|Fehler beim Verarbeiten eines Dokuments in der Eingabe. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020836C|-1071611028|DTS_E_TEXTMININGBASE_TESTPERIOD|Fehler beim Testen, ob ein Punkt Bestandteil eines Akronyms ist. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020836D|-1071611027|DTS_E_TERMLOOKUP_ENGINEADDREFERENCETERM|Fehler beim Festlegen von Verweisausdrücken. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020836E|-1071611026|DTS_E_TERMLOOKUP_PROCESSDOCUMENT|Fehler beim Verarbeiten eines Dokuments in der Eingabe. Der Fehlercode 0x%1!8.8X! wurde zurückgegeben.|  
|0xC020836F|-1071611025|DTS_E_INVALIDBULKINSERTPROPERTYVALUE|Die Eigenschaft %1 weist den Wert %2!d! auf, der unzulässig ist.  Dieser Wert muss größer oder gleich %3!d! sein.|  
|0xC0208370|-1071611024|DTS_E_INVALIDBULKINSERTFIRSTROWLASTROWVALUES|Die Eigenschaft %1 weist den Wert %2!d! auf. Dieser Wert muss kleiner oder gleich dem Wert von %3!d! für Eigenschaft %4 sein.|  
|0xC0208371|-1071611023|DTS_E_FUZZYLOOKUPUNABLETODELETEEXISTINGMATCHINDEX|Fehler beim Löschen des vorhandenen Fuzzyübereinstimmungsindexes "%1". Möglicherweise wurde die Tabelle nicht von der Fuzzysuche (oder dieser Version der Fuzzysuche) erstellt, sie wurde beschädigt, oder es liegt ein anderes Problem vor. Versuchen Sie die Tabelle "%2" manuell zu löschen, oder geben Sie einen anderen Namen für die MatchIndexName-Eigenschaft an.|  
|0xC0208372|-1071611022|DTS_E_TERMEXTRACTION_INCORRECTSCORETYPE|Für Ergebnistyp der Transformation ist nur Häufigkeit oder TFIDF möglich.|  
|0xC0208373|-1071611021|DTS_E_FUZZYLOOKUPREFTABLETOOBIG|Die angegebene Verweistabelle weist zu viele Zeilen auf. Die Fuzzysuche kann nur für Verweistabellen mit weniger als 1 Milliarde Zeilen verwendet werden. Verwenden Sie ggf. eine kleinere Verweistabellensicht.|  
|0xC0208374|-1071611020|DTS_E_FUZZYLOOKUPUNABLETODETERMINEREFERENCETABLESIZE|Die Größe der Verweistabelle '%1' kann nicht bestimmt werden.  Möglicherweise ist dieses Objekt keine Tabelle, sondern eine Sicht.  Die Fuzzysuche unterstützt keine Sichten, wenn CopyReferentaceTable=False ist.  Stellen Sie sicher, dass die Tabelle vorhanden ist und dass CopyReferenceTable=True ist.|  
|0xC0208377|-1071611017|DTS_E_XMLSRCOUTPUTCOLUMNDATATYPENOTSUPPORTED|Der Datentyp "%1" für den SSIS-Datenflusstask in %2 wird für %3 nicht unterstützt.|  
|0xC0208378|-1071611016|DTS_E_XMLSRCCANNOTFINDCOLUMNTOSETDATATYPE|Für die Ausgabespalte mit der ID %1!d! konnten in der Ausgabe mit der ID %2!d! keine Datentypeigenschaften festgelegt werden. Die Ausgabe oder Spalte wurde nicht gefunden.|  
|0xC0208379|-1071611015|DTS_E_CUSTOMPROPERTYISREADONLY|Der Wert der benutzerdefinierten Eigenschaft "%1" in %2 darf nicht geändert werden.|  
|0xC020837A|-1071611014|DTS_E_OUTPUTCOLUMNHASNOERRORCOLUMN|%1 in der Nichtfehlerausgabe weist keine entsprechende Ausgabespalte in der Fehlerausgabe auf.|  
|0xC020837B|-1071611013|DTS_E_ERRORCOLUMNHASNOOUTPUTCOLUMN|%1 in der Fehlerausgabe weist keine entsprechende Ausgabespalte in der Nichtfehlerausgabe auf.|  
|0xC020837C|-1071611012|DTS_E_ERRORCOLUMNHASINCORRECTPROPERTIES|%1 in der Fehlerausgabe weist Eigenschaften auf, die nicht mit den Eigenschaften der entsprechenden Datenquellspalte übereinstimmen.|  
|0xC020837D|-1071611011|DTS_E_ADOSRCOUTPUTCOLUMNDATATYPECANNOTBECHANGED|Der Datentyp von Ausgabespalten in %1 kann nicht geändert werden, außer bei den Spalten DT_WSTR und DT_NTEXT.|  
|0xC020837F|-1071611009|DTS_E_ADOSRCDATATYPEMISMATCH|Der Datentyp von "%1" stimmt nicht mit dem Datentyp "%2" der Quellspalte "%3" überein.|  
|0xC0208380|-1071611008|DTS_E_ADOSRCCOLUMNNOTINSCHEMAROWSET|%1 weist keine übereinstimmende Quellspalte im Schema auf.|  
|0xC0208381|-1071611007|DTS_E_TERMLOOKUP_INVALIDREFERENCETERMTABLEORCOLUMN|Die für die Verweisausdrücke verwendete Verweistabelle/Sicht ist ungültig.|  
|0xC0208382|-1071611006|DTS_E_TERMLOOKUP_REFERENCETERMTABLEANDCOLUMNNOTSET|Die für die Verweisausdrücke verwendete Verweistabelle/Sicht oder Spalte wurde nicht festgelegt.|  
|0xC0208383|-1071611005|DTS_E_COLUMNMAPPEDTOALREADYMAPPEDEXTERNALMETADATACOLUMN|%1 ist der externen Metadatenspalte mit der ID %2!ld! zugeordnet, die bereits einer anderen Spalte zugeordnet ist.|  
|0xC0208384|-1071611004|DTS_E_TXFUZZYLOOKUP_TOOMANYPREFIXES|Der für die Eigenschaft '%2' angegebene SQL-Objektname '%1' enthält mehr als die maximale Anzahl von Präfixen.  Maximal zulässig sind 2.|  
|0xC0208385|-1071611003|DTS_E_MGDSRCSTATIC_OVERFLOW|Der Wert war zu groß für die Spalte.|  
|0xC0208386|-1071611002|DTS_E_DATAREADERDESTREADERISCLOSED|Das SSIS-IDataReader-Objekt ist geschlossen.|  
|0xC0208387|-1071611001|DTS_E_DATAREADERDESTREADERISATEND|Das SSIS-IDataReader-Objekt liegt hinter dem Ende des Resultsets.|  
|0xC0208388|-1071611000|DTS_E_DATAREADERDESTINVALIDCOLUMNORDINAL|Die Ordnungsposition der Spalte ist ungültig.|  
|0xC0208389|-1071610999|DTS_E_DATAREADERDESTCANNOTCONVERT|%1 kann nicht vom Datentyp "%2" in den Datentyp "%3" konvertiert werden.|  
|0xC020838A|-1071610998|DTS_E_DATAREADERDESTINVALIDCODEPAGE|%1 weist die nicht unterstützte %2!d!-Codepage auf.|  
|0xC020838B|-1071610997|DTS_E_XMLSRCEXTERNALMETADATACOLUMNNOTINSCHEMA|%1 weist keine Zuordnung zum XML-Schema auf.|  
|0xC020838D|-1071610995|DTS_E_TXTERMLOOKUP_MISMATCHED_COLUMN_METADATA|Spalten mit den Herkunfts-IDs %1!d! und %2!d! weisen keine übereinstimmenden Metadaten auf. Die Eingabespalte, die einer Ausgabespalte zugeordnet ist, weist nicht dieselben Metadaten auf (Datentyp, Genauigkeit, Dezimalstellen, Länge oder Codepage).|  
|0xC020838E|-1071610994|DTS_E_DATAREADERDESTREADERTIMEOUT|Das SSIS-IDataReader-Objekt ist geschlossen. Das Lesetimeout ist abgelaufen.|  
|0xC020838F|-1071610993|DTS_E_ADOSRCINVALIDSQLCOMMAND|Fehler beim Ausführen des bereitgestellten SQL-Befehls: "%1". %2|  
|0xC0208390|-1071610992|DTS_E_JOINTYPEDOESNTMATCHETI|Die für die Eingabespalte '%1' angegebene JoinType-Eigenschaft unterscheidet sich vom JoinType, der für die entsprechende Verweistabellenspalte beim erstmaligen Erstellen des Übereinstimmungsindexes angegebenen wurde.  Erstellen Sie entweder den Übereinstimmungsindex mit dem angegebenen JoinType neu, oder ändern Sie den JoinType so, dass er mit dem Typ beim Erstellen des Übereinstimmungsindex übereinstimmt.|  
|0xC0208392|-1071610990|DTS_E_SQLCEDESTDATATYPENOTSUPPORTED|Der Datentyp "%1"in Spalte %2 wird für %3 nicht unterstützt.|  
|0xC0208393|-1071610989|DTS_E_DATAREADERDESTDATATYPENOTSUPPORTED|Der Datentyp "%1" in %2 wird für %3 nicht unterstützt.|  
|0xC0208394|-1071610988|DTS_E_RECORDSETDESTDATATYPENOTSUPPORTED|Der Datentyp von %1 wird für %2 nicht unterstützt.|  
|0xC0208446|-1071610810|DTS_E_TXSCRIPTMIGRATIONCOULDNOTADDREFERENCE|Fehler beim Hinzufügen des Projektverweises "%1" während der Migration von %2. Möglicherweise muss die Migration manuell abgeschlossen werden.|  
|0xC0208447|-1071610809|DTS_E_TXSCRIPTMIGRATIONMULTIPLEENTRYPOINTSFOUND|Während der Migration von %2 wurden mehrere Einstiegspunkte mit dem Namen "%1" gefunden. Möglicherweise muss die Migration manuell abgeschlossen werden.|  
|0xC0208448|-1071610808|DTS_E_TXSCRIPTMIGRATIONNOENTRYPOINTFOUND|Während der Migration von %1 wurde kein Einstiegspunkt gefunden. Möglicherweise muss die Migration manuell abgeschlossen werden.|  
|0xC020844B|-1071610805|DTS_E_ADODESTINSERTIONFAILURE|Ausnahme beim Einfügen von Daten. Die vom Anbieter zurückgegebene Meldung lautet: %1.|  
|0xC020844C|-1071610804|DTS_E_ADODESTCONNECTIONTYPENOTSUPPORTED|Der invariante Name des Anbieters konnte nicht aus %1 abgerufen werden, da dies derzeit von der ADO NET-Zielkomponente nicht unterstützt wird.|  
|0xC020844D|-1071610803|DTS_E_ADODESTARGUMENTEXCEPTION|Argumentausnahme beim Versuch des Datenanbieters, Daten in das Ziel einzufügen. Die zurückgegebene Meldung lautet: %1|  
|0xC020844E|-1071610802|DTS_E_ADODESTWRONGBATCHSIZE|Die BatchSize-Eigenschaft muss eine nicht negative ganze Zahl sein.|  
|0xC020844F|-1071610801|DTS_E_ADODESTERRORUPDATEROW|Fehler beim Senden dieser Zeile an die Zieldatenquelle.|  
|0xC0208450|-1071610800|DTS_E_ADODESTEXECUTEREADEREXCEPTION|Beim Ausführen des TSQL-Befehls wird eine Ausnahme zurückgegeben. Die Meldung lautet: %1|  
|0xC0208451|-1071610799|DTS_E_ADODESTDATATYPENOTSUPPORTED|Der Datentyp "%1"in Spalte %2 wird für %3 nicht unterstützt.|  
|0xC0208452|-1071610798|DTS_E_ADODESTFAILEDTOACQUIRECONNECTION|Das ADO NET-Ziel konnte die Verbindung %1 nicht abrufen. Die Verbindung ist möglicherweise beschädigt.|  
|0xC0208453|-1071610797|DTS_E_ADODESTNOTMANAGEDCONNECTION|Die angegebene Verbindung %1 wird nicht verwaltet. Verwenden Sie für das ADO NET-Ziel eine verwaltete Verbindung.|  
|0xC0208454|-1071610796|DTS_E_ADODESTNOERROROUTPUT|Die Zielkomponente verfügt nicht über eine Fehlerausgabe. Sie wurde möglicherweise beschädigt.|  
|0xC0208455|-1071610795|DTS_E_ADODESTNOLINEAGEID|Der der externen Spalte %2 zugeordnete lineageID-Wert %1 ist zur Laufzeit nicht vorhanden.|  
|0xC0208456|-1071610794|DTS_E_ADODESTEXTERNALCOLNOTEXIST|%1 ist nicht in der Datenbank vorhanden. Das Element wurde möglicherweise entfernt oder umbenannt.|  
|0xC0208457|-1071610793|DTS_E_ADODESTGETSCHEMATABLEFAILED|Fehler beim Abrufen von Eigenschaften externer Spalten. Der von Ihnen eingegebene Tabellenname ist möglicherweise nicht vorhanden, oder Sie verfügen nicht über die SELECT-Berechtigung für das Tabellenobjekt, und bei einem alternativen Versuch, Spalteneigenschaften über die Verbindung abzurufen, ist ein Fehler aufgetreten. Die genauen Fehlermeldungen lauten: %1|  
|0xC0208458|-1071610792|DTS_E_ADODESTCOLUMNERRORDISPNOTSUPPORTED|Die Fehlerdisposition für die Eingabespalte wird von der ADO NET-Zielkomponente nicht unterstützt.|  
|0xC0208459|-1071610791|DTS_E_ADODESTCOLUMNTRUNDISPNOTSUPPORTED|Die Abschneidedisposition für die Eingabespalte wird von der ADO NET-Zielkomponente nicht unterstützt.|  
|0xC020845A|-1071610790|DTS_E_ADODESTINPUTTRUNDISPNOTSUPPORTED|Die Abschneidezeilendisposition für die Eingabe wird von der ADO NET-Zielkomponente nicht unterstützt.|  
|0xC020845B|-1071610789|DTS_E_ADODESTTABLENAMEERROR|Der Tabellen- oder Sichtname wird nicht erwartet. \n\t Wenn Sie einen Tabellennamen angeben, verwenden Sie das Präfix %1 und das Suffix %2 des ausgewählten Datenanbieters. \n\t Wenn Sie einen mehrteiligen Namen verwenden, verwenden Sie höchstens drei Teile für den Tabellennamen.|  
|0xC0209001|-1071607807|DTS_E_FAILEDTOFINDCOLUMNINBUFFER|Fehler beim Suchen der Spalte "%1" mit der Herkunfts-ID %2!d! im Puffer. Der Puffer-Manager hat den Fehlercode 0x%3!8.8X! zurückgegeben.|  
|0xC0209002|-1071607806|DTS_E_FAILEDTOGETCOLUMNINFOFROMBUFFER|Fehler beim Abrufen von Informationen für die Spalte "%1" (%2!d!) aus dem Puffer. Der Fehlercode 0x%3!8.8X! wurde zurückgegeben.|  
|0xC0209011|-1071607791|DTS_E_TXAGG_ARITHMETICOVERFLOW|Arithmetischer Überlauf beim Aggregieren von "%1".|  
|0xC0209012|-1071607790|DTS_E_FAILEDTOGETCOLINFO|Fehler beim Abrufen von Informationen aus dem Puffer für Zeile %1!ld!, Spalte %2!ld! . Der Fehlercode 0x%3!8.8X! wurde zurückgegeben.|  
|0xC0209013|-1071607789|DTS_E_FAILEDTOSETCOLINFO|Fehler beim Eingeben von Informationen in den Puffer für Zeile %1!ld!, Spalte %2!ld! . Der Fehlercode 0x%3!8.8X! wurde zurückgegeben.|  
|0xC0209015|-1071607787|DTS_E_REQUIREDBUFFERISNOTAVAILBLE|Ein erforderlicher Puffer ist nicht verfügbar.|  
|0xC0209016|-1071607786|DTS_E_FAILEDTOGETBUFFERBOUNDARYINFO|Fehler beim Abrufen von Informationen zu den Puffergrenzwerten (Fehlercode: 0x%1!8.8X!).|  
|0xC0209017|-1071607785|DTS_E_FAILEDTOSETBUFFERENDOFROWSET|Fehler beim Festlegen des Rowsetendes für den Puffer (Fehlercode: 0x%1!8.8X!).|  
|0xC0209018|-1071607784|DTS_E_FAILEDTOGETDATAFORERROROUTPUTBUFFER|Fehler beim Abrufen von Daten für den Fehlerausgabepuffer.|  
|0xC0209019|-1071607783|DTS_E_FAILEDTOREMOVEROWFROMBUFFER|Fehler beim Entfernen einer Zeile aus dem Puffer (Fehlercode: 0x%1!8.8X!).|  
|0xC020901B|-1071607781|DTS_E_FAILEDTOSETBUFFERERRORINFO|Fehler beim Festlegen von Pufferfehlerinformationen (Fehlercode: 0x%1!8.8X!).|  
|0xC020901C|-1071607780|DTS_E_COLUMNSTATUSERROR|Fehler bei %1 für %2. Folgender Spaltenstatus wurde zurückgegeben: "%3".|  
|0xC020901D|-1071607779|DTS_E_TXLOOKUP_METADATAXMLCACHEERR|Verweismetadaten können nicht zwischengespeichert werden.|  
|0xC020901E|-1071607778|DTS_E_TXLOOKUP_ROWLOOKUPERROR|Die Zeile ergab bei der Suche keine Übereinstimmung.|  
|0xC020901F|-1071607777|DTS_E_INVALIDERRORDISPOSITION|%1 weist einen ungültigen Fehler oder eine Abschneidezeilendisposition auf.|  
|0xC0209022|-1071607774|DTS_E_FAILEDTODIRECTERRORROW|Fehler beim Umleiten der Zeile an die Fehlerausgabe (Fehlercode: 0x%1!8.8X!).|  
|0xC0209023|-1071607773|DTS_E_FAILEDTOPREPARECOLUMNSTATUSESFORINSERT|Fehler beim Vorbereiten der Spaltenstatus für das Einfügen (Fehlercode: 0x%1!8.8X!).|  
|0xC0209024|-1071607772|DTS_E_FAILEDTOFINDCOLUMNBYLINEAGEID|Fehler beim Suchen von %1 mit der Herkunfts-ID %2!d! im Datenflusstask-Puffer (Fehlercode: 0x%3!8.8X!).|  
|0xC0209025|-1071607771|DTS_E_FAILEDTOFINDNONSPECIALERRORCOLUMN|Fehler beim Suchen nicht spezieller Fehlerspalten in %1.|  
|0xC0209029|-1071607767|DTS_E_INDUCEDTRANSFORMFAILUREONERROR|SSIS-Fehlercode DTS_E_INDUCEDTRANSFORMFAILUREONERROR.  Fehler bei "%1" (Fehlercode: 0x%2!8.8X!). Die Fehlerzeilendisposition in "%3" gibt an, dass der Vorgang bei einem Fehler fehlschlägt. Im angegebenen Objekt in der angegebenen Komponente ist ein Fehler aufgetreten.  Möglicherweise wurden bereits Fehlermeldungen veröffentlicht, die weitere Fehlerinformationen beinhalten.|  
|0xC020902A|-1071607766|DTS_E_INDUCEDTRANSFORMFAILUREONTRUNCATION|Fehler bei "%1", weil Daten abgeschnitten wurden. Die Abschneidezeilendisposition in "%2" gibt einen Fehler beim Abschneiden an. Im angegebenen Objekt der angegebenen Komponente ist ein Abschneidefehler aufgetreten.|  
|0xC020902B|-1071607765|DTS_E_TXSPLITEXPRESSIONEVALUATEDTONULL|Der Ausdruck "%1" in "%2" ergab NULL, aber für "%3" ist ein boolesches Ergebnis erforderlich. Ändern Sie die Fehlerzeilendisposition in der Ausgabe, um das Ergebnis als 'False' zu behandeln (Fehler ignorieren) oder um die Zeile an die Fehlerausgabe umzuleiten (Zeile umleiten).  Für bedingtes Teilen müssen die Ausdrucksergebnisse boolesche Werte sein.  Das Ausdrucksergebnis NULL ist ein Fehler.|  
|0xC020902C|-1071607764|DTS_E_TXSPLITSTATIC_EXPRESSIONEVALUATEDTONULL|Der Ausdruck ergab NULL, aber ein boolesches Ergebnis ist erforderlich. Ändern Sie die Fehlerzeilendisposition in der Ausgabe, um das Ergebnis als 'False' zu behandeln (Fehler ignorieren) oder um die Zeile an die Fehlerausgabe umzuleiten (Zeile umleiten). Für bedingtes Teilen müssen die Ausdrucksergebnisse boolesche Werte sein.  Das Ausdrucksergebnis NULL ist ein Fehler.|  
|0xC020902D|-1071607763|DTS_E_UTF16BIGENDIANFORMATNOTSUPPORTED|Das Dateiformat UTF-16 Big-Endian wird nicht unterstützt.  Nur das Format UTF-16 Little-Endian wird unterstützt.|  
|0xC020902E|-1071607762|DTS_E_UTF8FORMATNOTSUPPORTEDASUNICODE|Das Dateiformat UTF-8 wird nicht als Unicode unterstützt.|  
|0xC020902F|-1071607761|DTS_E_DTPXMLCANTREADIDATTR|Das ID-Attribut kann nicht gelesen werden.|  
|0xC020903E|-1071607746|DTS_E_TXLOOKUP_INDEXCOLUMNREUSED|Auf die Cacheindexspalte %1 wird von mehr als einer Sucheingabespalte verwiesen.|  
|0xC020903F|-1071607745|DTS_E_TXLOOKUP_INDEXCOLUMNSMISMATCH|Die Suche verweist nicht auf alle Indexspalten des Cacheverbindungs-Managers. Anzahl verknüpfter Spalten in der Suche: %1!d!. Anzahl von Indexspalten: %2!d!.|  
|0xC0209069|-1071607703|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|Der Datenwert kann nicht konvertiert werden. Dieses Problem tritt nicht aufgrund nicht übereinstimmender Vorzeichen oder eines Datenüberlaufs auf.|  
|0xC020906A|-1071607702|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|Der Datenwert verletzte die Schemaeinschränkung.|  
|0xC020906B|-1071607701|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_TRUNCATED|Die Daten wurden abgeschnitten.|  
|0xC020906C|-1071607700|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Fehler bei der Konvertierung, da es sich um einen Datenwert mit Vorzeichen handelte und der vom Anbieter verwendete Datentyp kein Vorzeichen hatte.|  
|0xC020906D|-1071607699|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Fehler bei der Konvertierung, da der Datenwert zu einem Überlauf beim vom Anbieter verwendeten Datentyp führte.|  
|0xC020906E|-1071607698|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_UNAVAILABLE|Ein Status ist nicht verfügbar.|  
|0xC020906F|-1071607697|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|Der Benutzer verfügte nicht über die erforderlichen Berechtigungen, um in die Spalte zu schreiben.|  
|0xC0209070|-1071607696|DTS_E_COMMANDDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|Der Datenwert hat die Integritätseinschränkungen für die Spalte verletzt.|  
|0xC0209071|-1071607695|DTS_E_OLEDBSOURCEADAPTERSTATIC_UNAVAILABLE|Ein Status ist nicht verfügbar.|  
|0xC0209072|-1071607694|DTS_E_OLEDBSOURCEADAPTERSTATIC_CANTCONVERTVALUE|Der Datenwert kann nicht konvertiert werden. Dieses Problem tritt nicht aufgrund nicht übereinstimmender Vorzeichen oder eines Datenüberlaufs auf.|  
|0xC0209073|-1071607693|DTS_E_OLEDBSOURCEADAPTERSTATIC_TRUNCATED|Die Daten wurden abgeschnitten.|  
|0xC0209074|-1071607692|DTS_E_OLEDBSOURCEADAPTERSTATIC_SIGNMISMATCH|Fehler bei der Konvertierung, da es sich um einen Datenwert mit Vorzeichen handelte und der vom Anbieter verwendete Datentyp kein Vorzeichen hatte.|  
|0xC0209075|-1071607691|DTS_E_OLEDBSOURCEADAPTERSTATIC_DATAOVERFLOW|Fehler bei der Konvertierung, da der Datenwert zu einem Überlauf beim vom Anbieter verwendeten Datentyp führte.|  
|0xC0209076|-1071607690|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SCHEMAVIOLATION|Der Datenwert verletzte die Schemaeinschränkung.|  
|0xC0209077|-1071607689|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_CANTCONVERTVALUE|Der Datenwert kann nicht konvertiert werden. Dieses Problem tritt nicht aufgrund nicht übereinstimmender Vorzeichen oder eines Datenüberlaufs auf.|  
|0xC0209078|-1071607688|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_TRUNCATED|Die Daten wurden abgeschnitten.|  
|0xC0209079|-1071607687|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_SIGNMISMATCH|Fehler bei der Konvertierung, da es sich um einen Datenwert mit Vorzeichen handelte und der vom Anbieter verwendete Datentyp kein Vorzeichen hatte.|  
|0xC020907A|-1071607686|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_DATAOVERFLOW|Fehler bei der Konvertierung, da der Datenwert zu einem Überlauf beim vom Anbieter verwendeten Datentyp führte.|  
|0xC020907B|-1071607685|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_UNAVAILABLE|Ein Status ist nicht verfügbar.|  
|0xC020907C|-1071607684|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_PERMISSIONDENIED|Der Benutzer verfügte nicht über die erforderlichen Berechtigungen, um in die Spalte zu schreiben.|  
|0xC020907D|-1071607683|DTS_E_OLEDBDESTINATIONADAPTERSTATIC_INTEGRITYVIOLATION|Der Datenwert verletzt Integritätseinschränkungen.|  
|0xC020907F|-1071607681|DTS_E_TXDATACONVERTSTATIC_CANTCONVERTVALUE|Der Datenwert kann nicht konvertiert werden. Dieses Problem tritt nicht aufgrund nicht übereinstimmender Vorzeichen oder eines Datenüberlaufs auf.|  
|0xC0209080|-1071607680|DTS_E_TXDATACONVERTSTATIC_TRUNCATED|Die Daten wurden abgeschnitten.|  
|0xC0209081|-1071607679|DTS_E_TXDATACONVERTSTATIC_SIGNMISMATCH|Fehler bei der Konvertierung, da es sich um einen Datenwert mit Vorzeichen handelte und der vom Anbieter verwendete Datentyp kein Vorzeichen hatte.|  
|0xC0209082|-1071607678|DTS_E_TXDATACONVERTSTATIC_DATAOVERFLOW|Fehler bei der Konvertierung, da der Datenwert zu einem Überlauf beim Datentyp führte, der von der Transformation für Datenkonvertierung verwendet wird.|  
|0xC0209083|-1071607677|DTS_E_FLATFILESOURCEADAPTERSTATIC_UNAVAILABLE|Ein Status ist nicht verfügbar.|  
|0xC0209084|-1071607676|DTS_E_FLATFILESOURCEADAPTERSTATIC_CANTCONVERTVALUE|Der Datenwert kann nicht konvertiert werden. Dieses Problem tritt nicht aufgrund nicht übereinstimmender Vorzeichen oder eines Datenüberlaufs auf.|  
|0xC0209085|-1071607675|DTS_E_FLATFILESOURCEADAPTERSTATIC_TRUNCATED|Die Daten wurden abgeschnitten.|  
|0xC0209086|-1071607674|DTS_E_FLATFILESOURCEADAPTERSTATIC_SIGNMISMATCH|Fehler bei der Konvertierung, da es sich um einen Datenwert mit Vorzeichen handelte und der vom Flatfilequelladapter verwendete Datentyp kein Vorzeichen hatte.|  
|0xC0209087|-1071607673|DTS_E_FLATFILESOURCEADAPTERSTATIC_DATAOVERFLOW|Fehler bei der Konvertierung, da der Datenwert zu einem Überlauf beim vom Flatfilequelladapter verwendeten Datentyp führte.|  
|0xC020908E|-1071607666|DTS_E_TXDATACONVERTSTATIC_UNAVAILABLE|Ein Status ist nicht verfügbar.|  
|0xC0209090|-1071607664|DTS_E_FILEOPENERR_FORREAD|Fehler beim Öffnen der Datei "%1" zum Lesen (Fehlercode: 0x%2!8.8X!).|  
|0xC0209091|-1071607663|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD|Fehler beim Öffnen der Datei zum Lesen.|  
|0xC0209092|-1071607662|DTS_E_FILEOPENERR_FORWRITE|Fehler beim Öffnen der Datei "%1" zum Schreiben (Fehlercode: 0x%2!8.8X!).|  
|0xC0209093|-1071607661|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE|Fehler beim Öffnen der Datei zum Schreiben.|  
|0xC0209094|-1071607660|DTS_E_TXFILEINSERTERSTATIC_INSERTERCANTREAD|Fehler beim Lesen aus der Datei.|  
|0xC0209095|-1071607659|DTS_E_TXFILEEXTRACTORSTATIC_EXTRACTORCANTWRITE|Fehler beim Schreiben in die Datei.|  
|0xC0209099|-1071607655|DTS_E_DTPXMLINVALIDPROPERTYARRAYTOOMANYVALUES|Beim Analysieren einer Eigenschaft vom Typ Array wurden zu viele Arrayelemente gefunden. Der Wert des elementCount-Objekts ist niedriger als die Anzahl von gefundenen Arrayelementen.|  
|0xC020909A|-1071607654|DTS_E_DTPXMLINVALIDPROPERTYARRAYNOTENOUGHVALUES|Beim Analysieren einer Eigenschaft vom Typ Array wurden zu wenige Arrayelemente gefunden. Der Wert des elementCount-Objekts ist größer als die Anzahl von gefundenen Arrayelementen.|  
|0xC020909E|-1071607650|DTS_E_FILEOPENERR_FORWRITE_FILENOTFOUND|Fehler beim Öffnen der Datei "%1" zum Schreiben. Die Datei kann nicht gefunden werden.|  
|0xC020909F|-1071607649|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILENOTFOUND|Fehler beim Öffnen der Datei zum Schreiben. Die Datei kann nicht gefunden werden.|  
|0xC02090A0|-1071607648|DTS_E_FILEOPENERR_FORWRITE_PATHNOTFOUND|Fehler beim Öffnen der Datei "%1" zum Schreiben. Der Pfad kann nicht gefunden werden.|  
|0xC02090A1|-1071607647|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_PATHNOTFOUND|Fehler beim Öffnen der Datei zum Schreiben. Der Pfad kann nicht gefunden werden.|  
|0xC02090A2|-1071607646|DTS_E_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Fehler beim Öffnen der Datei "%1" zum Schreiben. Es sind zu viele Dateien geöffnet.|  
|0xC02090A3|-1071607645|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_TOOMANYOPENFILES|Fehler beim Öffnen der Datei zum Schreiben. Es sind zu viele Dateien geöffnet.|  
|0xC02090A4|-1071607644|DTS_E_FILEOPENERR_FORWRITE_ACCESSDENIED|Fehler beim Öffnen der Datei "%1" zum Schreiben. Sie verfügen nicht über die erforderlichen Berechtigungen.|  
|0xC02090A5|-1071607643|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_ACCESSDENIED|Fehler beim Öffnen der Datei zum Schreiben. Sie verfügen nicht über die erforderlichen Berechtigungen.|  
|0xC02090A6|-1071607642|DTS_E_FILEOPENERR_FORWRITE_FILEEXISTS|Fehler beim Öffnen der Datei "%1" zum Schreiben. Die Datei ist vorhanden und kann nicht überschrieben werden. Falls die Eigenschaften AllowAppend und ForceTruncate auf FALSE festgelegt sind, führt das Vorhandensein der Datei zu diesem Fehler.|  
|0xC02090A7|-1071607641|DTS_E_TXFILEEXTRACTORSTATIC_FILEOPENERR_FORWRITE_FILEEXISTS|Fehler beim Öffnen einer Datei zum Schreiben. Die Datei ist bereits vorhanden und kann nicht überschrieben werden. Falls die Eigenschaften AllowAppend und ForceTruncate auf FALSE festgelegt sind, führt das Vorhandensein der Datei zu diesem Fehler.|  
|0xC02090A8|-1071607640|DTS_E_INCORRECTCUSTOMPROPERTYVALUEFOROBJECT|Der Wert für die benutzerdefinierte Eigenschaft "%1 in %2 ist falsch.|  
|0xC02090A9|-1071607639|DTS_E_COLUMNSHAVEINCOMPATIBLEMETADATA|Die Spalten "%1" und "%2" weisen inkompatible Metadaten auf.|  
|0xC02090AD|-1071607635|DTS_E_FILEWRITEERR_DISKFULL|Fehler beim Öffnen der Datei "%1" zum Schreiben, weil der Datenträger voll ist. Es ist nicht genügend Speicherplatz zum Speichern dieser Datei vorhanden.|  
|0xC02090AE|-1071607634|DTS_E_TXFILEEXTRACTORSTATIC_FILEWRITEERR_DISKFULL|Fehler beim Öffnen der Datei zum Schreiben, weil der Datenträger voll ist.|  
|0xC02090B9|-1071607623|DTS_E_TXAGG_SORTKEYGENFAILED|Fehler beim Generieren eines Sortierschlüssels (Fehlercode: 0x%1!8.8X!). Die ComparisonFlags-Eigenschaft ist aktiviert, und mit LCMapString konnte kein Sortierschlüssel generiert werden.|  
|0xC02090BA|-1071607622|DTS_E_TXCHARMAPLCMAPFAILED|Die Transformation konnte keine Zeichenfolge zuordnen und hat den Fehler 0x%1!8.8X! zurückgegeben. Fehler bei LCMapString.|  
|0xC02090BB|-1071607621|DTS_E_FILEOPENERR_FORREAD_FILENOTFOUND|Fehler beim Öffnen der Datei "%1" zum Lesen. Die Datei wurde nicht gefunden.|  
|0xC02090BC|-1071607620|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_FILENOTFOUND|Fehler beim Öffnen einer Datei zum Lesen. Die Datei wurde nicht gefunden.|  
|0xC02090BD|-1071607619|DTS_E_FILEOPENERR_FORREAD_PATHNOTFOUND|Fehler beim Öffnen der Datei "%1" zum Lesen. Der Pfad kann nicht gefunden werden.|  
|0xC02090BE|-1071607618|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_PATHNOTFOUND|Fehler beim Öffnen einer Datei zum Lesen. Der Pfad wurde nicht gefunden.|  
|0xC02090BF|-1071607617|DTS_E_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Fehler beim Öffnen der Datei "%1" zum Lesen. Es sind zu viele Dateien geöffnet.|  
|0xC02090C0|-1071607616|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_TOOMANYOPENFILES|Fehler beim Öffnen der Datei zum Lesen. Es sind zu viele Dateien geöffnet.|  
|0xC02090C1|-1071607615|DTS_E_FILEOPENERR_FORREAD_ACCESSDENIED|Fehler beim Öffnen der Datei "%1" zum Lesen. Der Zugriff wird verweigert.|  
|0xC02090C2|-1071607614|DTS_E_TXFILEINSERTERSTATIC_FILEOPENERR_FORREAD_ACCESSDENIED|Fehler beim Öffnen der Datei zum Lesen. Sie verfügen nicht über die erforderlichen Berechtigungen.|  
|0xC02090C3|-1071607613|DTS_E_INSERTERINVALIDBOM|Der Wert für die Bytereihenfolgemarke (Byte Order Mark, BOM) für die Datei "%1" lautet 0x%2!4.4X!, es wurde jedoch der Wert 0x%3!4.4X! erwartet. Die ExpectBOM-Eigenschaft wurde für die Datei festgelegt, aber der BOM-Wert in der Datei fehlt oder ist ungültig.|  
|0xC02090C4|-1071607612|DTS_E_TXFILEINSERTERSTATIC_INSERTERINVALIDBOM|Der Wert für die Bytereihenfolgemarke (Byte Order Mark, BOM) für die Datei ist ungültig. Die ExpectBOM-Eigenschaft wurde für die Datei festgelegt, aber der BOM-Wert in der Datei fehlt oder ist ungültig.|  
|0xC02090C5|-1071607611|DTS_E_NOCOMPONENTATTACHED|%1 ist an keine Komponente angefügt.  Eine Komponente muss angefügt werden.|  
|0xC02090C9|-1071607607|DTS_E_TXLOOKUP_INVALIDMAXMEMORYPROP|Der Wert für die benutzerdefinierte Eigenschaft %1 ist falsch.  Der Wert sollte eine Zahl zwischen %2!d! und %3!I64d! sein.|  
|0xC02090CA|-1071607606|DTS_E_TXAGG_COMPFLAGS_BADAGGREGATIONTYPE|Die benutzerdefinierte Eigenschaft "%1" kann für den Aggregationstyp, der für die Spalte ausgewählt ist, nicht angegeben werden. Die benutzerdefinierte ComparisonFlags-Eigenschaft kann nur für die Aggregationstypen GROUP BY und COUNT DISTINCT angegeben werden.|  
|0xC02090CB|-1071607605|DTS_E_TXAGG_COMPFLAGS_BADDATATYPE|Die benutzerdefinierte ComparisonFlags-Eigenschaft "%1" kann nur für Spalten vom Datentyp DT_STR oder DT_WSTR angegeben werden.|  
|0xC02090CD|-1071607603|DTS_E_TXAGG_AGGREGATION_FAILURE|Fehler beim Aggregieren in %1 (Fehlercode: 0x%2!8.8X!).|  
|0xC02090CF|-1071607601|DTS_E_MAPPINGSETUPERROR|Fehler beim Einrichten der Zuordnung. %1|  
|0xC02090D0|-1071607600|DTS_E_XMLSRCUNABLETOREADXMLDATA|%1 konnte die XML-Daten nicht lesen.|  
|0xC02090D1|-1071607599|DTS_E_XMLSRCUNABLETOGETXMLDATAVARIABLE|%1 konnte die von der Eigenschaft "%2" angegebene Variable nicht abrufen.|  
|0xC02090D2|-1071607598|DTS_E_NODATATABLEMATCHROWID|%1 enthält für RowsetID den Wert %2, der nicht auf eine Datentabelle im Schema verweist.|  
|0xC02090D6|-1071607594|DTS_E_TXAGG_BADKEYSVALUE|Die Eigenschaft %1 muss entweder leer oder eine Zahl zwischen %2!u! und %3!u! sein. Die Keys-Eigenschaft oder die CountDistinctKeys-Eigenschaft weist einen ungültigen Wert auf. Die Eigenschaft sollte eine Zahl zwischen 0 (null) und ULONG_MAX inkl. aufweisen oder nicht festgelegt sein.|  
|0xC02090D7|-1071607593|DTS_E_TXAGG_TOOMANYKEYS|Die Aggregatkomponente hat zu viele unterschiedliche Schlüsselkombinationen erkannt. Es sind nicht mehr als %1!u! verschiedene Schlüsselwerte zulässig. Im Hauptarbeitsbereich sind mehr als ULONG_MAX verschiedene Schlüsselwerte vorhanden.|  
|0xC02090D8|-1071607592|DTS_E_TXAGG_TOOMANYCOUNTDISTINCTVALUES|Die Aggregatkomponente hat beim Berechnen des COUNT DISTINCT-Aggregats zu viele unterschiedliche Werte erkannt. Es sind nicht mehr als %1!u! verschiedene Werte zulässig. Beim Berechnen der COUNT DISTINCT-Aggregation waren mehr als ULONG_MAX verschiedene Werte vorhanden.|  
|0xC02090D9|-1071607591|DTS_E_FAILEDTOWRITETOTHEFILENAMECOLUMN|Fehler beim Schreiben in die Dateinamenspalte (Fehlercode: 0x%1!8.8X!).|  
|0xC02090DC|-1071607588|DTS_E_FAILEDTOFINDERRORCOLUMN|Ein Fehler ist aufgetreten, aber die Spalte, die den Fehler verursacht hat, kann nicht bestimmt werden.|  
|0xC02090E3|-1071607581|DTS_E_TXLOOKUP_FAILEDUPGRADE_BAD_VERSION|Suchmetadaten können von Version %1!d! nicht auf %2!d! aktualisiert werden. Die Transformation für Suche konnte Metadaten in einem Aufruf von PerformUpgrade() nicht von der vorhandenen Versionsnummer aktualisieren.|  
|0xC02090E5|-1071607579|DTS_E_TERMEXTRACTIONORLOOKUP_NTEXTSPLITED|Fehler beim Suchen der Begrenzung, die das Ende eines Satzes markiert.|  
|0xC02090E6|-1071607578|DTS_E_TERMEXTRACTION_EXCEED_MAXWORDNUM|Die Transformation zum Extrahieren von Ausdrücken kann den Eingabetext nicht verarbeiten, weil ein Satz aus dem Eingabetext zu lang ist. Der Satz wird in mehrere Sätze aufgeteilt.|  
|0xC02090E7|-1071607577|DTS_E_XMLSRCFAILEDTOCREATEREADER|%1 konnte die XML-Daten nicht lesen. %2|  
|0xC02090F0|-1071607568|DTS_E_TXLOOKUP_REINITMETADATAFAILED|Fehler beim Aufrufen der ReinitializeMetadata-Methode der Transformation für Suche.|  
|0xC02090F1|-1071607567|DTS_E_TXLOOKUP_NOJOINS|Die Transformation für Suche muss mindestens eine Eingabespalte enthalten, die mit einer Verweisspalte verknüpft ist. Es war jedoch keine angegeben. Sie müssen mindestens eine Joinspalte angeben.|  
|0xC02090F2|-1071607566|DTS_E_MANAGEDERR_BADFORMATSPECIFICATION|Die Meldungszeichenfolge, die von der verwalteten Fehlerinfrastruktur bereitgestellt wird, enthält eine Spezifikation mit einem fehlerhaften Format. Dies ist ein interner Fehler.|  
|0xC02090F3|-1071607565|DTS_E_MANAGEDERR_UNSUPPORTEDTYPE|Beim Formatieren einer Meldungszeichenfolge mithilfe der verwalteten Fehlerinfrastruktur war ein Variant-Typ vorhanden, der das Formatieren nicht unterstützt. Dies ist ein interner Fehler.|  
|0xC02090F5|-1071607563|DTS_E_DATAREADERSRCUNABLETOPROCESSDATA|%1 konnte die Daten nicht verarbeiten. %2|  
|0xC02090F6|-1071607562|DTS_E_XMLSRCEMPTYPROPERTY|Die Eigenschaft "%1" in %2 war leer.|  
|0xC02090F7|-1071607561|DTS_E_XMLSRCINVALIDOUTPUTNAME|Fehler beim Erstellen einer Ausgabe mit dem Namen "%1" für die XML-Tabelle mit dem Pfad "%2", weil der Name ungültig ist.|  
|0xC02090F8|-1071607560|DTS_E_MGDSRC_OVERFLOW|Der Wert war zu groß für %1.|  
|0xC02090F9|-1071607559|DTS_E_DATAREADERDESTUNABLETOPROCESSDATA|%1 konnte die Daten nicht verarbeiten.|  
|0xC02090FA|-1071607558|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONTRUNCATION|Fehler bei "%1", weil Daten abgeschnitten wurden. Die Abschneidezeilendisposition in "%2" bei "%3" gibt einen Fehler beim Abschneiden an. Im angegebenen Objekt der angegebenen Komponente ist ein Abschneidefehler aufgetreten.|  
|0xC02090FB|-1071607557|DTS_E_XMLSRC_INDUCEDTRANSFORMFAILUREONERROR|Fehler bei "%1" (Fehlercode: 0x%2!8.8X!). Die Fehlerzeilendisposition in "%3" bei "%4" gibt an, dass der Vorgang bei einem Fehler fehlschlägt. Im angegebenen Objekt in der angegebenen Komponente ist ein Fehler aufgetreten.|  
|0xC0209291|-1071607151|DTS_E_SQLCEDESTSTATIC_FAILEDTOSETVALUES|Das SQLCE-Ziel konnte die Spaltenwerte für die Zeile nicht festlegen.|  
|0xC0209292|-1071607150|DTS_E_SQLCEDESTSTATIC_FAILEDTOINSERT|Das SQLCE-Ziel konnte die Zeile nicht einfügen.|  
|0xC0209293|-1071607149|DTS_E_TXFUZZYLOOKUP_OLEDBERR_LOADCOLUMNMETADATA|OLE DB-Fehler beim Laden von Spaltenmetadaten.|  
|0xC0209294|-1071607148|DTS_E_TXFUZZYLOOKUP_TOOFEWREFERENCECOLUMNS|Die Verweismetadaten für die Suche enthalten zu wenige Spalten.|  
|0xC0209295|-1071607147|DTS_E_TXSCD_OLEDBERR_LOADCOLUMNMETADATA|OLE DB-Fehler beim Laden von Spaltenmetadaten.|  
|0xC0209296|-1071607146|DTS_E_TXSCD_TOOFEWREFERENCECOLUMNS|Die Verweismetadaten für die Suche enthalten zu wenige Spalten.|  
|0xC0209297|-1071607145|DTS_E_TXSCD_MALLOCERR_REFERENCECOLUMNINFO|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0209298|-1071607144|DTS_E_TXSCD_MALLOCERR_BUFFCOL|Arbeitsspeicher konnte nicht belegt werden.|  
|0xC0209299|-1071607143|DTS_E_TXSCD_MAINWORKSPACE_CREATEERR|Arbeitsbereichspuffer kann nicht erstellt werden.|  
|0xC020929A|-1071607142|DTS_E_DTPXMLDOMCREATEERROR|Das XML-DOM-Dokument kann nicht instanziiert werden. Überprüfen Sie, ob die MSXML-Binärdateien ordnungsgemäß installiert und registriert sind.|  
|0xC020929B|-1071607141|DTS_E_DTPXMLDOMLOADERROR|XML-Daten können zur Verarbeitung nicht in ein lokales DOM geladen werden.|  
|0xC020929C|-1071607140|DTS_E_RSTDESTBADVARIABLETYPE|Falscher Typ der Laufzeitvariable "%1". Die Laufzeitvariable muss vom Typ Object sein.|  
|0xC020929E|-1071607138|DTS_E_XMLDATAREADERMULTIPLEINLINEXMLSCHEMASNOTSUPPORTED|Der XML-Quelladapter konnte die XML-Daten nicht verarbeiten. Mehrere Inlineschemas werden nicht unterstützt.|  
|0xC020929F|-1071607137|DTS_E_XMLDATAREADERANYTYPENOTSUPPORTED|Der XML-Quelladapter konnte die XML-Daten nicht verarbeiten. Der Inhalt eines Elements kann nicht als anyType deklariert werden.|  
|0xC02092A0|-1071607136|DTS_E_XMLDATAREADERGROUPREFNOTSUPPORTED|Der XML-Quelladapter konnte die XML-Daten nicht verarbeiten. Der Inhalt eines Elements darf keinen Verweis auf eine Gruppe enthalten.|  
|0xC02092A1|-1071607135|DTS_E_XMLDATAREADERMIXEDCONTENTFORCOMPLEXTYPESNOTSUPPORTED|Der XML-Quelladapter unterstützt keine gemischten Inhaltsmodelle für Complex-Typen.|  
|0xC02092A2|-1071607134|DTS_E_XMLDATAREADERINLINESCHEMAFOUNDINSOURCEXML|Der XML-Quelladapter konnte die XML-Daten nicht verarbeiten. Ein Inlineschema muss der erste untergeordnete Knoten im XML-Code der Quelle sein.|  
|0xC02092A3|-1071607133|DTS_E_XMLDATAREADERNOINLINESCHEMAFOUND|Der XML-Quelladapter konnte die XML-Daten nicht verarbeiten. Im XML-Code der Quelle wurde kein Inlineschema gefunden, aber die UseInlineSchema-Eigenschaft war auf TRUE festgelegt.|  
|0xC02092A4|-1071607132|DTS_E_CONNECTIONMANAGERTRANSACTEDANDRETAINEDINBULKINSERT|Die Komponente kann keinen Verbindungs-Manager verwenden, der die Verbindung in einer Transaktion mit FASTLOAD oder BULK INSERT beibehält.|  
|0xC02092A5|-1071607131|DTS_E_OUTPUTREDIRECTINTRANSACTIONNOTALLOWED|%1 kann nicht festgelegt werden, um bei einem Fehler mithilfe einer Verbindung in einer Transaktion eine Umleitung auszuführen.|  
|0xC02092A6|-1071607130|DTS_E_FOUNDORPHANEDEXTERNALMETADATACOLUMN|%1 weist keine entsprechende Ein- oder Ausgabespalte auf.|  
|0xC02092A9|-1071607127|DTS_E_RAWDESTNOINPUTCOLUMNS|Es ist keine Spalte zum Schreiben in die Datei ausgewählt.|  
|0xC02092AA|-1071607126|DTS_E_RAWDESTBLOBDATATYPE|%1 weist einen ungültigen Datentyp auf. Spalten mit den Datentypen DT_IMAGE, DT_TEXT und DT_NTEXT können nicht in Rohdatendateien geschrieben werden.|  
|0xC02092AB|-1071607125|DTS_E_RAWDESTWRONGEXTERNALMETADATAUSAGE|Die Auflistung mit den externen Metadaten wird von dieser Komponente nicht ordnungsgemäß verwendet. Die Komponente sollte externe Metadaten beim Anfügen oder Abschneiden einer vorhandenen Datei verwenden. Andernfalls werden die externen Metadaten nicht benötigt.|  
|0xC02092AC|-1071607124|DTS_E_RAWDESTMAPPEDINPUTCOLUMN|%1 ist einer externen Metadatenspalte mit der ID %2!d! zugeordnet. Eingabespalten sollten nicht externen Metadatenspalten zugeordnet werden, wenn für Write Option der Wert Create Always ausgewählt ist.|  
|0xC02092AD|-1071607123|DTS_E_RAWFILECANTOPENFORMETADATA|Die Datei kann nicht zum Lesen der Metadaten geöffnet werden. Falls die Datei nicht vorhanden ist und für die Komponente bereits externe Metadaten definiert sind, können Sie die ValidateExternalMetadata-Eigenschaft auf 'false' festlegen. Die Datei wird dann zur Laufzeit erstellt.|  
|0xC02092AE|-1071607122|DTS_E_FAILEDTOACCESSLOBCOLUMN|Fehler beim Zugriff auf LOB-Daten im Datenflusspuffer für die Datenquellenspalte "%1" (Fehlercode: 0x%2!8.8X!).|  
|0xC02092AF|-1071607121|DTS_E_XMLSRCUNABLETOPROCESSXMLDATA|%1 konnte die XML-Daten nicht verarbeiten. %2|  
|0xC02092B0|-1071607120|DTS_E_XMLSRCSTATIC_UNABLETOPROCESSXMLDATA|Der XML-Quelladapter konnte die XML-Daten nicht verarbeiten.|  
|0xC02092B1|-1071607119|DTS_E_RAWINVALIDACCESSMODE|Der Wert %1!d! wird nicht als gültige Zugriffsmethode erkannt.|  
|0xC02092B2|-1071607118|DTS_E_INCOMPLETEDATASOURCECOLUMNFOUND|Für die Datenquellenspalte "%1" sind keine vollständigen Metadateninformationen verfügbar.  Stellen Sie sicher, dass die Spalte in der Datenquelle ordnungsgemäß definiert ist.|  
|0xC02092B3|-1071607117|DTS_E_TXAUDIT_ONLYSTRINGLENGTHCHANGEALLOWED|Es können nur die Längen der Spalten vom Typ Benutzername, Paketname, Taskname und Computername geändert werden.  Alle anderen Datentypinformationen von Überwachungsspalten sind schreibgeschützt.|  
|0xC02092B4|-1071607116|DTS_E_ROWSETUNAVAILABLE|Vom OLE DB-Anbieter wurde kein Rowset basierend auf dem SQL-Befehl zurückgegeben.|  
|0xC02092B5|-1071607115|DTS_E_COMMITFAILED|Fehler beim Commit.|  
|0xC02092B6|-1071607114|DTS_E_USEBINARYFORMATREQUIRESANSIFILE|Die benutzerdefinierte Eigenschaft "%1" in %2 kann nur mit ANSI-Dateien verwendet werden.|  
|0xC02092B7|-1071607113|DTS_E_USEBINARYFORMATREQUIRESBYTES|Die benutzerdefinierte Eigenschaft "%1" in %2 kann nur mit DT_BYTES verwendet werden.|  
|0xC0209302|-1071607038|DTS_E_OLEDB_NOPROVIDER_ERROR|SSIS-Fehlercode: DTS_E_OLEDB_NOPROVIDER_ERROR.  Der angeforderte OLE DB-Anbieter %2 ist nicht registriert. Fehlercode: 0x%1!8.8X!.|  
|0xC0209303|-1071607037|DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR|SSIS-Fehlercode: DTS_E_OLEDB_NOPROVIDER_64BIT_ERROR.  Der angeforderte OLE DB-Anbieter %2 ist nicht registriert – möglicherweise ist kein 64-Bit-Anbieter verfügbar.  Fehlercode: 0x%1!8.8X!.|  
|0xC0209306|-1071607034|DTS_E_MULTICACHECOLMAPPINGS|Die Cachespalte "%1" ist mehreren Spalten zugeordnet. Entfernen Sie die doppelten Spaltenzuordnungen.|  
|0xC0209307|-1071607033|DTS_E_COLNOTMAPPEDTOCACHECOL|%1 ist keiner gültigen Cachespalte zugeordnet.|  
|0xC0209308|-1071607032|DTS_E_CACHECOLDATATYPEINCOMPAT|Die Eingabespalte "%1" kann der Cachespalte "%2" nicht zugeordnet werden, da die Datentypen nicht übereinstimmen.|  
|0xC0209309|-1071607031|DTS_E_INCORRECTINPUTCACHECOLCOUNT|Die Anzahl der Eingabespalten stimmt nicht mit der Anzahl der Cachespalten überein.|  
|0xC020930A|-1071607030|DTS_E_INVALIDCACHEFILENAME|Der Cachedateiname ist entweder nicht bereitgestellt oder nicht gültig. Geben Sie einen gültigen Cachedateinamen an.|  
|0xC020930B|-1071607029|DTS_E_CACHECOLINDEXPOSMISMATCH|Die Indexposition der Spalte "%1" unterscheidet sich von der Indexposition der Spalte "%2" des Cacheverbindungs-Managers.|  
|0xC020930C|-1071607028|DTS_E_FAILEDTOLOADCACHE|Fehler beim Laden des Cache aus der Datei "%1".|  
|0xC020930D|-1071607027|DTS_E_TXLOOKUP_REFCOLUMNISNOTINDEX|Die Sucheingabespalte %1 verweist auf die Nicht-Indexcachespalte %2.|  
|0xC020930E|-1071607026|DTS_E_FAILEDTOGETCONNECTIONSTRING|Fehler beim Abrufen der Verbindungszeichenfolge.|  
|0xC020930F|-1071607025|DTS_E_CACHECOLDATATYPEPROPINCOMPAT|Die Eingabespalte "%1" und die Cachespalte "%2" können nicht zugeordnet werden, da eine oder mehrere Datentypeigenschaften nicht übereinstimmen.|  
|0xC0209311|-1071607023|DTS_E_CACHECOLUMNOTFOUND|Die Cachespalte "%1" wurde nicht im Cache gefunden.|  
|0xC0209312|-1071607022|DTS_E_CACHECOLUMNMAPPINGFAILED|Fehler beim Zuordnen von %1 zu einer Cachespalte. HRESULT lautet 0x%2!8.8X!.|  
|0xC0209313|-1071607021|DTS_E_CACHELOADEDFROMFILE|%1 kann nicht in den Cache schreiben, da der Cache von %2 aus einer Datei geladen wurde.|  
|0xC0209314|-1071607020|DTS_E_CACHERELOADEDDIFFERENTFILES|%1 kann den Cache nicht aus der Datei "%2" laden, da der Cache bereits aus der Datei "%3" geladen wurde.|  
|0xC0209316|-1071607018|DTS_E_OUTPUTNOTUSED|Die Ausgabe mit der ID %1!d! der Aggregatkomponente wird von keiner Komponente verwendet. Entfernen Sie die Ausgabe, oder verknüpfen Sie sie mit der Eingabe einer beliebigen Komponente.|  
|0xC0209317|-1071607017|DTS_E_CACHEFILEWRITEFAILED|%1 konnte den Cache nicht in die Datei "%2" schreiben. HRESULT lautet 0x%3!8.8X!.|  
|0xC0209318|-1071607016|DTS_E_XMLDATATYPECHANGED|Die Datentypinformationen des XML-Schemas für "%1" im Element "%2" wurden geändert.  Initialisieren Sie die Metadaten für diese Komponente neu, und überprüfen Sie die Spaltenzuordnungen.|  
|0xC0209319|-1071607015|DTS_E_TXLOOKUP_UNUSEDINPUTCOLUMN|%1 wird im Join oder in der Kopie nicht verwendet. Entfernen Sie die nicht verwendete Spalte aus der Eingabespaltenliste.|  
|0xC020931A|-1071607014|DTS_E_SORTSTACKOVERFLOW|Die Sortierung eines eingehenden Puffers ist aufgrund eines Stapelüberlaufs fehlgeschlagen.  Reduzieren Sie die DefaultBufferMaxRows-Eigenschaft im Datenflusstask.|  
|0xC020F42A|-1071582166|DTS_E_OLEDB_OLDPROVIDER_ERROR|Erwägen Sie, den ANBIETER in der Verbindungszeichenfolge auf %1 zu ändern, oder besuchen Sie http://www.microsoft.com/downloads, um Unterstützung für %2 zu finden und zu installieren.|  
|||DTS_E_INITTASKOBJECTFAILED|Fehler beim Initialisieren des Taskobjekts für Task „%1!s!“ vom Typ „%2!s!“. Es kann aufgrund des Fehlers 0x%3!8.8X! „%4! s!“ nicht erstellt werden.|  
|||DTS_E_GETCATMANAGERFAILED|Fehler beim Erstellen des COM-Komponenten-Kategorien-Managers aufgrund des Fehlers 0x%1!8.8X! „%2!s!“.|  
|||DTS_E_COMPONENTINITFAILED|Komponente %1!s! konnte nicht gestartet werden, und zwar aufgrund des Fehlers 0x%2!8.8X! „%3!s!“.|  
  
##  <a name="msgWarning"></a> Warnmeldungen  
 Die symbolischen Namen von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Warnmeldungen beginnen mit **DTS_W_**.  
  
|Hexadezimalcode|Dezimalcode|Symbolischer Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x80000036|-2147483594|DTS_W_COUNTDOWN|Es bleiben %1!lu! Tage für die Evaluierung. Nach Ablauf der Evaluierung können die Pakete nicht mehr ausgeführt werden.|  
|0x80010015|-2147418091|DTS_W_GENERICWARNING|Warnung(en) wurde(n) ausgelöst. Vorher sollten genauere Warnungen ausgegeben worden sein, die die Bedeutung der Warnung(en) erläutern.|  
|0x80012010|-2147409904|DTS_W_FAILEDXMLDOCCREATION|Eine Instanz des XML-Dokumentobjekts kann nicht erstellt werden. Überprüfen Sie, ob MSXML ordnungsgemäß installiert und registriert ist.|  
|0x80012011|-2147409903|DTS_W_FAILEDCONFIGLOAD|Die XML-Konfigurationsdatei kann nicht geladen werden. Möglicherweise ist die XML-Konfigurationsdatei fehlerhaft oder ungültig.|  
|0x80012012|-2147409902|DTS_W_CONFIGFILENAMEINVALID|Der Konfigurationsdateiname "%1" ist ungültig. Überprüfen Sie den Konfigurationsdateinamen.|  
|0x80012013|-2147409901|DTS_W_CONFIGFILEINVALID|Die Konfigurationsdatei wurde geladen, ist jedoch ungültig. Die Datei ist falsch formatiert, es fehlt ein Element, oder sie ist beschädigt.|  
|0x80012014|-2147409900|DTS_W_CONFIGFILENOTFOUND|Die Konfigurationsdatei "%1" wurde nicht gefunden. Überprüfen Sie den Verzeichnis- und Dateinamen.|  
|0x80012015|-2147409899|DTS_W_CONFIGKEYNOTFOUND|Der Konfigurationsregistrierungsschlüssel "%1" wurde nicht gefunden. Für einen Konfigurationseintrag ist ein nicht verfügbarer Registrierungsschlüssel angegeben. Überprüfen Sie die Registrierung, und stellen Sie sicher, dass der Schlüssel vorhanden ist.|  
|0x80012016|-2147409898|DTS_W_CONFIGTYPEINVALID|Der Konfigurationstyp in einem der Konfigurationseinträge war ungültig. Gültige Typen sind in der DTSConfigurationType-Enumeration aufgeführt.|  
|0x80012017|-2147409897|DTS_W_CANNOTFINDOBJECT|Der Paketpfad verwies auf ein Objekt, das nicht gefunden wurde: "%1". Dieses Problem tritt auf, wenn ein Paketpfad zu einem Objekt aufgelöst wird, das nicht gefunden wurde.|  
|0x80012018|-2147409896|DTS_W_CONFIGFORMATINVALID_PACKAGEDELIMITER|Der Konfigurationseintrag "%1" weist ein falsches Format auf, weil er nicht mit dem Pakettrennzeichen beginnt. Stellen Sie dem Paketpfad "\package" voran.|  
|0x80012019|-2147409895|DTS_W_CONFIGFORMATINVALID|Der Konfigurationseintrag "%1" weist ein falsches Format auf. Dies kann auf ein fehlendes Trennzeichen oder Formatierungsfehler, z. B ein ungültiges Arraytrennzeichen, zurückzuführen sein.|  
|0x8001201A|-2147409894|DTS_W_NOPARENTVARIABLES|Die Konfiguration der übergeordneten Variable "%1" ist nicht erfolgt, weil keine übergeordnete Variablenauflistung vorhanden war.|  
|0x8001201B|-2147409893|DTS_W_CONFIGFILEFAILEDIMPORT|Fehler beim Importieren der Konfigurationsdatei: "%1".|  
|0x8001201C|-2147409892|DTS_W_PARENTVARIABLENOTFOUND|Die Konfiguration der übergeordneten Variable "%1" ist nicht erfolgt, weil keine übergeordnete Variable vorhanden war. Fehlercode: 0x%2!8.8X!.|  
|0x8001201D|-2147409891|DTS_W_CONFIGFILEEMPTY|Die Konfigurationsdatei war leer und enthielt keine Konfigurationseinträge.|  
|0x80012023|-2147409885|DTS_W_INVALIDCONFIGURATIONTYPE|Der Konfigurationstyp für die Konfiguration "%1" ist ungültig. Dieses Problem tritt auf, wenn die Typeigenschaft eines Konfigurationsobjekts auf einen ungültigen Konfigurationstyp festgelegt wird.|  
|0x80012025|-2147409883|DTS_W_REGISTRYCONFIGURATIONTYPENOTFOUND|Der Konfigurationstyp für die Registrierungskonfiguration wurde im Schlüssel "%1" nicht gefunden. Fügen Sie dem Registrierungsschlüssel einen ConfigType-Wert mit dem Zeichenfolgenwert "Variable", "Property", "ConnectionManager", "LoggingProvider" oder "ForEachEnumerator" hinzu.|  
|0x80012026|-2147409882|DTS_W_REGISTRYCONFIGURATIONVALUENOTFOUND|Der Konfigurationswert für die Registrierungskonfiguration wurde im Schlüssel "%1" nicht gefunden. Fügen Sie dem Registrierungsschlüssel einen Value-Wert vom Typ DWORD oder String hinzu.|  
|0x80012028|-2147409880|DTS_W_PROCESSCONFIGURATIONFAILEDSET|Fehler beim Festlegen des Paketpfads für "%1" durch die Prozesskonfiguration. Dieses Problem tritt auf, wenn beim Festlegen der Zieleigenschaft oder -variablen ein Fehler auftritt. Überprüfen Sie die Zieleigenschaft oder -variable.|  
|0x80012032|-2147409870|DTS_W_CONFIGUREDVALUESECTIONEMPTY|Fehler beim Abrufen des Werts aus der INI-Datei. Der ConfiguredValue-Abschnitt ist entweder leer oder nicht vorhanden: "%1".|  
|0x80012033|-2147409869|DTS_W_CONFIGUREDTYPESECTIONEMPTY|Fehler beim Abrufen des Werts aus der INI-Datei. Der ConfiguredType-Abschnitt ist entweder leer oder nicht vorhanden: "%1".|  
|0x80012034|-2147409868|DTS_W_PACKAGEPATHSECTIONEMPTY|Fehler beim Abrufen des Werts aus der INI-Datei. Der PackagePath-Abschnitt ist entweder leer oder nicht vorhanden: "%1".|  
|0x80012035|-2147409867|DTS_W_CONFIGUREDVALUETYPE|Fehler beim Abrufen des Werts aus der INI-Datei. Der ConfiguredValueType-Abschnitt ist entweder leer oder nicht vorhanden: "%1".|  
|0x80012051|-2147409839|DTS_W_SQLSERVERFAILEDIMPORT|Die Konfiguration von SQL Server wurde nicht erfolgreich importiert: "%1".|  
|0x80012052|-2147409838|DTS_W_INICONFIGURATIONPROBLEM|Die INI-Konfigurationsdatei ist aufgrund leerer oder fehlender Felder ungültig.|  
|0x80012054|-2147409836|DTS_W_NORECORDSFOUNDINTABLE|Die Tabelle "%1" weist keine Einträge für die Konfiguration auf. Dieses Problem tritt beim Konfigurieren einer SQL Server-Tabelle auf, die keine Einträge für die Konfiguration besitzt.|  
|0x80012055|-2147409835|DTS_W_DUPLICATECUSTOMEVENT|Fehler beim Verwenden desselben Namens für verschiedene benutzerdefinierte Ereignisse. Das benutzerdefinierte Ereignis "%1" wurde von verschiedenen untergeordneten Elementen dieses Containers unterschiedlich definiert. Bei der Ausführung des Ereignishandlers kann ein Fehler auftreten.|  
|0x80012057|-2147409833|DTS_W_CONFIGREADONLYVARIABLE|Die Konfiguration hat versucht, eine schreibgeschützte Variable zu ändern. Die Variable befindet sich im Paketpfad "%1".|  
|0x80012058|-2147409832|DTS_W_CONFIGPROCESSCONFIGURATIONFAILED|Fehler beim Aufrufen der ProcessConfiguration-Eigenschaft im Paket. Die Konfiguration hat versucht, die Eigenschaft im Paketpfad "%1" zu ändern.|  
|0x80012059|-2147409831|DTS_W_ONEORMORECONFIGLOADFAILED|Fehler beim Laden von mindestens einem Konfigurationseintrag für das Paket. Überprüfen Sie die Konfigurationseinträge für "%1" und vorherige Warnungen, um herauszufinden, bei welcher Konfiguration der Fehler aufgetreten ist.|  
|0x8001205A|-2147409830|DTS_W_CONFIGNODEINVALID|Der Konfigurationseintrag "%1" in der Konfigurationsdatei war ungültig oder konnte die Variable nicht konfigurieren.  Der Name weist darauf hin, bei welchem Eintrag der Fehler aufgetreten ist. In manchen Fällen ist kein Name verfügbar.|  
|0x80014058|-2147401640|DTS_W_FAILURENOTRESTARTABLE|Fehler bei diesem Task oder Container. Da die FailPackageOnFailure-Eigenschaft auf FALSE festgelegt ist, wird die Verarbeitung des Pakets jedoch fortgesetzt. Die Warnung wird bereitgestellt, wenn die SaveCheckpoints-Eigenschaft des Pakets auf TRUE festgelegt ist und bei dem Task oder Container ein Fehler auftritt.|  
|0x80017101|-2147389183|DTS_W_EMPTYPATH|Der Pfad ist leer.|  
|0x80019002|-2147381246|DTS_W_MAXIMUMERRORCOUNTREACHED|SSIS-Warnungscode DTS_W_MAXIMUMERRORCOUNTREACHED.  Die Execution-Methode wurde erfolgreich ausgeführt, aber die Anzahl von ausgelösten Fehlern (%1!d!) hat den maximal zulässigen Wert erreicht (%2!d!). Deshalb tritt ein Fehler auf. Dieses Problem tritt auf, wenn die Anzahl von Fehlern den in MaximumErrorCount angegebenen Wert erreicht. Ändern Sie den Wert für MaximumErrorCount, oder beheben Sie die Fehler.|  
|0x80019003|-2147381245|DTS_W_CONFIGENVVARNOTFOUND|Die Konfigurationsumgebungsvariable wurde nicht gefunden.  Die Umgebungsvariable lautete: "%1". Dieses Problem tritt auf, wenn in einem Paket eine Umgebungsvariable für eine Konfigurationseinstellung angegeben ist, die nicht gefunden wurde. Überprüfen Sie die Configurations-Auflistung im Paket, und stellen Sie sicher, dass die angegebene Umgebungsvariable verfügbar und gültig ist.|  
|0x80019316|-2147380458|DTS_W_CONNECTIONPROVIDERCHANGE|Der Anbietername für den Verbindungs-Manager "%1" wurde von "%2" in "%3" geändert.|  
|0x80019317|-2147380457|DTS_W_READEXTMAPFAILED|Beim Lesen der Upgradezuordnungsdateien ist eine Ausnahme aufgetreten. Die Ausnahme lautet: "%1".|  
|0x80019318|-2147380456|DTS_W_DUPLICATEMAPPINGKEY|In der Datei ist eine doppelte Zuordnung vorhanden: "%1". Tag: "%2", Schlüssel: "%3".|  
|0x80019319|-2147380455|DTS_W_IMPLICITUPGRADEMAPPING|Die Erweiterung "%1" wurde implizit auf "%2" aktualisiert. Fügen Sie dem UpgradeMappings-Verzeichnis eine Zuordnung für diese Erweiterung zu.|  
|0x8001931A|-2147380454|DTS_W_INVALIDEXTENSIONMAPPING|Eine Zuordnung in der Datei ("%1") ist nicht gültig. Werte dürfen weder NULL noch leer sein. Tag: "%2", Schlüssel "%3" und Wert: "%4".|  
|0x8001931C|-2147380452|DTS_W_ADOCONNECTIONDATATYPECOMPATCHANGE|Die DataTypeCompatibility-Eigenschaft des ADO-Typ-Verbindungs-Managers "%1" wurde für Abwärtskompatibilität mit 80 festgelegt.|  
|0x8001C004|-2147368956|DTS_W_FILEENUMEMPTY|Der For Each File-Enumerator ist leer. Der For Each File-Enumerator hat keine Dateien gefunden, die mit dem Dateimuster übereinstimmen, oder das angegebene Verzeichnis war leer.|  
|0x8001F02F|-2147356625|DTS_W_COULDNOTRESOLVEPACKAGEPATH|Ein Paketpfad zu einem Objekt im Paket "%1" kann nicht aufgelöst werden. Überprüfen Sie, ob der Paketpfad gültig ist.|  
|0x8001F203|-2147356157|DTS_W_ITERATIONEXPRESSIONISNOTASSIGNMENT|Der Iterationsausdruck ist kein Zuweisungsausdruck: "%1". Dieser Fehler tritt gewöhnlich auf, wenn der Ausdruck im Zuweisungsausdruck für die For-Schleife kein Zuweisungsausdruck ist.|  
|0x8001F204|-2147356156|DTS_W_INITIALIZATIONEXPRESSIONISNOTASSIGNMENT|Der Initialisierungsausdruck ist kein Zuweisungsausdruck: "%1". Dieser Fehler tritt gewöhnlich auf, wenn der Ausdruck im Iterationsausdruck für die For-Schleife kein Zuweisungsausdruck ist.|  
|0x8001F205|-2147356155|DTS_W_LOGPROVIDERNOTDEFINED|Die ausführbare Datei "%1" wurde erfolgreich eingefügt. In der LogProviders-Auflistung konnte jedoch kein Protokollanbieter gefunden werden, der der ausführbaren Datei zugeordnet ist.  Die ausführbare Datei wurde ohne Informationen zum Protokollanbieter eingefügt.|  
|0x8001F300|-2147355904|DTS_W_PACKAGEUPGRADED|Das Paket wurde erfolgreich aktualisiert.|  
|0x8001F42B|-2147355605|DTS_W_LEGACYPROGID|Die ProgID "%1" ist veraltet. Stattdessen sollte die neue ProgID für die Komponente "%2" verwendet werden.|  
|0x80020918|-2147350248|DTS_W_FTPTASK_OPERATIONFAILURE|Fehler bei Vorgang "%1".|  
|0x800283A5|-2147318875|DTS_W_MSMQTASK_USE_WEAK_ENCRYPTION|Der Verschlüsselungsalgorithmus "%1" nutzt unsichere Verschlüsselung.|  
|0x80029164|-2147315356|DTS_W_FSTASK_OPERATIONFAILURE|Taskfehler beim Ausführen des Vorgangs "%1".|  
|0x80029185|-2147315323|DTS_W_EXECPROCTASK_FILENOTINPATH|Die Datei/der Prozess "%1" ist nicht im Pfad vorhanden.|  
|0x800291C6|-2147315258|DTS_W_SENDMAILTASK_SUBJECT_MISSING|Der Betreff ist leer.|  
|0x800291C7|-2147315257|DTS_W_SENDMAILTASK_ERROR_IN_TO_LINE|Die Adresse in der Zeile "An" ist falsch. Entweder es fehlt das Symbol "\@" oder die Adresse ist ungültig.|  
|0x800291C8|-2147315256|DTS_W_SENDMAILTASK_AT_MISSING_IN_FROM|Die Adresse in der Zeile "Von" ist falsch. Entweder es fehlt das Symbol "\@" oder die Adresse ist ungültig.|  
|0x8002927A|-2147315078|DTS_W_XMLTASK_DIFFFAILURE|Die beiden XML-Dokumente unterscheiden sich.|  
|0x8002928C|-2147315060|DTS_W_XMLTASK_DTDVALIDATIONWARNING|Die DTD-Überprüfung verwendet die DTD-Datei, die in der Zeile DOCTYPE im XML-Dokument definiert ist. Der der Eigenschaft "%1" zugewiesene Wert wird nicht verwendet.|  
|0x8002928D|-2147315059|DTS_W_XMLTASK_VALIDATIONFAILURE|Fehler beim Überprüfen von "%1" durch den Task.|  
|0x80029291|-2147315055|DTS_W_TRANSFERDBTASK_ACTIONSETTOCOPY|Ungültiger Wert für die Übertragungsaktion.  Er wird auf Kopieren festgelegt.|  
|0x80029292|-2147315054|DTS_W_TRANSFERDBTASK_METHODSETTOONLINE|Ungültiger Wert für die Übertragungsmethode.  Er wird auf Onlineübertragung festgelegt.|  
|0x8002F304|-2147290364|DTS_W_PROBLEMOCCURREDWITHFOLLOWINGMESSAGE|Problem bei folgenden Meldungen: "%1".|  
|0x8002F322|-2147290334|DTS_W_ERRMSGTASK_ERRORMESSAGEALREADYEXISTS|Die Fehlermeldung "%1" ist bereits auf dem Zielserver vorhanden.|  
|0x8002F331|-2147290319|DTS_W_JOBSTASK_JOBEXISTSATDEST|Der Auftrag "%1" ist bereits auf dem Zielserver vorhanden.|  
|0x8002F332|-2147290318|DTS_W_JOBSTASK_SKIPPINGJOBEXISTSATDEST|Die Übertragung des Auftrags "%1" wird ausgelassen, da er bereits am Ziel vorhanden ist.|  
|0x8002F333|-2147290317|DTS_W_JOBSTASK_OVERWRITINGJOB|Der Auftrag "%1" wird auf dem Zielserver überschrieben.|  
|0x8002F339|-2147290311|DTS_W_LOGINSTASK_ENUMVALUEINCORRECT|Der permanente Enumerationswert der FailIfExists-Eigenschaft wurde geändert und ist nicht mehr gültig. Der Standardwert wird wiederhergestellt.|  
|0x8002F343|-2147290301|DTS_W_LOGINSTASK_OVERWRITINGLOGINATDEST|Der Anmeldename "%1" wird am Ziel überschrieben.|  
|0x8002F356|-2147290282|DTS_W_TRANSOBJECTSTASK_SPALREADYATDEST|Die gespeicherte Prozedur "%1" ist am Ziel bereits vorhanden.|  
|0x8002F360|-2147290272|DTS_W_TRANSOBJECTSTASK_RULEALREADYATDEST|Die Regel "%1" ist bereits am Ziel vorhanden.|  
|0x8002F364|-2147290268|DTS_W_TRANSOBJECTSTASK_TABLEALREADYATDEST|Die Tabelle "%1" ist bereits am Ziel vorhanden.|  
|0x8002F368|-2147290264|DTS_W_TRANSOBJECTSTASK_VIEWALREADYATDEST|Die Sicht "%1" ist bereits am Ziel vorhanden.|  
|0x8002F372|-2147290254|DTS_W_TRANSOBJECTSTASK_UDFALREADYATDEST|Die benutzerdefinierte Funktion "%1" ist bereits am Ziel vorhanden.|  
|0x8002F376|-2147290250|DTS_W_TRANSOBJECTSTASK_DEFAULTALREADYATDEST|Der Standardwert "%1" ist bereits am Ziel vorhanden.|  
|0x8002F380|-2147290240|DTS_W_TRANSOBJECTSTASK_UDDTALREADYATDEST|Der benutzerdefinierte Datentyp "%1" ist bereits am Ziel vorhanden.|  
|0x8002F384|-2147290236|DTS_W_TRANSOBJECTSTASK_PFALREADYATDEST|Die Partitionsfunktion "%1" ist bereits am Ziel vorhanden.|  
|0x8002F388|-2147290232|DTS_W_TRANSOBJECTSTASK_PSALREADYATDEST|Das Partitionsschema "%1" ist bereits am Ziel vorhanden.|  
|0x8002F391|-2147290223|DTS_W_TRANSOBJECTSTASK_SCHEMAALREADYATDEST|Das Schema "%1" ist bereits am Ziel vorhanden.|  
|0x8002F396|-2147290218|DTS_W_TRANSOBJECTSTASK_SQLASSEMBLYALREADYATDEST|Das SqlAssembly-Objekt "%1" ist bereits am Ziel vorhanden.|  
|0x8002F400|-2147290112|DTS_W_TRANSOBJECTSTASK_AGGREGATEALREADYATDEST|Das benutzerdefinierte Aggregat "%1" ist bereits am Ziel vorhanden.|  
|0x8002F404|-2147290108|DTS_W_TRANSOBJECTSTASK_TYPEALREADYATDEST|Der benutzerdefinierte Typ "%1" ist bereits am Ziel vorhanden.|  
|0x8002F408|-2147290104|DTS_W_TRANSOBJECTSTASK_XMLSCHEMACOLLECTIONALREADYATDEST|Das XmlSchemaCollection-Objekt "%1" ist bereits am Ziel vorhanden.|  
|0x8002F412|-2147290094|DTS_W_TRANSOBJECTSTASK_NOELEMENTSPECIFIEDTOTRANSFER|Es sind keine zu übertragenden Elemente angegeben.|  
|0x8002F415|-2147290091|DTS_W_TRANSOBJECTSTASK_LOGINALREADYATDEST|Der Anmeldename "%1" ist bereits am Ziel vorhanden.|  
|0x8002F41A|-2147290086|DTS_W_TRANSOBJECTSTASK_USERALREADYATDEST|Der Benutzer "%1" ist bereits am Ziel vorhanden.|  
|0x80047007|-2147192825|DTS_W_NOLINEAGEVALIDATION|Die Herkunfts-IDs der Eingabespalten können nicht überprüft werden, weil die Ausführungsstrukturen Schleifen enthalten.|  
|0x80047034|-2147192780|DTS_W_EMPTYDATAFLOW|Der DataFlow-Task weist keine Komponenten auf. Fügen Sie Komponenten hinzu, oder entfernen Sie den Task.|  
|0x80047069|-2147192727|DTS_W_SORTEDOUTPUTHASNOSORTKEYPOSITIONS|Die IsSorted-Eigenschaft von %1 ist auf TRUE festgelegt, aber die SortKeyPositions-Eigenschaft aller Ausgabespalten ist auf 0 festgelegt.|  
|0x8004706F|-2147192721|DTS_W_SOURCEREMOVED|Die Quelle "%1" (%2!d!) wird nicht gelesen, weil außerhalb des Datenflusstasks keine Daten sichtbar werden.|  
|0x80047076|-2147192714|DTS_W_UNUSEDOUTPUTDATA|Die Ausgabespalte "%1" (%2!d!) in der Ausgabe "%3" (%4!d!) und der Komponente "%5" (%6!d!) wird nicht im Datenflusstask verwendet. Durch das Entfernen dieser nicht verwendeten Ausgabespalte kann die Leistung des Datenflusstasks optimiert werden.|  
|0x800470AE|-2147192658|DTS_W_COMPONENTREMOVED|Die Komponente "%1" (%2!d!) wurde aus dem Datenflusstask entfernt, weil ihre Ausgabe nicht verwendet wird und ihre Eingaben entweder keine nachteiligen Auswirkungen haben oder nicht mit Ausgaben anderer Komponenten verbunden sind. Falls die Komponente erforderlich ist, sollte die HasSideEffects-Eigenschaft mindestens einer Eingabe auf True festgelegt werden, oder die Ausgabe sollte mit einer Komponente verbunden sein.|  
|0x800470B0|-2147192656|DTS_W_NOWORKTODO|Zeilen wurden an einen Thread übergeben, aber dieser Thread befindet sich im Leerlauf. Das Layout weist eine getrennte Ausgabe auf. Wenn Sie die RunInOptimizedMode-Eigenschaft auf TRUE festlegen, wird die Pipeline schneller ausgeführt und die Warnung wird verhindert.|  
|0x800470C8|-2147192632|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|Die externen Spalten für %1 sind nicht mit den Datenquellspalten synchronisiert. %2|  
|0x800470C9|-2147192631|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSADDITION|Die Spalte "%1" muss den externen Spalten hinzugefügt werden.|  
|0x800470CA|-2147192630|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSUPDATE|Die externe Spalte "%1" muss aktualisiert werden.|  
|0x800470CB|-2147192629|DTS_W_EXTERNALMETADATACOLUMNCOLLECTIONNEEDSREMOVAL|%1 muss aus den externen Spalten entfernt werden.|  
|0x800470D8|-2147192616|DTS_W_EXPREVALPOTENTIALSTRINGTRUNCATION|Die Ergebniszeichenfolge für den Ausdruck "%1" wird möglicherweise abgeschnitten, wenn die maximale Länge von %2!d! Zeichen ist. Der Ausdruck kann einen Ergebniswert aufweisen, der die maximale Größe von DT_WSTR überschreitet.|  
|0x800470E9|-2147192599|DTS_W_COMPONENTLEAKPROCESSINPUT|Ein Aufruf der ProcessInput-Methode für die Eingabe %1!d! in %2 hat unerwartet einen Verweis auf den Puffer bewahrt, an den der Aufruf übertragen worden ist. Der refcount in diesem Puffer lautete vor dem Aufruf %3!d! und %4!d! nach der Rückgabe des Aufrufes.|  
|0x800470EB|-2147192597|DTS_W_EXPREVALUNREFERENCEDINPUTCOLUMN|"%1" in "%2" hat den Verwendungstyp READONLY, es gibt jedoch keinen Verweis durch einen Ausdruck. Entfernen Sie die Spalte aus der Liste der verfügbaren Eingabespalten, oder verweisen Sie in einem Ausdruck darauf.|  
|0x8004801E|-2147188706|DTS_W_COULDNOTFINDCURRENTVERSION|Der Wert "%1" für die Komponente "%2" wurde nicht gefunden. Der CurrentVersion-Wert für die Komponente wurde nicht gefunden. Dieser Fehler tritt auf, wenn in der Komponente für die Registrierungsinformationen kein CurrentVersion-Wert im DTSInfo-Abschnitt festgelegt ist. Die Meldung wird während der Komponentenentwicklung angezeigt, oder wenn die Komponente in einem Paket verwendet wird, wenn die Komponente nicht ordnungsgemäß registriert ist.|  
|0x80049300|-2147183872|DTS_W_BUFFERGETTEMPFILENAME|Der Puffer-Manager konnte einen temporären Dateinamen nicht abrufen.|  
|0x80049301|-2147183871|DTS_W_UNUSABLETEMPORARYPATH|Der Puffer-Manager konnte eine temporäre Datei im Pfad "%1" nicht erstellen. Der Pfad wird nicht mehr für den temporären Speicher berücksichtigt.|  
|0x80049304|-2147183868|DTS_W_DF_PERFCOUNTERS_DISABLED|Warnung: Der globale freigegebene Speicher konnte nicht geöffnet werden, um mit der Leistungs-DLL zu kommunizieren; es sind keine Datenfluss-Leistungsindikatoren verfügbar.  Führen Sie dieses Paket als Administrator oder auf der Systemkonsole aus, um dieses Problem zu beheben.|  
|0x8020200F|-2145378289|DTS_W_PARTIALROWFOUNDATENDOFFILE|Das Ende der Datei weist eine unvollständige Zeile auf.|  
|0x8020202B|-2145378261|DTS_W_ENDOFFILEREACHWHILEREADINGHEADERROWS|Beim Lesen des Headers wurde das Ende der Datendatei erreicht. Stellen Sie sicher, dass das Kopfzeilentrennzeichen und die Anzahl von auszulassenden Kopfzeilen richtig sind.|  
|0x80202066|-2145378202|DTS_W_CANTRETRIEVECODEPAGEFROMOLEDBPROVIDER|Die Codepageinformationen für die Spalte können nicht vom OLE DB-Anbieter abgerufen werden.  Falls die Eigenschaft "%1" von der Komponente unterstützt wird, wird die Codepage dieser Eigenschaft verwendet.  Ändern Sie den Wert der Eigenschaft, falls die aktuellen Codepagewerte falsch sind.  Falls die Eigenschaft nicht von der Komponente unterstützt wird, wird die Codepage des Gebietsschemabezeichners der Komponente verwendet.|  
|0x802020F7|-2145378057|DTS_W_TXSORTSORTISTHESAME|Die Daten sind bereits wie angegeben sortiert. Die Transformation kann deshalb entfernt werden.|  
|0x8020400D|-2145370099|DTS_W_NOPIPELINEDATATYPEMAPPINGAVAILABLE|%1 verweist auf einen externen Datentyp, der keinem Datenflusstask-Datentyp zugeordnet werden kann. Der Datenflusstask-Datentyp DT_WSTR wird stattdessen verwendet.|  
|0x802070CC|-2145357620|DTS_W_STATICTRUNCATIONINEXPRESSION|Mit dem Ausdruck "%1" werden Daten immer abgeschnitten. Der Ausdruck schneidet Daten statisch ab (ein fester Wert wird abgeschnitten).|  
|0x8020820C|-2145353204|DTS_W_UNMAPPEDINPUTCOLUMN|Die Eingabespalte "%1" mit der ID %2!d! ist beim Index %3!d! nicht zugeordnet. Die Herkunfts-ID für die Spalte ist 0.|  
|0x80208305|-2145352955|DTS_W_TXFUZZYLOOKUP_DELIMITERS_DONT_MATCH|Die angegebenen Trennzeichen stimmen nicht mit den Trennzeichen überein, die zum Erstellen des bereits vorhandenen Übereinstimmungsindexes "%1" verwendet wurden. Dieser Fehler tritt auf, wenn die Trennzeichen, über die Felder mit einem Token versehen werden, nicht übereinstimmen. Dies kann unbekannte Auswirkungen auf das Suchen nach Übereinstimmungen oder die Ergebnisse haben.|  
|0x80208308|-2145352952|DTS_W_TXFUZZYLOOKUP_MAXRESULTS_IS_ZERO|Die MaxOutputMatchesPerInput-Eigenschaft in der Transformation für Fuzzysuche ist 0. Es werden keine Ergebnisse erstellt.|  
|0x80208310|-2145352944|DTS_W_TXFUZZYLOOKUP_NO_FUZZY_JOIN_COLUMNS|Es waren keine gültigen Eingabespalten vorhanden, bei denen die JoinType-Spalteneigenschaft auf Fuzzy festgelegt ist.  Die Leistung von genauen Joins kann durch Verwenden der Transformation für Suche statt der Fuzzysuche verbessert werden.|  
|0x8020831C|-2145352932|DTS_W_TXFUZZYLOOKUP_TIMESTAMPCAVEAT|Die Verweisspalte "%1" ist möglicherweise eine SQL-Timestampspalte. Wenn der Fuzzyübereinstimmungsindex erstellt und eine Kopie der Verweistabelle erstellt wird, geben alle Verweistabellentimestamps den aktuellen Status der Tabelle zum Zeitpunkt des Kopierens wieder. Wenn CopyReferenceTable auf False festgelegt ist, kann unerwartetes Verhalten auftreten.|  
|0x80208321|-2145352927|DTS_W_MATCHINDEXALREADYEXISTS|Eine Tabelle mit dem Namen '%1', wie für MatchIndexName angegeben, ist bereits vorhanden, und die DropExistingMatchIndex-Eigenschaft ist auf FALSE festgelegt.  Die Transformation wird nur dann erfolgreich ausgeführt, wenn die Tabelle gelöscht wird, ein anderer Name angegeben oder DropExistingMatchIndex auf TRUE festgelegt wird.|  
|0x8020832B|-2145352917|DTS_W_TXFUZZYLOOKUP_JOINLENGTHMISMATCH|Die Länge der Eingabespalte '%1' und der Verweisspalte '%2', die für die Übereinstimmung verwendet wird, ist nicht gleich.|  
|0x8020832D|-2145352915|DTS_W_TXFUZZYLOOKUP_CODEPAGE_MISMATCH|Die Codepages der DT_STR-Quellspalte "%1" und der DT_STR-Zielspalte "%2" stimmen nicht überein.  Dies kann zu unerwarteten Ergebnissen führen.|  
|0x8020832E|-2145352914|DTS_W_FUZZYLOOKUP_TOOMANYEXACTMATCHCOLUMNS|Es sind mehr als 16 Joins für genaue Übereinstimmungen vorhanden. Die Leistung ist deshalb möglicherweise nicht optimal. Reduzieren Sie die Anzahl von Joins für genaue Übereinstimmungen, um die Leistung zu verbessern. Für SQL gilt ein Grenzwert von 16 Spalten pro Index, wobei der invertierte Index für alle Suchvorgänge verwendet wird.|  
|0x80208350|-2145352880|DTS_W_FUZZYLOOKUP_MEMLIMITANDEXHAUSTIVESPECIFIED|Für die Option Exhaustive muss der gesamte Verweis in den Hauptspeicher geladen werden.  Da für die MaxMemoryUsage-Eigenschaft eine Arbeitsspeichergrenze angegeben wurde, kann möglicherweise nicht die gesamte Verweistabelle geladen werden, sodass der Übereinstimmungsvorgang zur Laufzeit fehlschlägt.|  
|0x80208351|-2145352879|DTS_W_FUZZYLOOKUP_EXACTMATCHCOLUMNSEXCEEDBYTELIMIT|Die Gesamtlänge der in den Joins für genaue Übereinstimmung angegebenen Spalten überschreitet den Grenzwert von 900 Byte für Indexschlüssel.  Die Fuzzysuche erstellt einen Index für die Spalten für die genaue Übereinstimmung, um die Suchleistung zu optimieren. Es besteht die Möglichkeit, dass dieser Index nicht erstellt werden kann und für die Suche eine alternative und möglicherweise langsamere Methode für die Suche nach Übereinstimmungen verwendet wird. Falls die Leistung ein Problem darstellt, entfernen Sie Spalten für Joins für die genaue Übereinstimmung, oder reduzieren Sie die maximale Länge von Spalten für die genaue Übereinstimmung mit variabler Länge.|  
|0x80208352|-2145352878|DTS_W_FUZZYLOOKUP_EXACTMATCHINDEXCREATIONFAILED|Fehler beim Erstellen eines Indexes für Spalten für die genaue Übereinstimmung. Eine alternative Fuzzysuchmethode wird verwendet.|  
|0x80208353|-2145352877|DTS_W_FUZZYGROUPINGINTERNALPIPELINEWARNING|Die folgende interne Fuzzygruppierungs-Pipelinewarnung mit dem Warnungscode 0x%1!8.8X! ist aufgetreten: "%2".|  
|0x80208375|-2145352843|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTODEFAULT|Für %1 mit dem externen Datentyp %2 wurde keine maximale Länge angegeben. Der Datentyp für den SSIS-Datenflusstask „%3“ mit einer Länge von „%4!d!“ wird verwendet.|  
|0x80208376|-2145352842|DTS_W_XMLSRCOUTPUTCOLUMNDATATYPEMAPPEDTOSTRING|%1 verweist auf den externen Datentyp %2, der keinem SSIS-Datenflusstask-Datentyp zugeordnet werden kann.  Der Datentyp für den SSIS-Datenflusstask DT_WSTR mit einer Länge von %3!d! wird stattdessen verwendet.|  
|0x80208385|-2145352827|DTS_W_NOREDIRECTWITHATTACHEDERROROUTPUTS|An Fehlerausgaben werden keine Zeilen gesendet. Konfigurieren Sie Fehler- oder Abschneidedispositionen so, dass Zeilen an die Fehlerausgaben umgeleitet werden, oder löschen Sie Datenflusstransformationen oder -ziele, die an die Fehlerausgaben angefügt sind.|  
|0x80208386|-2145352826|DTS_W_REDIRECTWITHNOATTACHEDERROROUTPUTS|An die Fehlerausgaben gesendete Zeilen gehen verloren. Fügen Sie neue Datenflusstransformationen oder -ziele hinzu, um Fehlerzeilen zu empfangen, oder konfigurieren Sie die Komponente neu, um die Umleitung von Zeilen an die Fehlerausgaben zu beenden.|  
|0x80208391|-2145352815|DTS_W_XMLSRCOUTPUTCOLUMNLENGTHSETTOMAXIMUM|Für %1 mit dem externen Datentyp %2 gibt das XML-Schema eine maximale Längeneinschränkung von %3!d! an, die die maximal zulässige Spaltenlänge von %4!d! überschreitet. Der Datentyp für den SSIS-Datenflusstask "%5" mit einer Länge von %6!d! wird verwendet.|  
|0x802090E4|-2145349404|DTS_W_TXLOOKUP_DUPLICATE_KEYS|%1 hat beim Zwischenspeichern von Verweisdaten doppelte Verweisschlüsselwerte gefunden. Dieser Fehler tritt nur im Vollcachemodus auf. Entfernen Sie die doppelten Schlüsselwerte, oder ändern Sie den Cachemodus in PARTIAL oder NO_CACHE.|  
|0x802092A7|-2145348953|DTS_W_POTENTIALTRUNCATIONFROMDATAINSERTION|Daten werden möglicherweise abgeschnitten, weil Daten aus der Datenflussspalte "%1" mit der Länge %2!d! in die Datenbankspalte "%3" mit einer Länge von %4!d! eingefügt werden.|  
|0x802092A8|-2145348952|DTS_W_POTENTIALTRUNCATIONFROMDATARETRIEVAL|Daten werden möglicherweise abgeschnitten, weil in der Datenbankspalte "%1" mit einer Länge von %2!d! Daten aus der Datenflussspalte "%3" mit einer Länge von %4!d! abgerufen werden.|  
|0x802092AA|-2145348950|DTS_W_ADODESTBATCHNOTSUPPORTEDFORERRORDISPOSITION|Der Batchmodus wird derzeit nicht unterstützt, wenn die Fehlerzeilendisposition verwendet wird. Die BatchSize-Eigenschaft wird auf 1 festgelegt.|  
|0x802092AB|-2145348949|DTS_W_ADODESTNOROWSINSERTED|In das Ziel wurden keine Zeilen erfolgreich eingefügt. Dies liegt möglicherweise an einem Datentypkonflikt zwischen Spalten oder daran, dass ein Datentyp verwendet wurde, der von Ihrem ADO NET-Anbieter nicht unterstützt wird. Da die Fehlerdisposition für diese Komponente nicht "Fehler bei Komponente" lautet, werden Fehlermeldungen hier nicht angezeigt. Legen Sie die Fehlerdisposition auf "Fehler bei Komponente" fest, um Fehlermeldungen hier anzuzeigen.|  
|0x802092AC|-2145348948|DTS_W_ADODESTPOTENTIALDATALOSS|Es kann möglicherweise zu einem Datenverlust kommen, da Daten aus der Eingabespalte "%1" mit dem Datentyp "%2" in die externe Spalte "%3" mit dem Datentyp "%4" eingefügt wurden. Wenn dies beabsichtigt ist, können Sie für die Konvertierung alternativ eine Datenkonvertierungskomponente vor der ADO NET-Zielkomponente verwenden.|  
|0x802092AD|-2145348947|DTS_W_ADODESTEXTERNALCOLNOTMATCHSCHEMACOL|%1 ist nicht mit der Datenbankspalte synchronisiert.  Die aktuelle Spalte weist %2 auf. Verwenden Sie den erweiterten Editor, um verfügbare Zielspalten bei Bedarf zu aktualisieren.|  
|0x802092AE|-2145348946|DTS_W_ADODESTEXTERNALCOLNOTEXIST|%1 ist nicht in der Datenbank vorhanden. Das Element wurde möglicherweise entfernt oder umbenannt. Verwenden Sie den erweiterten Editor, um die verfügbaren Zielspalten nach Bedarf zu aktualisieren.|  
|0x802092AF|-2145348945|DTS_W_ADODESTNEWEXTCOL|Der externen Datenbanktabelle wurde eine neue Spalte mit dem Namen %1 hinzugefügt. Verwenden Sie den erweiterten Editor, um verfügbare Zielspalten bei Bedarf zu aktualisieren.|  
|0x8020930C|-2145348852|DTS_W_NOMATCHOUTPUTGETSNOROWS|Es werden keine Zeilen an die Ausgabe nicht übereinstimmender Einträge gesendet. Konfigurieren Sie die Transformation so, dass Zeilen ohne übereinstimmende Einträge an die Ausgabe nicht übereinstimmender Einträge umgeleitet werden, oder löschen Sie die Datenflusstransformationen oder Ziele, die mit der Ausgabe nicht übereinstimmender Einträge verbunden sind.|  
|0x8020931B|-2145348837|DTS_W_ADODESTINVARIANTEXCEPTION|Ausnahme beim Auflisten von ADO.NET-Anbietern. Die Invariante lautete "%1." Die Ausnahmemeldung lautet: "%2"|  
|0xC020822C|-1071611348|DTS_W_UNMAPPEDOUTPUTCOLUMN|%1 ist keine Eingabespalte zugeordnet.|  
|0x930D|37645|DTS_W_EXTERNALTABLECOLSOUTOFSYNC|Die Tabelle "%1" wurde geändert. Möglicherweise wurden der Tabelle neue Spalten hinzugefügt.|  
  
##  <a name="msgInfo"></a> Informationsmeldungen  
 Die symbolischen Namen von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Informationsmeldungen beginnen mit **DTS_I_**.  
  
|Hexadezimalcode|Dezimalcode|Symbolischer Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x4001100A|1073811466|DTS_I_STARTINGTRANSACTION|Verteilte Transaktion für diesen Container wird gestartet.|  
|0x4001100B|1073811467|DTS_I_COMMITTINGTRANSACTION|Commit für verteilte Transaktion, die von diesem Container gestartet wurde, wird ausgeführt.|  
|0x4001100C|1073811468|DTS_I_ABORTINGTRANSACTION|Aktuelle verteilte Transaktion wird abgebrochen.|  
|0x40013501|1073820929|DTS_I_GOTMUTEXFROMWAIT|Mutex "%1" wurde erfolgreich abgerufen.|  
|0x40013502|1073820930|DTS_I_RELEASEACQUIREDMUTEX|Mutex "%1" wurde erfolgreich freigegeben.|  
|0x40013503|1073820931|DTS_I_NEWMUTEXCREATED|Mutex "%1" wurde erfolgreich erstellt.|  
|0x40015101|1073828097|DTS_I_DUMP_ON_ANY_ERR|Debugdumpdateien werden für jedes Fehlerereignis generiert.|  
|0x40015102|1073828098|DTS_I_DUMP_ON_CODES|Debugdumpdateien werden für die folgenden Ereigniscodes generiert: "%1"|  
|0x40015103|1073828099|DTS_I_START_DUMP|Der Ereigniscode 0x%1!8.8X! hat das Generieren von Debugdumpdateien im Ordner "%2" ausgelöst.|  
|0x40015104|1073828100|DTS_I_SSIS_INFO_DUMP|Die SSIS-Informationsdumpdatei "%1" wird erstellt.|  
|0x40015106|1073828102|DTS_I_FINISH_DUMP|Debugdumpdateien wurden erfolgreich erstellt.|  
|0x40016019|1073831961|DTS_I_PACKAGEMIGRATED|Das Paketformat wurde von der Version %1!d! zur Version %2!d! migriert. Es muss gespeichert werden, um die Migrationsänderungen beizubehalten.|  
|0x4001601A|1073831962|DTS_I_SCRIPTSMIGRATED|Die Skripts im Paket wurden migriert. Das Paket muss gespeichert werden, um die Migrationsänderungen beizubehalten.|  
|0x40016025|1073831973|DTS_I_FTPRECEIVEFILE|Die Datei "%1" wird empfangen.|  
|0x40016026|1073831974|DTS_I_FTPSENDFILE|Die Datei "%1" wird gesendet.|  
|0x40016027|1073831975|DTS_I_FTPFILEEXISTS|Die Datei "%1" ist bereits vorhanden.|  
|0x40016028|1073831976|DTS_I_FTPERRORLOADINGMSG|Aufgrund eines internen Fehlers können keine zusätzlichen Fehlerinformationen abgerufen werden.|  
|0x40016036|1073831990|DTS_I_FTPDELETEFILE|Fehler beim Löschen der Datei "%1". Dieser Fehler tritt auf, wenn die Datei nicht vorhanden ist, der Dateiname falsch eingegeben wurde, oder wenn Sie nicht über die Berechtigungen zum Löschen der Datei verfügen.|  
|0x40016037|1073831991|DTS_I_CONFIGFROMREG|Paketkonfiguration von einem Registrierungseintrag mithilfe des Registrierungsschlüssels "%1" wird versucht.|  
|0x40016038|1073831992|DTS_I_CONFIGFROMENVVAR|Paketkonfiguration von der Umgebungsvariablen "%1" wird versucht.|  
|0x40016039|1073831993|DTS_I_CONFIGFROMINIFILE|Paketkonfiguration von der INI-Datei "%1" wird versucht.|  
|0x40016040|1073832000|DTS_I_CONFIGFROMSQLSERVER|Paketkonfiguration von SQL Server mithilfe der Konfigurationszeichenfolge "%1" wird versucht.|  
|0x40016041|1073832001|DTS_I_CONFIGFROMFILE|Paketkonfiguration von der XML-Datei "%1" wird versucht.|  
|0x40016042|1073832002|DTS_I_CONFIGFROMPARENTVARIABLE|Paketkonfiguration von der übergeordneten Variablen "%1" wird versucht.|  
|0x40016043|1073832003|DTS_I_ATTEMPTINGUPGRADEOFDTS|SSIS wird von Version "%1" auf Version "%2" aktualisiert. Das Paket versucht, die Laufzeitumgebung zu aktualisieren.|  
|0x40016044|1073832004|DTS_I_ATTEMPTINGUPGRADEOFANEXTOBJ|Upgradeversuch für "%1". Das Paket versucht, ein erweiterbares Objekt zu aktualisieren.|  
|0x40016045|1073832005|DTS_I_SAVECHECKPOINTSTOFILE|Das Paket wird während der Ausführung Prüfpunkte in der Datei "%1" speichern. Das Paket ist für das Speichern von Prüfpunkten konfiguriert.|  
|0x40016046|1073832006|DTS_I_RESTARTFROMCHECKPOINTFILE|Das Paket wurde von der Prüfpunktdatei "%1" neu gestartet. Das Paket wurde so konfiguriert, dass es vom Prüfpunkt neu gestartet wird.|  
|0x40016047|1073832007|DTS_I_CHECKPOINTSAVEDTOFILE|Die Prüfpunktdatei "%1" wurde aktualisiert, um das Abschließen dieses Containers aufzuzeichnen.|  
|0x40016048|1073832008|DTS_I_CHECKPOINTFILEDELETED|Die Prüfpunktdatei "%1" wurde nach dem erfolgreichen Abschließen des Pakets gelöscht.|  
|0x40016049|1073832009|DTS_I_CHECKPOINTSAVINGTOFILE|Update der Prüfpunktdatei "%1" wird gestartet.|  
|0x40016051|1073832017|DTS_I_CHOSENMAXEXECUTABLES|Basierend auf der Systemkonfiguration ist die maximale Anzahl von gleichzeitig ausführbaren Dateien auf %1!d! festgelegt.|  
|0x40016052|1073832018|DTS_I_MAXEXECUTABLES|Die maximale Anzahl von gleichzeitig ausführbaren Dateien ist auf %1!d! festgelegt.|  
|0x40016053|1073832019|DTS_I_PACKAGESTART|Beginn der Paketausführung.|  
|0x40016054|1073832020|DTS_I_PACKAGEEND|Ende der Paketausführung.|  
|0x40029161|1073910113|DTS_I_FSTASK_DIRECTORYDELETED|Das Verzeichnis "%1" wurde gelöscht.|  
|0x40029162|1073910114|DTS_I_FSTASK_FILEDELETED|Die Datei oder das Verzeichnis "%1" wurde gelöscht.|  
|0x400292A8|1073910440|DTS_I_TRANSFERDBTASK_OVERWRITEDB|Die Datenbank "%1" auf dem Zielserver "%2" wird überschrieben.|  
|0x4002F304|1073935108|DTS_I_SOMETHINGHAPPENED|"%1".|  
|0x4002F323|1073935139|DTS_I_ERRMSGTASK_SKIPPINGERRORMESSAGEALREADYEXISTS|Fehlermeldung "%1" wird ausgelassen, da sie auf dem Zielserver bereits vorhanden ist.|  
|0x4002F326|1073935142|DTS_I_ERRMSGTASK_TRANSFEREDNERRORMESSAGES|"%1" Fehlermeldungen wurden übertragen.|  
|0x4002F351|1073935185|DTS_I_STOREDPROCSTASKS_TRANSFEREDNSPS|Der Task hat "%1" gespeicherte Prozeduren übertragen.|  
|0x4002F352|1073935186|DTS_I_TRANSOBJECTSTASK_TRANSFEREDNOBJECTS|"%1" Objekte wurden übertragen.|  
|0x4002F358|1073935192|DTS_I_TRANSOBJECTSTASK_NOSPSTOTRANSFER|Es sind keine zu übertragenden gespeicherten Prozeduren vorhanden.|  
|0x4002F362|1073935202|DTS_I_TRANSOBJECTSTASK_NORULESTOTRANSFER|Es sind keine zu übertragenden Regeln vorhanden.|  
|0x4002F366|1073935206|DTS_I_TRANSOBJECTSTASK_NOTABLESTOTRANSFER|Es sind keine zu übertragenden Tabellen vorhanden.|  
|0x4002F370|1073935216|DTS_I_TRANSOBJECTSTASK_NOVIEWSTOTRANSFER|Es sind keine zu übertragenden Sichten vorhanden.|  
|0x4002F374|1073935220|DTS_I_TRANSOBJECTSTASK_NOUDFSTOTRANSFER|Es sind keine zu übertragenden benutzerdefinierten Funktionen vorhanden.|  
|0x4002F378|1073935224|DTS_I_TRANSOBJECTSTASK_NODEFAULTSTOTRANSFER|Es sind keine zu übertragenden Standardwerte vorhanden.|  
|0x4002F382|1073935234|DTS_I_TRANSOBJECTSTASK_NOUDDTSTOTRANSFER|Es sind keine zu übertragenden benutzerdefinierten Datentypen vorhanden.|  
|0x4002F386|1073935238|DTS_I_TRANSOBJECTSTASK_NOPFSTOTRANSFER|Es sind keine zu übertragenden Partitionsfunktionen vorhanden.|  
|0x4002F390|1073935248|DTS_I_TRANSOBJECTSTASK_NOPSSTOTRANSFER|Es sind keine zu übertragenden Partitionsschemas vorhanden.|  
|0x4002F394|1073935252|DTS_I_TRANSOBJECTSTASK_NOSCHEMASTOTRANSFER|Es sind keine zu übertragenden Schemas vorhanden.|  
|0x4002F398|1073935256|DTS_I_TRANSOBJECTSTASK_NOSQLASSEMBLIESTOTRANSFER|Es sind keine zu übertragenden SqlAssemblys-Objekte vorhanden.|  
|0x4002F402|1073935362|DTS_I_TRANSOBJECTSTASK_NOAGGREGATESTOTRANSFER|Es sind keine zu übertragenden benutzerdefinierten Aggregate vorhanden.|  
|0x4002F406|1073935366|DTS_I_TRANSOBJECTSTASK_NOTYPESTOTRANSFER|Es sind keine zu übertragenden benutzerdefinierten Typen vorhanden.|  
|0x4002F410|1073935376|DTS_I_TRANSOBJECTSTASK_NOXMLSCHEMACOLLECTIONSTOTRANSFER|Es sind keine zu übertragenden XmlSchemaCollections-Objekte vorhanden.|  
|0x4002F418|1073935384|DTS_I_TRANSOBJECTSTASK_NOLOGINSTOTRANSFER|Es sind keine zu übertragenden Anmeldenamen vorhanden.|  
|0x4002F41D|1073935389|DTS_I_TRANSOBJECTSTASK_NOUSERSTOTRANSFER|Es sind keine zu übertragenden Benutzer vorhanden.|  
|0x4002F41E|1073935390|DTS_I_TRANSOBJECTSTASK_TRUNCATINGTABLE|Tabelle "%1" wird abgeschnitten.|  
|0x40043006|1074016262|DTS_I_EXECUTIONPHASE_PREPAREFOREXECUTE|Die Phase Ausführung vorbereiten beginnt.|  
|0x40043007|1074016263|DTS_I_EXECUTIONPHASE_PREEXECUTE|Die Phase Vor der Ausführung beginnt.|  
|0x40043008|1074016264|DTS_I_EXECUTIONPHASE_POSTEXECUTE|Die Phase Nach der Ausführung beginnt.|  
|0x40043009|1074016265|DTS_I_EXECUTIONPHASE_CLEANUP|Die Phase Cleanup beginnt.|  
|0x4004300A|1074016266|DTS_I_EXECUTIONPHASE_VALIDATE|Die Phase Überprüfung beginnt.|  
|0x4004300B|1074016267|DTS_I_ROWS_WRITTEN|"%1" hat %2!ld! Zeilen zwischengespeichert.|  
|0x4004300C|1074016268|DTS_I_EXECUTIONPHASE_EXECUTE|Die Phase Ausführung beginnt.|  
|0x4004800C|1074036748|DTS_I_CANTRELIEVEPRESSURE|Der Puffer-Manager hat erkannt, dass im System wenig virtueller Arbeitsspeicher verfügbar ist, konnte aber keine Puffer austauschen. %1!d! Puffer wurden berücksichtigt und %2!d! gesperrt. Entweder ist nicht genügend Arbeitsspeicher für die Pipeline verfügbar, weil nicht genügend Arbeitsspeicher installiert ist, oder andere Prozesse belegen den Arbeitsspeicher, oder es sind zu viele Puffer gesperrt.|  
|0x4004800D|1074036749|DTS_I_CANTALLOCATEMEMORYPRESSURE|Der Puffer-Manager konnte %3!d! Bytes an Speicherbelegung nicht zuordnen und keine Puffer austauschen, um die Auslastung des Arbeitsspeichers zu reduzieren. %1!d! Puffer wurden berücksichtigt und %2!d! gesperrt. Entweder ist nicht genügend Arbeitsspeicher für die Pipeline verfügbar, weil nicht genügend Arbeitsspeicher installiert ist, oder andere Prozesse belegen den Arbeitsspeicher, oder es sind zu viele Puffer gesperrt.|  
|0x4004800E|1074036750|DTS_I_ALLOCATEDDURINGMEMORYPRESSURE|Der Puffer-Manager hat %1!d! Bytes zugewiesen, obwohl die Auslastung des Arbeitsspeichers erkannt und wiederholt erfolglos versucht wurde, Puffer auszutauschen.|  
|0x400490F4|1074041076|DTS_I_TXLOOKUP_CACHE_PROGRESS|%1 hat %2!d! Zeilen zwischengespeichert.|  
|0x400490F5|1074041077|DTS_I_TXLOOKUP_CACHE_FINAL|%1 hat insgesamt %2!d! Zeilen zwischengespeichert.|  
|0x4020206D|1075847277|DTS_I_RAWSOURCENOCOLUMNS|Der Rohdatenadapter öffnete eine Datei, aber die Datei enthält keine Spalten. Der Adapter erstellt keine Daten. Dies kann darauf hinweisen, dass die Datei beschädigt ist, oder dass 0 Spalten und damit keine Daten vorhanden sind.|  
|0x402020DA|1075847386|DTS_I_OLEDBINFORMATIONALMESSAGE|Eine OLE DB-Informationsmeldung ist verfügbar.|  
|0x40208327|1075872551|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_COLLATIONS_DONT_MATCH|Die Leistung der Fuzzyübereinstimmung kann verbessert werden, wenn die genau verknüpften FuzzyComparisonFlags der Eingabespalte "%1" so konfiguriert werden, dass Übereinstimmungen mit der standardmäßigen SQL-Sortierung für die Verweistabellenspalte "%2" vorhanden sind.  Außerdem dürfen in FuzzyComparisonFlagsEx keine Aufteilungsflags festgelegt sein.|  
|0x40208328|1075872552|DTS_I_TXFUZZYLOOKUP_EXACT_MATCH_PERF_INDEX_MISSING|Die Leistung der Fuzzyübereinstimmung kann verbessert werden, wenn in der Verweistabelle ein Index für alle angegebenen Spalten für die genaue Übereinstimmung erstellt wird.|  
|0x40208387|1075872647|DTS_I_DISPSNOTREVIEWED|Fehler- und Abschneidedispositionen wurden nicht geprüft. Konfigurieren Sie diese Komponente so, dass Zeilen an die Fehlerausgaben umgeleitet werden, falls Sie diese Zeile weiter transformieren möchten.|  
|0x402090DA|1075876058|DTS_I_TXAGG_WORKSPACE_REHASH|Die Transformation für das Aggregieren hat %1!d! Schlüsselkombinationen gefunden. Für Daten muss ein erneutes Hashing ausgeführt werden, weil die Anzahl von Schlüsselkombinationen höher als erwartet ist. Die Komponente kann so konfiguriert werden, dass ein erneutes Hashing der Daten vermieden wird, indem die Eigenschaften Keys, KeyScale und AutoExtendFactor angepasst werden.|  
|0x402090DB|1075876059|DTS_I_TXAGG_COUNTDISTINCT_REHASH|Die Transformation für das Aggregieren hat %1!d! unterschiedliche Werte gefunden, während für "%2" die COUNT DISTINCT-Aggregation ausgeführt wurde. Die Transformation wird für die Daten ein erneutes Hashing ausführen, weil die Anzahl von unterschiedlichen Werten höher als erwartet ist. Die Komponente kann so konfiguriert werden, dass ein erneutes Hashing der Daten vermieden wird, indem die Eigenschaften CountDistinctKeys, CountDistinctKeyScale und AutoExtendFactor angepasst werden.|  
|0x402090DC|1075876060|DTS_I_STARTPROCESSINGFILE|Die Verarbeitung der Datei "%1" wurde gestartet.|  
|0x402090DD|1075876061|DTS_I_FINISHPROCESSINGFILE|Die Verarbeitung der Datei "%1" wurde beendet.|  
|0x402090DE|1075876062|DTS_I_TOTALDATAROWSPROCESSEDFORFILE|Für die Datei "%1" wurden insgesamt %2!I64d! Datenzeilen verarbeitet.|  
|0x402090DF|1075876063|DTS_I_FINALCOMMITSTARTED|Der endgültige Commit für die Dateneinfügung in "%1" wurde gestartet.|  
|0x402090E0|1075876064|DTS_I_FINALCOMMITENDED|Der endgültige Commit für die Dateneinfügung in "%1" wurde abgeschlossen.|  
|0x402090E1|1075876065|DTS_I_BEGINHASHINGCACHE|%1!u! Zeilen werden dem Cache hinzugefügt. Das System verarbeitet die Zeilen.|  
|0x402090E2|1075876066|DTS_I_SUCCEEDEDHASHINGCACHE|%1 hat %2!u! Zeilen im Cache verarbeitet. Die Verarbeitungszeit betrug %3 Sekunden. Der Cache hat %4!I64u! Bytes verwendet.|  
|0x402090E3|1075876067|DTS_I_FAILEDHASHINGCACHE|%1 konnte die Zeilen im Cache nicht verarbeiten.  Die Verarbeitungszeit betrug %2 Sekunde(n).|  
|0x402090E4|1075876068|DTS_I_SUCCEEDEDPREPARINGCACHE|%1 hat den Cache erfolgreich vorbereitet. Die Vorbereitungszeit betrug %2 Sekunden.|  
|0x40209314|1075876628|DTS_I_TXLOOKUP_PARTIALPERF|%1 hat die folgenden Vorgänge ausgeführt: Verarbeitung von %2!I64u! Zeilen, Ausgabe von %3!I64u! Datenbankbefehlen an die Verweisdatenbank und Durchführung von %4!I64u! Suchen mit partiellem Cache.|  
|0x40209315|1075876629|DTS_I_TXLOOKUP_PARTIALPERF2|%1 hat die folgenden Vorgänge ausgeführt: Verarbeitung von %2!I64u! Zeilen, Ausgabe von %3!I64u! Datenbankbefehlen an die Verweisdatenbank und Durchführung von %4!I64u! Suchen mit partiellem Cache sowie %5!I64u! Suchen, wobei der Cache für Zeilen ohne übereinstimmende Einträge in der anfänglichen Suche verwendet wurde.|  
|0x40209316|1075876630|DTS_I_CACHEFILEWRITESTARTED|%1 schreibt den Cache in die Datei "%2".|  
|0x40209317|1075876631|DTS_I_CACHEFILEWRITESUCCEEDED|%1 hat den Cache in die Datei "%2" geschrieben.|  
|0x4020F42C|1075901484|DTS_I_OLEDBDESTZEROMAXCOMMITSIZE|Die Eigenschaft der maximalen Einfügungscommitgröße des OLE DB-Ziels "%1" wird auf 0 (null) festgelegt. Diese Einstellung kann dazu führen, dass das ausgeführte Paket nicht mehr antwortet. Weitere Informationen finden Sie im F1-Hilfethema 'Ziel-Editor für OLE DB' (Verbindungs-Manager-Seite).|  
  
##  <a name="msgGeneral"></a> Allgemeine Meldungen und Ereignismeldungen  
 Die symbolischen Namen von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Fehlermeldungen beginnen mit **DTS_MSG_**.  
  
|Hexadezimalcode|Dezimalcode|Symbolischer Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x1|1|DTS_MSG_CATEGORY_SERVICE_CONTROL|Falsche Funktion.|  
|0x2|2|DTS_MSG_CATEGORY_RUNNING_PACKAGE_MANAGEMENT|Die angegebene Datei wurde nicht gefunden.|  
|0x100|256|DTS_MSG_SERVER_STARTING|Microsoft SSIS-Dienst wird gestartet.<br /><br /> Server-Version %1|  
|0x101|257|DTS_MSG_SERVER_STARTED|Microsoft SSIS-Dienst wurde gestartet.<br /><br /> Server-Version %1|  
|0x102|258|DTS_MSG_SERVER_STOPPING|Timeout bei Wartevorgang.|  
|0x103|259|DTS_MSG_SERVER_STOPPED|Es sind keine weiteren Daten verfügbar.|  
|0x104|260|DTS_MSG_SERVER_START_FAILED|Fehler beim Starten des Microsoft SSIS-Diensts.<br /><br /> Fehler: %1|  
|0x105|261|DTS_MSG_SERVER_STOP_ERROR|Fehler beim Beenden des Microsoft SSIS-Diensts.<br /><br /> Fehler: %1|  
|0x110|272|DTS_MSG_SERVER_MISSING_CONFIG|Die Konfigurationsdatei für den Microsoft SSIS-Dienst ist nicht vorhanden.<br /><br /> Wird mit Standardeinstellungen geladen.|  
|0x111|273|DTS_MSG_SERVER_BAD_CONFIG|Falsche Konfigurationsdatei für den Microsoft SSIS-Dienst.<br /><br /> Fehler beim Lesen der Konfigurationsdatei: %1<br /><br /> Server wird mit Standardeinstellungen geladen.|  
|0x112|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Microsoft SSIS-Dienst:<br /><br /> Registrierungseinstellung mit Angabe der Konfigurationsdatei ist nicht vorhanden.<br /><br /> Es wird versucht, die Standardkonfigurationsdatei zu laden.|  
|0x150|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Microsoft SSIS-Dienst: Ausgeführtes Paket wird beendet.<br /><br /> Paketinstanz-ID: %1<br /><br /> Paket-ID: %2<br /><br /> Paketname: %3<br /><br /> Paketbeschreibung: %4<br /><br /> Paket gestartet von: %5.|  
|0x40013000|1073819648|DTS_MSG_PACKAGESTART|Paket "%1" wurde gestartet.|  
|0x40013001|1073819649|DTS_MSG_PACKAGESUCCESS|Paket "%1" wurde erfolgreich abgeschlossen.|  
|0x40013002|1073819650|DTS_MSG_PACKAGECANCEL|Paket "%1" wurde abgebrochen.|  
|0x40013003|1073819651|DTS_MSG_PACKAGEFAILURE|Fehler bei Paket "%1".|  
|0x40013004|1073819652|DTS_MSG_CANTDELAYLOADDLL|Das Modul %1 kann die DLL %2 zum Aufrufen des Einstiegspunkts %3 aufgrund des Fehlers %4 nicht laden. Zum Ausführen des Produkts ist die DLL erforderlich, doch sie wurde im Pfad nicht gefunden.|  
|0x40013005|1073819653|DTS_MSG_CANTDELAYLOADDLLFUNCTION|Das Modul %1 hat die DLL %2 geladen, kann aber aufgrund des Fehlers %4 den Einstiegspunkt %3 nicht finden. Die benannte DLL wurde im Pfad nicht gefunden, doch zum Ausführen des Produkts ist diese DLL erforderlich.|  
|0x40103100|1074802944|DTS_MSG_EVENTLOGENTRY|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103101|1074802945|DTS_MSG_EVENTLOGENTRY_PREEXECUTE|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103102|1074802946|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103103|1074802947|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103104|1074802948|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103105|1074802949|DTS_MSG_EVENTLOGENTRY_WARNING|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103106|1074802950|DTS_MSG_EVENTLOGENTRY_ERROR|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103107|1074802951|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103108|1074802952|DTS_MSG_EVENTLOGENTRY_PROGRESS|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x40103109|1074802953|DTS_MSG_EVENTLOGENTRY_EXECSTATCHANGE|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x4010310A|1074802954|DTS_MSG_EVENTLOGENTRY_VARVALCHANGE|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x4010310B|1074802955|DTS_MSG_EVENTLOGENTRY_CUSTOMEVENT|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x4010310C|1074802956|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x4010310D|1074802957|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
|0x4010310E|1074802958|DTS_MSG_EVENTLOGENTRY_INFORMATION|Ereignisname: %1<br /><br /> Meldung: %9<br /><br /> Operator: %2<br /><br /> Quellenname: %3<br /><br /> Quellen-ID: %4<br /><br /> Ausführungs-ID: %5<br /><br /> Startzeit: %6<br /><br /> Beendigungszeit: %7<br /><br /> Datencode: %8|  
  
##  <a name="msgSuccess"></a> Erfolgsmeldungen  
 Die symbolischen Namen von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Erfolgsmeldungen beginnen mit **DTS_S_**.  
  
|Hexadezimalcode|Dezimalcode|Symbolischer Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0x40003|262147|DTS_S_NULLDATA|Der Wert ist NULL.|  
|0x40005|262149|DTS_S_TRUNCATED|Der Zeichenfolgenwert war abgeschnitten. Der Puffer hat eine Zeichenfolge empfangen, die für die Spalte zu lang war. Die Zeichenfolge wurde deshalb vom Puffer abgeschnitten.|  
|0x200001|2097153|DTS_S_EXPREVALTRUNCATIONOCCURRED|Beim Auswerten des Ausdrucks wurden Daten abgeschnitten. Der Abschneidevorgang erfolgte während der Auswertung, wozu jeder beliebige Punkt in einem Zwischenschritt zählen kann.|  
  
##  <a name="msgPipeline"></a> Fehlermeldungen der Datenflusskomponenten  
 Die symbolischen Namen von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Fehlermeldungen beginnen mit **DTSBC_E_**, wobei „BC“ auf die systemeigene Basisklasse verweist, von der die meisten Microsoft-Datenflusskomponenten abgeleitet werden.  
  
|Hexadezimalcode|Dezimalcode|Symbolischer Name|Description|  
|----------------------|------------------|-------------------|-----------------|  
|0xC8000002|-939524094|DTSBC_E_INCORRECTEXACTNUMBEROFTOTALOUTPUTS|Die Gesamtanzahl der Ausgaben und Fehlerausgaben (%1!lu!) ist falsch. Dieser Wert muss genau %2!lu! betragen.|  
|0xC8000003|-939524093|DTSBC_E_FAILEDTOGETOUTPUTBYINDEX|Die Ausgabe mit dem Index %1!lu! kann nicht abgerufen werden.|  
|0xC8000005|-939524091|DTSBC_E_INCORRECTEXACTNUMBEROFERROROUTPUTS|Die Anzahl der Fehlerausgaben (%1!lu!) ist falsch. Dieser Wert muss genau %2!lu! betragen.|  
|0xC8000006|-939524090|DTSBC_E_INVALIDVALIDATIONSTATUSVALUE|Der folgende Überprüfungsstatuswert ist falsch: "%1!lu! ".  Dieser Wert muss einer der Werte in der DTSValidationStatus-Enumeration sein.|  
|0xC8000007|-939524089|DTSBC_E_INPUTHASNOOUTPUT|Die Eingabe „%1!lu!“ hat keine synchrone Ausgabe.|  
|0xC8000008|-939524088|DTSBC_E_INPUTHASNOERROROUTPUT|Die Eingabe „%1!lu!“ weist keine synchrone Fehlerausgabe auf.|  
|0xC8000009|-939524087|DTSBC_E_INVALIDHTPIVALUE|Der HowToProcessInput-Wert %1!lu! ist ungültig. Dieser Wert muss einer der Werte aus der HowToProcessInput-Enumeration sein.|  
|0xC800000A|-939524086|DTSBC_E_FAILEDTOGETCOLINFO|Fehler beim Abrufen von Informationen aus dem Puffer für Zeile „%1!ld!“, Spalte „%2!ld!“ .  Der Fehlercode 0x%3!8.8X! wurde zurückgegeben.|  
|0xC800000B|-939524085|DTSBC_E_FAILEDTOSETCOLINFO|Fehler beim Festlegen von Informationen für Zeile „%1!ld!“, Spalte „%2!ld!“ im Puffer .  Der Fehlercode 0x%3!8.8X! wurde zurückgegeben.|  
|0xC800000C|-939524084|DTSBC_E_INVALIDPROPERTY|Die Eigenschaft "%1" ist ungültig.|  
|0xC800000D|-939524083|DTSBC_E_PROPERTYNOTFOUND|Die Eigenschaft "%1" wurde nicht gefunden.|  
|0xC8000010|-939524080|DTSBC_E_READONLYPROPERTY|Fehler beim Zuweisen eines Werts zur schreibgeschützten Eigenschaft "%1".|  
|0xC8000011|-939524079|DTSBC_E_CANTINSERTOUTPUTCOLUMN|%1 lässt das Einfügen von Ausgabespalten nicht zu.|  
|0xC8000012|-939524078|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCH|Die Metadaten der Ausgabespalten stimmen nicht mit den Metadaten der zugeordneten Eingabespalten überein.  Die Metadaten der Ausgabespalten werden aktualisiert.|  
|0xC8000013|-939524077|DTSBC_E_OUTPUTCOLUMNSMISSING|Es gibt Eingabespalten, denen keine Ausgabespalten zugeordnet sind. Die Ausgabespalten werden hinzugefügt.|  
|0xC8000014|-939524076|DTSBC_E_TOOMANYOUTPUTCOLUMNS|Es gibt Ausgabespalten, denen keine Eingabespalten zugeordnet sind. Die Ausgabespalten werden entfernt.|  
|0xC8000015|-939524075|DTSBC_E_OUTPUTCOLUMNSMETADATAMISMATCHUNMAP|Die Metadaten der Ausgabespalten stimmen nicht mit den Metadaten der zugeordneten Eingabespalten überein.  Die Zuordnung der Eingabespalten wird aufgehoben.|  
|0xC8000016|-939524074|DTSBC_E_UNMAPINPUTCOLUMNS|Es gibt Eingabespalten, denen keine Ausgabespalten zugeordnet sind. Die Zuordnung der Eingabespalten wird aufgehoben.|  
|0xC8000017|-939524073|DTSBC_E_MULTIPLEINCOLSTOOUTCOL|Eine Eingabespalte ist einer Ausgabespalte zugeordnet, und diese Ausgabespalte ist bereits einer anderen Eingabespalte in derselben Eingabe zugeordnet.|  
|0xC8000018|-939524072|DTSBC_E_CANTINSERTEXTERNALMETADATACOLUMN|%1 lässt das Einfügen von externen Metadatenspalten nicht zu.|  
  
  
