---
title: "Übergeben von Parametern an Updategrams (SQLXML 4.0) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
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
- nullvalue attribute
- passing parameters [SQLXML]
- parameters [SQLXML]
- updategrams [SQLXML], passing parameters
- null values [SQLXML]
ms.assetid: 2354e6e7-1860-471f-8711-4e374c5a4ed2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aba948424591ed7edbb4bba89a6452a2f8d1d21a
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>Übergeben von Parametern an Updategrams (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Updategrams sind Vorlagen. Daher können Sie ihnen Parameter übergeben. Weitere Informationen zum Übergeben von Parametern an Vorlagen finden Sie unter [Sicherheitsüberlegungen zu Updategrams &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md).  
  
 Mit Updategrams können Sie NULL als Parameterwert übergeben. Um den NULL-Parameterwert zu übergeben, geben Sie die **Nullvalue** Attribut. Der Wert, der zugewiesen ist die **Nullvalue** Attribut wird dann als Wert des Parameters bereitgestellt. Updategrams behandeln diesen Wert als NULL.  
  
> [!NOTE]  
>  In  **\<SQL: Header >** und  **\<Updg:header >**, geben Sie die **Nullvalue** nicht als qualifizierte, während im  **\<updg: Sync >**, Sie geben die **Nullvalue** als qualifiziert (z. B. **updg: NullValue**).  
  
## <a name="examples"></a>Beispiele  
 Um funktionierende Beispiele, die über folgende Beispiele zu erstellen, müssen Sie in angegebenen Anforderungen erfüllen [Anforderungen für die Ausführung von SQLXML-Beispielen](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Bevor Sie die updategrambeispiele verwenden, ist Folgendes zu beachten:  
  
-   Die Beispiele verwenden die Standardzuordnung (d. h. es ist kein Zuordnungsschema im Updategram angegeben). Weitere Beispiele für Updategrams, die Zuordnungsschemas verwenden, finden Sie unter [ein Mapping-Schema mit Anmerkungen angeben, in einem Updategram &#40; SQLXML 4.0 &#41; ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. Übergeben von Parametern an ein Updategram  
 In diesem Beispiel ändert das Updategram den Nachnamen eines Angestellten in der HumanResources.Shift-Tabelle. An das Updategram werden zwei Parameter übergeben: ShiftID zur eindeutigen Identifizierung der Schicht und Name.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
  <updg:param name="ShiftID"/>  
  <updg:param name="Name" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="$ShiftID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="$Name" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie das oben angegebene Updategram in Editor, und speichern Sie es als Datei unter UpdategramWithParameters.xml.  
  
2.  Vorbereiten der SQLXML 4.0-Testskript (Sqlxml4test.vbs) in [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) das Updategram ausgeführt wird, durch die folgenden Zeilen nach dem Hinzufügen der `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>B. Übergeben von NULL als Parameterwert an ein Updategram  
 Durch Ausführen eines Updategrams wird der Wert "isnull" dem Parameter zugewiesen, der auf NULL gesetzt werden soll. Das Updategram konvertiert den "isnulll"-Parameterwert in NULL und verarbeitet ihn entsprechend.  
  
 Das folgende Updategram legt einen Mitarbeitertitel auf NULL fest:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header nullvalue="isnull" >  
  <updg:param name="EmployeeID"/>  
  <updg:param name="ManagerID" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Employee EmployeeID="$EmployeeID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Employee ManagerID="$ManagerID" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>So testen Sie das Updategram  
  
1.  Kopieren Sie das oben angegebene Updategram in Editor, und speichern Sie es als Datei unter UpdategramPassingNullvalues.xml.  
  
2.  Vorbereiten der SQLXML 4.0-Testskript (Sqlxml4test.vbs) in [mithilfe von ADO zum Ausführen von SQLXML 4.0-Abfragen](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) das Updategram ausgeführt wird, durch die folgenden Zeilen nach dem Hinzufügen der `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheitsüberlegungen zu Updategrams &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
