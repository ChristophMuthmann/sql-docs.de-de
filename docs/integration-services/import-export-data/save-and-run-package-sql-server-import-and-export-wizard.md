---
title: "Speichern und Ausführen von Paketen (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: "69"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 84d128eafce53fb4de337d0a835155850a09c2e5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>Speichern und Ausführen von Paketen (SQL Server-Import/Export-Assistent)
  Nachdem Sie die Datenquelle und das Ziel angegeben haben, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent **Paket speichern und ausführen**. Auf dieser Seite geben Sie an, ob der Kopiervorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration können Sie Ihre Einstellungen möglicherweise auch als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket (SSIS) speichern, um es anzupassen und später wiederzuverwenden.
  
**Was ist ein Paket?** Der Assistent verwendet SQL Server Integration Services (SSIS) zum Kopieren von Daten. In SSIS stellt das Paket die Basiseinheit dar. Der Assistent erstellt ein SSIS-Paket im Arbeitsspeicher, während Sie die Seiten des Assistenten durchlaufen und Optionen festlegen.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Screenshot der Seite „Paket speichern und ausführen“  
Die folgende Abbildung zeigt die Seite **Paket speichern und ausführen** des Assistenten. 
   
![Speichern und Ausführen der Paketseite des Import/Export-Assistenten](../../integration-services/import-export-data/media/save-and-run.png "Save and run package page of the Import and Export Wizard") 
  
## <a name="run-and-save-the-package"></a>Ausführen und Speichern des Pakets 
 Um den Vorgang fortzusetzen, müssen Sie mindestens eine der beiden folgenden Optionen auswählen.  
  
 **Run immediately**  
 Wählen Sie diese Option aus, um die Daten sofort zu importieren und zu exportieren. Standardmäßig ist dieses Kontrollkästchen aktiviert, und der Vorgang wird sofort ausgeführt.
  
 **SSIS-Paket speichern**  
 Speichern Sie die Einstellungen als SSIS-Paket. Später können Sie das Paket optional anpassen und erneut ausführen. Wenn Sie das Paket speichern möchten, gibt es auf der nächsten Seite, **SSIS-Paket speichern**, zusätzliche Optionen.
 
Die Option zum Speichern des Pakets ist nur verfügbar, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition oder eine höhere Edition installiert ist.   
  
> [!NOTE]
> Wenn Sie den Assistenten beenden, den Vorgang ausführen, diesen jedoch vor Abschluss der Ausführung beenden, wird das Paket nicht gespeichert, auch wenn Sie das Kontrollkästchen **SSIS-Paket speichern** aktiviert haben.  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Vorgehensweise beim Starten des Assistenten über Visual Studio
Wenn Sie den Assistenten in einem Integration Services-Projekt in Visual Studio mit SQL Server Data Tools (SSDT) gestartet haben, gehen Sie wie folgt vor:
-   Das Paket kann erst **ausgeführt** werden, wenn Sie den Assistenten beendet haben. Danach können Sie das Paket über Visual Studio ausführen.
-   Der Assistent **speichert** das Paket im Integration Services-Projekt, in dem Sie den Assistenten gestartet haben.

## <a name="specify-options-for-saving-the-package"></a>Angeben von Optionen zum Speichern des Pakets
**SQL Server**  
 Wählen Sie diese Option zum Speichern des Pakets unter SQL Server in der **msdb**-Datenbank in der Tabelle **sysssispackages** aus.
 
> [!IMPORTANT]
> Mit dieser Option wird das Paket nicht in der SSIS-Katalogdatenbank (SSISDB) gespeichert.  

 Wählen Sie den Zielserver aus, und geben Sie die Anmeldeinformationen zum Herstellen der Verbindung mit dem Server auf der nächsten Seite, **SSIS-Paket speichern**, an. Weitere Informationen finden Sie unter [SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **File system**  
 Wählen Sie diese Option aus, um das Paket als Datei mit der Erweiterung **DTSX** zu speichern.  
  
 Sie wählen auf der nächsten Seite, **SSIS-Paket speichern**, den Zielordner und Dateinamen für das Paket aus. Weitere Informationen finden Sie unter [SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
 
 ## <a name="specify-the-package-protection-level"></a>Angeben der Paketschutzebene
 **Paketschutzebene**  
 Wählen Sie in der Liste eine Schutzebene zum Schutz der Daten im Paket aus.  
  
 Die Schutzebene bestimmt die Methode, das Kennwort oder den Benutzerschlüssel und den Bereich des Paketschutzes. Der Schutz kann alle Daten oder nur vertrauliche Daten einschließen. Weitere Informationen zu den verfügbaren Optionen finden Sie unter [Zugriffssteuerung für vertrauliche Daten in Paketen](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
 **Kennwort**  
 Geben Sie ein Kennwort ein.  
  
 **Kennwort erneut eingeben**  
 Geben Sie das Kennwort erneut ein.  
  
> [!NOTE]
> Die Kennwortoptionen sind nur verfügbar, wenn Sie eine durch ein Kennwort zu schützende **Paketschutzebene** angeben, d.h., wenn Sie entweder **Sensible Daten mit einem Kennwort verschlüsseln** oder **Alle Daten mit einem Kennwort verschlüsseln** angeben.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Informationen zu den beiden Seiten der Optionen für das Speichern des Pakets  
 Die Seite **Paket speichern und ausführen** ist eine der beiden Seiten, die auf der Sie Optionen für das Speichern des SSIS-Pakets auswählen.  
  
-   Auf der aktuellen Seite wählen Sie aus, ob das Paket in SQL Server oder als Datei gespeichert werden soll. Sie können auch Sicherheitseinstellungen für das gespeicherte Paket wählen.  
  
-   Als Nächstes geben Sie auf der Seite **SSIS-Paket speichern** einen Namen für das Paket und weitere Informationen dazu an, wo Sie es speichern möchten. Weitere Informationen finden Sie unter [SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 Diese Optionen sind nur verfügbar, wenn Sie auf dieser Seite die Option **SSIS-Paket speichern** auswählen.  
  
## <a name="whats-next"></a>Wie geht es weiter?  
 Nach der Angabe, ob der Kopiervorgang sofort ausgeführt und das Paket gespeichert werden soll, hängt die nächste Seite von den Optionen ab, die Sie auswählen.  
  
-   Wenn Sie die Option zum sofortigen Ausführen des Pakets, ohne es zu speichern, ausgewählt haben, heißt die nächste Seite **Assistenten abschließen**. Auf dieser Seite überprüfen Sie die im Assistenten ausgewählten Optionen und starten dann den Kopiervorgang. Weitere Informationen finden Sie unter [Assistenten abschließen](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
  
-   Wenn Sie die Option zum Speichern des Pakets ausgewählt haben, ist die nächste Seite **SSIS-Paket speichern**. Auf dieser Seite geben Sie zusätzliche Optionen für das Speichern des Pakets an. (Dann, nachdem Sie das Paket gespeichert haben, heißt die folgende Seite **Assistenten abschließen**.) Weitere Informationen finden Sie unter [SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Siehe auch  
[Speichern von Paketen](../../integration-services/save-packages.md)  
[Ausführen von Integration Services-Paketen (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  

