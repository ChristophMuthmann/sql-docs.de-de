---
title: GET_FILESTREAM_TRANSACTION_CONTEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GET_FILESTREAM_TRANSACTION_CONTEXT_TSQL
- GET_FILESTREAM_TRANSACTION_CONTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- GET_FILESTREAM_TRANSACTION_CONTEXT FILESTREAM [SQL Server]
ms.assetid: 459e6b79-4420-41e6-85bf-89d90f43b4f1
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5ba8077d0df80044a66da4863bba1dd603d369f
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="getfilestreamtransactioncontext-transact-sql"></a>GET_FILESTREAM_TRANSACTION_CONTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt ein Token zurück, das den aktuellen Transaktionskontext einer Sitzung darstellt. Eine Anwendung verwendet dieses Token, um FILESTREAM-Dateisystem-Streamingvorgänge an die Transaktion zu binden. Eine Liste der FILESTREAM-Themen finden Sie [Binary Large Object &#40; BLOB &#41; Daten &#40; SQLServer &#41; ](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GET_FILESTREAM_TRANSACTION_CONTEXT ()  
```  
  
## <a name="return-type"></a>Rückgabetyp  
 **varbinary(max)**  
  
## <a name="return-value"></a>Rückgabewert  
 NULL wird zurückgegeben, wenn die Transaktion nicht gestartet wurde, wenn sie abgebrochen wurde oder wenn ein Commit durchgeführt wurde.  
  
## <a name="remarks"></a>Hinweise  
 Die Transaktion muss explizit sein. Verwenden Sie BEGIN TRANSACTION gefolgt von COMMIT TRANSACTION oder ROLLBACK TRANSACTION.  
  
 Wenn Sie GET_FILESTREAM_TRANSACTION_CONTEXT aufrufen, wird dem Aufrufer für die Dauer der Transaktion Zugriff auf das Dateisystem für die Transaktion gewährt. Um einem anderen Benutzer den Zugriff auf die Transaktion über das Dateisystem zu ermöglichen, verwenden Sie EXECUTE AS, um GET_FILESTREAM_TRANSACTION_CONTEXT als dieser andere Benzutzer auszuführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird `GET_FILESTREAM_TRANSACTION_CONTEXT` in einem [!INCLUDE[tsql](../../includes/tsql-md.md)] Transaktion an den Transaktionskontext abzurufen.  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using System.Data;  
  
namespace ConsoleApplication  
{  
    /// <summary>  
    /// This class is a wrapper that contains methods for:  
    ///   
    ///     GetTransactionContect() - Returns the current transaction context.  
    ///     BeginTransaction() - Begins a transaction.  
    ///     CommmitTransaction() - Commits the current transaction.  
    ///   
    /// </summary>  
  
    class SqlAccessWrapper  
    {  
        /// <summary>  
        /// Returns a byte array that contains the current transaction  
        /// context.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the instance of SQL Server  
        /// from which to obtain the transaction context.   
        /// </param>  
        /// <returns>  
        /// If there is a current transaction context, the return  
        /// value is an Object that represents the context.  
        /// If there is not a current transaction context, the  
        /// value returned is DBNull.Value.  
        /// </returns>  
  
        public Object GetTransactionContext(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
            cmd.CommandText = "SELECT GET_FILESTREAM_TRANSACTION_CONTEXT()";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            return cmd.ExecuteScalar();  
  
        }  
  
        /// <summary>  
        /// Begins the transaction.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the server  
        /// on which to run the BEGIN TRANSACTION statement.  
        /// </param>  
  
        public void BeginTransaction(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
  
            cmd.CommandText = "BEGIN TRANSACTION";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            cmd.ExecuteNonQuery();  
        }  
  
        /// <summary>  
        /// Commits the transaction.  
        /// </summary>  
        /// <param name="sqlConnection">  
        /// SqlConnection object that represents the instance of SQL Server  
        /// on which to run the COMMIT statement.  
        /// </param>  
  
        public void CommitTransaction(SqlConnection sqlConnection)  
        {  
            SqlCommand cmd = new SqlCommand();  
  
            cmd.CommandText = "COMMIT TRANSACTION";  
            cmd.CommandType = CommandType.Text;  
            cmd.Connection = sqlConnection;  
  
            cmd.ExecuteNonQuery();  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            //Open a connection to the local instance of SQL Server.  
  
            SqlConnection sqlConnection = new SqlConnection("Integrated Security=true;server=(local)");  
            sqlConnection.Open();  
  
            SqlAccessWrapper sql = new SqlAccessWrapper();  
  
            //Create a transaction so that sql.GetTransactionContext() will succeed.  
            sql.BeginTransaction(sqlConnection);  
  
            //The transaction context will be stored in this array.  
            Byte[] transactionToken;     
  
            Object txObj = sql.GetTransactionContext(sqlConnection);  
            if (DBNull.Value != txObj)  
            {  
                transactionToken = (byte[])txObj;  
                Console.WriteLine("Transaction context obtained.\n");  
            }  
  
            sql.CommitTransaction(sqlConnection);  
        }  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data  
  
Namespace ConsoleApplication  
    ''' <summary>   
    ''' This class is a wrapper that contains methods for:   
    '''   
    ''' GetTransactionContect() - Returns the current transaction context.   
    ''' BeginTransaction() - Begins a transaction.   
    ''' CommmitTransaction() - Commits the current transaction.   
    '''   
    ''' </summary>   
  
    Class SqlAccessWrapper  
        ''' <summary>   
        ''' Returns a byte array that contains the current transaction   
        ''' context.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the instance of SQL Server   
        ''' from which to obtain the transaction context.   
        ''' </param>   
        ''' <returns>   
        ''' If there is a current transaction context, the return   
        ''' value is an Object that represents the context.   
        ''' If there is not a current transaction context, the   
        ''' value returned is DBNull.Value.   
        ''' </returns>   
  
        Public Function GetTransactionContext(ByVal sqlConnection As SqlConnection) As Object  
            Dim cmd As New SqlCommand()  
            cmd.CommandText = "SELECT GET_FILESTREAM_TRANSACTION_CONTEXT()"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            Return cmd.ExecuteScalar()  
  
        End Function  
  
        ''' <summary>   
        ''' Begins the transaction.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the server   
        ''' on which to run the BEGIN TRANSACTION statement.   
        ''' </param>   
  
        Public Sub BeginTransaction(ByVal sqlConnection As SqlConnection)  
            Dim cmd As New SqlCommand()  
  
            cmd.CommandText = "BEGIN TRANSACTION"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            cmd.ExecuteNonQuery()  
        End Sub  
  
        ''' <summary>   
        ''' Commits the transaction.   
        ''' </summary>   
        ''' <param name="sqlConnection">   
        ''' SqlConnection object that represents the instance of SQL Server   
        ''' on which to run the COMMIT statement.   
        ''' </param>   
  
        Public Sub CommitTransaction(ByVal sqlConnection As SqlConnection)  
            Dim cmd As New SqlCommand()  
  
            cmd.CommandText = "COMMIT TRANSACTION"  
            cmd.CommandType = CommandType.Text  
            cmd.Connection = sqlConnection  
  
            cmd.ExecuteNonQuery()  
        End Sub  
    End Class  
  
    Class Program  
        Shared Sub Main()  
            '''Open a connection to the local instance of SQL Server.  
  
            Dim sqlConnection As New SqlConnection("Integrated Security=true;server=(local)")  
            sqlConnection.Open()  
  
            Dim sql As New SqlAccessWrapper()  
  
            '''Create a transaction so that sql.GetTransactionContext() will succeed.   
            sql.BeginTransaction(sqlConnection)  
  
            '''The transaction context will be stored in this array.   
            Dim transactionToken As Byte()  
  
            Dim txObj As Object = sql.GetTransactionContext(sqlConnection)  
  
            '''If the returned object is not NULL, there is a valid transaction  
            '''token, and it must be converted into a format that is usable within  
            '''the application.  
  
            If Not txObj.Equals(DBNull.Value) Then  
                transactionToken = DirectCast(txObj, Byte())  
                Console.WriteLine("Transaction context obtained." & Chr(10) & "")  
            End If  
  
            sql.CommitTransaction(sqlConnection)  
        End Sub  
    End Class  
End Namespace  
```  
  
## <a name="see-also"></a>Siehe auch  
 [PathName &#40; Transact-SQL &#41;](../../relational-databases/system-functions/pathname-transact-sql.md)   
 [Binary Large Object &#40;Blob&#41; Daten &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  
  
  
