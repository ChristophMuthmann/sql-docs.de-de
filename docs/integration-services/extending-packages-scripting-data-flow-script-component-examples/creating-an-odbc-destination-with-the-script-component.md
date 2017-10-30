---
title: Erstellen ein ODBC-Ziel mit der Skriptkomponente | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5eb539f0d18f473b10ed8d49bcee9c298292fb41
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>Erstellen eines ODBC-Ziels mit der Skriptkomponente
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], Sie speichern in der Regel Daten in einer ODBC-Ziel mithilfe einer [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Ziel und die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieter für ODBC. Sie können jedoch auch ein Ad-hoc-ODBC-Ziel für die Verwendung in einem einzelnen Paket erstellen. Zur Erstellung dieses Ad-hoc-ODBC-Ziels verwenden Sie die Skriptkomponente, wie in dem folgenden Beispiel dargestellt.  
  
> [!NOTE]  
>  Wenn Sie eine Komponente erstellen möchten, die Sie einfacher in mehreren Datenflusstasks und Paketen wiederverwenden können, empfiehlt es sich, den Code in diesem Skriptkomponentenbeispiel als Ausgangspunkt für eine benutzerdefinierte Datenflusskomponente zu verwenden. Weitere Informationen finden Sie unter [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie eine Zielkomponente, die einen vorhandenen ODBC verwendet Verbindungs-Manager zum Speichern von Daten aus dem Datenfluss in einem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle.  
  
 In diesem Beispiel ist eine geänderte Version des benutzerdefinierten [!INCLUDE[vstecado](../../includes/vstecado-md.md)] Ziel, das im Thema veranschaulicht wurde [Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). In diesem Beispiel wurde das benutzerdefinierte [!INCLUDE[vstecado](../../includes/vstecado-md.md)]-Ziel jedoch so geändert, dass es mit einem ODBC-Verbindungs-Manager funktioniert und Daten in einem ODBC-Ziel speichert. Die Modifizierungen umfassen die folgenden Änderungen:  
  
-   Sie können nicht Aufrufen der **AcquireConnection** Methode des ODBC-Verbindungs-Managers aus verwaltetem Code, da es sich um ein systemeigenes Objekt zurückgegeben. In diesem Beispiel wird daher die Verbindungszeichenfolge des Verbindungs-Managers verwendet, um eine direkte Verbindung mit der Datenquelle mithilfe des verwalteten ODBC-[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Datenanbieters herzustellen.  
  
-   Die **"OdbcCommand"** Positionsparameter erwartet. Die Position von Parametern wird durch die Fragezeichen (?) im Text des Befehls angegeben. (Im Gegensatz dazu eine **"SqlCommand"** benannte Parameter erwartet.)  
  
 Dieses Beispiel verwendet die **Person.Address** -Tabelle in der **AdventureWorks** -Beispieldatenbank. Das Beispiel übergibt die erste und vierte Spalte, die  **Int*AddressID*** und **Nvarchar (30) City** Spalten dieser Tabelle durch den Datenfluss. Diese Daten werden in der Quelle, Transformation und zielbeispielen in diesem Thema, [Entwickeln von bestimmten Arten von Skriptkomponenten](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
#### <a name="to-configure-this-script-component-example"></a>So konfigurieren Sie dieses Skriptkomponentenbeispiel  
  
1.  Erstellen einer ODBC-Verbindungs-Manager die Herstellung der **AdventureWorks** Datenbank.  
  
2.  Erstellen Sie eine Zieltabelle mit dem folgenden Transact-SQL-Befehl der **AdventureWorks** Datenbank:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Fügen Sie der Oberfläche des Datenfluss-Designers eine neue Skriptkomponente hinzu, und konfigurieren Sie sie als Ziel.  
  
4.  Verbinden Sie die Ausgabe einer Upstreamquelle oder Transformation mit der Zielkomponente im [!INCLUDE[ssIS](../../includes/ssis-md.md)]-Designer. (Sie können eine Quelle ohne Transformationen direkt mit einem Ziel verbinden.) Um sicherzustellen, dass dieses Beispiel funktioniert, muss die Ausgabe der upstreamkomponente enthalten mindestens die **AddressID** und **City** Spalten aus der **Person.Address** Tabelle mit den **AdventureWorks** -Beispieldatenbank.  
  
5.  Öffnen der **Skript Transformations-Editor**. Auf der **Eingabespalten** Seite der **AddressID** und **City** Spalten.  
  
6.  Auf der **Eingaben und Ausgaben** Seite, benennen Sie die Eingabe einen aussagekräftigeren Namen wie z. B. **"myaddressinput"**.  
  
7.  Auf der **Verbindungs-Manager** Seite, hinzufügen oder Erstellen der ODBC-Verbindungs-Manager mit einem aussagekräftigen Namen wie z. B. **"myodbcconnectionmanager"**.  
  
8.  Auf der **Skript** auf **Bearbeitungsskript**, und geben Sie dann das folgende Skript in die **ScriptMain** Klasse.  
  
9. Schließen Sie die skriptentwicklungsumgebung, schließen die **Skript Transformations-Editor**, und führen Sie das Beispiel.  
  
    ```vb  
    Imports System.Data.Odbc  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim odbcConn As OdbcConnection  
        Dim odbcCmd As OdbcCommand  
        Dim odbcParam As OdbcParameter  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connectionString As String  
            connectionString = Me.Connections.MyODBCConnectionManager.ConnectionString  
            odbcConn = New OdbcConnection(connectionString)  
            odbcConn.Open()  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            odbcCmd = New OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
                "VALUES(?, ?)", odbcConn)  
            odbcParam = New OdbcParameter("@addressid", OdbcType.Int)  
            odbcCmd.Parameters.Add(odbcParam)  
            odbcParam = New OdbcParameter("@city", OdbcType.NVarChar, 30)  
            odbcCmd.Parameters.Add(odbcParam)  
  
        End Sub  
  
        Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
            With odbcCmd  
                .Parameters("@addressid").Value = Row.AddressID  
                .Parameters("@city").Value = Row.City  
                .ExecuteNonQuery()  
            End With  
  
        End Sub  
  
        Public Overrides Sub ReleaseConnections()  
  
            odbcConn.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.Data.Odbc;  
    ...  
    public class ScriptMain :  
        UserComponent  
    {  
        OdbcConnection odbcConn;  
        OdbcCommand odbcCmd;  
        OdbcParameter odbcParam;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            string connectionString;  
            connectionString = this.Connections.MyODBCConnectionManager.ConnectionString;  
            odbcConn = new OdbcConnection(connectionString);  
            odbcConn.Open();  
  
        }  
  
        public override void PreExecute()  
        {  
  
            odbcCmd = new OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " +  
                "VALUES(?, ?)", odbcConn);  
            odbcParam = new OdbcParameter("@addressid", OdbcType.Int);  
            odbcCmd.Parameters.Add(odbcParam);  
            odbcParam = new OdbcParameter("@city", OdbcType.NVarChar, 30);  
            odbcCmd.Parameters.Add(odbcParam);  
  
        }  
  
        public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
        {  
  
            {  
                odbcCmd.Parameters["@addressid"].Value = Row.AddressID;  
                odbcCmd.Parameters["@city"].Value = Row.City;  
                odbcCmd.ExecuteNonQuery();  
            }  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            odbcConn.Close();  
  
        }  
    }  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Ziels mit der Skriptkomponente](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  

