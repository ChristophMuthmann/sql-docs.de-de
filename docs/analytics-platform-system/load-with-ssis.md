---
title: Laden von Daten mit Integrationsservices
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: Stellt Referenz- und Bereitstellung von Informationen zum Laden von Daten in SQL Server Parallel Data Warehouse mithilfe von SQL Server Integration Services (SSIS)-Pakete bereit.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 9bdb559a-a91c-4342-8a6e-438cb93f975c
caps.latest.revision: "69"
ms.openlocfilehash: f00f72886a10c8be05db6a28adf3df89f8116081
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="load-data-with-integration-services"></a>Laden von Daten mit Integration Services
Stellt Referenz- und Bereitstellung von Informationen zum Laden von Daten in SQL Server Parallel Data Warehouse mithilfe von SQL Server Integration Services (SSIS)-Pakete bereit.  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](http://msdn.microsoft.com/library/ms141091&#40;v=sql11&#40;.aspx) on MSDN.  

-->
  
## <a name="Basics"></a>Grundlagen  
Integrationsservices ist die Komponente von SQL Server für leistungsstarke Extraktion, Transformation und laden (ETL) von Daten und wird häufig verwendet, um Auffüllen und ein Datawarehouse aktualisiert.  
  
PDW-Zieladapter ist ein Integration Services-Komponente, mit dem Sie Daten mithilfe von Integration Services-Dtsx-Paketen in PDW zu laden. Sie können in einem Paketworkflow für SQL-ServerPDW laden und Zusammenführen von Daten aus mehreren Quellen und Daten an mehrere Ziele laden. Die Ladevorgänge erfolgen parallel innerhalb eines Pakets und unter mehreren gleichzeitig ausgeführten Paketen, bis zu einem Maximum von 10 in der gleichen Anwendung parallel ausgeführten Ladevorgängen.  
  
Zusätzlich zu den Aufgaben, die in diesem Thema beschrieben wird können Sie andere Funktionen von Integration Services verwenden, um zu filtern, zu transformieren, analysieren und Bereinigen der Daten vor dem Laden in das Datawarehouse. Sie können auch den Workflow des Pakets verbessern, indem Sie SQL-Anweisungen ausführen, untergeordnete Pakete ausführen oder E-Mails versenden.  
  
Vollständige Dokumentation der Integrationsdienste finden Sie unter [SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026(v=sql11).aspx).  
  
## <a name="HowToDeployPackage"></a>Methoden zum Ausführen eines Integration Services-Pakets  
Verwenden Sie eine der folgenden Methoden an, um ein Integration Services-Paket auszuführen.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Ausführen von SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)  
Führen Sie das Paket in BIDS mit der rechten Maustaste auf das Paket, und wählen Sie **Paketausführungs**.  
  
Standardmäßig führt die BIDS-Paketen mit 64-Bit-Binärdateien. Dies richtet sich nach der **Run64BitRuntime** Paket-Eigenschaft. Um diese Eigenschaft festzulegen, wechseln Sie zu **Projektmappen-Explorer**mit der rechten Maustaste auf das Projekt, und wählen Sie **Eigenschaften**. Auf der **Integration Services-Eigenschaftenseiten**, wechseln Sie zu **Konfigurationseigenschaften** , und wählen Sie **Debuggen**. Daraufhin werden die **Run64BitRuntime** Eigenschaft mit dem der **Debug-Optionen**. Verwendung von 32-Bit-Laufzeiten, legen Sie **"false"**. Um 64-Bit-Laufzeiten verwenden zu können, legen Sie **"true"**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Ausführen von SQL Server 2012, SQL Server Data Tools  
Führen Sie das Paket in SQL Server Data Tools, mit der rechten Maustaste auf das Paket, und wählen Sie **Paketausführungs**.  
  
### <a name="run-from-powershell"></a>Ausführen von PowerShell  
Zum Ausführen des Pakets von Windows PowerShell mit der **Dtexec** Hilfsprogramm:`dtexec /FILE <packagePath>`  
  
Beispielsweise `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Ausführen von Windows-Befehlszeile 
Zum Ausführen des Pakets aus einer Windows-Eingabeaufforderung mit dem **Dtexec** Hilfsprogramm:`dtexec /FILE <packagePath>`  
  
Beispiel: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>Datentypen  
Verwendung von Integration Services zum Laden von Daten aus einer Datenquelle mit einer SQL Server PDW-Datenbank, werden zuerst die Daten aus den Quelldaten in Integration Services-Datentypen zugeordnet. Dies ermöglicht die Zuordnung von Daten aus mehreren Datenquellen zu einem allgemeinen Satz von Datentypen.  
  
Anschließend werden die Daten von Integration Services in SQL Server PDW-Datentypen zugeordnet. Der folgenden Tabelle aufgeführt für jeden SQL Server PDW-Datentyp der Integration Services-Datentypen, die in der SQL Server PDW-Datentyp konvertiert werden können.  
  
|PDW-Datentyp|Integration Services-Datentypen (s), die PDW-Datentyp zugeordnet werden soll.|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|GLEITKOMMAZAHL|DT_R4, DT_R8|  
|INT|DT_I1, DTI2, DT_I4, DT_UI1, DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|NVARCHAR|DT_WSTR, DT_STR|  
|real|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1, DT_I2, DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**Eingeschränkte Unterstützung für datentypgenauigkeit**  
  
PDW tritt ein Validierungsfehler generiert, wenn Sie eine DT_NUMERIC oder "DT_DECIMAL" Eingabespalte zugeordnet werden, die einen Wert mit einer höheren Genauigkeit als 28 enthält.  
  
**Nicht unterstützte Datentypen**  
  
Die folgenden Datentypen von Integration Services von SQL Server PDW nicht unterstützt:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Um Spalten zu laden, die Daten dieser Typen in SQL Server PDW enthalten, müssen Sie eine transformationsupstream für Datenkonvertierung in den Datenfluss für die Daten in einen kompatiblen Datentyp konvertieren hinzufügen.  
  
## <a name="permissions"></a>Berechtigungen  
Führen Sie ein Integration Services-Paket laden, müssen wie folgt vor:  
  
-   Laden Sie die Berechtigung für die Datenbank.  
  
-   Zutreffend INSERT, UPDATE, DELETE-Berechtigung für die Zieltabelle.  
  
-   Wenn eine Stagingdatenbank verwendet wird, über die Berechtigung für die staging-Datenbank erstellen. Dies ist zum Erstellen einer temporären Tabelle.  
  
-   Wenn keine Stagingdatenbank verwendet wird, über die Berechtigung "erstellen" in der Zieldatenbank. Dies ist zum Erstellen einer temporären Tabelle.  
  
## <a name="GenRemarks"></a>Allgemeine Hinweise  
Wenn ein Integration Services-Paket verfügt über mehrere SQL Server PDW-Ziele, die ausgeführt wird, und der Verbindungen beendet wird, beendet Integration Services Daten auf alle SQL Server PDW-Ziele übertragen.  
  
## <a name="Limits"></a>Einschränkungen  
Bei einem Integration Services-Paket ist die Anzahl der SQL Server PDW-Ziele für die gleiche Datenquelle durch die maximale Anzahl aktiver Ladevorgänge beschränkt. Das Maximum ist vorkonfiguriert und kann nicht durch den Benutzer konfiguriert werden. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Jedes Ziel des Integration Services-Paket für die gleiche Datenquelle zählt als ein Ladevorgang, wenn das Paket ausgeführt wird. Angenommen die maximale Anzahl aktiver Ladevorgänge ist z. B. 10. Das Paket wird nicht ausgeführt, wenn es versucht, 11 oder mehr Ziele für die gleiche Datenquelle zu öffnen.  
  
Es können mehrere Pakete gleichzeitig ausgeführt werden, solange jedes Paket nicht mehr als die maximale Anzahl aktiver Ladevorgänge verwendet. Wenn die maximale Anzahl aktiver Ladevorgänge beispielsweise 10 beträgt, können Sie zwei Pakete mit je 10 Zielen gleichzeitig ausführen. Ein Paket wird ausgeführt während das andere in der Warteschlange steht.  
  
Das Paket wird nicht ausgeführt, wenn die Anzahl der Ladevorgänge in der Warteschlange die maximal zulässige Anzahl der in Warteschlange gestellten Ladevorgänge überschreitet. Beispielsweise, wenn die maximale Anzahl von Ladevorgängen 10 pro Anwendung ist, und die maximale Anzahl der in Warteschlange stehenden Ladevorgänge 40 pro Anwendung beträgt, Sie können gleichzeitig ausgeführt werden fünf Integration Services-Pakete, die je 10 Ziele öffnen. Ein sechstes Paket kann nicht ausgeführt werden.  

> [!IMPORTANT]
> Eine OLE DB-Datenquelle in SSIS mit PDW-Zieladapter verwenden, können Daten beschädigt werden, wenn die Quelltabelle Char und Varchar-Spalten mit SQL-Sortierungen enthält. Es wird empfohlen, eine ADO NET-Quelle verwenden, wenn die Quelltabelle char- oder Varchar-Spalten mit SQL-Sortierungen enthält. 

  
## <a name="Locks"></a>Sperrverhalten  
Beim Laden von Daten mit Integration Services verwendet SQL ServerPDW Sperren auf Zeilenebene zum Aktualisieren von Daten in der Zieltabelle an. Dies bedeutet, dass jede Zeile während des Updates für den Lese- und Schreibzugriff gesperrt wird. Die Zeilen in der Zieltabelle werden nicht gesperrt, während die Daten in die Stagingtabelle geladen werden.  
  
## <a name="Examples"></a>Beispiele für  
  
### <a name="Walkthrough"></a>A. Einfache Last von Flatfile-Datei  
Die folgende exemplarische Vorgehensweise zeigt ein einfaches Laden mithilfe von Integration Services zum Laden von Flatfile-Daten in einer SQL Server PDW-Anwendung.  In diesem Beispiel wird davon ausgegangen, dass Integration Services wurde bereits auf dem Clientcomputer installiert, und das SQL Server PDW-Ziel installiert ist, wie oben beschrieben.  
  
In diesem Beispiel laden wir in der `Orders` Tabelle, die der folgenden DDL-Code hat. Die `Orders` Tabelle ist Teil der `LoadExampleDB` Datenbank.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
So sieht die Daten laden aus:  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
Als Vorbereitung für das Laden, erstellen Sie die Flatfile `exampleLoad.txt`, mit den Daten laden:  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
Erstellen Sie zunächst ein Integration Services-Paket, indem Sie diese Schritte ausführen:  
  
1.  In SQL Server Data Tools \(SSDT\)Option **Datei**, **neu**, und klicken Sie dann **Projekt**. Wählen Sie **Integration Services-Projekts** aufgeführten Optionen aus. Nennen Sie dieses Projekt `ExampleLoad`, und klicken Sie auf **OK**.  
  
2.  Klicken Sie auf die **Control Flow** Registerkarte, und ziehen Sie dann die **Data Flow Task** aus der **Toolbox** auf die **Control Flow** Bereich.  
  
3.  Klicken Sie auf die **Datenfluss** Registerkarte, und ziehen Sie dann **Flat File Source** aus der **Toolbox** auf die **Datenfluss** Bereich. Doppelklicken Sie auf das Sie gerade erstellt, zum Öffnen haben der **Quelleneditor für Flatfiles**.  
  
4.  Klicken Sie auf **Verbindungs-Manager** , und klicken Sie dann auf **neu**.  
  
5.  In der **Namen Verbindungs-Managers** Geben Sie einen Anzeigenamen für die Verbindung. In diesem Beispiel `Example Load Flat File CM`.  
  
6.  Klicken Sie auf **Durchsuchen** , und wählen Sie die `ExampleLoad.txt` Datei auf dem lokalen Computer.  
  
7.  Da die Flatfile-Datei eine Zeile mit den Spaltennamen enthält, klicken Sie auf die **Spaltennamen in der ersten Datenzeile** Feld.  
  
8.  Klicken Sie auf **Spalten** in der linken Spalte und eine Vorschau der Daten, die geladen werden, um sicherzustellen, dass die Spaltennamen und die Daten wurden ordnungsgemäß interpretiert.  
  
9. Klicken Sie auf **erweitert** in der linken Spalte. Klicken Sie auf jeder Spaltenname, um den Datentyp zu überprüfen, der mit den Daten zugeordnet wurde. Geben Sie Änderungen in das Feld, damit die Datentypen der geladenen Daten mit den Zieltypen für die Spalte kompatibel ist.  
  
10. Klicken Sie auf **OK** um den Verbindungs-Manager zu speichern.  
  
11. Klicken Sie auf **OK** zum Beenden der **Quelleneditor für Flatfiles**.  
  
Geben Sie das Ziel für den Datenfluss.  
  
1.  Ziehen Sie die **SQL Server PDW-Ziel** aus der **Toolbox** auf die **Datenfluss** Bereich.  
  
2.  Doppelklicken Sie auf das Sie gerade erstellt haben, um das Laden der **Ziel-Editor für SQL Server PDW**.  
  
3.  Klicken Sie auf den Pfeil nach unten neben **Verbindungs-Manager**.  
  
4.  Wählen Sie **Create a New Connection**.  
  
5.  Füllen Sie die Informationen für die Server, Benutzer, Kennwort und Ziel-Datenbank mit Informationen, die spezifisch für Ihre Anwendung ein. (Beispiele werden unten gezeigt). Klicken Sie dann auf **OK**.  
  
    InfiniBand-Verbindungen **Servernamen**: Geben Sie < Gerätename >-SQLCTL01 17001.  
  
    Für Ethernet-Verbindungen **Servernamen**: Geben Sie die IP-Adresse der Steuerelement-Knoten-Cluster, Komma, Port 17001. Beispielsweise 10.192.63.134,17001.  
  
    **Benutzer:**`user1`  
  
    **Kennwort:**`password1`  
  
    **Zieldatenbank:**`LoadExampleDB`  
  
6.  Wählen Sie die Zieltabelle: `Orders`.  
  
7.  Wählen Sie **Append** als Lademodus und auf **OK**.  
  
Geben Sie den Datenfluss aus der Quelle zum Ziel.  
  
1.  Auf der **Datenfluss** Bereich, ziehen Sie den grünen Pfeil aus der **Flat File Source** Feld der **SQL Server PDW-Ziel** Feld.  
  
2.  Doppelklicken Sie auf die **SQL Server PDW-Ziel** aktivieren, damit Sie sehen die **Ziel-Editor für SQL Server PDW** erneut aus. Daraufhin sollte die Spaltennamen aus der Flatfile-Datei auf der linken Seite unter **nicht zugeordnete Eingabespalten**. Daraufhin sollte die Spaltennamen aus der Zieltabelle auf der rechten Seite unter **nicht zugeordnete Zielspalten**. Ordnen Sie die Spalten durch Ziehen oder Doppelklicken auf die zugehörigen Spaltennamen in der **nicht zugeordnete Eingabespalten** und **nicht zugeordnete Zielspalten** aufgeführt die **zugeordnete Spalten**Feld. Klicken Sie auf **OK** zum Speichern der Einstellungen.  
  
3.  Speichern Sie das Paket, indem Sie auf **speichern** in der **Datei** Menü.  
  
Führen Sie das Paket auf dem Integration Services-Computer.  
  
1.  In den Integrationsdiensten**Projektmappen-Explorer** (rechte Spalte), mit der rechten Maustaste `Package.dtsx` , und wählen Sie **Execute**.  
  
2.  Das Paket wird ausgeführt, und auf den Fortschritt sowie alle Fehler angezeigt werden die **Fortschritt** Bereich. Verwenden Sie einen SQL-Client, um die Last zu bestätigen, oder überwachen Sie die Last über die SQL Server PDW-Verwaltungskonsole.  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen Sie einen Skripttask, der den SSIS-PDW-Zieladapter verwendet.](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](http://msdn.microsoft.com/library/ms141026&#40;v=sql11&#40;.aspx)  
[Entwerfen und Implementieren von Paketen (Integration Services)](http://msdn.microsoft.com/library/ms141091&#40;v=sql11&#40;.aspx)  
[Lernprogramm: Erstellen eines einfachen Pakets mithilfe eines Assistenten](http://technet.microsoft.com/library/ms365330&#40;v=sql11&#40;.aspx)  
[Erste Schritte (Integration Services)](http://go.microsoft.com/fwlink/?LinkId=202412)  
[Dynamische Generierung (Paketbeispiel)](http://go.microsoft.com/fwlink/?LinkId=202413)  
[Entwerfen der SSIS-Pakete für Parallelität (SQL Server-Video)](http://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server-Community-Beispiele: Integrationsservices](http://go.microsoft.com/fwlink/?LinkId=202415)  
[Verbessern des inkrementellen Ladens mit Change Data Capture](http://msdn.microsoft.com/library/bb895315&#40;v=sql11&#40;.aspx)  
[Transformation für langsam veränderliche Dimensionen](http://msdn.microsoft.com/library/ms141715&#40;v=sql11&#40;.aspx)  
[Masseneinfügungstask](http://msdn.microsoft.com/library/ms141239&#40;v=sql11&#40;.aspx)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
