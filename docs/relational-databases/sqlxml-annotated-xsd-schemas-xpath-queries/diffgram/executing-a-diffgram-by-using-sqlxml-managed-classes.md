---
title: Ausführen eines Diffgrams mit SQLXML, verwaltete Klassen | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], Managed Classes
- SQLXML Managed Classes, DiffGrams
- Managed Classes [SQLXML], DiffGrams
- SQLXML, Managed Classes
ms.assetid: 81c687ca-8c9f-4f58-801f-8dabcc508a06
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fa04e87ef14c0a863cbace5e2dfa41a31ec2c7a8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="executing-a-diffgram-by-using-sqlxml-managed-classes"></a>Ausführen eines DiffGram-Objekts mit verwalteten SQLXML-Klassen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In diesem Beispiel wird gezeigt, wie auszuführende eine DiffGram-Datei in die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework-Umgebung anzuwenden, aktualisiert auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tabellen mit verwalteten SQLXML-Klassen (Microsoft.Data.SqlXml).  
  
 In diesem Beispiel aktualisiert das DiffGram Kundeninformationen (CompanyName und ContactName) für den Kunden ALFKI.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 Die  **\<vor >** -Block enthält ein  **\<Kunden >** Element (**diffgr: ID = "Customer1"**). Die  **\<DataInstance >** -Block enthält das entsprechende  **\<Kunden >** -Element mit derselben **Id**. Die  **\<Kunden >** Element in der  **\<NewDataSet >** überdies **diffgr: HasChanges = "modified"**. Dadurch wird ein Updatevorgang angezeigt und der Kundendatensatz in der Cust-Tabelle entsprechend aktualisiert. Beachten Sie, dass bei der **diffgr: HasChanges** -Attribut nicht angegeben ist, das DiffGram-Verarbeitungslogik ignoriert diese-Element, und keine Updates ausgeführt werden.  
  
 Im folgenden finden Sie Code für ein C#-Lernprogramm Anwendung, die zeigt, wie verwaltete SQLXML-Klassen zum Ausführen des oben genannten Diffgrams und Updates zweier Tabellen (Cust, Ord) Sie auch in Erstellen der **Tempdb** Datenbank.  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=MyServer;database=tempdb;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlAdapter ad;  
      // Need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandStream = new FileStream("MyDiffgram.xml", FileMode.Open, FileAccess.Read);  
      cmd.CommandType = SqlXmlCommandType.DiffGram;  
      cmd.SchemaPath = "DiffGramSchema.xml";  
      // Load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
### <a name="to-test-the-application"></a>So testen Sie die Anwendung  
  
1.  Stellen Sie sicher, dass .NET Framework auf dem Computer installiert ist.  
  
2.  Speichern Sie das folgende XSD-Schema (DiffGramSchema.xml) in einem Ordner:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
     </xsd:annotation>  
     <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
     </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Erstellen Sie diese Tabellen in der **Tempdb** Datenbank.  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
4.  Fügen Sie diese Beispieldaten hinzu:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
5.  Kopieren Sie das oben stehende DiffGram, und fügen Sie es in eine Textdatei ein. Speichern Sie die Datei als MyDiffGram.xml in demselben Ordner, den Sie in Schritt 1 verwendet haben.  
  
6.  Speichern Sie den C#-Code (DiffgramSample.cs) aus dem Beispiel oben im selben Ordner, in dem DiffGramSchema.xml und MyDiffGram.xml aus den vorherigen Schritten gespeichert wurden.  
  
    > [!NOTE]  
    >  Sie müssen den Namen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz in der Verbindungszeichenfolge von '`MyServer`' in den tatsächlichen Namen Ihrer installierten Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ändern.  
  
     Wenn Sie die Dateien in einem anderen Ordner speichern, müssen Sie den Code bearbeiten und den entsprechenden Verzeichnispfad für das Zuordnungsschema angeben.  
  
7.  Kompilieren Sie den Code. Verwenden Sie zur Kompilierung des Codes an der Eingabeaufforderung die folgende Zeichenfolge:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DiffgramSample.cs  
    ```  
  
     Dadurch wird eine ausführbare Datei (DiffgramSample.exe) erstellt.  
  
8.  Führen Sie DiffgramSample.exe an der Eingabeaufforderung aus.  
  
## <a name="see-also"></a>Siehe auch  
 [DiffGram-Beispiele & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/diffgram/diffgram-examples-sqlxml-4-0.md)  
  
  
