---
title: Servereigenschaften (Seite „Datenbankeinstellungen“) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.serverproperties.databasesettings.f1
ms.assetid: 1cebdbd3-cbfd-4a02-bba6-a5addf4e3ada
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 669088b678c04de730f83ebf8de59d10751cd676
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="server-properties---database-settings-page"></a>Servereigenschaften (Seite „Datenbankeinstellungen“)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Auf dieser Seite können Sie Ihre Datenbankeinstellungen anzeigen und ändern.  
  
## <a name="options"></a>Tastatur  
 **Standardfüllfaktor für Indizes**  
 Gibt an, bis zu welchem Grad die einzelnen Seiten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gefüllt werden sollen, wenn das Programm mithilfe der vorhandenen Daten einen neuen Index erstellt. Der Füllfaktor wirkt sich auf die Leistung aus, da von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Zeit für das Teilen von Seiten benötigt wird, wenn diese aufgefüllt werden.  
  
 Der Standardwert ist 0. Die gültigen Werte liegen zwischen 0 und 100. Bei einem Füllfaktor von 0 bzw. 100 werden gruppierte Indizes mit vollen Datenseiten und nicht gruppierte Indizes mit vollen Blattseiten erstellt; in der obersten Ebene der Indexstruktur wird aber noch Platz gelassen. Die Füllfaktorwerte 0 und 100 sind in jeglicher Hinsicht identisch.  
  
 Niedrige Werte für den Füllfaktor bewirken, dass von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neue Indizes mit Seiten erstellt werden, die nicht gefüllt sind. Jeder Index belegt mehr Speicherplatz, aber für später einzufügende Einträge ist mehr Platz. Dadurch müssen nicht zwangsläufig die Seiten geteilt werden.  
  
 **Unbegrenzt warten**  
 Gibt an, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] während des Wartens auf ein neues Sicherungsband nie ein Timeout auftritt.  
  
 **Einmal versuchen**  
 Gibt an, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Timeout abläuft, wenn bei Bedarf kein Sicherungsband verfügbar ist.  
  
 **Versuchsdauer Minute(n)**  
 Gibt an, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Timeout erstellt wird, wenn innerhalb des angegebenen Zeitraums kein Sicherungsband verfügbar ist.  
  
 **Standardbeibehaltungsdauer für Sicherungsmedien (in Tagen)**  
 Gibt eine systemweite Standardbeibehaltungsdauer für jedes Sicherungsmedium an, nachdem es für eine Datenbank- oder Transaktionsprotokollsicherung verwendet wurde. Durch die Option wird verhindert, dass Sicherungen vor Ablauf der angegebenen Anzahl von Tagen überschrieben werden.  
  
 **Sicherung komprimieren**  
 Gibt in [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (oder höhere Versionen) die aktuelle Einstellung der Option **Komprimierungsstandard für Sicherung** an. Durch diese Option wird die Standardeinstellung für die Sicherungskomprimierung auf Serverebene wie folgt festgelegt:  
  
-   Wenn das Feld **Sicherung komprimieren** leer ist, werden neue Sicherungen nicht komprimiert.  
  
-   Wenn das Kontrollkästchen **Sicherung komprimieren** aktiviert ist, werden neue Sicherungen standardmäßig komprimiert.  
  
    > [!IMPORTANT]  
    >  Standardmäßig steigt die CPU-Nutzung durch die Komprimierung erheblich, und die bei der Komprimierung zusätzlich verbrauchten CPU-Ressourcen können sich negativ auf gleichzeitige Vorgänge auswirken. Daher ist es u. U. sinnvoll, in einer Sitzung, bei der die CPU-Nutzung durch die [Ressourcenkontrolle](../../relational-databases/resource-governor/resource-governor.md) eingeschränkt ist, komprimierte Sicherungen mit niedriger Priorität zu erstellen. Weitere Informationen finden Sie unter [Einschränken der CPU-Nutzung durch die Sicherungskomprimierung mithilfe der Ressourcenkontrolle &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md).  
  
 Wenn Sie Mitglied der festen Serverrolle **sysadmin** oder **serveradmin** sind, können Sie die Einstellung durch Klicken auf das Kontrollkästchen **Sicherung komprimieren** ändern.  
  
 Informationen finden Sie unter [Anzeigen oder Konfigurieren der Serverkonfigurationsoption „Standardeinstellung für die Sicherungskomprimierung“](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) und [Sicherungskomprimierung &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
 **Wiederherstellungsintervall (Minuten)**  
 Legt die maximale Anzahl von Minuten pro Datenbank für die Wiederherstellung von Datenbanken fest. Die Standardeinstellung ist 0; bei dieser Einstellung wird die Option automatisch von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]konfiguriert. In der Praxis bedeutet dies eine Wiederherstellungszeit von weniger als einer Minute und das Auftreten eines Prüfpunktes in Abständen von ungefähr einer Minute bei aktiven Datenbanken. Weitere Informationen finden Sie unter [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md).  
  
 **Data**  
 Gibt den Standardspeicherort für Datendateien an. Klicken Sie auf die Schaltfläche Durchsuchen, um zu einem neuen Standardspeicherort zu navigieren. Wird erst nach dem Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wirksam.  
  
 **Log**  
 Gibt den Standardspeicherort für Protokolldateien an. Klicken Sie auf die Schaltfläche Durchsuchen, um zu einem neuen Standardspeicherort zu navigieren. Wird erst nach dem Neustart von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wirksam.  
  
 **Konfigurierte Werte**  
 Zeigt für die Optionen in diesem Bereich konfigurierte Werte an. Wenn Sie diese Werte ändern, klicken Sie anschließend auf **Ausgeführte Werte** , um zu sehen, ob die Änderungen wirksam sind. Sind sie nicht wirksam, muss die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zuerst neu gestartet werden.  
  
 **Ausgeführte Werte**  
 Zeigt die gegenwärtig ausgeführten Werte für die Optionen in diesem Bereich an. Diese Werte sind schreibgeschützt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Angeben des Füllfaktors für einen Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
  
