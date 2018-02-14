---
title: Foreach-Schleifencontainer | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.foreachloopcontainer.f1
- sql13.dts.designer.foreachloopcontainer.general.f1
- sql13.dts.designer.foreachloopcontainer.collection.f1
- sql13.dts.designer.foreachloopcontainer.mapping.f1
- sql13.dts.designer.schemarestrictions.f1
- sql13.dts.designer.foreachitemcolumns.f1
- sql13.dts.designer.selectsmoenumeration.f1
- sql14.dts.designer.foreachloopcontainer.f1
- sql14.dts.designer.foreachloopcontainer.general.f1
- sql14.dts.designer.foreachloopcontainer.collection.f1
- sql14.dts.designer.foreachloopcontainer.mapping.f1
- sql14.dts.designer.schemarestrictions.f1
- sql14.dts.designer.foreachitemcolumns.f1
- sql14.dts.designer.selectsmoenumeration.f1
helpviewer_keywords:
- repeating control flow
- Foreach Loop containers
- foreach enumerators [Integration Services]
- containers [Integration Services], Foreach Loop
ms.assetid: dd6cc2ba-631f-4adf-89dc-29ef449c6933
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 834bdc1febf1f066847b33f1490f076151357e98
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="foreach-loop-container"></a>Foreach-Schleifencontainer
  Der Foreach-Schleifencontainer definiert die Wiederholung einer Ablaufsteuerung in einem Paket. Die Schleifenimplementierung ist mit der **Foreach** -Schleifenstruktur in Programmiersprachen zu vergleichen. In einem Paket wird die Schleife mithilfe eines Foreach-Enumerators ermöglicht.  Der Foreach-Schleifencontainer wiederholt die Ablaufsteuerung für jedes Mitglied eines angegebenen Enumerators.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt die folgenden Enumeratortypen bereit:  
  
-   Foreach-ADO-Enumerator zum Aufzählen von Zeilen in Tabellen. Beispielsweise können Sie die Zeilen in einem ADO-Recordset abrufen.  
  
     Stattdessen speichert das Recordsetziel Daten im Speicher eines Recordsets, das in einer **Object** -Paketvariablen des Datentyps gespeichert ist. Sie verwenden typischerweise einen Foreach-Schleifencontainer mit dem Foreach-ADO-Enumerator zum Verarbeiten jeweils einer Zeile des Recordsets. Die für den Foreach-ADO-Enumerator angegebene Variable muss den Datentyp <ui>Object>/ui> haben. Weitere Informationen zum Recordsetziel finden Sie unter [Use a Recordset Destination (Verwenden eines Recordsetziels)](../../integration-services/data-flow/use-a-recordset-destination.md).  
  
-   Enumerator für Foreach-ADO.NET-Schemarowset zum Aufzählen der Schemainformationen zu einer Datenquelle. Beispielsweise können Sie die Tabellen in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank aufzählen und eine Liste dafür abrufen.  
  
-   Foreach-Dateienumerator zum Aufzählen von Dateien in einem Ordner. Der Enumerator kann Unterordner durchsuchen. Beispielsweise können Sie alle Dateien mit der Dateinamenerweiterung LOG im Windows-Ordner und deren Unterordner lesen.  
  
-   Foreach-Enumerator für Daten aus Variable zum Aufzählen des aufzählbaren Objekts, das eine angegebene Variable enthält. Das aufzählbare Objekt kann z. B. ein Array, ein ADO.NET **DataTable**-Objekt oder ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Enumerator sein. Beispielsweise können Sie die Werte eines Arrays aufzählen, das den Namen der Server enthält.  
  
-   Foreach Item-Enumerator zum Aufzählen von Elementen, bei denen es sich um Auflistungen handelt. Beispielsweise können Sie die Namen der ausführbaren Dateien und Arbeitsverzeichnisse aufzählen, die ein Task Prozess ausführen verwendet.  
  
-   Foreach-NodeList-Enumerator zum Aufzählen des Resultsets eines XPATH-Ausdrucks (XML Path Language). Beispielsweise kann dieser Ausdruck alle Autoren der Klassik aufzählen und eine Liste dafür abrufen: `/authors/author[@period='classical']`.  
  
-   Foreach-SMO-Enumerator zum Aufzählen von SMO-Objekten ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects). Beispielsweise können Sie die Sichten in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank aufzählen und eine Liste dafür abrufen.  
  
-   Foreach-HDFS-File-Enumerator zum Aufzählen von HDFS-Dateien am angegebenen HDFS-Speicherort.  
  
-   Foreach-Azure-Blob-Enumerator zum Aufzählen von Blobs in einem Blobcontainer in Azure Storage.  

-   Foreach-ADLS-Datei-Enumerator zum Aufzählen von Dateien in einem Verzeichnis in Azure Data Lake Store.
  
 Das folgende Diagramm zeigt einen Foreach-Schleifencontainer mit einem Task Dateisystem. Die Foreach-Schleife verwendet den Foreach-Dateienumerator, und der Task Dateisystem ist so konfiguriert, dass eine Datei kopiert wird. Falls der vom Enumerator angegebene Ordner vier Dateien enthält, wird die Schleife viermal wiederholt, und die vier Dateien werden kopiert.  
  
 ![Ein Foreach-Schleifencontainer der einen Ordner aufzählt](../../integration-services/control-flow/media/ssis-foreachloop.gif "A Foreach Loop container that enumerates a folder")  
  
 Sie können eine Kombination aus Variablen und Eigenschaftsausdrücken verwenden, um für die Paketobjekteigenschaft den Enumeratorauflistungswert zu aktualisieren. Zunächst ordnen Sie den Auflistungswert einer benutzerdefinierten Variablen zu. Anschließend implementieren Sie einen Eigenschaftsausdruck für die Eigenschaft, die die Variable verwendet. Beispielsweise wird der Auflistungswert des Foreach-Dateienumerators der Variablen **MyFile** zugeordnet, und die Variable wird dann im Eigenschaftsausdruck für die „Subject“-Eigenschaft des Tasks „Mail senden“ verwendet. Beim Ausführen des Pakets wird die „Subject“-Eigenschaft bei jeder Wiederholung der Schleife mit dem Namen einer Datei aktualisiert. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Variablen, die dem Enumeratorauflistungswert zugeordnet sind, können ebenfalls in Ausdrücken und Skripts verwendet werden.  
  
 Ein Foreach-Schleifencontainer kann mehrere Tasks und Container einschließt, kann aber nur einen Enumeratortyp verwenden. Falls der Foreach-Schleifencontainer mehrere Tasks einschließt, können Sie den Enumeratorauflistungswert mehreren Eigenschaften jedes Tasks zuordnen.  
  
 Sie können ein Transaktionsattribut für den Foreach-Schleifencontainer festlegen, um eine Transaktion für eine Teilmenge der Paketablaufsteuerung zu definieren. Auf diese Weise können Sie Transaktionen statt auf der Paketebene auf der Ebene der Foreach-Schleife verwalten. Wenn z. B. ein Foreach-Schleifencontainer eine Ablaufsteuerung wiederholt, die Dimensions- und Faktentabellen in einem Sternschema aktualisiert, können Sie eine Transaktion konfigurieren, um sicherzustellen, dass entweder alle oder überhaupt keine Faktentabellen aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Transaktionen](../../integration-services/integration-services-transactions.md).  
  
## <a name="enumerator-types"></a>Enumeratortypen  
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
|Foreach-ADLS-Datei|Geben Sie das Azure Data Lake Store-Verzeichnis an, das die aufzuzählenden Dateien enthält.|

## <a name="add-enumeration-to-a-control-flow-with-a-foreach-loop-container"></a>Hinzufügen einer Enumeration zu einer Ablaufsteuerung mit einem Foreach-Schleifencontainer
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] schließt den Foreach-Schleifencontainer ein. Dabei handelt es sich um ein Ablaufsteuerungselement, mit dem Sie auf einfache Weise eine Schleifenkonstruktion einschließen können, mit der Dateien und Objekte in der Ablaufsteuerung eines Pakets aufgezählt werden. Weitere Informationen finden Sie unter [Foreach Loop Container](../../integration-services/control-flow/foreach-loop-container.md).  
  
 Der Foreach-Schleifencontainer stellt keine Funktionalität bereit. Er stellt lediglich die Struktur bereit, in der Sie die wiederholbare Ablaufsteuerung erstellen, einen Enumeratortyp angeben und den Enumerator konfigurieren. Sie müssen mindestens einen Task in den Foreach-Schleifencontainer einschließen, um Containerfunktionalität bereitzustellen. Weitere Informationen finden Sie unter [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md).  
  
 Der Foreach-Schleifencontainer kann eine Ablaufsteuerung mit mehreren Tasks und anderen Containern einschließen. Das Hinzufügen von Tasks und Containern zu einem Foreach-Schleifencontainer ist mit dem Hinzufügen von Tasks und Containern zu einem Paket vergleichbar, außer dass Sie die Tasks und Container nicht in das Paket, sondern in den Foreach-Schleifencontainer ziehen. Falls der Foreach-Schleifencontainer mehrere Tasks oder Container einschließt, können Sie diese wie bei einem Paket mithilfe von Rangfolgeneinschränkungen verbinden. Weitere Informationen finden Sie unter [Rangfolgeneinschränkungen](../../integration-services/control-flow/precedence-constraints.md).  
  
### <a name="add-and-configure-a-foreach-loop-container"></a>Hinzufügen und Konfigurieren eines Foreach-Schleifencontainers
  
1.  Fügen Sie dem Paket den Foreach-Schleifencontainer hinzu. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen eines Tasks oder Containers in einer Ablaufsteuerung](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
2.  Fügen Sie dem Foreach-Schleifencontainer Tasks und Container hinzu. Weitere Informationen finden Sie unter [Hinzufügen oder Löschen eines Tasks oder Containers in einer Ablaufsteuerung](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
3.  Verbinden Sie Tasks und Container im Foreach-Schleifencontainer mithilfe von Rangfolgeneinschränkungen. Weitere Informationen finden Sie unter [Verbinden von Tasks und Containern mithilfe einer Standardrangfolgeneinschränkung](http://msdn.microsoft.com/library/8f31f15f-98ff-4c35-b41f-8b8cfd148d75).  
  
4.  Konfigurieren Sie den Foreach-Schleifencontainer. Weitere Informationen finden Sie unter [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  

## <a name="configure-a-foreach-loop-container"></a>Konfigurieren eines Foreach-Schleifencontainers
In diesem Verfahren wird das Konfigurieren eines Foreach-Schleifencontainers beschrieben, einschließlich der Eigenschaftsausdrücke auf Enumerator- und Containerebene.  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Klicken Sie auf die Registerkarte **Ablaufsteuerung** , und doppelklicken Sie auf die Foreach-Schleife.  
  
3.  Klicken Sie im Dialogfeld **Foreach-Schleifen-Editor** auf **Allgemein** , und ändern Sie optional den Namen und die Beschreibung der Foreach-Schleife.  
  
4.  Klicken Sie auf **Auflistung** , und wählen Sie aus der Liste **Enumerator** einen Enumeratortyp aus.  
  
5.  Geben Sie einen Enumerator an, und legen Sie wie folgt Enumeratoroptionen fest:  
  
    -   Wenn Sie den Foreach-Datei-Enumerator verwenden möchten, stellen Sie den Ordner bereit, der die aufzuzählenden Dateien enthält. Geben Sie einen Filter für den Dateinamen und den Typ an, und geben Sie an, ob der vollqualifizierte Dateiname zurückgegeben werden soll. Zeigen Sie außerdem an, ob Unterordner nach weiteren Dateien durchsucht werden sollen.  
  
    -   Wenn Sie den Foreach Item-Enumerator verwenden möchten, klicken Sie auf **Spalten**, und klicken Sie im Dialogfeld **For Each Item-Spalten** auf **Hinzufügen** , um Spalten hinzuzufügen. Wählen Sie aus der Liste **Datentyp** einen Datentyp für jede Spalte aus, und klicken Sie auf **OK**.  
  
         Geben Sie Werte in die Spalten ein, oder wählen Sie in Listen Werte aus.  
  
        > [!NOTE]  
        >  Klicken Sie an einer beliebigen Stelle außerhalb der Zelle, in die Sie Werte eingegeben haben, um eine neue Zeile hinzuzufügen.  
  
        > [!NOTE]  
        >  Falls ein Wert nicht mit dem Spaltendatentyp kompatibel ist, wird der Text hervorgehoben dargestellt.  
  
    -   Wenn Sie den Foreach-ADO-Enumerator verwenden möchten, wählen Sie eine vorhandene Variable aus, oder klicken Sie in der Liste **ADO-Objektquellvariable** auf **Neue Variable** , um die Variable anzugeben, die den Namen des aufzuzählenden ADO-Objekts enthält, und wählen Sie eine Option für den Enumerationsmodus aus.  
  
         Wenn Sie eine neue Variable erstellen, legen Sie die Variableneigenschaften im Dialogfeld **Variable hinzufügen** fest.  
  
    -   Wenn Sie den Enumerator für Foreach-ADO.NET-Schemarowset verwenden möchten, wählen Sie eine vorhandene ADO.NET-Verbindung aus, oder klicken Sie in der Liste **Verbindung** auf **Neue Verbindung** , und wählen Sie ein Schema aus.  
  
         Klicken Sie optional auf **Einschränkungen festlegen** , und wählen Sie Schemaeinschränkungen aus, wählen Sie die Variable aus, die den Einschränkungswert enthält, oder geben Sie den Einschränkungswert ein, und klicken Sie auf **OK**.  
  
    -   Wenn Sie einen Foreach-Enumerator für Daten aus Variable verwenden möchten, wählen Sie aus der Liste **Variable** eine Variable aus.  
  
    -   Um den Foreach-NodeList-Enumerator zu verwenden, klicken Sie auf DocumentSourceType und wählen den Quelltyp aus der Liste aus. Anschließend klicken Sie auf DocumentSource. Je nach dem für DocumentSourceType ausgewählten Wert wählen Sie eine Variable bzw. eine Dateiverbindung aus der Liste aus, erstellen Sie eine neue Variable bzw. Dateiverbindung, oder geben Sie die XML-Quelle in den **Dokumentquellen-Editor**ein.  
  
         Klicken Sie anschließend auf „EnumerationType“, und wählen Sie einen Enumerationstyp aus der Liste aus. Wenn EnumerationType den Wert **Navigator, Node oder NodeText**hat, klicken Sie auf OuterXPathStringSourceType, wählen Sie den Quelltyp aus, und klicken Sie dann auf OuterXPathString. Je nach dem für OuterXPathStringSourceType festgelegten Wert wählen Sie eine Variable bzw. eine Dateiverbindung aus der Liste aus, erstellen Sie eine neue Variable bzw. Dateiverbindung, oder geben Sie die Zeichenfolge für den äußeren XPath-Ausdruck (XML Path Language) ein.  
  
         Wenn EnumerationType den Wert **ElementCollection** hat, legen Sie OuterXPathStringSourceType und OuterXPathString wie oben beschrieben fest. Klicken Sie anschließend auf InnerElementType, und wählen Sie einen Enumerationstyp für die inneren Elemente aus. Klicken Sie dann auf InnerXPathStringSourceType. Je nachdem, welchen Wert Sie für InnerXPathStringSourceType festgelegt haben, wählen Sie eine Variable bzw. eine Dateiverbindung aus, erstellen Sie eine neue Variable bzw. Dateiverbindung, oder geben Sie die Zeichenfolge für den inneren XPath-Ausdruck ein.  
  
    -   Wenn Sie den Foreach-SMO-Enumerator verwenden möchten, wählen Sie eine vorhandene ADO.NET-Verbindung aus, oder klicken Sie in der Liste **Verbindung** auf **Neue Verbindung** , und geben Sie die zu verwendende Zeichenfolge ein, oder klicken Sie auf **Durchsuchen**. **Dadurch** haben Sie im Dialogfeld **SMO-Enumeration auswählen** die Möglichkeit, den aufzuzählenden Objekttyp und den Enumerationstyp auszuwählen. Klicken Sie dann auf **OK**.  
  
6.  Klicken Sie optional im Textfeld **Ausdrücke** auf der Seite **Sammlung** auf die Schaltfläche mit den drei Punkten **(…)** , um Ausdrücke zu erstellen, mit denen Eigenschaftswerte aktualisiert werden. Weitere Informationen finden Sie unter [Hinzufügen oder Ändern eines Eigenschaftsausdrucks](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
    > [!NOTE]  
    >  Die in der Liste **Eigenschaft** aufgeführten Eigenschaften hängen vom Enumerator ab.  
  
7.  Klicken Sie optional auf **Variablenzuordnungen**, um Objekteigenschaften dem Auflistungswert zuzuordnen, und führen Sie dann folgende Aktionen aus:  
  
    1.  Wählen Sie in der Liste **Variablen** eine Variable aus, oder klicken Sie auf **\<Neue Variable>**, um eine neue Variable zu erstellen.  
  
    2.  Wenn Sie eine neue Variable hinzufügen, legen Sie die Variableneigenschaften im Dialogfeld **Variable hinzufügen** fest, und klicken Sie auf **OK**.  
  
    3.  Wenn Sie den Foreach Item-Enumerator verwenden, können Sie den Indexwert in der Liste **Index** aktualisieren.  
  
        > [!NOTE]  
        >  Der Indexwert zeigt an, welche Spalte im Element der Variablen zugeordnet werden soll. Nur der Foreach Item-Enumerator kann einen anderen Indexwert als 0 verwenden.  
  
8.  Klicken Sie optional auf **Ausdrücke** , und erstellen Sie auf der Seite **Ausdrücke** Eigenschaftsausdrücke für die Eigenschaften des Foreach-Schleifencontainers. Weitere Informationen finden Sie unter [Hinzufügen oder Ändern eines Eigenschaftsausdrucks](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
9. Klicken Sie auf **OK**.  

## <a name="general-page---foreach-loop-editor"></a>Foreach-Schleifen-Editor: Seite „Allgemein“
Auf der Seite **Allgemein** des Dialogfelds **Foreach-Schleifen-Editor** können Sie Namen und Beschreibung für einen Foreach-Schleifencontainer angeben, der mithilfe eines festgelegten Enumerators den gleichen Workflow für alle Elemente einer Auflistung wiederholt.  
  
 Weitere Informationen für Foreach-Schleifencontainer und wie diese zu konfigurieren sind, finden Sie unter [Foreach-Schleifencontainer](../../integration-services/control-flow/foreach-loop-container.md) und [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
### <a name="options"></a>Tastatur  
 **Name**  
 Geben Sie einen eindeutigen Namen für den Foreach-Schleifencontainer an. Dieser Name wird als Bezeichnung des Tasksymbols und in Protokollen verwendet.  
  
> [!NOTE]  
>  Objektnamen müssen innerhalb eines Pakets eindeutig sein.  
  
 **Beschreibung**  
 Geben Sie eine Beschreibung des Foreach-Schleifencontainers an.  

## <a name="collection-page---foreach-loop-editor"></a>Foreach-Schleifen-Editor: Seite „Collection“
 Mithilfe der Seite **Collection** (Sammlung) des Dialogfelds **Foreach-Schleifen-Editor** können Sie den Enumeratortyp angeben und den Enumerator konfigurieren.  
  
 Weitere Informationen für Foreach-Schleifencontainer und wie diese zu konfigurieren sind, finden Sie unter [Foreach-Schleifencontainer](../../integration-services/control-flow/foreach-loop-container.md) und [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
### <a name="static-options"></a>Statische Optionen  
 **Enumerator**  
 Wählen Sie den Enumeratortyp aus der Liste aus. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|value|Description|  
|-----------|-----------------|  
|**Foreach-Datei-Enumerator**|Zählt Dateien auf. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-Dateienumerator**die dynamischen Optionen angezeigt.|  
|**Foreach-Element-Enumerator**|Zählt Werte in einem Element auf. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-Elementenumerator**die dynamischen Optionen angezeigt.|  
|**Foreach-ADO-Enumerator**|Zählt Tabellen oder Zeilen in Tabellen auf. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-ADO-Enumerator**die dynamischen Optionen angezeigt.|  
|**Enumerator für Foreach-ADO.NET-Schemarowset**|Zählt ein Schema auf. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-ADO-Enumerator**die dynamischen Optionen angezeigt.|  
|**Foreach-Enumerator für Daten aus Variable**|Zählt den Wert in einer Variable auf. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-Enumerator für Daten aus Variable**die dynamischen Optionen angezeigt.|  
|**Foreach-NodeList-Enumerator**|Zählt Knoten in einem XML-Dokument auf. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-NodeList-Enumerator**die dynamischen Optionen angezeigt.|  
|**Foreach-SMO-Enumerator**|Zählt ein SMO-Objekt auf. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-SMO-Enumerator**die dynamischen Optionen angezeigt.|  
|**Foreach-HDFS-Datei-Enumerator**|Aufzählen von HDFS-Dateien am angegebenen HDFS-Speicherort. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-HDFS-Datei-Enumerator**die dynamischen Optionen angezeigt.|  
|**Foreach-Azure-Blob-Enumerator**|Auflisten von Blob-Dateien am angegebenen Blob-Speicherort. Wenn Sie diesen Wert auswählen, werden die dynamischen Optionen im Abschnitt **Foreach-Azure-Blob-Enumerator**angezeigt.|  
|**Foreach-ADLS-Datei-Enumerator**|Aufzählen von Dateien im angegebenen Data Lake Store-Verzeichnis. Wenn Sie diesen Wert auswählen, werden im Abschnitt **Foreach-ADLS-Datei-Enumerator** die dynamischen Optionen angezeigt.|
  
 **Ausdrücke**  
 Klicken Sie auf die Option **Ausdrücke** , oder erweitern Sie diese, um die Liste der vorhandenen Eigenschaftsausdrücke anzuzeigen. Klicken Sie auf die Schaltfläche mit den Auslassungspunkten**(…)**, um einer Enumeratoreigenschaft einen Eigenschaftsausdruck hinzuzufügen, oder um einen vorhandenen Eigenschaftsausdruck zu bearbeiten und auszuwerten.  
  
 **Verwandte Themen:** [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Eigenschaftsausdrucks-Editor](../../integration-services/expressions/property-expressions-editor.md), [Ausdrucks-Generator](../../integration-services/expressions/expression-builder.md)  
  
### <a name="enumerator-dynamic-options"></a>Enumerator (dynamische Optionen)  
  
#### <a name="enumerator--foreach-file-enumerator"></a>Enumerator = Foreach-Dateienumerator  
 Mithilfe des Foreach-Dateienumerators können Dateien in einem Ordner aufgezählt werden. Wenn die Foreach-Schleife z. B. einen Task SQL ausführen enthält, können Sie mithilfe des Foreach-Dateienumerators Dateien aufzählen, die vom Task SQL ausführen ausgeführte SQL-Anweisungen enthalten. Der Enumerator kann so konfiguriert werden, dass Unterordner in der Aufzählung berücksichtigt werden.  
  
 Der Inhalt der Ordner und Unterordner, die der Foreach-Dateienumerator aufzählt, ändert sich möglicherweise beim Durchlaufen der Schleife, da externe Prozesse oder Tasks in der Schleife beim Durchlaufen der Schleife Dateien hinzufügen, umbenennen oder löschen. Diese Änderungen können zu unerwarteten Ergebnissen führen:  
  
-   Wenn Dateien gelöscht werden, beeinflussen die Aktionen einer Aufgabe in der Foreach-Schleife möglicherweise einen anderen Dateisatz als den, der von nachfolgenden Aufgaben genutzt wird.  
  
-   Wenn Dateien umbenannt werden, und ein externer Prozess automatisch Dateien hinzufügt, um die umbenannten Dateien zu ersetzen, kann die Foreach-Schleife zweimal die selben Dateien beeinflussen.  
  
-   Wenn Dateien hinzugefügt werden, können die von der Foreach-Schleife beeinflussten Dateien schwer erkennbar sein.  
  
 **Ordner**  
 Gibt den Pfad für den Stammordner für die Aufzählung an.  
  
 **Durchsuchen**  
 Mit dieser Option können Sie den Stammordner suchen.  
  
 **Dateien**  
 Geben Sie die aufzuzählenden Dateien an.  
  
> [!NOTE]  
>  Sie können Platzhalterzeichen (*) verwenden, um die in der Sammlung zu berücksichtigenden Dateien anzugeben. Um Dateien einzubeziehen, deren Name „abc“ enthält, verwenden Sie beispielsweise den folgenden Filter: \*abc\*.  
>   
>  Wenn Sie eine Dateierweiterung angeben, gibt der Enumerator auch Dateien mit derselben Erweiterung mit angehängten zusätzlichen Zeichen zurück. (Dieses Verhalten entspricht dem Verhalten des **dir**-Befehls im Betriebssystem, mit dem 8.3-Dateinamen auf Abwärtskompatibilität überprüft werden.) Dieses Verhalten des Enumerators könnte unerwartete Ergebnisse verursachen. Angenommen, Sie möchten nur Excel 2003-Dateien auflisten und geben "*.xls" an. Der Enumerator gibt in diesem Fall auch Excel 2007-Dateien zurück, da sie die Erweiterung „.xlsx“ haben.  
>   
>  Sie können einen Ausdruck verwenden, um die in eine Sammlung einzubeziehenden Dateien anzugeben. Erweitern Sie dazu **Ausdrücke** auf der Seite **Sammlung** , wählen Sie die **FileSpec** -Eigenschaft aus, und klicken Sie dann auf die Schaltfläche mit den Auslassungspunkten (…), um den Eigenschaftsausdruck hinzuzufügen.  
  
 **Vollqualifiziert**  
 Wählen Sie diese Option aus, um den vollqualifizierten Pfad von Dateinamen abzurufen. Wenn in der Dateioption Platzhalterzeichen angegeben wurden, stimmen die zurückgegebenen vollqualifizierten Pfade mit dem Filter überein.  
  
 **Nur Name**  
 Wählen Sie diese Option aus, um nur die Dateinamen abzurufen. Wenn in der Dateioption Platzhalterzeichen angegeben wurden, stimmen die zurückgegebenen Dateinamen mit dem Filter überein.  
  
 **Name und Erweiterung**  
 Wählen Sie diese Option aus, um die Dateinamen und die Dateinamenerweiterungen abzurufen. Wenn in der Dateioption Platzhalterzeichen angegeben wurden, stimmen die zurückgegebenen Dateinamen und Dateierweiterungen mit dem Filter überein.  
  
 **Unterordner durchsuchen**  
 Wählen Sie diese Option aus, wenn die Unterordner in der Aufzählung berücksichtigt werden sollen.  
  
#### <a name="enumerator--foreach-item-enumerator"></a>Enumerator = Foreach-Elementenumerator  
 Mithilfe des Foreach Item-Numerators können Elemente in einer Auflistung aufgezählt werden. Sie definieren die Elemente in der Auflistung, indem Sie Spalten und Spaltenwerte angeben. Ein Element wird durch die Spalten in einer Zeile definiert. Ein Element, das die von einem Task Prozess ausführen ausgeführten ausführbaren Dateien sowie das vom Task verwendete Arbeitsverzeichnis angibt, verfügt über zwei Spalten. Eine Spalte listet die Namen der ausführbaren Dateien auf und eine andere das Arbeitsverzeichnis. Die Anzahl von Zeilen bestimmt, wie oft die Schleife wiederholt wird. Wenn die Tabelle 10 Zeilen aufweist, wird die Schleife 10-mal wiederholt.  
  
 Um die Eigenschaften des Task Prozess ausführen zu aktualisieren, ordnen Sie Elementspalten mithilfe des Spaltenindex Variablen zu. Die erste im Enumeratorelement definierte Spalte verfügt über den Indexwert 0, die zweite über den Wert 1 usw. Die Variablenwerte werden bei jeder Wiederholung der Schleife aktualisiert. Die Eigenschaften **Executable** und **WorkingDirectory** des Tasks Prozess ausführen können dann mithilfe von Eigenschaftsausdrücken, die diese Variablen verwenden, aktualisiert werden.  
  
 **Definieren Sie die Elemente für die ForEach-Elementauflistung**  
 Geben Sie einen Wert für jede Spalte in der Tabelle an.  
  
> [!NOTE]  
>  Nachdem Sie die Werte in Zeilenspalten eingegeben haben, wird der Tabelle automatisch eine neue Zeile hinzugefügt.  
  
> [!NOTE]  
>  Wenn die angegebenen Werte nicht mit dem Spaltendatentyp kompatibel sind, wird der Text rot angezeigt.  
  
 **Datentyp der Spalte**  
 Führt den Datentyp der aktiven Spalte auf.  
  
 **Entfernen**  
 Wählen Sie ein Element aus, und klicken Sie anschließend auf **Entfernen** , um es aus der Liste zu entfernen.  
  
 **Spalten**  
 Klicken Sie auf diese Option, um den Datentyp der Spalten im Element zu konfigurieren.  
  
 **Verwandte Themen:** [ForEach-Elementspalten (Dialogfeld, Referenz zur Benutzeroberfläche)](http://msdn.microsoft.com/library/ea76aae0-8798-4677-8ab8-4a579de4957c)  
  
#### <a name="enumerator--foreach-ado-enumerator"></a>Enumerator = Foreach-ADO-Enumerator  
 Mithilfe des Foreach-ADO-Enumerators werden Zeilen oder Tabellen in einem in einer Variablen gespeicherten ADO- oder ADO.NET-Objekt aufgezählt. Wenn die Foreach-Schleife z. B. einen Skripttask enthält, mit dem ein Dataset in eine Variable geschrieben wird, können Sie mithilfe des Foreach-ADO-Enumerators die Zeilen im Dataset aufzählen. Wenn die Variable ein ADO.NET-Dataset enthält, kann der Enumerator zum Aufzählen von Zeilen in mehreren Tabellen oder zum Aufzählen von Tabellen konfiguriert werden.  
  
 **ADO-Objektquellvariable**  
 Wählen Sie eine benutzerdefinierte Variable aus der Liste aus, oder klicken Sie auf \<**Neue Variable...**>, um eine neue Variable zu erstellen.  
  
> [!NOTE]  
>  Die Variable muss den Datentyp Objekt besitzen, andernfalls tritt ein Fehler auf.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **Zeilen in der ersten Tabelle**  
 Wählen Sie diese Option aus, um nur Zeilen in der ersten Tabelle aufzuzählen.  
  
 **Zeilen in allen Tabellen (nur ADO.NET-Dataset)**  
 Wählen Sie diese Option aus, um Zeilen in allen Tabellen aufzuzählen. Diese Option ist nur verfügbar, wenn die aufzuzählenden Objekte alle Mitglieder desselben ADO.NET-Datasets sind.  
  
 **Alle Tabellen (nur ADO.NET-Dataset)**  
 Wählen Sie diese Option aus, um nur Tabellen aufzuzählen.  
  
#### <a name="enumerator--foreach-adonet-schema-rowset-enumerator"></a>Enumerator = Enumerator für Foreach-ADO.NET-Schemarowset  
 Mithilfe des Enumerators für Foreach ADO.NET-Schemarowset kann ein Schema für eine angegebene Datenquelle aufgezählt werden. Wenn die Foreach-Schleife z. B. einen Task SQL ausführen enthält, können Sie mit dem Enumerator für Foreach ADO.NET-Schemarowset Schemas aufzählen (beispielsweise die Spalten in der **AdventureWorks** -Datenbank) und mit dem Task SQL ausführen Schemaberechtigungen abrufen.  
  
 **Verbindung**  
 Wählen Sie einen ADO.NET-Verbindungs-Manager aus der Liste aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen ADO.NET-Verbindungs-Manager zu erstellen.  
  
> [!IMPORTANT]  
>  Der ADO.NET-Verbindungs-Manager muss einen .NET-Anbieter für OLE DB verwenden. Wenn Sie eine Verbindung mit SQL Server herstellen, ist der empfohlene Anbieter der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, der im Dialogfeld **Verbindungs-Manager** im Abschnitt **.Net-Anbieter für OleDb** aufgeführt ist.  
  
 **Verwandte Themen:** [ADO Connection Manager](../../integration-services/connection-manager/ado-connection-manager.md), [Configure ADO.NET Connection Manager](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 **Schema**  
 Wählen Sie das aufzuzählende Schema aus.  
  
 **Einschränkungen festlegen**  
 Legen Sie die Einschränkungen fest, die auf das angegebene Schema angewendet werden sollen.  
  
 **Verwandte Themen:** [Schemaeinschränkungen (Dialogfeld)](http://msdn.microsoft.com/library/92e5fd32-4944-4f7c-a448-b458df93d0d5)  
  
#### <a name="enumerator--foreach-from-variable-enumerator"></a>Enumerator = Foreach-Enumerator für Daten aus Variable  
 Mithilfe des Foreach-Enumerators für Daten aus Variable werden aufzählbare Objekte in einer angegebenen Variable aufgezählt. Wenn die Foreach-Schleife z. B. einen Task SQL ausführen enthält, der eine Abfrage ausführt und das Ergebnis in einer Variable speichert, können Sie den Foreach-Enumerator für Daten aus Variable zum Aufzählen der Abfrageergebnisse verwenden.  
  
 **Variable**  
 Wählen Sie in der Liste eine Variable aus, oder klicken Sie auf \<**Neue Variable…**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="enumerator--foreach-nodelist-enumerator"></a>Enumerator = Foreach-NodeList-Enumerator  
 Mithilfe des Foreach-Nodelist-Enumerators wird der XML-Knotensatz, der das Ergebnis der Anwendung eines XPath-Ausdrucks auf eine XML-Datei ist, aufgezählt. Wenn die Foreach-Schleife einen Skripttask enthält, können Sie mit dem Foreach-NodeList-Enumerator einen Wert, der den Kriterien des XPath-Ausdrucks entspricht, von der XML-Datei an den Skripttask übergeben.  
  
 Der XPath-Ausdruck, der auf die XML-Datei angewendet wird, ist der in der OuterXPathString-Eigenschaft gespeicherte äußere XPath-Vorgang. Wenn der XPath-Enumerationstyp auf **ElementCollection**festgelegt ist, kann der Foreach-NodeList-Enumerator einen in der InnerXPathString-Eigenschaft gespeicherten inneren XPath-Ausdruck auf eine Sammlung von Elementen anwenden.  
  
 Weitere Informationen zum Arbeiten mit XML-Dokumenten und Daten finden Sie unter "[XML im .NET Framework](http://go.microsoft.com/fwlink/?LinkId=56214)" in der MSDN Library.  
  
 **DocumentSourceType**  
 Wählen Sie den Quelltyp des XML-Dokuments aus. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|value|Description|  
|-----------|-----------------|  
|**Direct input**|Legen Sie als Quelle ein XML-Dokument fest.|  
|**File connection**|Wählen Sie eine Datei aus, die das XML-Dokument enthält.|  
|**Variable**|Legen Sie als Quelle eine Variable fest, die das XML-Dokument enthält.|  
  
 **DocumentSource**  
 Wenn für **DocumentSourceType** die Option **Direkteingabe** festgelegt ist, geben Sie den XML-Code an, oder klicken Sie auf die Schaltfläche mit den Auslassungspunkten (…), um mithilfe des Dialogfelds **Dokumentquellen-Editor** XML bereitzustellen.  
  
 Wenn **DocumentSourceType** auf **Dateiverbindung** festgelegt ist, wählen Sie einen Dateiverbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Wenn **DocumentSourceType** auf **Variable** festgelegt ist, wählen Sie eine vorhandene Variable aus, oder klicken Sie auf \<**Neue Variable...**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **EnumerationType**  
 Wählen Sie einen Enumerationstyp aus der Liste aus. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|value|Description|  
|-----------|-----------------|  
|**Navigator**|Die Aufzählung erfolgt mithilfe eines XPathNavigators.|  
|**Node**|Zählt Knoten auf, die durch einen XPath-Vorgang zurückgegeben wurden.|  
|**NodeText**|Zählt Textknoten auf, die durch einen XPath-Vorgang zurückgegeben wurden.|  
|**ElementCollection**|Zählt Elementknoten auf, die durch einen XPath-Vorgang zurückgegeben wurden.|  
  
 **OuterXPathStringSourceType**  
 Wählen Sie den Quelltyp der XPath-Zeichenfolge aus. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar: 
  
|value|Description|  
|-----------|-----------------|  
|**Direct input**|Legen Sie als Quelle ein XML-Dokument fest.|  
|**File connection**|Wählen Sie eine Datei aus, die das XML-Dokument enthält.|  
|**Variable**|Legen Sie als Quelle eine Variable fest, die das XML-Dokument enthält.|  
  
 **OuterXPathString**  
 Wenn **OuterXPathStringSourceType** auf **Direkteingabe** festgelegt ist, geben Sie die XPath-Zeichenfolge an.  
  
 Wenn **OuterXPathStringSourceType** auf **Dateiverbindung** festgelegt ist, wählen Sie einen Dateiverbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Wenn **OuterXPathStringSourceType** auf **Variable** festgelegt ist, wählen Sie eine vorhandene Variable aus, oder klicken Sie auf \<**Neue Variable...**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
 **InnerElementType**  
 Wenn **EnumerationType** auf **ElementCollection**festgelegt ist, wählen Sie den Typ des inneren Elements in der Liste aus.  
  
 **InnerXPathStringSourceType**  
 Wählen Sie den Quelltyp der inneren XPath-Zeichenfolge aus. Für diese Eigenschaft sind die in der folgenden Tabelle aufgeführten Optionen verfügbar:  
  
|value|Description|  
|-----------|-----------------|  
|**Direct input**|Legen Sie als Quelle ein XML-Dokument fest.|  
|**File connection**|Wählen Sie eine Datei aus, die das XML-Dokument enthält.|  
|**Variable**|Legen Sie als Quelle eine Variable fest, die das XML-Dokument enthält.|  
  
 **InnerXPathString**  
 Wenn **InnerXPathStringSourceType** auf **Direkteingabe** festgelegt ist, geben Sie die XPath-Zeichenfolge an.  
  
 Wenn **InnerXPathStringSourceType** auf **Dateiverbindung** festgelegt ist, wählen Sie einen Dateiverbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung...**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Verwandte Themen:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
 Wenn **InnerXPathStringSourceType** auf **Variable** festgelegt ist, wählen Sie eine vorhandene Variable aus, oder klicken Sie auf \<**Neue Variable...**>, um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
#### <a name="enumerator--foreach-smo-enumerator"></a>Enumerator = Foreach-SMO-Enumerator  
 Mithilfe des Foreach-SMO-Enumerators werden SQL Server Management Object (SMO)-Objekte aufgezählt. Wenn die Foreach-Schleife z.B. einen Task „SQL ausführen“ enthält, können Sie den Foreach-SMO-Enumerator zum Aufzählen der Tabellen in der **AdventureWorks**-Datenbank und Ausführen von Abfragen, mit denen die Anzahl von Zeilen pro Tabelle ermittelt wird, verwenden.  
  
 **Verbindung**  
 Wählen Sie einen vorhandenen ADO.NET-Verbindungs-Manager aus, oder klicken Sie auf \<**Neue Verbindung…**>, um einen neuen Verbindungs-Manager zu erstellen.  
  
 Verwandte Themen: [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md), [Configure ADO.NET Connection Manager](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 **Aufzählen**  
 Geben Sie das aufzuzählende SMO-Objekt an.  
  
 **Durchsuchen**  
 Wählen Sie die SMO-Enumeration aus.  
  
 **Verwandte Themen:** [SMO-Enumeration auswählen (Dialogfeld)](http://msdn.microsoft.com/library/64ada1fe-21a2-4675-98fc-d5c803aa32f0)  
  
####  <a name="ForeachHDFSFile"></a> Enumerator = Foreach-HDFS-Datei-Enumerator  
 Der **Foreach-HDFS-Datei-Enumerator** ermöglicht einem SSIS-Paket das Aufzählen von HDFS-Dateien am angegebenen HDFS-Speicherort. Der Name jeder HDFS-Datei Dateien kann in einer Variablen gespeichert und in Aufgaben innerhalb des Foreach-Schleifencontainers verwendet werden.  
  
 **Hadoop-Verbindungs-Manager**  
 Geben Sie einen vorhandenen Hadoop-Verbindungs-Manager an, oder erstellen Sie einen neuen Hadoop-Verbindungs-Manager, der angibt, wo die HDFS-Dateien gehostet werden. Weitere Informationen finden Sie unter [Hadoop Connection Manager](../../integration-services/connection-manager/hadoop-connection-manager.md).  
  
 **Verzeichnispfad**  
 Geben Sie den Namen des HDFS-Verzeichnisses an, das die aufzuzählenden HDFS-Dateien enthält.  
  
 **Dateinamensfilter**  
 Geben Sie einen Namensfilter zum Auswählen von Dateien mit einem bestimmten Namensmuster an. Zum Beispiel schließt „MySheet*.xls\*“ Dateien wie „MySheet001.xls“ und „MySheetABC.xlsx“ ein.  
  
 **Dateinamen abrufen**  
 Geben Sie den Typ der von SSIS abgerufenen Dateinamen an.  
  
-   **Vollqualifizierter Name** bezeichnet den vollständigen Namen, der den Verzeichnispfad und Dateinamen enthält.  
  
-   **Nur Name** bedeutet, dass nur der Dateiname ohne Verzeichnispfad abgerufen wird.  
  
 **Unterordner durchsuchen**  
 Geben Sie an, ob Unterordner rekursiv in einer Schleife durchlaufen werden sollen.  
  
 Erstellen oder wählen Sie auf der Seite **Variablenzuordnungen** eine Variable zum Speichern des Namens der aufgezählten HDFS-Datei.  
  
####  <a name="ForeachAzureBlob"></a> Enumerator = Foreach-Azure-Blob-Enumerator  
 Der  **Azure-Blob-Enumerator** ermöglicht einem SSIS-Paket das Aufzählen von Blob-Dateien am angegebenen Blob-Speicherort. Sie können die Namen von aufgezählten Blob-Dateien in einer Variablen speichern, und in Aufgaben innerhalb des Foreach-Schleifencontainers verwenden.  
  
 Der **Azure-Blob-Enumerator** ist eine Komponente des SQL Server Integration Services (SSIS) Feature Pack für Azure für [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Laden Sie das Feature Pack [hier](http://go.microsoft.com/fwlink/?LinkID=626967)herunter.  
  
 **Azure Storage-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Azure Storage-Verbindungs-Manager aus, oder erstellen Sie einen neuen, der auf ein Azure Storage-Konto verweist.  
  
 Verwandte Themen: [Azure Storage Connection Manager](../../integration-services/connection-manager/azure-storage-connection-manager.md).  
  
 **Blob-Containername**  
 Geben Sie den Namen des Blob-Containers an, der die aufzuzählenden Blob-Dateien enthält.
  
 **Blob-Verzeichnis**  
 Geben Sie das Blob-Verzeichnis an, das die aufzuzählenden Blob-Dateien enthält. Das Blob-Verzeichnis ist eine virtuelle hierarchische Struktur.  
  
 **Blob-Namensfilter**  
 Geben Sie einen Namensfilter zum Auflisten von Dateien mit einem bestimmten Namensmuster an. Zum Beispiel schließt `MySheet*.xls\*` Dateien wie „MySheet001.xls“ und „MySheetABC.xlsx“ ein.  
  
 **Blob-Zeitbereichsfilter „von/bis“**  
 Geben Sie einen Filter für den Zeitbereich an. Zählt Dateien auf, die nach **TimeRangeFrom** und vor **TimeRangeTo** geändert wurden. 

####  <a name="ForeachAdlsFile"></a> Enumerator = Foreach-ADLS-Datei-Enumerator 
Der **ADLS-Datei-Enumerator** ermöglicht einem SSIS-Paket das Aufzählen von Dateien in Azure Data Lake Store. Sie können den vollständigen Pfad der aufgelisteten Datei (mit einem Schrägstrich `/` als Präfix) in einer Variablen speichern und den Dateipfad in Aufgaben im Foreach-Schleifencontainer verwenden.
  
**AzureDataLakeConnection**  
Gibt einen Azure Data Lake-Verbindungs-Manager an oder erstellt einen neuen, der auf ein ADLS-Konto verweist.   
  
**AzureDataLakeDirectory**  
Gibt das ADLS-Verzeichnis an, das die aufzuzählenden Dateien enthält.
  
**FileNamePattern**  
Gibt einen Dateinamensfilter an. Nur Dateien, deren Namen dem angegebenen Muster entsprechen, werden aufgelistet. Die Platzhalterzeichen `*` und `?` werden unterstützt. 
  
**SearchRecursively**  
Gibt an, ob im angegebenen Verzeichnis rekursiv gesucht werden soll.  

## <a name="variable-mappings-page---foreach-loop-editor"></a>Foreach-Schleifen-Editor: Seite „Variablenzuordnungen“
 Mithilfe der Seite **Variablenzuordnungen** des Dialogfelds **Foreach-Schleifen-Editor** können Sie dem Auflistungswert Variablen zuordnen. Der Wert der Variable wird bei jeder Iteration der Schleife mit den Ausflistungswerten aktualisiert.  
  
 Informationen zum Verwenden des Foreach-Schleifencontainers in einem Integration Services-Paket finden Sie unter [Foreach Loop Container (Foreach-Schleifen-Editor)](../../integration-services/control-flow/foreach-loop-container.md). Informationen zum Konfigurieren dieses Containers finden Sie unter [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
 Das Lernprogramm für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zum Erstellen eines einfachen ETL-Pakets enthält eine Lektion, die Ihnen zeigt, wie Sie eine Foreach-Schleife hinzufügen und konfigurieren können.  
  
### <a name="options"></a>Tastatur  
 **Variable**  
 Wählen Sie eine vorhandene Variable aus, oder klicken Sie auf **Neue Variable...**, um eine neue Variable zu erstellen.  
  
> [!NOTE]  
>  Nachdem Sie eine Variable zugeordnet haben, wird der Liste **Variable** automatisch eine neue Zeile hinzugefügt.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **Index**  
 Geben Sie bei Verwendung des Foreach-Elementenumerators den Index der Spalte im Auflistungswert an, der der Variable zugeordnet werden soll. Bei anderen Enumeratortypen ist der Index schreibgeschützt.  
  
> [!NOTE]  
>  Der Index basiert auf 0.  
  
**Delete**  
 Wählen Sie eine Variable aus, und klicken Sie auf **Löschen**.  

## <a name="schema-restrictions-dialog-box-adonet"></a>Dialogfeld „Schemaeinschränkungen“ (ADO.NET)
Mit dem Dialogfeld **Schemaeinschränkungen** legen Sie die Schemaeinschränkungen fest, die für den Enumerator für das Foreach-ADO.NET-Schemarowset gelten.  
  
### <a name="options"></a>Tastatur  
 **Einschränkungen**  
 Wählen Sie die Einschränkungen aus, die für das Schema gelten.  
  
 **Variable**  
 Verwendet eine Variable, um die Einschränkungen zu definieren. Wählen Sie eine Variable aus der Liste aus, oder klicken Sie auf **Neue Variable…** , um eine neue Variable zu erstellen.  
  
 **Verwandte Themen:** [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Hinzufügen von Variablen](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
 **Text**  
 Geben Sie den Text an, um Einschränkungen zu definieren.  
 
## <a name="for-each-item-columns-dialog-box"></a>ForEach-Elementspalten (Dialogfeld)
Mithilfe des Dialogfelds **ForEach-Elementspalten** definieren Sie Spalten, die in den Elementen des ForEach-Elementenumerators enthalten sind.  
  
### <a name="options"></a>Tastatur  
 **Column**  
 Listet die Spalten auf.  
  
 **Datentyp**  
 Wählen Sie den Datentyp aus.  
  
 **Hinzufügen**  
 Fügen Sie eine neue Spalte hinzu.  
  
 **Entfernen**  
 Wählen Sie eine Spalte aus, und klicken Sie auf **Entfernen**.  
 
 ## <a name="select-smo-enumeration-dialog-box"></a>SMO-Enumeration auswählen (Dialogfeld)
Verwenden Sie das Dialogfeld **SMO-Enumeration auswählen** , um das aufzuzählende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects-Objekt (SMO-Objekt) für die angegebene [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz anzugeben und den Enumerationstyp auszuwählen.  
  
### <a name="options"></a>Tastatur  
 **Aufzählen**  
 Erweitern des Servers und Auswählen eines SMO-Objekts.  
  
 **Objekte**  
 Verwenden des Enumerationstyps Objekte.  
  
 **Vorauffüllen**  
 Verwenden der Option **Vorauffüllen** mit dem Enumerationstyp „Objekte“.  
  
 **Namen**  
 Verwenden des Enumerationstyps Namen.  
  
 **URNs**  
 Verwenden des Enumerationstyps URNs.  
  
 **Speicherorte**  
 Verwenden des Enumerationstyps Speicherorte. Diese Option ist nur für Dateien verfügbar.  

## <a name="use-property-expressions-with-foreach-loop-containers"></a>Verwenden von Eigenschaftsausdrücken mit Foreach-Schleifencontainern  
 Pakete können so konfiguriert werden, dass mehrere ausführbare Dateien gleichzeitig ausgeführt werden. Diese Konfiguration sollte mit Vorsicht verwendet werden, wenn das Paket einen Foreach-Schleifencontainer enthält, der Eigenschaftsausdrücke implementiert.  
  
 Es ist häufig nützlich, einen Eigenschaftsausdruck zu implementieren, um den Wert der „ConnectionString“-Eigenschaft des Verbindungs-Managers festzulegen, den die „Foreach“-Schleifenenumeratoren verwenden. Der Eigenschaftsausdruck der „ConnectionString“-Eigenschaft wird durch eine Variable festgelegt, die dem Auflistungswert des Enumerators zugeordnet ist und bei jeder Iteration der Schleife aktualisiert wird.  
  
 Das Paket sollte so konfiguriert sein, dass jeweils nur eine ausführbare Datei ausgeführt wird, um in der Schleife negative Auswirkungen einer unbestimmten Zeitvorgabe der parallelen Taskausführung zu vermeiden. Wenn beispielsweise ein Paket mehrere Tasks gleichzeitig ausführen kann, können bei einem Foreach-Schleifencontainer, der im Ordner vorhandene Dateien aufzählt, die Dateinamen abruft und dann mithilfe eines Tasks "SQL ausführen" die Dateinamen in eine Tabelle einfügt, Schreibkonflikte auftreten, falls zwei Instanzen des Tasks "SQL ausführen" versuchen, zur selben Zeit zu schreiben. Weitere Informationen finden Sie unter [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ablaufsteuerung](../../integration-services/control-flow/control-flow.md)   
 [SQL Server Integration Services-Container](../../integration-services/control-flow/integration-services-containers.md)  
  
  
