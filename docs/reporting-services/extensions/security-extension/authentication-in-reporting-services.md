---
title: Authentifizierung in Reporting Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], authentication
- forms-based authentication [Reporting Services]
- authentication [Reporting Services]
- custom authentication [Reporting Services]
ms.assetid: 103ce1f9-31d8-44bb-b540-2752e4dcf60b
caps.latest.revision: "25"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8cb93e668b5b9ebec50e1f97aafc680507470cdb
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="authentication-in-reporting-services"></a>Authentifizierung in Reporting Services
  Unter Authentifizierung versteht man den Prozess, Benutzerrechte für eine bestimmte Identität einzurichten. Es gibt viele Techniken, die Sie verwenden können, um einen Benutzer zu authentifizieren. Die gängigste Methode ist die Verwendung von Kennwörtern. Wenn Sie beispielsweise die Formularauthentifizierung implementieren, benötigen Sie eine Implementierung, bei der die Benutzer nach den Anmeldeinformationen durchsucht werden (normalerweise über eine Oberfläche, in der Anmeldename und Kennwort angefordert werden) und bei der die Benutzer mit einem Datenspeicher, z. B. einer Datenbanktabelle oder einer Konfigurationsdatei, abgeglichen werden. Wenn die Anmeldeinformationen nicht validiert werden können, schlägt der Authentifizierungsprozess fehl, und der Benutzer nimmt eine anonyme Identität an.  
  
## <a name="custom-authentication-in-reporting-services"></a>Benutzerdefinierte Authentifizierung in den Reporting Services  
 In [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] behandelt das Windows-Betriebssystem die Benutzerauthentifizierung entweder über integrierte Sicherheitsfunktionen oder über die ausdrückliche Annahme und Validierung der Anmeldeinformationen des Benutzers. Die benutzerdefinierte Authentifizierung kann in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] so entwickelt werden, dass zusätzliche Authentifizierungsschemen unterstützt werden. Dies wird durch die Sicherheitserweiterungsschnittstelle <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> ermöglicht. Alle Erweiterungen erben für jede vom Berichtsserver bereitgestellte und verwendete Erweiterung von der <xref:Microsoft.ReportingServices.Interfaces.IExtension>-Basisschnittstelle. <xref:Microsoft.ReportingServices.Interfaces.IExtension> und <xref:Microsoft.ReportingServices.Interfaces.IAuthenticationExtension2> sind Elemente des <xref:Microsoft.ReportingServices.Interfaces>-Namespace.  
  
 Die primäre Möglichkeit, auf einem Berichtsserver in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] authentifiziert zu werden, ist die <xref:ReportService2010.ReportingService2010.LogonUser%2A>-Methode. Dieses Element des Reporting Services-Webdiensts kann verwendet werden, um die Benutzeranmeldeinformationen zur Validierung an einen Berichtsserver zu übergeben. Die zugrunde liegende Sicherheitserweiterung implementiert **IAuthenticationExtension2.LogonUser**, das den benutzerdefinierten Authentifizierungscode enthält. Im Beispiel zur Formularauthentifizierung wird mit **LogonUser** eine Authentifizierungsprüfung der angegebenen Anmeldeinformationen und eines benutzerdefinierten Benutzerspeichers in einer Datenbank durchgeführt. Ein Beispiel für die Implementierung von **LogonUser** sieht folgendermaßen aus:  
  
```  
public bool LogonUser(string userName, string password, string authority)  
{  
   return AuthenticationUtilities.VerifyPassword(userName, password);  
}  
  
```  
  
 Die folgende Beispielfunktion wird verwendet, um die angegebenen Anmeldeinformationen zu überprüfen:  
  
```  
  
internal static bool VerifyPassword(string suppliedUserName,  
   string suppliedPassword)  
{   
   bool passwordMatch = false;  
   // Get the salt and pwd from the database based on the user name.  
   // See "How To: Use DPAPI (Machine Store) from ASP.NET," "How To:  
   // Use DPAPI (User Store) from Enterprise Services," and "How To:  
   // Create a DPAPI Library" for more information about how to use  
   // DPAPI to securely store connection strings.  
   SqlConnection conn = new SqlConnection(  
      "Server=localhost;" +   
      "Integrated Security=SSPI;" +  
      "database=UserAccounts");  
   SqlCommand cmd = new SqlCommand("LookupUser", conn);  
   cmd.CommandType = CommandType.StoredProcedure;  
  
   SqlParameter sqlParam = cmd.Parameters.Add("@userName",  
       SqlDbType.VarChar,  
       255);  
   sqlParam.Value = suppliedUserName;  
   try  
   {  
      conn.Open();  
      SqlDataReader reader = cmd.ExecuteReader();  
      reader.Read(); // Advance to the one and only row  
      // Return output parameters from returned data stream  
      string dbPasswordHash = reader.GetString(0);  
      string salt = reader.GetString(1);  
      reader.Close();  
      // Now take the salt and the password entered by the user  
      // and concatenate them together.  
      string passwordAndSalt = String.Concat(suppliedPassword, salt);  
      // Now hash them  
      string hashedPasswordAndSalt =  
         FormsAuthentication.HashPasswordForStoringInConfigFile(  
         passwordAndSalt,  
         "SHA1");  
      // Now verify them. Returns true if they are equal.  
      passwordMatch = hashedPasswordAndSalt.Equals(dbPasswordHash);  
   }  
   catch (Exception ex)  
   {  
       throw new Exception("Exception verifying password. " +  
          ex.Message);  
   }  
   finally  
   {  
       conn.Close();  
   }  
   return passwordMatch;  
}  
```  
  
## <a name="authentication-flow"></a>Authentifizierungsablauf  
 Der Reporting Services-Webdienst verfügt über benutzerdefinierte Authentifizierungserweiterungen, um eine Formularauthentifizierung durch das Webportal und den Berichtsserver zu ermöglichen.  
  
 Mit der <xref:ReportService2010.ReportingService2010.LogonUser%2A>-Methode des Reporting Services Webdiensts werden dem Berichtsserver die Anmeldeinformationen zur Authentifizierung vorgelegt. Der Webdienst verwendet HTTP-Header, um für validierte Anmeldeanforderungen ein Authentifizierungsticket („Cookie“) vom Server an den Client zu übergeben.  
  
 In folgender Abbildung sehen Sie die Methode, wie Benutzer im Webdienst authentifiziert werden, wenn Ihre Anwendung mit einem Berichtsserver eingesetzt wird, der für die Verwendung einer benutzerdefinierten Authentifizierungserweiterung konfiguriert ist.  
  
 ![Reporting Services-Sicherheitsauthentifizierungsfluss](../../../reporting-services/extensions/security-extension/media/rosettasecurityextensionauthenticationflow.gif "Reporting Services security authentication flow")  
  
 Wie in Abbildung 2 gezeigt, sieht der Authentifizierungsprozess folgendermaßen aus:  
  
1.  Eine Clientanwendung ruft die Webdienstmethode <xref:ReportService2010.ReportingService2010.LogonUser%2A> auf, um einen Benutzer zu authentifizieren.  
  
2.  Der Webdienst ruft die Methode <xref:ReportService2010.ReportingService2010.LogonUser%2A> Ihrer Sicherheitserweiterung auf, genauer gesagt die Klasse, von der **IAuthenticationExtension2** implementiert wird.  
  
3.  Die Implementierung von <xref:ReportService2010.ReportingService2010.LogonUser%2A> überprüft den Benutzernamen und das Kennwort im Benutzerspeicher oder in der Sicherheitsinstanz.  
  
4.  Nach der erfolgreichen Authentifizierung erstellt der Webdienst ein Cookie und verwaltet es für die Sitzung.  
  
5.  Der Webdienst gibt das Authentifizierungsticket an die aufrufende Anwendung im HTTP-Header zurück.  
  
 Hat der Webdienst einen Benutzer erfolgreich über die Sicherheitserweiterung authentifiziert, generiert er ein Cookie, das für nachfolgende Anforderungen verwendet wird. Das Cookie wird möglicherweise nicht persistent mit der benutzerdefinierten Sicherheitsinstanz gespeichert, da der Berichtsserver über keine eigene Sicherheitsinstanz verfügt. Das Cookie wird von der Webdienstmethode <xref:ReportService2010.ReportingService2010.LogonUser%2A> zurückgegeben und wird in Folgeaufrufen der Webdienstmethode und beim URL-Zugriff verwendet.  
  
> [!NOTE]  
>  Um zu verhindern, dass das Cookie während der Übertragung beschädigt wird, sollten Authentifizierungscookies, die von <xref:ReportService2010.ReportingService2010.LogonUser%2A> zurückgegeben werden, über SSL-Verschlüsselung (Secure Sockets Layer) verschlüsselt werden.  
  
 Wenn Sie einen Berichtsserver über URL-Zugriff aufrufen, während eine benutzerdefinierte Sicherheitserweiterung installiert ist, verwalten IIS (Internet Information Services) und [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] die Übertragung des Authentifizierungstickets automatisch. Wenn Sie über die SOAP-API auf den Berichtsserver zugreifen, muss Ihre Implementierung der Proxyklasse zusätzliche Unterstützung für die Verwaltung des Authentifizierungstickets enthalten. Weitere Informationen zur Verwendung der SOAP-API und zur Verwendung des Authentifizierungstickets finden Sie unter „Verwenden des Webdiensts mit benutzerdefinierter Sicherheit“.  
  
## <a name="forms-authentication"></a>Formularauthentifizierung  
 Die Formularauthentifizierung ist eine Art der [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]-Authentifizierung, bei der ein authentifizierter Benutzer zu einem HTML-Formular geleitet wird. Sobald der Benutzer seine Anmeldeinformationen angibt, gibt das System ein Cookie aus, das ein Authentifizierungsticket enthält. Bei späteren Anforderungen prüft das System zuerst das Cookie, um festzustellen, ob der Benutzer bereits durch den Berichtsserver authentifiziert wurde.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] kann so erweitert werden, dass die Formularauthentifizierung unterstützt wird. Hierzu werden Sicherheitserweiterungsschnittstellen verwendet, die über die Reporting Services-API zur Verfügung gestellt werden. Wenn Sie [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] so erweitern, dass die Formularauthentifizierung verwendet wird, verwenden Sie für die gesamte Kommunikation mit dem Berichtsserver SSL (Secure Sockets Layer), damit sich unberechtigte Benutzer keinen Zugang auf das Cookie eines anderen Benutzers verschaffen können. SSL ermöglicht Clients und dem Berichtsserver eine gegenseitige Authentifizierung, um sicherzustellen, dass keine anderen Computer den Inhalt der Kommunikation zwischen zwei Computern lesen können. Alle Daten, die über SSL-Verbindung von einem Client versendet werden, sind verschlüsselt, sodass unberechtigte Benutzer an den Berichtsserver gesandte Kennwörter und Daten nicht abfangen können.  
  
 Die Formularauthentifizierung wird normalerweise implementiert, um Konten und die Authentifizierung für Nicht-Windows-Plattformen zu unterstützen. Einem Benutzer, der auf einen Berichtsserver zugreifen möchte, wird eine grafische Oberfläche angezeigt, und die angegebenen Anmeldeinformationen werden zur Authentifizierung an eine Sicherheitsinstanz übergeben.  
  
 Bei der Formularauthentifizierung muss eine Person anwesend sein, um die Anmeldeinformationen einzugeben. Bei unbeaufsichtigten Anwendungen, die direkt mit dem Reporting Services-Webdienst kommunizieren, muss die Formularauthentifizierung mit einem benutzerdefinierten Authentifizierungsschema kombiniert werden.  
  
 Die Formularauthentifizierung ist für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] in folgenden Fällen geeignet:  
  
-   Sie müssen Benutzer speichern und authentifizieren, die keine [!INCLUDE[msCoName](../../../includes/msconame-md.md)]-Windows-Konten haben, und  
  
-   Sie müssen Ihr eigenes Benutzeroberflächenformular als Anmeldeseite zwischen den verschiedenen Seiten auf einer Website angeben.  
  
 Beachten Sie Folgendes, wenn Sie eine benutzerdefinierte Sicherheitserweiterung schreiben, die die Formularauthentifizierung unterstützt:  
  
-   Wenn Sie die Formularauthentifizierung verwenden, muss der anonyme Zugriff auf dem virtuellen Verzeichnis des Berichtsservers in IIS (Internet Information Services) aktiviert sein.  
  
-   Die [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]-Authentifizierung muss auf „Formular“ eingestellt sein. Sie konfigurieren die [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]-Authentifizierung für den Berichtsserver in der Datei Web.config.  
  
-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] kann Benutzer entweder über die Windows-Authentifizierung oder die benutzerdefinierte Authentifizierung authentifizieren, jedoch nicht über beide. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] unterstützt nicht die gleichzeitige Verwendung von mehreren Sicherheitserweiterungen.  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von Sicherheitserweiterungen](../../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
  
  
