---
title: Exportieren von Informationen zum registrierten Server (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-registration
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.exportregisteredservers.f1
helpviewer_keywords:
- Registered Servers [SQL Server], exporting
- exporting registered server information
- transferring registered server information
ms.assetid: b65e168f-b6bf-489c-b8ad-3b8644acf0b6
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f65431cfdc98981e8bf4bcd6ae3fe2cd592a3e0e
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="export-registered-server-information-sql-server-management-studio"></a>Exportieren von Informationen zum registrierten Server (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] In diesem Thema wird beschrieben, wie Sie Informationen zum registrierten Server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] speichern und exportieren und an andere Mitarbeiter oder Server verteilen. Diese Exportfunktion ermöglicht eine konsistente Benutzeroberfläche auf mehreren Computern.  
  
 Durch Exportieren und Reimportieren von Dateien mit registrierten Servern können Sie schnell und einfach mehrere Computer mit denselben Servern konfigurieren. Besonders hilfreich ist dies, wenn Sie eine große Anzahl von Servern über Computer an mehreren Standorten verwalten oder einen weniger erfahrenden Benutzer mit elementaren Verbindungseinstellungen konfigurieren möchten.  
  
> [!NOTE]  
>  Serverregistrierungen, die die SQL Server-Authentifizierung nutzen, speichern die Kennwörter auf Benutzerbasis. Nach dem Export und Reimport der Serverregistrierungen müssen Benutzer beim ersten Herstellen der Verbindung für jeden Server ein Kennwort eingeben. Diese werden in den Listen der registrierten Server gespeichert. Bei Servern, die mit der Windows-Authentifizierung registriert wurden, ist dies nicht erforderlich.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-export-registered-server-information"></a>So exportieren Sie Informationen zum registrierten Server  
  
1.  Klicken Sie unter „Registrierte Server“ mit der rechten Maustaste auf eine Servergruppe, und klicken Sie dann auf **Exportieren**.  
  
    > [!NOTE]  
    >  Sie können einen einzelnen Server, die gesamte Struktur registrierter Server oder eine Teilmenge der Struktur registrierter Server exportieren.  
  
2.  Nehmen Sie im Dialogfeld **Registrierte Server exportieren** die folgenden Einstellungen vor.  
  
     **Servergruppe**  
     Geben Sie die zu exportierende Servergruppe an. Sie können alle registrierten Server, die registrierten Server in einer bestimmten Servergruppe bzw. einzelne registrierte Server in die Exportdatei exportieren. Die Exportfunktion ist rekursiv. Wenn z. B. Servergruppe A die Servergruppe B enthält und Servergruppe B die Servergruppen C und D enthält, werden beim Export von Servergruppe A alle Einträge in A, B, C und D exportiert.  
  
     In der Servergruppe werden nur die Servergruppen der Baumstruktur des aktuellen registrierten Servers angezeigt.  
  
     **Datei exportieren**  
     Geben Sie den Namen der Exportdatei in das Textfeld ein, oder verwenden Sie die Schaltfläche zum Durchsuchen (**...**), um eine Exportdatei auf dem Clientcomputer zu suchen. Wenn Sie eine vorhandene Datei auswählen, werden die Daten der registrierten Server an die Datei angehängt. Verwenden Sie die Erweiterung .regsrvr. Wenn die Informationen zum registrierten Server für andere Benutzer oder einen anderen Computer verfügbar sein sollen, können Sie die Datei im Netzwerk speichern. Andere Benutzer können auf die Datei zugreifen und die Informationen zum registrierten Server vollständig oder teilweise importieren. Wenn Sie eine vorhandene Datei als Exportdatei auswählen, wird der Inhalt der Datei mit den Informationen zum registrierten Server überschrieben.  
  
     **Benutzernamen und Kennwörter nicht in die Exportdatei einschließen**  
     Schließen Sie Benutzernamen vom Export in die Datei aus.  
  
    > [!IMPORTANT]  
    >  Die Exportdateien sind zwar verschlüsselt, der Zugriff auf die Datei sollte dennoch sorgfältig kontrolliert werden, wenn diese Benutzernamen und SQL Server-Authentifizierungskennwörter enthält. Benutzernamen und Kennwörter werden deshalb standardmäßig von der Exportdatei ausgeschlossen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Importieren von Informationen zum registrierten Server &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)   
 [Erstellen eines neuen registrierten Servers &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)  
  
  
