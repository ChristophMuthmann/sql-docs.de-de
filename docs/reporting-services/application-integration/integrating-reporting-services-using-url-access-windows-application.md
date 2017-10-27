---
title: Verwenden von URL-Zugriff in einer Windows-Anwendung | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Windows applications [Reporting Services]
- Web Browser controls [Reporting Services]
- Windows Forms [Reporting Services]
- browser controls [Reporting Services]
- URL access [Reporting Services], Windows applications
ms.assetid: a4b222e5-0cbd-409c-92c4-046a674db8ac
caps.latest.revision: 48
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 782be214cb491e1fdddf6ff7d45ac377fcfbf8a4
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="integrating-reporting-services-using-url-access---windows-application"></a>Integrieren von Reporting Services mit URL-Zugriff - Windows-Anwendung
  Obwohl der URL-Zugriff auf einen Berichtsserver für eine Webumgebung optimiert ist, können Sie mit dem URL-Zugriff auch [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Berichte in eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anwendung integrieren. Aber der URL-Zugriff, der auch Windows Forms umfasst, erfordert trotzdem die Verwendung der Webbrowsertechnologie. Sie können folgende Integrationsszenarien mit dem URL-Zugriff und Windows Forms verwenden:  
  
-   Zeigen Sie einen Bericht in einer Windows Forms-Anwendung an, indem Sie einen Webbrowser programmgesteuert starten.  
  
-   Verwenden Sie das <xref:System.Windows.Forms.WebBrowser>-Steuerelement auf einer Windows Form, um einen Bericht anzuzeigen.  
  
## <a name="starting-internet-explorer-from-a-windows-form"></a>Starten von Internet Explorer von einer Windows Form  
 Sie können über die <xref:System.Diagnostics.Process>-Klasse auf einen Prozess zugreifen, der auf einem Computer ausgeführt wird. Die <xref:System.Diagnostics.Process> -Klasse ist ein nützliches [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Konstrukt zum Starten, beenden, steuern und Überwachen von Anwendungen. Um einen bestimmten Bericht in der Berichtsserver-Datenbank anzuzeigen, starten Sie den **"Iexplore"** Prozess, in der URL für den Bericht übergeben. Folgendes Codebeispiel kann verwendet werden, um [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer zu starten und eine spezielle URL zu übergeben, wenn ein Benutzer auf eine Schaltfläche in einer Windows Form klickt.  
  
```vb  
Private Sub viewReportButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles viewReportButton.Click  
   ' Build the URL access string based on values supplied by a user  
   Dim url As String = serverUrlTextBox.Text + "?" & reportPathTextBox.Text & _  
   "&rs:Command=Render" & "&rs:Format=HTML4.0"  
  
   ' If the user does not select the toolbar check box,  
   ' turn the toolbar off in the HTML Viewer  
   If toolbarCheckBox.Checked = False Then  
      url += "&rc:Toolbar=False"  
   End If  
   ' load report in the Web browser  
   Try  
      System.Diagnostics.Process.Start("IExplore", url)  
   Catch  
      MessageBox.Show("The system could not start the specified report using Internet Explorer.", _  
      "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error)  
   End Try  
End Sub 'viewReportButton_Click  
```  
  
```csharp  
// Sample click event for a Button control on a Windows Form  
private void viewReportButton_Click(object sender, System.EventArgs e)  
{  
   // Build the URL access string based on values supplied by a user  
   string url = serverUrlTextBox.Text + "?" + reportPathTextBox.Text +  
      "&rs:Command=Render" + "&rs:Format=HTML4.0";  
  
   // If the user does not check the toolbar check box,  
   // turn the toolbar off in the HTML Viewer  
   if (toolbarCheckBox.Checked == false)  
      url += "&rc:Toolbar=False";  
  
   // load report in the Web browser  
   try  
   {  
      System.Diagnostics.Process.Start("IExplore", url);  
   }  
  
   catch (Exception)  
   {  
      MessageBox.Show(  
         "The system could not open the specified report using Internet Explorer.",   
         "An error has occurred", MessageBoxButtons.OK, MessageBoxIcon.Error);  
   }  
}  
```  
  
## <a name="embedding-a-browser-control-on-a-windows-form"></a>Integrieren eines Browsersteuerelements auf einer Windows Form  
 Wenn Sie den Bericht nicht in einem externen Webbrowser anzeigen möchten, können Sie einen Webbrowser nahtlos als Teil der Windows Form integrieren, indem Sie das <xref:System.Windows.Forms.WebBrowser>-Steuerelement verwenden.  
  
###### <a name="to-add-the-webbrowser-control-to-your-windows-form"></a>So fügen Sie der Windows Form das Webbrowser-Steuerelement hinzu  
  
1.  Erstellen Sie eine neue Windows-Anwendung – entweder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
2.  Suchen Sie die <xref:System.Windows.Forms.WebBrowser> steuern, der **Toolbox** (Dialogfeld).  
  
     Wenn die **Toolbox** ist nicht sichtbar. Sie erreichen sie durch Klicken auf die **Ansicht** Menüelement und Auswählen von **Toolbox**.  
  
3.  Ziehen Sie die <xref:System.Windows.Forms.WebBrowser>Steuerelement auf die Entwurfsoberfläche der Windows Form.  
  
     Die <xref:System.Windows.Forms.WebBrowser>mit dem Namen webBrowser1 Steuerelement dem Formular hinzugefügt wird  
  
 Sie leiten die <xref:System.Windows.Forms.WebBrowser> Steuerelement an eine URL durch Aufrufen seiner **navigieren** Methode. Sie können dem <xref:System.Windows.Forms.WebBrowser>-Steuerelement zur Laufzeit eine bestimmte URL-Zugriffszeichenfolge zuordnen, wie in folgendem Beispiel gezeigt.  
  
```vb  
Dim url As String = "http://localhost/reportserver?/" & _  
                    "AdventureWorks2012 Sample Reports/" & _  
                    "Company Sales&rs:Command=Render"  
WebBrowser1.Navigate(url)  
```  
  
```csharp  
string url = "http://localhost/reportserver?/" +  
             "AdventureWorks2012 Sample Reports/" +  
             "Company Sales&rs:Command=Render";  
webBrowser1.Navigate(url);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Integrieren von Reporting Services in Anwendungen](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Integrieren von Reporting Services mit URL-Zugriff](../../reporting-services/application-integration/integrating-reporting-services-using-url-access.md)   
 [Integrieren von Reporting Services mit SOAP](../../reporting-services/application-integration/integrating-reporting-services-using-soap.md)   
 [Integrieren von Reporting Services, die mit den ReportViewer-Steuerelementen](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)   
 [URL-Zugriff &#40; SSRS &#41;](../../reporting-services/url-access-ssrs.md)  
  
  

