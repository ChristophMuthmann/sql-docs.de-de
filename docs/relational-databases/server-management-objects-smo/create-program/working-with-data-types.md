---
title: Arbeiten mit Datentypen | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 68e89b1615013947bd4f249b6ddfd67084db1d68
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="working-with-data-types"></a>Arbeiten mit Datentypen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Viele Typen und Größen verfügbar, z. B. eine Zeichenfolge ist eine definierte Länge, eine Zahl, die bestimmten Genauigkeit oder einen benutzerdefinierten Datentyp, der ein anderes Objekt ist, das über einen eigenen Satz von Regeln verfügt, gibt Daten. Die <xref:Microsoft.SqlServer.Management.Smo.DataType> -Objekt klassifiziert den Typ der Daten, damit sie ordnungsgemäß durch verarbeitet werden kann [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Das <xref:Microsoft.SqlServer.Management.Smo.DataType>-Objekt ist Objekten zugeordnet, die Daten akzeptieren. Die folgenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO)-Objekte akzeptieren Daten, die von definiert werden, müssen ein <xref:Microsoft.SqlServer.Management.Smo.DataType> -Objekteigenschaft:  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 Die **DataType** -Eigenschaft für Objekte, die Daten akzeptieren, kann auf unterschiedliche Weise festgelegt werden.  
  
-   Verwenden Sie den Standardkonstruktor und geben <xref:Microsoft.SqlServer.Management.Smo.DataType> -Objekteigenschaften explizit  
  
-   Verwenden Sie einen überladenen Konstruktor, und geben Sie die <xref:Microsoft.SqlServer.Management.Smo.DataType> Eigenschaften als Parameter.  
  
-   Geben Sie die <xref:Microsoft.SqlServer.Management.Smo.DataType> Inline im Objektkonstruktor.  
  
-   Verwenden Sie eine der statischen Elemente der der <xref:Microsoft.SqlServer.Management.Smo.DataType> Klasse, zum Beispiel **Int**. In diesem Fall wird eine Instanz eines <xref:Microsoft.SqlServer.Management.Smo.DataType>-Objekts zurückgegeben.  
  
 Das <xref:Microsoft.SqlServer.Management.Smo.DataType>-Objekt verfügt über einige Eigenschaften, die den Datentyp definieren. Beispielsweise gibt die <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>-Eigenschaft den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentyp an. Die Konstante Werte, die darstellen, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen sind aufgeführt, der <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> Enumeration. Dies gilt für Datentypen wie **varchar**, **nchar**, **currency**, **integer**, **float**und **datetime**.  
  
 Nachdem der Datentyp definiert wurde, müssen bestimmte Eigenschaften für die Daten festgelegt werden. Beispielsweise muss bei einem **nchar** -Typ die Länge der Zeichenfolgenddaten mit der **Length** -Eigenschaft angegeben werden. Das Gleiche gilt für numerische Werte, für die Genauigkeit und Dezimalstellenanzahl angegeben werden muss.  
  
 Der <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>-Datentyp und der <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>-Datentyp beziehen sich auf Objekte, die die Definition des vom Benutzer definierten Datentyps enthalten. <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> basiert auf den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentypen aus der <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>-Enumeration. Die <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> basiert auf [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Datentypen. In der Regel würden diese Daten eines bestimmten Typs darstellen, der wegen der von der Organisation definierten Geschäftsregeln in der Datenbank häufig verwendet wird. Beispielsweise wäre ein Datentyp, mit dem ein Währungsbetrag und ein Währungsbezeichner gespeichert wird, für eine Firma hilfreich, die mit mehreren Währungen arbeitet.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> -Enumeration enthält eine Liste aller der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentypen unterstützt.  
  
## <a name="examples"></a>Beispiele  
Zum Verwenden eines angegebenen Codebeispiels müssen Sie die Programmierumgebung, Programmiervorlage und die zu verwendende Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>Konstruktion eines DataType-Objekts mit der Spezifikation im Konstruktor in Visual Basic  
 In diesem Codebeispiel wird veranschaulicht, wie mit dem Konstruktor Instanzen von Datentypen erstellt werden, die auf anderen basieren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> und die XML-Typen erfordern einen Namenswert zur Identifizierung des Objekts.  
  
```VBNET
'Declare a DataType object variable and define the data type in the constructor.
Dim dt As DataType
'For the decimal data type the following two arguements specify precision, and scale.
dt = New DataType(SqlDataType.Decimal, 10, 2)
``` 
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>Konstruktion eines DataType-Objekts mit der Spezifikation im Konstruktor in Visual C#  
 In diesem Codebeispiel wird veranschaulicht, wie mit dem Konstruktor Instanzen von Datentypen erstellt werden, die auf anderen basieren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen.  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> und die XML-Typen erfordern einen Namenswert zur Identifizierung des Objekts.  
  
```csharp  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguements specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>Konstruktion eines DataType-Objekts mithilfe des Standardkonstruktors in Visual Basic  
 Dieses Codebeispiel zeigt, wie Sie den Standardkonstruktor verwenden, um Instanzen von Datentypen zu erstellen, die auf anderen basieren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen. Mithilfe der Eigenschaften wird der Datentyp dann angegeben.  
  
 **Hinweis** der <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, und die XML-Typen erfordern einen Namenswert zur Identifizierung des Objekts.  
  
```VBNET
'Declare and create a DataType object variable.
Dim dt As DataType
dt = New DataType
'Define the data type by setting the SqlDataType property.
dt.SqlDataType = SqlDataType.VarChar
'The VarChar data type requires a value for the MaximumLength property.
dt.MaximumLength = 100
```
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>Konstruktion eines DataType-Objekts mithilfe des Standardkonstruktors in Visual C#  
 Dieses Codebeispiel zeigt, wie Sie den Standardkonstruktor verwenden, um Instanzen von Datentypen zu erstellen, die auf anderen basieren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datentypen. Mithilfe der Eigenschaften wird der Datentyp dann angegeben.  
  
 **Hinweis** der <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, und die XML-Typen erfordern einen Namenswert zur Identifizierung des Objekts.  
  
```csharp  
{   
//Declare and create a DataType object variable.   
DataType dt;   
dt = new DataType();   
//Define the data type by setting the SqlDataType property.   
dt.SqlDataType = SqlDataType.VarChar;   
//The VarChar data type requires a value for the MaximumLength property.   
dt.MaximumLength = 100;   
}  
```  
  
  
