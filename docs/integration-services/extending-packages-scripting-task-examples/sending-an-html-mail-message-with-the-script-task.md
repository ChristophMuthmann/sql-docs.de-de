---
title: Senden einer HTML-Mail-Nachricht mit dem Skripttask | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b5f50a79ca83243ea130c77a0d95ab402ba2d31a
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>Senden einer HTML-E-Mail mit dem Skripttask
  Der Task „Mail senden“ in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] unterstützt nur E-Mails im Nur-Text-Format. Sie können jedoch problemlos HTML-E-Mails mithilfe des Skripttasks und den E-Mail-Funktionen des .NET Framework senden.  
  
> [!NOTE]  
>  Wenn Sie einen Task erstellen möchten, den Sie einfacher in mehreren Paketen wiederverwenden können, empfiehlt es sich, den Code in diesem Skripttaskbeispiel als Ausgangspunkt für einen benutzerdefinierten Task zu verwenden. Weitere Informationen finden Sie unter [Entwickeln eines benutzerdefinierten Tasks](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Description  
 Im folgenden Beispiel wird die **System.Net.Mail** Namespace zu konfigurieren und eine HTML-Nachricht zu senden. Das Skript an, von, Betreff und Text der E-mail aus Paketvariablen erhält, verwendet sie zum Erstellen eines neuen **MailMessag**e und legt seine **IsBodyHtml** Eigenschaft **"true"**. Er den SMTP-Servernamen aus einer weiteren Paketvariablen ab, initialisiert eine Instanz von ruft dann die **System.Net.Mail.SmtpClient**, und ruft seine **senden** Methode, um die HTML-Nachricht zu senden. Im Beispiel wird die Funktionalität zum Senden der Nachricht in eine Unterroutine gekapselt, die in anderen Skripts wiederverwendet werden kann.  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>So konfigurieren Sie dieses Skripttaskbeispiel ohne einen SMTP-Verbindungs-Manager  
  
1.  Erstellen Sie Zeichenfolgenvariablen mit den Namen `HtmlEmailTo`, `HtmlEmailFrom` und `HtmlEmailSubject`, und weisen Sie diesen entsprechende Werte für eine gültige Testnachricht zu.  
  
2.  Erstellen Sie eine Zeichenfolgenvariable mit dem Namen `HtmlEmailBody`, und weisen Sie dieser eine Zeichenfolge eines HTML-Markups zu. Zum Beispiel:  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  Erstellen Sie eine Zeichenfolgenvariable mit dem Namen `HtmlEmailServer`, und weisen Sie den Namen eines verfügbaren SMTP-Servers zu, der anonyme ausgehende Nachrichten akzeptiert.  
  
4.  Weisen Sie alle fünf Variablen der **ReadOnlyVariables** Eigenschaft eines neuen Skripttasks.  
  
5.  Importieren der **System.Net** und **System.Net.Mail** Namespaces in Ihren Code.  
  
 In dem Beispielcode in diesem Thema wird der Name des SMTP-Servers aus einer Paketvariablen abgerufen. Sie könnten jedoch auch einen SMTP-Verbindungs-Manager nutzen, um die Verbindungsinformationen zu kapseln, und den Servernamen aus dem Verbindungs-Manager in Ihrem Code extrahieren. Die <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A>-Methode des SMTP-Verbindungs-Managers gibt eine Zeichenfolge im folgenden Format zurück:  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 Sie können die **String.Split** Methode, um diese Argumentliste in ein Array einzelner Zeichenfolgen an jedem Semikolon (;) trennen oder gleich (=) anmelden, und extrahieren Sie das zweite Argument (Subskript 1) aus dem Array als den Namen des Servers.  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>So konfigurieren Sie dieses Skripttaskbeispiel mit einem SMTP-Verbindungs-Manager  
  
1.  Ändern Sie den Skripttask, der zuvor konfigurierten durch das Entfernen der `HtmlEmailServer` Variable aus der Liste der **ReadOnlyVariables**.  
  
2.  Ersetzen Sie die folgende Codezeile, die den Servernamen abruft:  
  
    ```  
    Dim smtpServer As String = _  
      Dts.Variables("HtmlEmailServer").Value.ToString  
    ```  
  
     durch die folgenden Zeilen:  
  
    ```  
    Dim smtpConnectionString As String = _  
      DirectCast(Dts.Connections("SMTP Connection Manager").AcquireConnection(Dts.Transaction), String)  
    Dim smtpServer As String = _  
      smtpConnectionString.Split(New Char() {"="c, ";"c})(1)  
    ```  
  
## <a name="code"></a>Code  
  
```vb  
Public Sub Main()  
  
  Dim htmlMessageTo As String = _  
    Dts.Variables("HtmlEmailTo").Value.ToString  
  Dim htmlMessageFrom As String = _  
    Dts.Variables("HtmlEmailFrom").Value.ToString  
  Dim htmlMessageSubject As String = _  
    Dts.Variables("HtmlEmailSubject").Value.ToString  
  Dim htmlMessageBody As String = _  
    Dts.Variables("HtmlEmailBody").Value.ToString  
  Dim smtpServer As String = _  
    Dts.Variables("HtmlEmailServer").Value.ToString  
  
  SendMailMessage( _  
      htmlMessageTo, htmlMessageFrom, _  
      htmlMessageSubject, htmlMessageBody, _  
      True, smtpServer)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Sub SendMailMessage( _  
    ByVal SendTo As String, ByVal From As String, _  
    ByVal Subject As String, ByVal Body As String, _  
    ByVal IsBodyHtml As Boolean, ByVal Server As String)  
  
  Dim htmlMessage As MailMessage  
  Dim mySmtpClient As SmtpClient  
  
  htmlMessage = New MailMessage( _  
    SendTo, From, Subject, Body)  
  htmlMessage.IsBodyHtml = IsBodyHtml  
  
  mySmtpClient = New SmtpClient(Server)  
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials  
  mySmtpClient.Send(htmlMessage)  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();  
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();  
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();  
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();  
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();  
  
            SendMailMessage(htmlMessageTo, htmlMessageFrom, htmlMessageSubject, htmlMessageBody, true, smtpServer);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private void SendMailMessage(string SendTo, string From, string Subject, string Body, bool IsBodyHtml, string Server)  
        {  
  
            MailMessage htmlMessage;  
            SmtpClient mySmtpClient;  
  
            htmlMessage = new MailMessage(SendTo, From, Subject, Body);  
            htmlMessage.IsBodyHtml = IsBodyHtml;  
  
            mySmtpClient = new SmtpClient(Server);  
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;  
            mySmtpClient.Send(htmlMessage);  
  
        }  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Task "Mail" Senden](../../integration-services/control-flow/send-mail-task.md)  
  
  
