---
title: "Vorbereiten zur Abfrage der Änderungsdaten | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],preparing query
ms.assetid: 9ea2db7a-3dca-4bbf-9903-cccd2d494b5f
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b15733feeca10976315834b2dfc897cc8a9d1216
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="prepare-to-query-for-the-change-data"></a>Vorbereiten zur Abfrage der Änderungsdaten
  In der Ablaufsteuerung eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets, das ein inkrementelles Laden von Änderungsdaten ausführt, besteht der dritte und letzte Task darin, die Abfrage der Änderungsdaten vorzubereiten und einen Datenflusstask hinzuzufügen.  
  
> [!NOTE]  
>  Beim zweiten Task für die Ablaufsteuerung muss sichergestellt werden, dass die Änderungsdaten für das ausgewählte Intervall bereit sind. Weitere Informationen zu diesem Task finden Sie unter [Bestimmen, ob die Änderungsdaten bereit sind](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md). Eine Beschreibung des Gesamtprozesses zum Entwurf der Ablaufsteuerung finden Sie unter [Change Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="design-considerations"></a>Entwurfsaspekte  
 Wenn Sie die Änderungsdaten abrufen möchten, müssen Sie eine Transact-SQL-Tabellenwertfunktion aufrufen, die die Endpunkte des Intervalls als Eingabeparameter akzeptiert und für das angegebene Intervall Änderungsdaten zurückgibt. Eine Quellkomponente im Datenfluss ruft diese Funktion auf. Weitere Informationen zu dieser Quellkomponente finden Sie unter [Abrufen und Verstehen der Änderungsdaten](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md).  
  
 Die am häufigsten verwendeten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Quellkomponenten, einschließlich der OLE DB-Quelle, der ADO-Quelle und der ADO NET-Quelle, können für eine Tabellenwertfunktion keine Parameterinformationen ableiten. Deshalb können die meisten Quellen eine parametrisierte Funktion nicht direkt aufrufen.  
  
 Ihnen stehen zwei Entwurfsoptionen zur Verfügung, um die Eingabeparameter an die Funktion zu übergeben:  
  
-   **Assemblieren Sie die parametrisierte Abfrage als Zeichenfolge**. Sie können einen Skripttask oder einen Task "SQL ausführen" verwenden, um eine dynamische SQL-Zeichenfolge mit Parameterwerten hartcodiert in die Zeichenfolge zu assemblieren. Sie können dann diese Zeichenfolge in einer Paketvariablen speichern und diese verwenden, um die SqlCommand-Eigenschaft einer Quellkomponente festzulegen. Dieser Ansatz ist erfolgreich, da die Quellkomponente nicht länger Parameterinformationen benötigt.  
  
    > [!NOTE]  
    >  Ein vorkompiliertes Skript verursacht weniger Aufwand als ein Task "SQL ausführen".  
  
-   **Verwenden Sie einen parametrisierten Wrapper**. Alternativ können Sie eine parametrisierte gespeicherte Prozedur als Wrapper erstellen, der die parametrisierte Tabellenwertfunktion aufruft. Dieser Ansatz ist erfolgreich, da eine Quellkomponente Parameterinformationen für eine gespeicherte Prozedur erfolgreich ableiten kann.  
  
 Dieses Thema verwendet die erste Entwurfsoption und assembliert eine parametrisierte Abfrage als Zeichenfolge.  
  
## <a name="preparing-the-query"></a>Vorbereiten der Abfrage  
 Bevor Sie die Werte der Eingabeparameter in eine einzelne Abfragezeichenfolge verketten können, müssen Sie die für die Abfrage erforderlichen Paketvariablen einrichten.  
  
#### <a name="to-set-up-package-variables"></a>So richten Sie Paketvariablen ein  
  
-   Erstellen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]im Fenster **Variablen** eine Variable mit einem Zeichenfolgen-Datentyp, damit die Abfragezeichenfolge durch den Task "SQL ausführen" zurückgegeben wird.  
  
     In diesem Beispiel wird der Variablenname "SqlDataQuery" verwendet.  
  
 Wenn die Paketvariable erstellt wurde, können Sie einen Skripttask oder einen Task "SQL ausführen" verwenden, um die Werte der Eingabeparameter zu verketten. Die folgenden zwei Prozeduren beschreiben, wie diese Komponenten konfiguriert werden.  
  
#### <a name="to-use-a-script-task-to-concatenate-the-query-string"></a>So verwenden Sie einen Skripttask zur Verkettung der Abfragezeichenfolge  
  
1.  Fügen Sie dem Paket auf der Registerkarte **Ablaufsteuerung** nach dem For-Schleifencontainer einen Skripttask hinzu, und verbinden Sie den For-Schleifencontainer mit dem Task.  
  
    > [!NOTE]  
    >  In dieser Prozedur wird davon ausgegangen, dass das Paket ein inkrementelles Laden aus einer einzelnen Tabelle ausführt. Wenn das Paket aus mehreren Tabellen lädt und ein übergeordnetes Paket mit mehreren untergeordneten Paketen hat, würde dieser Task jedem untergeordneten Paket als erste Komponente hinzugefügt werden. Weitere Informationen finden Sie unter [Ausführen eines inkrementellen Ladens von mehreren Tabellen](../../integration-services/change-data-capture/perform-an-incremental-load-of-multiple-tables.md).  
  
2.  Aktivieren Sie im **Skripttask-Editor**auf der Seite **Skript** die folgenden Optionen:  
  
    1.  Wählen Sie für **ReadOnlyVariables**die Optionen **User::DataReady**, **User::ExtractStartTime**und **User::ExtractEndTime** aus.  
  
    2.  Wählen Sie für **ReadWriteVariables**die Option User::SqlDataQuery aus der Liste aus.  
  
3.  Klicken Sie im **Skripttask-Editor**auf der Seite **Skript** auf **Skript bearbeiten** , um die Skriptentwicklungsumgebung zu öffnen.  
  
4.  Geben Sie in der Main-Prozedur eines der folgenden Codesegmente ein:  
  
    -   Wenn Sie in C# programmieren, geben Sie die folgenden Codezeilen ein:  
  
        ```  
        int dataReady;  
        System.DateTime extractStartTime;  
        System.DateTime extractEndTime;  
        string sqlDataQuery;  
  
        dataReady = (int)Dts.Variables["DataReady"].Value;  
        extractStartTime = (System.DateTime)Dts.Variables["ExtractStartTime"].Value;  
        extractEndTime = (System.DateTime)Dts.Variables["ExtractEndTime"].Value;  
  
        if (dataReady == 2)  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) + "', '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
        else  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" + ", '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
  
        Dts.Variables["SqlDataQuery"].Value = sqlDataQuery;  
        ```  
  
         \- oder –  
  
    -   Wenn Sie in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]programmieren, geben Sie die folgenden Codezeilen ein:  
  
        ```  
        Dim dataReady As Integer  
        Dim extractStartTime As Date  
        Dim extractEndTime As Date  
        Dim sqlDataQuery As String  
  
        dataReady = CType(Dts.Variables("DataReady").Value, Integer)  
        extractStartTime = CType(Dts.Variables("ExtractStartTime").Value, Date)  
        extractEndTime = CType(Dts.Variables("ExtractEndTime").Value, Date)  
  
        If dataReady = 2 Then  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) & _  
              "', '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        Else  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" & _  
              ", '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        End If  
  
        Dts.Variables("SqlDataQuery").Value = sqlDataQuery  
  
        ```  
  
5.  Verlassen Sie die Standardcodezeile, die **DtsExecResult.Success** aus der Ausführung des Skripts zurückgibt.  
  
6.  Schließen Sie die Skriptentwicklungsumgebung und den **Skripttask-Editor**.  
  
#### <a name="to-use-an-execute-sql-task-to-concatenate-the-query-string"></a>So verwenden Sie einen Task "SQL ausführen" zur Verkettung der Abfragezeichenfolge  
  
1.  Fügen Sie dem Paket auf der Registerkarte **Ablaufsteuerung** nach dem For-Schleifencontainer einen Task "SQL ausführen" hinzu, und verbinden Sie den For-Schleifencontainer mit diesem Task.  
  
    > [!NOTE]  
    >  In dieser Prozedur wird davon ausgegangen, dass das Paket ein inkrementelles Laden aus einer einzelnen Tabelle ausführt. Wenn das Paket aus mehreren Tabellen lädt und ein übergeordnetes Paket mit mehreren untergeordneten Paketen hat, würde dieser Task jedem untergeordneten Paket als erste Komponente hinzugefügt werden. Weitere Informationen finden Sie unter [Ausführen eines inkrementellen Ladens von mehreren Tabellen](../../integration-services/change-data-capture/perform-an-incremental-load-of-multiple-tables.md).  
  
2.  Aktivieren Sie im **Skripttask-Editor**auf der Seite **Skript** die folgenden Optionen:  
  
    1.  Wählen Sie für **ResultSet**die Option **Einzelne Zeile**aus.  
  
    2.  Konfigurieren Sie zur Quelldatenbank eine gültige Verbindung.  
  
    3.  Wählen Sie für **SQLSourceType**die Option **Direkteingabe**aus.  
  
    4.  Geben Sie für **SQLStatement**die folgende SQL-Anweisung ein:  
  
        ```  
        declare @ExtractStartTime datetime,  
        @ExtractEndTime datetime,   
        @DataReady int  
  
        select @DataReady = ?,   
        @ExtractStartTime = ?,   
        @ExtractEndTime = ?  
  
        if @DataReady = 2  
        select N'select * from CDCSample.uf_Customer'  
        + N'('''+ convert(nvarchar(30),@ExtractStartTime,120)  
        + ''', '''  
        + convert(nvarchar(30),@ExtractEndTime,120) + ''') '   
        as SqlDataQuery  
        else  
        select N'select * from CDCSample.uf_Customer'  
        + N'(null, '''  
        + convert(nvarchar(30),@ExtractEndTime,120)  
        + ''') '  
        as SqlDataQuery  
  
        ```  
  
        > [!NOTE]  
        >  Die **else** -Klausel in diesem Beispiel generiert eine Abfrage für das erste Laden der Änderungsdaten, indem für das Startdatum und die Startzeit ein NULL-Wert übergeben wird. Dieses Beispiel befasst sich nicht mit dem Szenario, in dem Änderungen, die vor der Aktivierung von Change Data Capture vorgenommen wurden, auch ins Data Warehouse hochgeladen werden müssen.  
  
3.  Nehmen Sie auf der Seite **Parameterzuordnung** vom **Editor für den Task 'SQL ausführen'**die folgende Zuordnung vor:  
  
    1.  Ordnen Sie dem Parameter 0 die DataReady-Variable zu.  
  
    2.  Ordnen Sie dem Parameter 1 die ExtractStartTime-Variable zu.  
  
    3.  Ordnen Sie dem Parameter 2 die ExtractEndTime-Variable zu.  
  
4.  Ordnen Sie auf der Seite **Resultset** vom **Editor für den Task 'SQL ausführen'**der SqlDataQuery-Variablen den Ergebnisnamen zu.  
  
     Der Ergebnisname ist der Name der einzelnen Spalte, die zurückgegeben wird, SqlDataQuery.  
  
 Die oben beschriebenen Prozeduren konfigurieren einen Task, der eine Abfragezeichenfolge mit hartcodierten Zeichenfolgewerten für die Eingabeparameter vorbereitet. Der folgende Code ist ein Beispiel für eine solche Abfragezeichenfolge:  
  
 `select * from CDCSample. uf_Customer('2007-06-11 14:21:58', '2007-06-12 14:21:58')`  
  
## <a name="adding-a-data-flow-task"></a>Hinzufügen eines Datenflusstasks  
 Das Hinzufügen eines Datenflusstasks ist der letzte Schritt beim Entwerfen einer Ablaufsteuerung für ein Paket.  
  
#### <a name="to-add-a-data-flow-task-and-complete-the-control-flow"></a>So fügen Sie einen Datenflusstask hinzu und vervollständigen Sie die Ablaufsteuerung  
  
-   Fügen Sie auf der Registerkarte **Ablaufsteuerung** einen Datenflusstask hinzu, und verbinden Sie den Task, der die Abfragezeichenfolge verkettet hat.  
  
## <a name="next-step"></a>Nächster Schritt  
 Nach der Vorbereitung der Abfragezeichenfolge und der Konfiguration des Datenflusstasks besteht der nächste Schritt darin, die Tabellenwertfunktion zu erstellen, mit der die Änderungsdaten von der Datenbank abgerufen werden.  
  
 **Nächstes Thema:** [Erstellen der Funktion zum Abrufen der Änderungsdaten](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)  
  
  

