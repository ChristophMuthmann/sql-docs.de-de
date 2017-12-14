---
title: Lokale Sprachversionen in SQL Server | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/23/2017
ms.prod: install
ms.prod_service: sql-non-specified
ms.service: database-engine
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 20b99363-0490-4aa3-9a3d-262f827d81e8
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 72c20d3c087be9a08f63035e1207645c36f8c2f1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="local-language-versions-in-sql-server"></a>Lokale Sprachversionen in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt alle Sprachen, die von Windows-Betriebssystemen unterstützt werden.  
  
## <a name="cross-language-support"></a>Sprachübergreifende Unterstützung  
  
-   Die englische Sprachversion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird für alle lokalisierten Betriebssystemversionen unterstützt.  
  
-   Lokalisierte Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden durch die Verwendung der MUI (Multilingual User Interface Pack)-Einstellungen von Windows unter lokalisierten Betriebssystemen in der entsprechenden Sprache sowie unter englischsprachigen Versionen der unterstützten Betriebssysteme unterstützt. Weitere Informationen finden Sie unter [Configure Operating System to Support Localized Versions](../../sql-server/install/local-language-versions-in-sql-server.md#BK_ConfigureOS).  
  
-   Lokalisierte Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können ausschließlich auf lokalisierte Versionen in derselben Sprache aktualisiert werden, nicht jedoch auf die englischsprachige Version.  
  
-   Lokalisierte Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] können auch parallel mit englischsprachigen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert werden.  
  
##  <a name="BK_ConfigureOS"></a> Configure Operating System to Support Localized Versions  
 Lokalisierte Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden in englischsprachigen Versionen der unterstützten Betriebssysteme durch die MUI-Einstellungen (Multilingual User Interface Pack) von Windows unterstützt.  
  
 Sie müssen jedoch bestimmte Betriebssystemeinstellungen überprüfen, bevor Sie eine lokalisierte Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf einem Server installieren, auf dem ein englischsprachiges Betriebssystem mit einer anderen MUI-Einstellung als Englisch ausgeführt wird. Die folgenden Betriebssystemeinstellungen müssen der Sprache der zu installierenden lokalisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angepasst werden:  
  
-   Die Einstellung für die Benutzeroberfläche des Betriebssystems  
  
-   Die Einstellung für das Benutzergebietsschema des Betriebssystems  
  
-   Die Einstellung für das Systemgebietsschema  
  
 Legen Sie mithilfe der folgenden Prozeduren diese Betriebssystemeinstellungen richtig fest, wenn die Einstellungen nicht der Sprache der zu installierenden lokalisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entsprechen.  
  
> [!CAUTION]  
>  Installationen verschiedener Sprachversionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen auf demselben Computer werden nicht unterstützt.  
  
#### <a name="to-change-the-operating-system-user-interface-setting"></a>So ändern Sie die Betriebssystemeinstellung für die Benutzeroberfläche  
  
1.  Installieren Sie ggf. das Betriebssystem-MUI, das Ihrer lokalisierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version entspricht.  
  
2.  Öffnen Sie in der Systemsteuerung **Regions- und Sprachoptionen**.  
  
3.  Wählen Sie auf der Registerkarte **Sprachen** für **Sprache für Menüs und Dialogfelder**einen Wert aus der Liste aus.  
  
     Diese Einstellung hat Auswirkungen auf die Sprache der Benutzeroberfläche von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sie muss daher Ihrer lokalisierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]entsprechen.  
  
4.  Klicken Sie auf **Übernehmen** , um die Änderung zu bestätigen, und dann auf **OK** , um das Fenster zu schließen.  
  
#### <a name="to-change-the-operating-system-user-locale-setting"></a>So ändern Sie die Betriebssystemeinstellung für das Benutzergebietsschema  
  
1.  Installieren Sie ggf. das Betriebssystem-MUI, das Ihrer lokalisierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version entspricht.  
  
2.  Öffnen Sie in der Systemsteuerung **Regions- und Sprachoptionen**.  
  
3.  Wählen Sie auf der Registerkarte **Regionale Einstellungen** für **Wählen Sie ein Element, um dessen Einstellungen anzuzeigen**einen Wert aus der Liste aus.  
  
     Diese Einstellung betrifft die länderspezifische Datumsformatierung.  
  
4.  Klicken Sie auf **Übernehmen** , um die Änderung zu bestätigen, und dann auf **OK** , um das Fenster zu schließen.  
  
#### <a name="to-change-the-system-locale-setting"></a>So ändern Sie die Einstellung für das Systemgebietsschema  
  
1.  Installieren Sie ggf. das Betriebssystem-MUI, das Ihrer lokalisierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version entspricht.  
  
2.  Öffnen Sie in der Systemsteuerung **Regions- und Sprachoptionen**.  
  
3.  Wählen Sie auf der Registerkarte **Erweitert** für **Wählen Sie die Sprachversion der Programme aus, die Unicode nicht unterstützen**einen Wert aus der Liste aus.  
  
     Diese Einstellung ermöglicht es dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setup, die beste Standardsortierung für Ihre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installation auszuwählen.  
  
4.  Klicken Sie auf **Übernehmen** , um die Änderung zu bestätigen, und dann auf **OK** , um das Fenster zu schließen.  
  
## <a name="see-also"></a>Siehe auch  
 [Hardware- und Softwareanforderungen für die Installation von SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Installieren von SQL Server](../../database-engine/install-windows/install-sql-server.md)  
  
  
