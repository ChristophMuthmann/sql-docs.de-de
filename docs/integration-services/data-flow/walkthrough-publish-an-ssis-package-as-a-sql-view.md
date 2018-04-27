---
title: 'Exemplarische Vorgehensweise: Veröffentlichen eines SSIS-Pakets als eine SQL-Ansicht | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.packagepublishwizard.f1
ms.assetid: d32d9761-93fb-4020-bf82-231439c6f3ac
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4aca75d9495d628c314c1382a73dc889cdcc367
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="walkthrough-publish-an-ssis-package-as-a-sql-view"></a>Exemplarische Vorgehensweise: Veröffentlichen eines SSIS-Pakets als eine SQL-Ansicht
  Diese exemplarische Vorgehensweise enthält detaillierte Schritte zum Veröffentlichen eines SSIS-Pakets als SQL-Ansicht in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 Die folgende Software muss auf Ihrem Computer installiert sein, bevor Sie diese exemplarische Vorgehensweise durchführen können.  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oder höher mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
2.  [SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md).  
  
## <a name="step-1-build-and-deploy-ssis-project-to-the-ssis-catalog"></a>Schritt 1: Erstellen und Bereitstellen des SSIS-Projekts im SSIS-Katalog  
 In diesem Schritt erstellen Sie ein SSIS-Paket, das Daten aus einer von SSIS unterstützten Datenquelle extrahiert (in diesem Beispiel verwenden wir eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank) und die Daten mithilfe einer Datenstreamingziel-Komponente ausgibt. Dann erstellen Sie das SSIS-Projekt und stellen es im SSIS-Katalog bereit.  
  
1.  Starten Sie **SQL Server Data Tools**. Zeigen Sie im Menü **Start** auf **Alle Programme**, dann auf **Microsoft SQL Server**, und klicken Sie auf **SQL Server Data Tools**.  
  
2.  Erstellen Sie ein neues [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt.  
  
    1.  Klicken Sie auf der Menüleiste auf **Datei** , zeigen Sie auf **Neu**, und klicken Sie dann auf **Projekt**.  
  
    2.  Erweitern Sie im linken Bereich **Business Intelligence** , und klicken Sie dann in der Strukturansicht auf **Integration Services** .  
  
    3.  Wählen Sie **Integration Services-Projekt** aus, sofern nicht bereits ausgewählt.  
  
    4.  Geben Sie **SSISPackagePublishing** für **Projektname**an.  
  
    5.  Geben Sie einen Speicherort für das Projekt an.  
  
    6.  Klicken Sie auf **OK** , um das Dialogfeld **Neues Projekt** zu schließen.  
  
3.  Ziehen Sie die Komponente **Datenfluss** aus der **SSIS-Toolbox** auf die Entwurfsoberfläche der Registerkarte **Ablaufsteuerung** .  
  
4.  Doppelklicken Sie auf die Komponente **Datenfluss** in der **Ablaufsteuerung** , um den **Datenfluss-Designer**zu öffnen.  
  
5.  Ziehen Sie eine **Quellkomponente** aus der Toolbox auf den **Datenfluss-Designer** , und konfigurieren Sie ihn für das Extrahieren von Daten aus einer Datenquelle.  
  
    1.  Erstellen Sie im Rahmen der exemplarischen Vorgehensweise eine Testdatenbank: **TestDB** mit einer Tabelle: **Employee**. Erstellen Sie die Tabelle mit drei Spalten **ID**, **FirstName** und **LastName**.  
  
    2.  Legen Sie **ID** als Primärschlüssel fest.  
  
    3.  Fügen Sie zwei Datensätze mit den folgenden Daten ein.  
  
        |im Elementknoten &lt;Customer ID="1"|FirstName|LastName|  
        |--------|---------------|--------------|  
        |1|John|Doe|  
        |2|Jane|Doe|  
  
    4.  Ziehen Sie die Komponente **OLE DB-Quelle** aus der **SSIS-Toolbox** auf die Registerkarte **Datenfluss-Designer**.  
  
    5.  Konfigurieren Sie die Komponente für das Extrahieren von Daten aus der Tabelle **Mitarbeiter** in die Datenbank **TestDB** . Wählen Sie **(local).TestDB** für **OLE DB-Verbindungs-Manager**, **Tabelle oder Sicht** für **Datenzugriffsmodus**und **[dbo].[Employee** ] für **Name der Tabelle oder Sicht**.  
  
         ![Datenstreamingziel – OLE DB-Verbindung](../../integration-services/data-flow/media/dsd-oledbconnectionmanager.jpg "Datenstreamingziel – OLE DB-Verbindung")  
  
6.  Ziehen Sie nun das **Datenstreamingziel** von der Toolbox in den Datenfluss. Diese Komponente sollte sich im allgemeinen Abschnitt der Toolbox befinden.  
  
7.  Verbinden Sie die Komponente **OLE DB-Datenquelle** im Datenfluss mit der Komponente **Datenstreamingziel** .  
  
8.  Erstellen und Bereitstellen des SSIS-Projekts im SSIS-Katalog  
  
    1.  Klicken Sie auf der Menüleiste auf **Projekt** und dann auf **Bereitstellen**.  
  
    2.  Befolgen Sie im Assistenten die Anweisungen, um das Projekt im SSIS-Katalog auf dem lokalen Datenbankserver bereitzustellen. Im folgenden Beispiel wird **Power BI** als Ordnername und **SSISPackagePublishing** als Projektname im SSIS-Katalog verwendet.  
  
## <a name="step-2-use-the-ssis-data-feed-publishing-wizard-to-publish-ssis-package-as-a-sql-view"></a>Schritt 2: Verwenden des SSIS-Datenfeedveröffentlichungs-Assistent zum Veröffentlichen des SSIS-Pakets als eine SQL-Ansicht  
 In diesem Schritt verwenden Sie den SSIS-Datenfeedveröffentlichungs-Assistent (SQL Server Integration Services), um das SSIS-Paket als Sicht in einer SQL Server-Datenbank zu veröffentlichen. Die Ausgabedaten des Pakets können durch Abfragen dieser Sicht genutzt werden.  
  
 Der SSIS-Datenfeedveröffentlichungs-Assistent erstellt einen Verbindungsserver mithilfe des OLE DB-Anbieters für SSIS (SSISOLEDB) und anschließend eine SQL-Ansicht, die aus einer Abfrage auf den Verbindungsserver besteht. Diese Abfrage umfasst den Ordnernamen, den Projektnamen und den Paketnamen im SSIS-Katalog.  
  
 Die Ansicht sendet über den von Ihnen erstellten Verbindungsserver zur Laufzeit eine Abfrage an den OLE DB-Anbieter für SSIS. Der OLE DB-Anbieter für SSIS führt das Paket aus, das Sie in der Abfrage angegeben haben und gibt das tabellarische Resultset an die Abfrage zurück.  
  
1.  Starten Sie den **SSIS-Datenfeedveröffentlichungs-Assistenten** durch Ausführen von „ISDataFeedPublishingWizard.exe“ in „C:\Programme\Microsoft SQL Server\130\DTS\Binn“, oder indem Sie auf „Microsoft SQL Server 2016\Datenfeedveröffentlichungs-Assistent für SQL Server 2016“ unter „Start\Alle Programme“ klicken.  
  
2.  Klicken Sie auf der Seite **Einführung** auf **Weiter** .  
  
     ![Datenfeedveröffentlichungs-Assistent – Seite „Einführung“](../../integration-services/data-flow/media/dsd-feedpublishingwizard-introductionpage.jpg "Datenfeedveröffentlichungs-Assistent – Seite „Einführung“")  
  
3.  Führen Sie auf der Seite **Paketeinstellungen** die folgenden Aufgaben aus:  
  
    1.  Geben Sie den **Namen** der SQL Server-Instanz ein, die den SSIS-Katalog enthält, oder klicken Sie zum Auswählen des Servers auf **Durchsuchen** .  
  
         ![Datenfeedveröffentlichungs-Assistent – Seite „Paketeinstellungen“](../../integration-services/data-flow/media/dsd-feedpublishingwizard-packagesettingspage.jpg "Datenfeedveröffentlichungs-Assistent – Seite „Paketeinstellungen“")  
  
    2.  Klicken Sie neben dem Pfadfeld auf **Durchsuchen** , durchsuchen Sie den SSIS-Katalog, wählen Sie das zu veröffentlichende SSIS-Paket aus (Beispiel: **SSISDB**->**SSISPackagePublishing**->**Package.dtsx**), und klicken Sie dann auf **OK**.  
  
         ![Datenfeedveröffentlichungs-Assistent – Suchen nach Paket](../../integration-services/data-flow/media/dsd-feedpublishingwizard-browseforpackage.jpg "Datenfeedveröffentlichungs-Assistent – Suchen nach Paket")  
  
    3.  Geben Sie mithilfe der Paketparameter, Projektparameter und Registerkarten des Verbindungs-Managers am unteren Seitenrand die Werte für alle Paketparameter, Projektparameter oder Einstellungen des Verbindungs-Managers für das Paket ein. Sie können auch einen Umgebungsverweis angeben, der für die Ausführung des Pakets verwendet wird, und Projekt-/Paketparameter an Umgebungsvariablen binden.  
  
         Es wird empfohlen, dass sensible Parameter an Umgebungsvariablen gebunden werden. Dadurch wird sichergestellt, dass der Wert eines sensiblen Parameters nicht im Nur-Text-Format in der vom Assistenten erstellten SQL-Ansicht gespeichert wird.  
  
    4.  Klicken Sie auf **Weiter** , um zur Seite **Veröffentlichungseinstellungen** zu wechseln.  
  
4.  Führen Sie auf der Seite **Veröffentlichungseinstellungen** die folgenden Aufgaben aus:  
  
    1.  Wählen Sie die **Datenbank** für die zu erstellende Sicht aus.  
  
         ![Datenfeedveröffentlichungs-Assistent – Seite „Veröffentlichungseinstellungen“](../../integration-services/data-flow/media/dsd-feedpublishingwizard-publishsettingspage.jpg "Datenfeedveröffentlichungs-Assistent – Seite „Veröffentlichungseinstellungen“")  
  
    2.  Geben Sie einen **Namen** für die **Sicht**ein. Sie können auch eine vorhandene Sicht aus der Dropdownliste auswählen.  
  
    3.  Geben Sie in der Liste **Einstellungen** einen **Namen** für den **Verbindungsserver** an, der der Sicht zugeordnet werden soll. Wenn der Verbindungsserver nicht bereits vorhanden ist, erstellt der Assistent den Verbindungsserver vor dem Erstellen der Sicht. Sie können hier auch Werte für **User32BitRuntime** - und **Timeout** -Werte festlegen.  
  
    4.  Klicken Sie auf die Schaltfläche **Erweitert** . Das Dialogfeld **Erweiterte Einstellungen** sollte angezeigt werden.  
  
    5.  Gehen Sie im Dialogfeld **Erweiterte Einstellungen** folgendermaßen vor:  
  
        1.  Geben Sie das Datenbankschema an, in dem die Sicht (Feld „Schema“) erstellt werden soll.  
  
        2.  Geben Sie an, ob die Daten vor dem Senden über das Netzwerk verschlüsselt werden sollen (Feld „Verschlüsselung“). Weitere Informationen zu dieser Einstellung und der „TrustServerCertificate“-Einstellung finden Sie unter [Verwenden von Verschlüsselung ohne Überprüfung](http://msdn.microsoft.com/library/ms131691.aspx) .  
  
        3.  Geben Sie an, ob ein selbstsigniertes Serverzertifikat verwendet werden kann, wenn die Verschlüsselungseinstellung aktiviert ist (Feld**TrustServerCertificate** ).  
  
        4.  Klicken Sie auf **OK** , um das Dialogfeld **Erweiterte Einstellungen** zu schließen.  
  
    6.  Klicken Sie auf **Weiter** , um zur Seite **Überprüfung** zu wechseln.  
  
5.  Auf der Seite **Überprüfung** überprüfen Sie die Ergebnisse der Überprüfung der Werte für alle Einstellungen. Im folgenden Beispiel wird eine **Warnung** für das Vorhandensein des Verbindungsservers angezeigt, da der Verbindungsserver für die ausgewählte SQL Server-Instanz nicht vorhanden ist. Wenn für **Ergebnis** der Wert **Fehler**angezeigt wird, bewegen Sie den Mauszeiger über **Fehler** , um die Details zu diesem Fehler anzuzeigen. Wenn Sie z. B. die Option „InProcess zulassen“ für den SSISOLEDB-Anbieter nicht aktiviert haben, erhalten Sie einen Fehler zur Aktion „Konfiguration des Verbindungsservers“.  
  
     ![Datenfeedveröffentlichungs-Assistent – Seite „Überprüfung“](../../integration-services/data-flow/media/dsd-feedpublishingwizard-validationpage.jpg "Datenfeedveröffentlichungs-Assistent – Seite „Überprüfung“")  
  
6.  Klicken Sie auf „Bericht speichern“, um diesen Bericht als XML-Datei zu speichern.  
  
7.  Klicken Sie auf der Seite **Überprüfung** auf **Weiter** , um zur Seite **Zusammenfassung** zu wechseln.  
  
8.  Überprüfen Sie Ihre Auswahl auf der Seite **Zusammenfassung** , und klicken Sie auf **Veröffentlichen** , um den Veröffentlichungsprozess zu starten. Dadurch wird der Verbindungsserver erstellt, wenn er nicht bereits auf dem Server vorhanden ist. Anschließend wird die Sicht mithilfe des Verbindungsservers erstellt.  
  
     ![Datenfeedveröffentlichungs-Assistent – Seite „Zusammenfassung“](../../integration-services/data-flow/media/dsd-feedpublishingwizard-summarypage.jpg "Datenfeedveröffentlichungs-Assistent – Seite „Zusammenfassung“")  
  
     Die Ausgabedaten des Pakets können jetzt durch Ausführen der folgenden SQL-Anweisung für die TestDB-Datenbank abgefragt werden: SELECT * FROM [SSISPackageView].  
  
9. Klicken Sie auf **Bericht speichern**, um diesen Bericht als XML-Datei zu speichern.  
  
10. Überprüfen Sie die Ergebnisse des Veröffentlichungsprozesses, und klicken Sie auf **Fertig stellen** , um den Assistenten zu schließen.  
  
    > [!NOTE]  
    >  Die folgenden Datentypen werden nicht unterstützt: text, ntext, image, nvarchar(max), varchar(max) und varbinary(max).  
  
## <a name="step-3-test-the-sql-view"></a>Schritt 3: Testen der SQL-Ansicht  
 In diesem Schritt führen Sie die vom SSIS-Datenfeedveröffentlichungs-Assistenten erstellte SQL-Ansicht aus.  
  
1.  Starten Sie SQL Server Management Studio.  
  
2.  Erweitern Sie \<**Computername**>, **Datenbanken**, \<**Im Assistenten ausgewählte Datenbank**> und **Sichten**.  
  
3.  Klicken Sie mit der rechten Maustaste auf die \<**vom Assistenten erstellte Sicht**>, und klicken Sie dann auf **Die ersten 1000 Zeilen auswählen**.  
  
4.  Vergewissern Sie sich, dass die Ergebnisse aus dem SSIS-Paket angezeigt werden.  
  
## <a name="step-4-verify-the-ssis-package-execution"></a>Schritt 4: Überprüfen der SSIS-Paketausführung  
 In diesem Schritt überprüfen Sie, ob das SSIS-Paket ausgeführt wurde.  
  
1.  Erweitern Sie in SQL Server Management Studio **Integration Services-Kataloge**und dann **SSISDB**. Anschließend erweitern Sie den **Ordner** , der Ihr SSIS-Projekt enthält, dann **Projekte**sowie Ihren Projektknoten, und abschließend erweitern Sie **Pakete**.  
  
2.  Klicken Sie mit der rechten Maustaste auf das SSIS-Paket, klicken Sie auf **Berichte**, und zeigen Sie dann auf **Standardberichte**. Anschließend klicken Sie auf **Alle Ausführungen**.  
  
3.  Im Bericht sollte die Ausführung des SSIS-Pakets angezeigt werden.  
  
    > [!NOTE]  
    >  Auf einem Computer mit Windows Vista Service Pack 2 werden möglicherweise zwei Ausführungen des SSIS-Pakets im Bericht angezeigt, d. h. eine erfolgreiche und eine fehlgeschlagene Ausführung. Ignorieren Sie die fehlerhafte Ausführung, da sie durch ein in dieser Version bekanntes Problem verursacht wird.  
  
## <a name="more-info"></a>Weitere Informationen  
 Der Datenfeedveröffentlichungs-Assistent führt die folgenden wichtigen Schritte aus:  
  
1.  Erstellung einen Verbindungsservers und dessen Konfiguration für die Verwendung des OLE DB-Anbieters für SSIS.  
  
2.  Erstellung einer SQL-Ansicht in der angegebenen Datenbank, die den Verbindungsserver mit Kataloginformationen für das ausgewählte Paket abfragt.  
  
 Dieser Abschnitt enthält Verfahren zum Erstellen eines Verbindungsservers und einer SQL-Ansicht ohne den Datenfeedveröffentlichungs-Assistenten. Außerdem enthält er weitere Informationen zur Verwendung der OPENQUERY-Funktion mit dem OLE DB-Anbieter für SSIS.  
  
### <a name="create-a-linked-server-using-the-ole-db-provider-for-ssis"></a>Erstellen eines Verbindungsservers mithilfe des OLE DB-Anbieters für SSIS  
 Erstellen Sie einen Verbindungsserver mithilfe des OLE DB-Anbieters für SSIS (SSISOLEDB) durch Ausführen der folgenden Abfrage in SQL Server Management Studio.  
  
```sql 
  
USE [master]  
GO  
  
EXEC sp_addlinkedserver  
@server = N'SSISFeedServer',  
@srvproduct = N'Microsoft',  
@provider = N'SSISOLEDB',  
@datasrc = N'.'  
GO  
  
```  
  
### <a name="create-a-view-using-linked-server-and-ssis-catalog-information"></a>Erstellen einer Ansicht mithilfe des Verbindungsservers und der SSIS-Kataloginformationen  
 In diesem Schritt erstellen Sie eine SQL-Ansicht, die eine Abfrage auf dem Verbindungsserver ausführt, den Sie im vorherigen Abschnitt erstellt haben. Die Abfrage umfasst den Ordnernamen, Projektnamen und Paketnamen im SSIS-Katalog.  
  
 Zur Laufzeit, wenn die Sicht ausgeführt wird, startet die Verbindungsserverabfrage, die in der Sicht definiert ist, das in der Abfrage angegebene SSIS-Paket und empfängt die Paketausgabe als tabellarisches Resultset.  
  
1.  Geben Sie vor der Erstellung der Sicht die folgende Abfrage in das neue Abfragefenster ein, und führen Sie diese anschließend aus. OPENQUERY ist eine von SQL Server unterstützte Rowsetfunktion. Sie führt die angegebene Pass-Through-Abfrage auf dem angegebenen Verbindungsserver mit dem OLE DB-Anbieter aus, der dem Verbindungsserver zugeordnet ist. Auf OPENQUERY kann in der FROM-Klausel einer Abfrage so verwiesen werden, als ob es ein Tabellenname wäre. Weitere Informationen finden Sie in der [OPENQUERY-Dokumentation in der MSDN Library](http://msdn.microsoft.com/library/ms188427.aspx) .  
  
    ```sql
    SELECT * FROM OPENQUERY(SSISFeedServer,N'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  Aktualisieren Sie bei Bedarf den Ordnernamen, Projektnamen und Paketnamen. Wenn bei der OPENQUERY-Funktion ein Fehler auftritt, erweitern Sie in **SQL Server Management Studio**die Option **Serverobjekte**, **Verbindungsserver**sowie **Anbieter**, und doppelklicken Sie auf den Anbieter **SSISOLEDB** . Stellen Sie anschließend sicher, dass die Option **InProcess zulassen** aktiviert ist.  
  
2.  Erstellen Sie in der Datenbank **TestDB** im Rahmen dieser exemplarischen Vorgehensweise eine Sicht, indem Sie die folgende Abfrage ausführen.  
  
    ```sql
  
    USE [TestDB]   
    GO   
  
    CREATE VIEW SSISPackageView AS   
    SELECT * FROM OPENQUERY(SSISFeedServer, 'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
  
    ```  
  
3.  Testen Sie die Sicht durch Ausführen der folgenden Abfrage.  
  
    ```sql
    SELECT * FROM SSISPackageView  
    ```  
  
### <a name="openquery-function"></a>OPENQUERY-Funktion  
 Syntax der OPENQUERY-Funktion:  
  
```sql 
SELECT * FROM OPENQUERY(<LinkedServer Name>, N’Folder=<Folder Name from SSIS Catalog>; Project=<SSIS Project Name>; Package=<SSIS Package Name>; Use32BitRuntime=[True | False];Parameters=”<parameter_name_1>=<value1>; parameter_name_2=<value2>”;Timeout=<Number of Seconds>;’)  
```  
  
 Parameter für Ordner, Projekt und Paket müssen angegeben werden. Use32BitRuntime, Timeout und Parameter sind optional.  
  
 Der Wert von „Use32BitRuntime“ kann „0“, „1“, „true“ oder „false“ sein. Er gibt an, ob das Paket mit der 32-Bit-Laufzeit ausgeführt werden soll („1“ oder „true“), wenn die Plattform von SQL Server eine 64-Bit-Version ist.  
  
 „Timeout“ gibt die Anzahl der Sekunden an, die der OLE DB-Anbieter für SSIS warten kann, bevor neue Daten aus dem SSIS-Paket eingehen. Der Standardwert für „Timeout“ beträgt 60 Sekunden. Sie können einen ganzzahligen Wert für „Timeout“ zwischen 20 und 32000 angeben.  
  
 Parameter enthalten den Wert von Paket- und Projektparametern. Die Regeln für die Parameter sind mit denen für die Parameter in [DTExec](http://msdn.microsoft.com/library/hh231187.aspx)identisch.  
  
 Die folgende Liste gibt die in der Abfrageklausel zulässigen Sonderzeichen an:  
  
-   Einfache Anführungszeichen ('): Dies wird vom standardmäßigen OPENQUERY unterstützt. Wenn Sie das einfache Anführungszeichen in der Abfrageklausel verwenden möchten, verwenden Sie zwei einfache Anführungszeichen ('').  
  
-   Doppelte Anführungszeichen ("): Die Parameter, die Teil der Abfrage sind, werden in doppelte Anführungszeichen eingeschlossen. Wenn ein Parameter selbst ein doppeltes Anführungszeichen enthält, verwenden Sie das Escapezeichen. Beispiel: \".  
  
-   Linke und rechte eckige Klammern ([ und ]): Diese Zeichen werden verwendet, um führende/nachstehende Leerzeichen anzugeben. Der Eintrag „[ einige Leerzeichen ]“ stellt z. B. die Zeichenfolge „ einige Leerzeichen “ mit einem führenden und einem nachstehenden Leerzeichen dar. Wenn diese Zeichen selbst in der Abfrageklausel verwendet werden, müssen sie mit Escapezeichen versehen werden. Beispiel: \\[ und \\].  
  
-   Schrägstrich (\\): Jeder in der Abfrageklausel verwendete Schrägstrich (\) muss mit Escapezeichen versehen werden. Beispiel: \\\ wird in der Abfrageklausel als \ ausgewertet.  
  
 Schrägstrich (\\): Jeder in der Abfrageklausel verwendete Schrägstrich (\) muss mit Escapezeichen versehen werden. Beispiel: \\\ wird in der Abfrageklausel als \ ausgewertet.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenstreamingziel](../../integration-services/data-flow/data-streaming-destination.md)   
 [Konfigurieren des Datenstreamingziels](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
  
