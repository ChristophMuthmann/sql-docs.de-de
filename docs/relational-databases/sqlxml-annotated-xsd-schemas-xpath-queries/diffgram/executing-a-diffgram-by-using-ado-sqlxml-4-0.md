---
title: "Ausführen eines DiffGram-Objekts mit ADO (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- providers [SQLXML], SQLOLEDB Provider
- ADO [SQLXML]
- SQLXMLOLEDB Provider, DiffGrams
- data providers [SQLXML], SQLOLEDB Provider
- DiffGrams [SQLXML], ADO
ms.assetid: 741fce82-de83-4923-86eb-30acb5b9a5e6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3baa16c0f283e8066a764801f31422c6c2eb8f7
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="executing-a-diffgram-by-using-ado-sqlxml-40"></a>Ausführen eines DiffGram-Objekts mit ADO (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Diese [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic-Anwendung verwendet ADO, um eine Verbindung mit einer Instanz von Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herzustellen, und führt dann ein DiffGram-Objekt aus. In dieser Anwendung werden das DiffGram-Objekt und das XSD-Schema in einer Datei gespeichert. Die Anwendung lädt das DiffGram-Objekt aus der angegebenen Datei. Verwenden Sie eines der DiffGram-Objekte (und das zugehörige XSD-Schema) in der beschriebenen [DiffGram-Beispiele](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
 Das ist der Ablauf bei der Beispielanwendung:  
  
-   Die **Conn** Objekt (**ADODB. Verbindung**) stellt eine Verbindung mit einer ausgeführten Instanz von SQL Server auf einem bestimmten Server her.  
  
-   Die **Cmd** Objekt (**ADODB.Command**) für die hergestellte Verbindung ausgeführt wird.  
  
-   Der Befehlsdialekt wird auf DBGUID_MSSQLXML festgelegt.  
  
-   Das DiffGram-Objekt wird in den befehlsdatenstrom kopiert (**StrmIn**) aus einer Datei.  
  
-   Ausgabedatenstrom des Befehls wird festgelegt, um die **StrmOut** Objekt (**ADODB. Streamen**) auf den Empfang hat Daten zurückgegeben.  
  
-   Wenn Sie den SQLOLEDB-Anbieter verwenden, wird die Microsoft SQLXML-Funktionalität standardmäßig von Sqlxmlx.dll bereitgestellt. Um Sqlxml4.dll mit SQLOLEDB-Anbieter verwenden die **SQLXML Version** Eigenschaft muss festgelegt werden, um **SQLXML.4.0** für den SQLOLEDB-Anbieter **Verbindung** Objekt.  
  
-   Der Befehl (DiffGram) wird ausgeführt.  
  
 Der folgende Code stellt die Beispielanwendung dar.  
  
> [!NOTE]  
>  Im Code müssen Sie den Namen der Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in der Verbindungszeichenfolge bereitstellen.  
  
```  
Private Sub Command1_Click()  
  Dim cmd As New ADODB.Command  
  Dim conn As New ADODB.Connection  
  Dim strmOut As New ADODB.Stream  
  Dim strmIn As New ADODB.Stream  
  
  'Open a connection to SQL Server.  
  conn.Provider = "SQLOLEDB"  
  conn.Open "server=SqlServerName; database=tempdb; Integrated Security=SSPI; "  
  conn.Properties("SQLXML Version") = "SQLXML.4.0"  
  Set cmd.ActiveConnection = conn  
  strmIn.Open  
  strmIn.Charset = "UTF-8"  
  strmIn.LoadFromFile "C:\SomeFilePath\SampleDiffGram.xml"  
  strmIn.Position = 0  
  Set cmd.CommandStream = strmIn  
  
  strmOut.Open  
  cmd.Properties("Output Stream").Value = strmOut  
  cmd.Properties("Output Encoding").Value = "UTF-8"  
  
  cmd.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
  cmd.Properties("Mapping Schema") = "C:\SomeFilePath\SampleDiffGram.xml"  
  cmd.Execute , , adExecuteStream  
  strmOut.Position = 0  
  Set cmd = Nothing  
  strmOut.Charset = "UTF-8"  
  strmOut.SaveToFile "C:\DropIt.txt", adSaveCreateOverWrite  
  strmOut.Close  
  Set strmOut = Nothing  
  
End Sub  
```  
  
### <a name="to-test-the-diffgram"></a>So testen Sie das DiffGram-Objekt  
  
1.  Kopieren Sie auf den Ordner auf dem Computer eines DiffGram-Objekte und die entsprechenden XSD-Schema aus einem der in den Beispielen in [DiffGram-Beispiele](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md).  
  
2.  Öffnen Sie Visual Basic, und erstellen Sie ein Standard-EXE-Projekt.  
  
3.  Fügen Sie dem Projekt die folgenden Verweise hinzu:  
  
    ```  
    Microsoft ActiveX Data Objects 2.8 Library  
    ```  
  
4.  Klicken Sie in der Toolbox auf **CommandButton**, und zeichnen Sie dann auf dem Formular eine Schaltfläche.  
  
5.  Doppelklicken Sie auf die Schaltfläche, um den Code zu bearbeiten, und fügen Sie den Anwendungscode aus dem Dokument hinzu.  
  
6.  Bearbeiten Sie den Code, um das DiffGram-Objekt und die XSD-Dateinamen anzugeben. Bearbeiten Sie außerdem die Verbindungszeichenfolge nach Bedarf.  
  
7.  Führen Sie die Anwendung. Das Ergebnis der Ausführung hängt davon ab, was für ein DiffGram-Objekt Sie ausführen.  
  
  
