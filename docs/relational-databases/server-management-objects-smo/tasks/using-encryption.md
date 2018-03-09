---
title: "Verwenden der Verschlüsselung | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database master key [SMO]
- cryptography [SMO]
- cryptography [SQL Server], SMO
- encryption keys [SMO]
- encryption [SQL Server], SMO
- encryption [SMO]
- certificates [SMO]
- service master key [SMO]
ms.assetid: 405e0ed7-50a9-430e-a343-471f54b4af76
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad74e5242702ace386fb8c14a034a56886f27191
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="using-encryption"></a>Verwenden der Verschlüsselung
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In SMO wird der Diensthauptschlüssel durch dargestellt die <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> Objekt. Dies verweist auf die <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> Eigenschaft von der <xref:Microsoft.SqlServer.Management.Smo.Server> Objekt. Es kann erneut generiert werden, mithilfe der <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A> Methode.  
  
 Datenbank-Hauptschlüssels wird dargestellt, indem die <xref:Microsoft.SqlServer.Management.Smo.MasterKey> Objekt. Die <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> Eigenschaft gibt an, und zwar unabhängig davon, ob die Datenbank-Hauptschlüssel mit dem Diensthauptschlüssel verschlüsselt ist. Die verschlüsselte Kopie in der Hauptdatenbank wird immer dann automatisch aktualisiert, wenn der Datenbank-Hauptschlüssel geändert wird.  
  
 Es ist möglich, drop Service Schlüsselverschlüsselung mithilfe der <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> Methode und die Datenbank-Hauptschlüssel mit einem Kennwort verschlüsseln. In diesem Fall müssen Sie den Datenbank-Hauptschlüssel explizit öffnen, bevor Sie auf die privaten Schlüssel zugreifen, die von diesem gesichert wurden.  
  
 Wenn eine Datenbank mit einer Instanz von angehängt wird [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], müssen Sie das Kennwort für den Datenbank-Hauptschlüssel bereitstellen oder Ausführen der <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> Methode, um eine unverschlüsselte Kopie des Datenbank-Hauptschlüssels für die Verschlüsselung mit dem Dienst verfügbar machen Hauptschlüssel. Dieser Schritt wird empfohlen, um zu vermeiden, dass der Datenbank-Hauptschlüssel explizit geöffnet werden muss.  
  
 Die <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> Methode generiert den Datenbank-Hauptschlüssel neu. Wenn der Datenbank-Hauptschlüssel neu generiert wird, werden alle Schlüssel, die durch den Datenbank-Hauptschlüssel verschlüsselt wurden, entschlüsselt. Daraufhin werden diese mit dem neuen Datenbank-Hauptschlüssel verschlüsselt. Die <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> Methode entfernt die Verschlüsselung des Datenbank-Hauptschlüssels durch den Diensthauptschlüssel. Mit <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> wird eine Kopie des Hauptschlüssels mithilfe des Diensthauptschlüssels verschlüsselt und in der aktuellen Datenbank und in der Masterdatenbank gespeichert.  
  
 In SMO werden Zertifikate dargestellt werden, durch die <xref:Microsoft.SqlServer.Management.Smo.Certificate> Objekt. Die <xref:Microsoft.SqlServer.Management.Smo.Certificate> Objekt verfügt über Eigenschaften, die den öffentlichen Schlüssel, der Name des Antragstellers, Zeitraum Gültigkeitsdauer und Informationen über den Aussteller festlegen. Die Berechtigung, auf das Zertifikat zuzugreifen, wird über die Methoden **Grant**, **Revoke** und **Deny** gesteuert.  
  
## <a name="example"></a>Beispiel  
 Für die folgenden Codebeispiele müssen Sie die Programmierungsumgebung, die Programmiervorlage und die Programmiersprache auswählen, um Ihre Anwendung zu erstellen. Weitere Informationen finden Sie unter [Erstellen eines Visual C &#35; SMO-Projekts in Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="adding-a-certificate-in-visual-c"></a>Hinzufügen eines Zertifikats in Visual C#  
 Im Codebeispiel wird ein einfaches Zertifikat mit einem Verschlüsselungskennwort erstellt. Im Gegensatz zu anderen Objekten die <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> -Methode weist mehrere Überladungen. Die im Beispiel verwendete Überladung erstellt ein Zertifikat mit einem Verschlüsselungskennwort.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            {  
                Server srv = new Server();  
  
                //Reference the AdventureWorks2012 database.   
                Database db = srv.Databases["AdventureWorks2012"];  
  
                //Define a Certificate object variable by supplying the parent database and name in the constructor.   
                Certificate c = new Certificate(db, "Test_Certificate");  
  
                //Set the start date, expiry date, and description.   
                System.DateTime dt;  
                DateTime.TryParse("January 01, 2010", out dt);  
                c.StartDate = dt;  
                DateTime.TryParse("January 01, 2015", out dt);  
                c.ExpirationDate = dt;  
                c.Subject = "This is a test certificate.";  
                //Create the certificate on the instance of SQL Server by supplying the certificate password argument.   
                c.Create("pGFD4bb925DGvbd2439587y");  
            }  
        }   
```  
  
## <a name="adding-a-certificate-in-powershell"></a>Hinzufügen eines Zertifikats in PowerShell  
 Im Codebeispiel wird ein einfaches Zertifikat mit einem Verschlüsselungskennwort erstellt. Im Gegensatz zu anderen Objekten die <xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> -Methode weist mehrere Überladungen. Die im Beispiel verwendete Überladung erstellt ein Zertifikat mit einem Verschlüsselungskennwort.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
#Create a certificate  
  
$c = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Certificate -argumentlist $db, "Test_Certificate"  
$c.StartDate = "January 01, 2010"  
$c.Subject = "This is a test certificate."  
$c.ExpirationDate = "January 01, 2015"  
  
#Create the certificate on the instance of SQL Server by supplying the certificate password argument.  
$c.Create("pGFD4bb925DGvbd2439587y")  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Unter Verwendung von Verschlüsselungsschlüsseln](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)  
  
  
