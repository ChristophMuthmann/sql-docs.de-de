---
title: Festlegen von Datenquelleneigenschaften (SSAS – mehrdimensional) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2dde88aed74f71bda5dc4178ae558dd6aa953eee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="set-data-source-properties-ssas-multidimensional"></a>Festlegen von Datenquelleneigenschaften (SSAS – mehrdimensional)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]gibt ein Datenquellenobjekt eine Verbindung mit einem externen Data Warehouse oder einer relationalen Datenbank an, das oder die für ein mehrdimensionales Modell Daten bereitstellt. Durch Eigenschaften in der Datenquelle werden die Verbindungszeichenfolge, ein Timeoutintervall, die maximale Anzahl der Verbindungen sowie die Transaktionsisolationsstufe bestimmt.  
  
## <a name="set-data-source-properties-in-sql-server-data-tools"></a>Festlegen von Datenquelleneigenschaften in SQL Server Data Tools  
  
1.  Doppelklicken Sie im Projektmappen-Explorer auf eine Datenquelle, um den Datenquellen-Designer zu öffnen.  
  
2.  Klicken Sie im Datenquellen-Designer auf die Registerkarte **Identitätswechselinformationen** . Weitere Informationen zum Erstellen einer Datenquelle finden Sie unter [Erstellen einer Datenquelle &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
## <a name="set-data-source-properties-in-management-studio"></a>Festlegen von Datenquelleneigenschaften in Management Studio  
  
1.  Erweitern Sie den Datenbankorder, öffnen Sie den Ordner **Datenquelle** unter dem Datenbanknamen, klicken Sie im **Objekt-Explorer** mit der rechten Maustaste auf eine Datenquelle, und wählen Sie **Eigenschaften**aus.  
  
2.  Ändern Sie optional den Namen, die Beschreibung oder die Identitätswechseloption. Weitere Informationen finden Sie unter [Festlegen von Identitätswechseloptionen &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
## <a name="data-source-properties"></a>Datenquelleneigenschaften  
  
|Begriff|Definition|  
|----------|----------------|  
|**Name, ID, Beschreibung**|Name, ID und Beschreibung werden verwendet, um das Datenquellenobjekt im mehrdimensionalen Modell zu identifizieren und zu beschreiben.<br /><br /> Name und Beschreibung können in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oder in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] angegeben werden, nachdem Sie die Lösung bereitgestellt oder verarbeitet haben.<br /><br /> ID wird beim Erstellen des Objekts generiert. Zwar können Sie den Namen und die Beschreibung leicht ändern, doch sind die IDs schreibgeschützt und dürfen nicht geändert werden. Durch die feste Objekt-ID werden Objektabhängigkeiten und Verweise im gesamten Modell beibehalten.|  
|**Timestamp erstellen**|Diese schreibgeschützte Eigenschaft wird in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]angezeigt. Sie zeigt das Datum und die Uhrzeit der Erstellung der Datenquelle an.|  
|**Letztes Schemaupdate**|Diese schreibgeschützte Eigenschaft wird in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]angezeigt. Sie zeigt das Datum und die Uhrzeit des letzten Updates der Metadaten für die Datenquelle an. Dieser Wert wird beim Bereitstellen der Lösung aktualisiert.|  
|**Abfragetimeout**|Gibt an, wie lang versucht wird, eine Verbindungsanforderung auszuführen, bevor aufgegeben wird.<br /><br /> Geben Sie den Abfragetimeout in folgendem Format ein:<br /><br /> *\<Stunden >*:*\<Minuten >*:*\<Sekunden >*<br /><br /> Diese Eigenschaft kann von der **DatabaseConnectionPoolTimeoutConnection** -Servereigenschaft überschrieben werden. Wenn die Servereigenschaft kleiner ist, wird sie anstelle des **Abfragetimeouts**verwendet.<br /><br /> Weitere Informationen zur **Abfragetimeout** -Eigenschaft finden Sie unter <xref:Microsoft.AnalysisServices.DataSource.Timeout%2A>. Weitere Informationen zur Servereigenschaft finden Sie unter [OLAP Properties](../../analysis-services/server-properties/olap-properties.md).|  
|**Verbindungszeichenfolge**|Gibt den physischen Speicherort einer Datenbank, die Daten für ein mehrdimensionales Modell bereitstellt, sowie den für die Verbindung verwendeten Datenanbieter an. Diese Informationen werden für eine Clientbibliothek bereitgestellt, die die Verbindungsanforderung auslöst. Der Anbieter bestimmt, welche Eigenschaften für die Verbindungszeichenfolge festgelegt werden können.<br /><br /> Die Verbindungszeichenfolge wird mit den Informationen erstellt, die Sie im Dialogfeld **Verbindungs-Manager** angeben. Sie können die Verbindungszeichenfolge auch in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] auf der Eigenschaftenseite der Datenquelle anzeigen und bearbeiten.<br /><br /> Bei einer SQL Server-Datenbank gibt eine Verbindungszeichenfolge, die die **Benutzer-ID** enthält, die Datenbankauthentifizierung an. Eine Verbindung, die **Integrierte Sicherheit=SSPI** enthält, gibt die Windows-Authentifizierung an.<br /><br /> Sie können den Server- oder Datenbanknamen ändern, wenn die Datenbank an einen neuen Speicherort verschoben wurde. Überprüfen Sie, ob die eben für die Verbindung angegebenen Anmeldeinformationen einer Datenbankanmeldung zugeordnet sind.|  
|**Maximale Anzahl von Verbindungen**|Gibt Sie die maximale Anzahl an Verbindungen an, die von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] für die Verbindung mit der Datenquelle zugelassen werden. Wenn mehr Verbindungen benötigt werden, wartet [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , bis eine Verbindung verfügbar wird. Der Standardwert lautet 10. Durch Begrenzung der Verbindungszahl wird sichergestellt, dass die externe Datenquelle nicht mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Anforderungen überlastet wird.|  
|**Isolation**|Gibt das Sperr- und Zeilenversionsverwaltungsverhalten von SQL-Befehlen an, die von einer Verbindung mit einer relationalen Datenbank ausgegeben werden. Gültige Werte sind ReadCommitted oder Snapshot. Der Standard ist ReadCommitted, der angibt, dass für Daten ein Commit ausgeführt werden muss, bevor sie gelesen werden. Dadurch werden Dirty Reads verhindert. Momentaufnahme gibt an, dass Lesevorgänge aus einer Momentaufnahme von Daten mit zuvor ausgeführtem Commit stammen. Weitere Informationen zur Isolationsstufe in SQL Server finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).|  
|**Verwalteter Anbieter**|Zeigt den Namen des verwalteten Anbieters an, z. B. System.Data.SqlClient oder System.Data.OracleClient, wenn die Datenquelle einen verwalteten Anbieter verwendet.<br /><br /> Wenn die Datenquelle keinen verwalteten Anbieter verwendet, zeigt diese Eigenschaft eine leere Zeichenfolge an.<br /><br /> Diese Eigenschaft ist in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]schreibgeschützt. Um den für die Verbindung verwendeten Anbieter zu ändern, bearbeiten Sie die Verbindungszeichenfolge.|  
|**Identitätswechselinformationen**|Gibt die Windows-Identität an, unter der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ausgeführt wird, wenn eine Verbindung mit einer Datenquelle hergestellt wird, von der die Windows-Authentifizierung verwendet wird. Zu den Optionen zählen die Verwendung eines vordefinierten Satzes aus Windows-Anmeldeinformationen, Dienstkonto und Identität des aktuellen Benutzers sowie eine Vererbungsoption, die geeignet sein kann, wenn das Modell mehrere Datenquellenobjekte enthält. Weitere Informationen finden Sie unter [Festlegen von Identitätswechseloptionen &#40;SSAS – mehrdimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).<br /><br /> In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]enthält die Liste gültiger Werte folgende Werte:<br /><br /> **ImpersonateAccount** (verwenden Sie einen bestimmten Windows-Benutzernamen und ein Kennwort, um eine Verbindung mit der Datenquelle herzustellen).<br /><br /> **ImpersonateServiceAccount** (verwenden Sie die Sicherheitsidentität des Dienstkontos, um eine Verbindung mit der Datenquelle herzustellen). Dies ist der Standardwert.<br /><br /> **ImpersonateCurrentUser** (verwenden Sie die Sicherheitsidentität des aktuellen Benutzers, um eine Verbindung mit der Datenquelle herzustellen). Diese Option ist nur für Data Mining-Abfragen gültig, die Daten aus einem externen Data Warehouse oder einer solchen Datenbank abrufen. Wählen Sie sie nicht für Datenverbindungen aus, die zum Verarbeiten oder Laden einer mehrdimensionalen Datenbank oder zum Zurückschreiben in eine solche verwendet werden.<br /><br /> **Erben** oder **Standard** (verwenden Sie die Identitätswechseleinstellungen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank, die dieses Datenquellenobjekt enthält). Datenbankeigenschaften beinhalten Identitätswechseloptionen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Datenquellen in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Erstellen einer Datenquelle & #40; SSAS – mehrdimensional & #41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
