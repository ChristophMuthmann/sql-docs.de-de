---
title: Verbinden mit SQL Server Integration Services (Seite Anmeldung) | Microsoft-Dokumentation
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
- sql13.swb.connecttodts.login.f1
- sql13.swb.connecttodtsserver.login.f1
ms.assetid: 402c2de4-f4ea-40b0-909f-3ddf3bd59950
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 18699131b8268dedfb0e47f05ec4032d81b498ef
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-login-page-integration-services"></a>Verbinden mit SQL Server Integration Services (Seite Anmeldung)
Verwenden Sie diese Registerkarte, um die folgenden Optionen für Verbindungen mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]anzuzeigen oder anzugeben.  
  
## <a name="options"></a>enthalten  
**Servertyp**  
Wenn Sie einen Server über den Objekt-Explorer registrieren, wählen Sie den Typ des Servers aus, mit dem eine Verbindung hergestellt wird: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services oder Integration Services. Im verbleibenden Bereich des Dialogfelds werden nur die Optionen angezeigt, die auf den ausgewählten Servertyp zutreffen. Wenn Sie einen Server über „Registrierte Server“ registrieren, ist das Feld **Servertyp** schreibgeschützt, wobei der Feldeintrag mit dem in der Komponente „Registrierte Server“ angezeigten Servertyp übereinstimmt. Zum Registrieren eines anderen Servertyps wählen Sie auf der Symbolleiste "Registrierte Server" die Option [!INCLUDE[ssDE](../../includes/ssde_md.md)], "Analysis Services", "Reporting Services" oder "Integration Services" aus. Anschließend können Sie mit der Registrierung eines neuen Servers beginnen.  
  
**Servername**  
Wählen Sie den Server für die Verbindungsherstellung aus. Standardmäßig wird die Serverinstanz angezeigt, mit der zuletzt eine Verbindung bestanden hat.  
  
> [!NOTE]  
> Verwenden Sie nicht *<servername>*\\*<instancename>*, weil [!INCLUDE[ssIS](../../includes/ssis_md.md)] mehrere Instanzen auf einem Computer nicht unerstützt.  
  
**Authentifizierung**  
Für [!INCLUDE[msCoName](../../includes/msconame_md.md)] steht nur die [!INCLUDE[ssIS](../../includes/ssis_md.md)]Windows-Authentifizierung zur Verfügung. Der Windows Authentifizierungsmodus ermöglicht Benutzern die Verbindung über ein Windows-Benutzerkonto.  
  
**Benutzername**  
Diese Option ist nicht verfügbar, da für [!INCLUDE[ssIS](../../includes/ssis_md.md)]nur die Windows-Authentifizierung zur Verfügung steht.  
  
**Kennwort**  
Diese Option ist nicht verfügbar, da für [!INCLUDE[ssIS](../../includes/ssis_md.md)]nur die Windows-Authentifizierung zur Verfügung steht.  
  
**Kennwort speichern**  
Diese Option ist nicht verfügbar, da für [!INCLUDE[ssIS](../../includes/ssis_md.md)]nur die Windows-Authentifizierung zur Verfügung steht.  
  
**Connect**  
Stellt eine Verbindung zu dem oben ausgewählten Server her.  
  
**enthalten**  
Klicken Sie hier, um die Anzeige des Dialogfelds zu ändern und die zusätzlichen Serververbindungsoptionen, z. B. Speichern des Kennworts, auszublenden.  
  

