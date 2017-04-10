---
title: "Foreach-Schleifencontainer | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.foreachloopcontainer.f1"
  - "sql13.dts.designer.foreachloopcontainer.general.f1"
  - "sql13.dts.designer.foreachloopcontainer.collection.f1"
  - "sql13.dts.designer.foreachloopcontainer.mapping.f1"
  - "sql13.dts.designer.schemarestrictions.f1"
  - "sql13.dts.designer.foreachitemcolumns.f1"
  - "sql13.dts.designer.selectsmoenumeration.f1"
helpviewer_keywords: 
  - "Wiederholen der Ablaufsteuerung"
  - "Foreach-Schleifencontainer"
  - "Foreach-Enumeratoren [Integration Services]"
  - "Container [Integration Services], Foreach-Schleife"
ms.assetid: dd6cc2ba-631f-4adf-89dc-29ef449c6933
caps.latest.revision: 73
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 72
---
# Foreach-Schleifencontainer
  Der Foreach-Schleifencontainer definiert die Wiederholung einer Ablaufsteuerung in einem Paket. Die Schleifenimplementierung ist mit der **Foreach** -Schleifenstruktur in Programmiersprachen zu vergleichen. In einem Paket wird die Schleife mithilfe eines Foreach-Enumerators ermöglicht.  Der Foreach-Schleifencontainer wiederholt die Ablaufsteuerung für jedes Mitglied eines angegebenen Enumerators.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt die folgenden Enumeratortypen bereit:  
  
-   Foreach-ADO-Enumerator zum Aufzählen von Zeilen in Tabellen. Beispielsweise können Sie die Zeilen in einem ADO-Recordset abrufen.  
  
     Stattdessen speichert das Recordsetziel Daten im Speicher eines Recordsets, das in einer **Object** -Paketvariablen des Datentyps gespeichert ist. Sie verwenden typischerweise einen Foreach-Schleifencontainer mit dem Foreach-ADO-Enumerator zum Verarbeiten jeweils einer Zeile des Recordsets. Die für den Foreach-ADO-Enumerator angegebene Variable muss den Datentyp <ui>Object>/ui> haben. Weitere Informationen zum Recordsetziel finden Sie unter [Use a Recordset Destination](../../integration-services/data-flow/use-a-recordset-destination.md).  
  
-   Enumerator für Foreach-ADO.NET-Schemarowset zum Aufzählen der Schemainformationen zu einer Datenquelle. Beispielsweise können Sie die Tabellen in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank aufzählen und eine Liste dafür abrufen.  
  
-   Foreach-Dateienumerator zum Aufzählen von Dateien in einem Ordner. Der Enumerator kann Unterordner durchsuchen. Beispielsweise können Sie alle Dateien mit der Dateinamenerweiterung LOG im Windows-Ordner und deren Unterordner lesen.  
  
-   Foreach-Enumerator für Daten aus Variable zum Aufzählen des aufzählbaren Objekts, das eine angegebene Variable enthält. Das aufzählbare Objekt kann z. B. ein Array, ein ADO.NET **DataTable**-Objekt oder ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Enumerator sein. Beispielsweise können Sie die Werte eines Arrays aufzählen, das den Namen der Server enthält.  
  
-   Foreach Item-Enumerator zum Aufzählen von Elementen, bei denen es sich um Auflistungen handelt. Beispielsweise können Sie die Namen der ausführbaren Dateien und Arbeitsverzeichnisse aufzählen, die ein Task Prozess ausführen verwendet.  
  
-   Foreach-NodeList-Enumerator zum Aufzählen des Resultsets eines XPATH-Ausdrucks (XML Path Language). Beispielsweise kann dieser Ausdruck alle Autoren der Klassik aufzählen und eine Liste dafür abrufen: `/authors/author[@period='classical']`.  
  
-   Foreach-SMO-Enumerator zum Aufzählen von SMO-Objekten ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects). Beispielsweise können Sie die Sichten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank aufzählen und eine Liste dafür abrufen.  
  
-   Foreach-HDFS-File-Enumerator zum Aufzählen von HDFS-Dateien am angegebenen HDFS-Speicherort.  
  
-   Foreach-Azure-Blob-Enumerator zum Aufzählen von Blobs in einem Blobcontainer in Azure Storage.  
  
 Das folgende Diagramm zeigt einen Foreach-Schleifencontainer mit einem Task Dateisystem. Die Foreach-Schleife verwendet den Foreach-Dateienumerator, und der Task Dateisystem ist so konfiguriert, dass eine Datei kopiert wird. Falls der vom Enumerator angegebene Ordner vier Dateien enthält, wird die Schleife viermal wiederholt, und die vier Dateien werden kopiert.  
  
 ![Foreach-Schleifencontainer, der einen Ordner aufzählt](../../integration-services/control-flow/media/ssis-foreachloop.gif "Foreach-Schleifencontainer, der einen Ordner aufzählt")  
  
 Sie können eine Kombination aus Variablen und Eigenschaftsausdrücken verwenden, um für die Paketobjekteigenschaft den Enumeratorauflistungswert zu aktualisieren. Zunächst ordnen Sie den Auflistungswert einer benutzerdefinierten Variablen zu. Anschließend implementieren Sie einen Eigenschaftsausdruck für die Eigenschaft, die die Variable verwendet. Beispielsweise wird der Auflistungswert des Foreach-Dateienumerators der Variablen **MyFile** zugeordnet, und die Variable wird dann im Eigenschaftsausdruck für die „Subject“-Eigenschaft des Tasks „Mail senden“ verwendet. Beim Ausführen des Pakets wird die „Subject“-Eigenschaft bei jeder Wiederholung der Schleife mit dem Namen einer Datei aktualisiert. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Variablen, die dem Enumeratorauflistungswert zugeordnet sind, können ebenfalls in Ausdrücken und Skripts verwendet werden.  
  
 Ein Foreach-Schleifencontainer kann mehrere Tasks und Container einschließt, kann aber nur einen Enumeratortyp verwenden. Falls der Foreach-Schleifencontainer mehrere Tasks einschließt, können Sie den Enumeratorauflistungswert mehreren Eigenschaften jedes Tasks zuordnen.  
  
 Sie können ein Transaktionsattribut für den Foreach-Schleifencontainer festlegen, um eine Transaktion für eine Teilmenge der Paketablaufsteuerung zu definieren. Auf diese Weise können Sie Transaktionen statt auf der Paketebene auf der Ebene der Foreach-Schleife verwalten. Wenn z. B. ein Foreach-Schleifencontainer eine Ablaufsteuerung wiederholt, die Dimensions- und Faktentabellen in einem Sternschema aktualisiert, können Sie eine Transaktion konfigurieren, um sicherzustellen, dass entweder alle oder überhaupt keine Faktentabellen aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Transaktionen](../../integration-services/integration-services-transactions.md).  
  
## Enumeratortypen  
 Enumeratoren sind konfigurierbar, und je nach Enumerator müssen Sie unterschiedliche Informationen bereitstellen.  
  
 In der folgenden Tabelle sind die Informationen zusammengefasst, die für jeden Enumeratortyp erforderlich sind.  
  
|Enumerator|Konfigurationsanforderungen|  
|----------------|--------------------------------|  
|Foreach-ADO-Enumerator|Geben Sie die ADO-Objektquellvariable und den Enumeratormodus an. Die Variable muss den Datentyp <ui>Object>/ui> haben.|  
|Enumerator für Foreach-ADO.NET-Schemarowset|Geben Sie die Verbindung mit einer Datenbank und das aufzuzählende Schema an.|  
|Foreach-Dateienumerator|Geben Sie einen Ordner sowie die aufzuzählenden Dateien und das Format des Dateinamens der abgerufenen Dateien an. Geben Sie darüber hinaus an, ob Unterordner durchsucht werden sollen.|  
|Foreach-Enumerator für Daten aus Variable|Geben Sie die Variable an, die die aufzuzählenden Objekte enthält.|  
|Foreach Item-Enumerator|Definieren Sie die Elemente in der Foreach Item-Auflistung, einschließlich der Spalten und Spaltendatentypen.|  
|Foreach-NodeList-Enumerator|Geben Sie die Quelle des XML-Dokuments an, und konfigurieren Sie den XPath-Vorgang.|  
|Foreach-SMO-Enumerator|Geben Sie die Verbindung mit einer Datenbank und die aufzuzählenden SMO-Objekte an.|  
|Foreach-HDFS-Datei-Enumerator|Geben Sie einen Ordner sowie die aufzuzählenden Dateien und das Format des Dateinamens der abgerufenen Dateien an. Geben Sie darüber hinaus an, ob Unterordner durchsucht werden sollen.|  
|Foreach-Azure-Blob-Enumerator|Geben Sie den Azure-BLOB-Container mit den aufzuzählenden Blobs an.|  
  
## Eigenschaftsausdrücke in Foreach-Schleifencontainern  
 Pakete können so konfiguriert werden, dass mehrere ausführbare Dateien gleichzeitig ausgeführt werden. Diese Konfiguration sollte mit Vorsicht verwendet werden, wenn das Paket einen Foreach-Schleifencontainer enthält, der Eigenschaftsausdrücke implementiert.  
  
 Es ist häufig nützlich, einen Eigenschaftsausdruck zu implementieren, um den Wert der „ConnectionString“-Eigenschaft des Verbindungs-Managers festzulegen, den die „Foreach“-Schleifenenumeratoren verwenden. Der Eigenschaftsausdruck der „ConnectionString“-Eigenschaft wird durch eine Variable festgelegt, die dem Auflistungswert des Enumerators zugeordnet ist und bei jeder Iteration der Schleife aktualisiert wird.  
  
 Das Paket sollte so konfiguriert sein, dass jeweils nur eine ausführbare Datei ausgeführt wird, um in der Schleife negative Auswirkungen einer unbestimmten Zeitvorgabe der parallelen Taskausführung zu vermeiden. Wenn beispielsweise ein Paket mehrere Tasks gleichzeitig ausführen kann, können bei einem Foreach-Schleifencontainer, der im Ordner vorhandene Dateien aufzählt, die Dateinamen abruft und dann mithilfe eines Tasks "SQL ausführen" die Dateinamen in eine Tabelle einfügt, Schreibkonflikte auftreten, falls zwei Instanzen des Tasks "SQL ausführen" versuchen, zur selben Zeit zu schreiben. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## Verwandte Aufgaben  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um nähere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Konfigurieren eines Foreach-Schleifencontainers](../Topic/Configure%20a%20Foreach%20Loop%20Container.md)  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften anzuzeigen:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
## Verwandte Inhalte  
 Blogeintrag, [SSIS For Each Node List Enumerator](http://go.microsoft.com/fwlink/?LinkId=220671), auf bidn.com.  
  
## Siehe auch  
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)   
 [SQL Server Integration Services-Container](../../integration-services/control-flow/integration-services-containers.md)  
  
  