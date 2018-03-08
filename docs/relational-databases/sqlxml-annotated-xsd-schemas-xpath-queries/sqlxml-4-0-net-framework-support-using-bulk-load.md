---
title: Verwenden von SQLXML-Massenladen in der .NET-Umgebung | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- SQLXML, XML Bulk Load
- XML Bulk Load [SQLXML], .NET environment
- .NET Framework [SQLXML], XML Bulk Load
- bulk load [SQLXML], .NET environment
ms.assetid: b85df83b-ba56-43bf-bcdf-b2a6fca43276
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c7e12a75ecd120c99a2e658c47acb8b28ffb260
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="sqlxml-40-net-framework-support---using-bulk-load"></a>SQLXML 4.0 .NET Framework-Unterstützung - verwenden von Massenkopieren
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
In diesem Thema wird erklärt, wie die XML-Massenladefunktionalität in der .NET-Umgebung verwendet werden kann. Ausführliche Informationen zu XML-Massenladen, finden Sie unter [Ausführen von Massenladen von XML von Daten &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md).  
  
 Um das SQLXML-Massenladen-COM-Objekt in einer verwalteten Umgebung zu verwenden, müssen Sie diesem Objekt eine Projektreferenz hinzufügen. Dies generiert eine verwaltete Wrapperschnittstelle um das Massenladen-COM-Objekt.  
  
> [!NOTE]  
>  Verwaltetes XML-Massenladen funktioniert nicht mit verwalteten Datenströmen und erfordert einen Wrapper um systemeigene Datenströme. Die SQLXML-Massenladenkomponente wird nicht in einer Multithreadumgebung ('[MTAThread]'-Attribut) ausgeführt. Wenn Sie versuchen, die massenladenkomponente in einer Multithreadumgebung auszuführen, erhalten Sie eine InvalidCastException-Ausnahme mit der folgenden zusätzlichen Informationen: "Fehler bei QueryInterface für Schnittstelle SQLXMLBULKLOADLib.ISQLXMLBulkLoad." Die problemumgehung besteht darin, das Objekt zu machen, die das Massenladen singlethreads zugänglich enthält (z. B. mithilfe der **[STAThread]** -Attribut wie im Beispiel gezeigt).  
  
 Dieses Thema stellt eine funktionierende C#-Beispielanwendung für das Massenladen von XML-Daten in der Datenbank bereit. Gehen Sie folgendermaßen vor, um ein funktionierendes Beispiel zu erstellen:  
  
1.  Erstellen Sie die folgenden Tabellen:  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5))  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20))  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID))  
    GO  
    ```  
  
2.  Speichern Sie das folgende Schema in einer Datei (schema.xml):  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
    <xsd:annotation>  
      <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Speichern Sie das folgende Beispiel-XML-Dokument in einer Datei (data.xml):  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  Starten Sie Visual Studio.  
  
5.  Erstellen Sie eine C#-Konsolenanwendung.  
  
6.  Aus der **Projekt** klicken Sie im Menü **Verweis hinzufügen**.  
  
7.  In der **COM** Registerkarte **Microsoft SQLXML Bulkload 4.0 Type Library** (xblkld4.dll), und klicken Sie auf **OK**. Daraufhin werden die **Interop.SQLXMLBULKLOADLib** Assembly im Projekt erstellt.  
  
8.  Ersetzen Sie die Main()-Methode durch den folgenden Code. Update der **"ConnectionString"** -Eigenschaft und den Dateipfad, auf das Schema und die Datendateien.  
  
    ```  
    [STAThread]  
       static void Main(string[] args)  
       {     
             try  
             {  
                SQLXMLBULKLOADLib.SQLXMLBulkLoad4Class objBL = new SQLXMLBULKLOADLib.SQLXMLBulkLoad4Class();  
                objBL.ConnectionString = "Provider=sqloledb;server=server;database=databaseName;integrated security=SSPI";  
                objBL.ErrorLogFile = "error.xml";  
                objBL.KeepIdentity = false;  
                objBL.Execute ("schema.xml","data.xml");  
             }  
             catch(Exception e)  
             {  
             Console.WriteLine(e.ToString());  
             }  
       }  
    ```  
  
9. Um das XML in die erstellte Tabelle zu laden, erstellen Sie das Projekt, und führen Sie es aus.  
  
    > [!NOTE]  
    >  Die Referenz zur Massenladenkomponente (xblkld4.dll) kann auch mithilfe des Tools tlbimp.exe hinzugefügt werden, das als Teil von .NET Framework zur Verfügung steht. Dieses Tool erstellt einen verwalteten Wrapper für die systemeigene DLL (xblkld4.dll), der in allen .NET-Projekten verwendet werden kann. Beispiel:  
  
    ```  
    c:\>tlbimp xblkld4.dll  
    ```  
  
     Dies erstellt die verwaltete Wrapper-DLL (SQLXMLBULKLOADLib.dll), die Sie im .NET Framework-Projekt verwenden können. In .NET Framework fügen Sie der neu erstellten DLL Projektverweise hinzu.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Massenladen von XML-Daten &#40; SQLXML 4.0 &#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
  
  
