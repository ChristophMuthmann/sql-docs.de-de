---
title: "Verwenden von ADO zum Ausführen von SQLXML 4.0 Abfragen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- query testers [SQLXML]
- test scripts
- ADO [SQLXML]
- queries [SQLXML], ADO
- SQLXML, ADO
ms.assetid: 3d54e3bb-7c5f-427e-82f8-1403a54c4f53
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0488f2e0e78fc2f915619a6ef0ee7caf6efe5531
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="using-ado-to-execute-sqlxml-40-queries"></a>Verwenden von ADO zum Ausführen von SQLXML 4.0-Abfragen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]In früheren Versionen von SQLXML wurde die HTTP-basierte abfrageausführung mit virtuellen SQLXML IIS-Verzeichnisse und dem SQLXML ISAPI-Filter unterstützt. In SQLXML 4.0 sind diese Komponenten nicht mehr verfügbar, da ähnliche und überlappende Funktionen mit systemeigenen Web-Diensten ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] bereitgestellt werden.  
  
 Als Alternative können Sie Abfragen ausführen und SQLXML 4.0 mit Ihren COM-basierten Anwendungen verwenden, indem Sie die SQLXML-Erweiterungen für ActiveX Data Objects (ADO) nutzen, die in Microsoft Data Access Components (MDAC) 2.6 eingeführt wurden.  
  
 Dieses Thema veranschaulicht die Verwendung von SQLXML und ADO als Teil einer Visual Basic Scripting Edition (VBScript)-Anwendung (ein Skript mit der Erweiterung ".vbs"). Es enthält erste Setupschritte, die Ihnen helfen, Abfragebeispiele in der SQLXML 4.0-Dokumentation erneut zu erstellen und zu testen.  
  
## <a name="creating-the-sqlxml-40-test-script"></a>Erstellen des SQLXML 4.0-Testskripts  
 In diesem Schritt erstellen Sie eine VBScript-Datei (VBS), Sqlxml4test.vbs, mit der SQLXML-Abfragen durch Nutzen der SQLXML ADO-Erweiterungen in ADO 2.6 und höher ausgeführt werden können.  
  
#### <a name="to-create-the-sqlxml-40-query-tester-using-ado-vbscript"></a>So erstellen Sie den SQLXML 4.0-Abfragetester mit ADO (VBScript)  
  
1.  Kopieren Sie den unten stehenden Code, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen Sqlxml4test.vbs.  
  
    ```  
    WScript.Echo "Query process may take a few seconds to complete. Please be patient."  
  
    ' Note that for SQL Server Native Client to be used as the data provider,  
    ' it needs to be installed on the client computer first. Also, SQLXML extensions   
    ' for ADO are used and available in MDAC 2.6 or later.  
  
    'Set script variables.  
    inputFile = "@@FILE_NAME@@"  
    strServer = "@@SERVER_NAME@@"  
    strDatabase = "@@DATABASE_NAME@@"  
    dbGuid = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  
    ' Establish ADO connection to SQL Server and   
    ' create an instance of the ADO Command object.  
    Set conn = CreateObject("ADODB.Connection")  
    Set cmd = CreateObject("ADODB.Command")  
    conn.Open "Provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Server=" & strServer & _  
              ";Database=" & strDatabase & ";Integrated Security=SSPI"  
    Set cmd.ActiveConnection = conn  
  
    ' Create the input stream as an instance of the ADO Stream object.  
    Set inStream = CreateObject("ADODB.Stream")  
    inStream.Open  
    inStream.Charset = "utf-8"  
    inStream.LoadFromFile inputFile  
  
    ' Set ADO Command instance to use input stream.  
    Set cmd.CommandStream = inStream  
  
    ' Set the command dialect.  
    cmd.Dialect = dbGuid  
  
    ' Set a second ADO Stream instance for use as a results stream.   
    Set outStream = CreateObject("ADODB.Stream")  
    outStream.Open  
  
    ' Set dynamic properties used by the SQLXML ADO command instance.   
    cmd.Properties("XML Root").Value = "ROOT"  
    cmd.Properties("Output Encoding").Value = "UTF-8"  
  
    ' Connect the results stream to the command instance and execute the command.  
    cmd.Properties("Output Stream").Value = outStream  
    cmd.Execute , , 1024  
  
    ' Echo cropped/partial results to console.  
    WScript.Echo Left(outStream.ReadText, 1023)  
  
    inStream.Close  
    outStream.Close  
    ```  
  
2.  Aktualisieren Sie die folgenden Skriptwerte für das Beispiel, das Sie testen möchten, sowie die Testumgebung.  
  
    -   Suchen Sie den Namen "`@@FILE_NAME@@`", und ersetzen Sie ihn durch den Namen der Vorlagendatei.  
  
    -   Suchen Sie den Namen "`@@SERVER_NAME@@`", und ersetzen Sie ihn durch den Namen Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz (z. B. "`(local)`", wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lokal ausgeführt wird).  
  
    -   Suchen Sie den Namen "`@@DATABASE_NAME@@`", und ersetzen Sie ihn durch den Namen der Datenbank (z. B. entweder "`AdventureWorks2012`" oder "`tempdb`").  
  
     Aktualisieren Sie ggf. andere Werte, sofern dies in den entsprechenden Anweisungen für das Beispiel angegeben ist, das Sie lokal auf dem Computer neu erstellen möchten.  
  
3.  Speichern Sie die Datei, und schließen Sie es.  
  
4.  Überprüfen Sie, ob Sie zusätzliche Dateien wie XML-Vorlagen oder Schemas erstellt haben, die zu dem Beispiel gehören, das Sie lokal auf dem Computer neu erstellen möchten. Diese Dateien sollten sich in dem gleichen Verzeichnis befinden wie die Testskriptdatei (Sqlxml4test.vbs).  
  
5.  Folgen Sie den Anweisungen im nächsten Abschnitt zur Verwendung des SQLXML 4.0-Testskripts.  
  
## <a name="using-the-sqlxml-40-test-script"></a>Verwenden des SQLXML 4.0-Testskripts  
 Im folgenden Verfahren wird beschrieben, wie Sie die Sqlxml4test.vbs-Dateien zum Testen der in dieser Dokumentation enthaltenen Beispielabfragen verwenden.  
  
#### <a name="to-use-the-sqlxml-40-query-tester"></a>So verwenden Sie den SQLXML 4.0-Abfragetester  
  
1.  Überprüfen Sie, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client installiert ist. Gehen Sie dazu wie folgt vor:  
  
    1.  Aus der **starten** Sie im Menü **Einstellungen**, und klicken Sie dann auf **Systemsteuerung**.  
  
    2.  Öffnen Sie in der Systemsteuerung **Software**  
  
    3.  Vergewissern Sie sich, die in der Liste der installierten Programme **Microsoft SQL Server Native Client** in der Liste angezeigt.  
  
        > [!NOTE]  
        >  Wenn Sie installieren müssen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client finden Sie unter [Installieren von SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
2.  Überprüfen Sie, ob die für den Clientcomputer installierte MDAC-Version 2.6 oder höher ist. Zum Überprüfen der Versionsinformationen von MDAC können Sie das MDAC Component Checker-Tool verwenden, das Sie kostenlos von der Microsoft-Website (www.microsoft.com) herunterladen können. Weitere Informationen finden Sie auf der Microsoft-Website unter dem Suchbegriff "MDAC Component Checker".  
  
3.  Führen Sie das Skript aus.  
  
     Sie können die VBScript-Datei entweder an der Befehlszeile mit Cscript.exe oder durch Doppelklicken auf die Sqlxml4test.vbs-Datei ausführen, um Windows Script Host (WScript.exe) aufzurufen.  
  
     Bei der Ausführung sollte das Skript eine Meldung mit dem Hinweis anzeigen, dass die Ausführung des Skripts eine Weile in Anspruch nehmen kann, bevor Abfrageergebnisse als Skriptausgabe zurückgegeben und angezeigt werden. Wenn die Ausgabe angezeigt wird, vergleichen Sie den Inhalt mit den für das Beispiel erwarteten Ergebnissen.  
  
  
