---
title: "Speichern und Ausführen des Pakets (SQL Server-Import / Export-Assistent) | Microsoft Docs"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 40b8677cddf363e8789a2fc15b1c2aab5f49f58c
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>Speichern Sie und führen Sie des Pakets (SQL Server-Import / Export-Assistent aus)
  Nachdem Sie die Datenquelle und das Ziel angegeben haben, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Import/Export-Assistent **Paket speichern und ausführen**. Auf dieser Seite geben Sie an, ob der Kopiervorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration Sie möglicherweise auch zum Speichern der Einstellungen als ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets (SSIS), um ihn anzupassen und späteren Wiederverwendung.
  
**Was ist ein Paket?** Der Assistent verwendet SQL Server Integration Services (SSIS) zum Kopieren von Daten. In SSIS stellt das Paket die Basiseinheit dar. Der Assistent erstellt ein SSIS-Paket im Arbeitsspeicher, während Sie die Seiten des Assistenten durchlaufen und Optionen festlegen.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Screenshot der Seite „Paket speichern und ausführen“  
Die folgende Abbildung zeigt die Seite **Paket speichern und ausführen** des Assistenten. 
   
![Speichern und Ausführen des Import / Export-Assistenten die Seite "Paket"](../../integration-services/import-export-data/media/save-and-run.png "speichern, und führen Sie die Seite "Paket" des Import / Export-Assistenten") 
  
## <a name="run-and-save-the-package"></a>Ausführen und Speichern des Pakets 
 Um den Vorgang fortzusetzen, müssen Sie mindestens eine der beiden folgenden Optionen auswählen.  
  
 **Run immediately**  
 Wählen Sie diese Option zum Importieren und exportieren die Daten sofort. Standardmäßig ist dieses Kontrollkästchen aktiviert, und der Vorgang wird sofort ausgeführt.
  
 **SSIS-Paket speichern**  
 Speichern Sie die Einstellungen als ein SSIS-Paket. Später können Sie das Paket optional anpassen und erneut ausführen. Wenn Sie das Paket speichern möchten, gibt es auf der nächsten Seite, **SSIS-Paket speichern**, zusätzliche Optionen.
 
Die Option zum Speichern des Pakets ist nur verfügbar, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition oder eine höhere Edition installiert ist.   
  
> [!NOTE]
> Wenn Sie den Assistenten abzuschließen, führen Sie den Vorgang, aber beenden den Vorgang vor dem Abschluss der Ausführung, das Paket wird nicht gespeichert, auch wenn Sie die **SSIS-Paket speichern** Kontrollkästchen.  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Wenn Sie den Assistenten von Visual Studio gestartet
Wenn Sie den Assistenten aus einem Integration Services-Projekt in Visual Studio mit SQL Server Data Tools (SSDT) gestartet:
-   Sie können keine **ausführen** des Pakets erst nach dem Sie den Assistenten zu beenden. Anschließend können Sie das Paket von Visual Studio ausführen.
-   Der Assistent **speichert** des Pakets in Integration Services-Projekt, von dem Sie den Assistenten gestartet.

## <a name="specify-options-for-saving-the-package"></a>Angeben von Optionen zum Speichern des Pakets
**SQL Server**  
 Wählen Sie diese Option zum Speichern des Pakets in SQL Server in der **Msdb** -Datenbank in die **Sysssispackages** Tabelle.
 
> [!IMPORTANT]
> Mit dieser Option wird das Paket nicht in der SSIS-Katalogdatenbank (SSISDB) gespeichert.  

 Wählen Sie den Zielserver aus, und geben Sie die Anmeldeinformationen zum Herstellen der Verbindung mit dem Server auf der nächsten Seite, **SSIS-Paket speichern**, an. Weitere Informationen finden Sie unter [SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **File system**  
 Wählen Sie diese Option zum Speichern des Pakets als eine Datei mit der **DTSX** Erweiterung.  
  
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
> Die Kennwortoptionen stehen Geben Sie nur, wenn eine **Schutzebene Paket** , die benötigt ein Kennwort - d. h., wenn Sie entweder angeben **sensible Daten mit einem Kennwort verschlüsseln** oder **alle Daten mit einem Kennwort verschlüsseln**.  

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
[Erste Schritte mit diesem einfachen Beispiel des Import / Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  


