---
title: Verbindung mit Server herstellen (Integration Services) | Microsoft-Dokumentation
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
- sql13.swb.connection.login.dtsserver.f1
ms.assetid: 5be897bd-f36c-4c6a-a91a-13d0d016f8b6
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4d7f292d113fb3d9bc8197f7be3134524e8116af
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-integration-services"></a>Verbindung mit Server herstellen (Integration Services)
Verwenden Sie dieses Dialogfeld, um Optionen für Verbindungen mit Computern mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] anzuzeigen oder anzugeben.  
  
## <a name="options"></a>enthalten  
**Servertyp**  
Wenn Sie einen Server über den Objekt-Explorer registrieren, wählen Sie den Typ des Servers aus, mit dem eine Verbindung hergestellt wird: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services oder Integration Services. Im verbleibenden Bereich des Dialogfelds werden nur die Optionen angezeigt, die auf den ausgewählten Servertyp zutreffen. Wenn Sie einen Server über Registrierte Server registrieren, ist das Feld Servertyp schreibgeschützt, wobei der Feldeintrag mit dem in der Komponente Registrierte Server angezeigten Servertyp übereinstimmt. Zum Registrieren eines anderen Servertyps wählen Sie auf der Symbolleiste "Registrierte Server" die Option [!INCLUDE[ssDE](../../includes/ssde_md.md)], "Analysis Services", "Reporting Services" oder "Integration Services" aus. Anschließend können Sie mit der Registrierung eines neuen Servers beginnen.  
  
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
  
**Connect**  
Klicken Sie hier, um eine Verbindung mit dem oben ausgewählten Server herzustellen.  
  
**enthalten**  
Klicken Sie auf diese Schaltfläche, um zusätzliche Optionen für die Serververbindung anzuzeigen, z. B. zum Registrieren eines Servers oder zum Speichern des Kennworts.  
  

