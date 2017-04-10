---
title: "Save and Run Package (SQL Server Import and Export Wizard) | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.saveschedule.f1"
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 69
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 65
---
# Save and Run Package (SQL Server Import and Export Wizard)
  Nachdem Sie die Datenquelle und das Ziel angegeben haben, zeigt der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Import/Export-Assistent **Paket speichern und ausführen**. Auf dieser Seite geben Sie an, ob der Kopiervorgang sofort ausgeführt werden soll. Abhängig von Ihrer Konfiguration können Sie möglicherweise auch das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paket (SSIS) speichern, das der Assistent erstellt hat, um es anzupassen und später wiederzuverwenden.
  
**Was ist ein Paket?** Der Assistent verwendet SQL Server Integration Services (SSIS) zum Kopieren von Daten. In SSIS stellt das Paket die Basiseinheit dar. Der Assistent erstellt ein SSIS-Paket im Arbeitsspeicher, während Sie die Seiten des Assistenten durchlaufen und Optionen festlegen.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Screenshot der Seite „Paket speichern und ausführen“  
Die folgende Abbildung zeigt die Seite **Paket speichern und ausführen** des Assistenten. 
   
![Save and run package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-and-run.png "Save and run package page of the Import and Export Wizard") 
  
## <a name="run-and-save-the-package"></a>Ausführen und Speichern des Pakets 
 Um den Vorgang fortzusetzen, müssen Sie mindestens eine der beiden folgenden Optionen auswählen.  
  
 **Sofort ausführen**  
 Wählen Sie diese Option aus, um das Paket sofort auszuführen.  
  
 **SSIS-Paket speichern**  
 Speichern Sie das Paket. Später können Sie das Paket optional anpassen und erneut ausführen. Wenn Sie das Paket speichern möchten, gibt es auf der nächsten Seite, **SSIS-Paket speichern**, zusätzliche Optionen. Die Option zum Speichern des Pakets ist nur verfügbar, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition oder eine höhere Edition installiert ist.   
  
> [!NOTE] Wenn Sie den Assistenten beenden und ein Paket vor dem Abschluss der Ausführung beenden, wird das Paket nicht gespeichert, auch wenn Sie das Kontrollkästchen **Speichern** auf dieser Seite aktiviert haben.  
  
## <a name="specify-options-for-saving-the-package"></a>Angeben von Optionen zum Speichern des Pakets
**SQL Server**  
 Wählen Sie diese Option zum Speichern des Pakets in der Datenbank **msdb** in der Tabelle **sysssispackages** aus.
 
> [!NOTE] Mit dieser Option wird das Paket nicht in der SSIS-Katalogdatenbank (SSISDB) gespeichert.  

 Wählen Sie den Zielserver aus, und geben Sie die Anmeldeinformationen zum Herstellen der Verbindung mit dem Server auf der nächsten Seite, **SSIS-Paket speichern**, an. Weitere Informationen finden Sie unter [SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **Dateisystem**  
 Wählen Sie diese Option aus, um das Paket als Datei mit der Erweiterung **.dtsx** zu speichern.  
  
 Sie wählen auf der nächsten Seite, **SSIS-Paket speichern**, den Zielordner und Dateinamen für das Paket aus. Weitere Informationen finden Sie unter [SSIS-Paket speichern](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
 
 ## <a name="specify-the-package-protection-level"></a>Angeben der Paketschutzebene
 **Paketschutzebene**  
 Wählen Sie in der Liste eine Schutzebene zum Schutz der Daten im Paket aus.  
  
 Die Schutzebene bestimmt die Methode, das Kennwort oder den Benutzerschlüssel und den Bereich des Paketschutzes. Der Schutz kann alle Daten oder nur vertrauliche Daten einschließen. Weitere Informationen zu den verfügbaren Optionen finden Sie unter [Zugriffssteuerung für vertrauliche Daten in Paketen](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
 **Kennwort**  
 Geben Sie ein Kennwort ein.  
  
 **Kennwort erneut eingeben**  
 Geben Sie das Kennwort erneut ein.  
  
> [!NOTE] Die Kennwortoptionen sind nur verfügbar, wenn Sie die Option **Paketschutzebene** angeben, die ein Kennwort benötigt, das entweder **Sensible Daten mit einem Kennwort verschlüsseln** oder **Alle Daten mit einem Kennwort verschlüsseln** ist.  

## <a name="can-i-run-and-save-the-package"></a>Kann ich das Paket ausführen und speichern?
 Die Methode zum Starten des Assistenten bestimmt, ob Sie das Paket ausführen und speichern können, das der Assistent erstellt. In einigen Fällen wird entweder die Option **Ausführen** oder die Option **Speichern** auf dieser Seite des Assistenten deaktiviert.
 
|Starten des Assistenten|Können Sie das Paket ausführen?|Können Sie das Paket speichern?|
|------------------------|------------------------|-------------------------|
|Sie können den Assistenten über das Startmenü, die Eingabeaufforderung oder SQL Server Management Studio starten.|Sie können das Paket sofort ausführen, indem Sie am Ende des Assistenten das Kontrollkästchen **Sofort ausführen** aktivieren. Standardmäßig ist dieses Kontrollkästchen aktiviert, und das Paket wird sofort ausgeführt.|Wenn SQL Server Standard Edition oder höher installiert ist, können Sie das Paket optional speichern.|
|Sie starten den Assistenten in einem Integration Services-Projekt in SQL Server Data Tools (SSDT).|Das Paket kann erst ausgeführt werden, nachdem Sie den Assistenten beendet haben. Dann können Sie das Paket in SQL Server Data Tools ausführen.|Der Assistent speichert das Paket im Integration Services-Projekt, in dem Sie den Assistenten gestartet haben.|

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
 
  
