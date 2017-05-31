---
title: Verbinden mit SQL Server Reporting Services (Seite &quot;Anmeldung&quot;) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttors.login.f1
helpviewer_keywords:
- Connect to Server dialog box, Reporting Services
ms.assetid: d312c740-19d7-4931-84a2-88b805ec8439
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f1dfb11e842436e8787624e3b16ba178423859b2
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-login-page-reporting-services"></a>Verbinden mit SQL Server Reporting Services (Seite 'Anmeldung')
Verwenden Sie diese Registerkarte, um die folgenden Optionen für Verbindungen mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] anzuzeigen oder anzugeben.  
  
## <a name="options"></a>enthalten  
**Servertyp**  
Wenn Sie einen Server über den Objekt-Explorer registrieren, wählen Sie den Typ des Servers aus, mit dem eine Verbindung hergestellt wird: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services oder Integration Services. Im verbleibenden Bereich des Dialogfelds werden nur die Optionen angezeigt, die auf den ausgewählten Servertyp zutreffen. Wenn Sie einen Server über „Registrierte Server“ registrieren, ist das Feld **Servertyp** schreibgeschützt, wobei der Feldeintrag mit dem in der Komponente „Registrierte Server“ angezeigten Servertyp übereinstimmt. Zum Registrieren eines anderen Servertyps wählen Sie auf der Symbolleiste "Registrierte Server" die Option [!INCLUDE[ssDE](../../includes/ssde_md.md)], "Analysis Services", "Reporting Services" oder "Integration Services" aus. Anschließend können Sie mit der Registrierung eines neuen Servers beginnen.  
  
**Servername**  
Welche Werte Sie eingeben müssen, hängt von dem Servermodus der Berichtsserverinstanz ab, mit der Sie eine Verbindung herstellen.  
  
Wenn es sich um einen Berichtsserver handelt, der im einheitlichen Modus ausgeführt wird, geben Sie die Berichtsserverinstanz an, mit der eine Verbindung hergestellt werden soll. Wenn Sie die Standardinstanz verwenden, ist der Servername in der Regel der Name des Computers. Wenn Sie eine benannte Instanz installiert haben, hängen Sie den Namen der Instanz im folgenden Format an den Servernamen an: <servername>\\<InstanceName>. Reporting Services verwendet den umgekehrten Schrägstrich zur Trennung des Instanznamens.  
  
Für einen Berichtsserver, der im integrierten SharePoint-Modus ausgeführt wird, müssen Sie eine SharePoint-Site angeben. Sie können eine beliebige Site aus einer Sitesammlung angeben, die mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]integriert ist. Die URL, die Sie bereitstellen, muss das HTTP oder HTTPS-Präfix enthalten. Um in Management Studio eine Verbindung mit der SharePoint-Site herstellen zu können, müssen Sie über Zugriffsberechtigungen für die SharePoint-Site verfügen. Die Ihnen zugewiesene Berechtigungsstufe bestimmt, welche Elemente Sie anzeigen und verwalten können. Weitere Informationen finden Sie unter [Vorgehensweise: Registrieren eines Berichtsservers und Herstellen einer Verbindung mit dem Berichtsserver](http://msdn.microsoft.com/en-us/c875ff87-ee7d-443a-a702-bdb4b6c27c6e).  
  
**Authentifizierung**  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] kann so konfiguriert werden, dass Windows-Authentifizierungsanforderungen oder Formularauthentifizierungsanforderungen angenommen werden, die von einer von Ihnen bereitgestellten benutzerdefinierten Authentifizierungserweiterung verarbeitet werden. Wählen Sie beim Herstellen einer Verbindung mit Reporting Services einen der folgenden Authentifizierungsmodi aus:  
  
**Windows-Authentifizierungsmodus (Windows-Authentifizierung)**  
Stellt die Verbindung zur Berichtsserverinstanz mithilfe der Anmeldeinformationen von [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows her.  
  
**Standardauthentifizierung**  
Stellen Sie die Verbindung mit **Standardauthentifizierung** her, wenn die Reporting Services-Installation für die Verwendung der Standardauthentifizierung konfiguriert ist.  
  
**Formularauthentifizierung**  
Stellen Sie die Verbindung mit **Formularauthentifizierung** her, wenn die Reporting Services-Installation für die Verwendung der Formularauthentifizierung konfiguriert ist.  
  
**Benutzername**  
Geben Sie den Benutzernamen ein, der für die Verbindung verwendet werden soll. Diese Option ist nur verfügbar, wenn Sie **Standardauthentifizierung** oder **Formularauthentifizierung**ausgewählt haben.  
  
**Kennwort**  
Geben Sie das Kennwort für den Benutzernamen ein. Diese Option kann nur bearbeitet werden, wenn Sie **Standardauthentifizierung** oder **Formularauthentifizierung**ausgewählt haben.  
  
**Kennwort speichern**  
Speichert das eingegebene Kennwort. Diese Option wird nur angezeigt, wenn Sie auf **Optionen**klicken, und kann nur bearbeitet werden, wenn Sie für das Herstellen der Verbindung die **Standardauthentifizierung** oder die **Formularauthentifizierung**ausgewählt haben.  
  
**Connect**  
Stellt eine Verbindung zum ausgewählten Server her.  
  
**enthalten**  
Zeigt zusätzliche Serververbindungsoptionen an, z. B. zum Speichern des Kennworts.  
  
## <a name="see-also"></a>Siehe auch  
[Konfigurieren einer Berichtsserververbindung](http://msdn.microsoft.com/en-us/9759a9fb-35e9-4215-969b-a9f1fea18487)  
[Vorgehensweise: Registrieren eines Berichtsservers und Herstellen einer Verbindung mit dem Berichtsserver](http://msdn.microsoft.com/en-us/c875ff87-ee7d-443a-a702-bdb4b6c27c6e)  
[Konfigurieren der Authentifizierung in Reporting Services](http://msdn.microsoft.com/en-us/753c2542-0e97-4d8f-a5dd-4b07a5cd10ab)  
  

