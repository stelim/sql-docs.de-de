---
title: Registrieren eines .NET Framework-Standarddatenproviders (SSRS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- .NET Framework data providers for Reporting Services
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
ms.assetid: d92add64-e93c-4598-8508-55d1bc46acf6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 24482f0120f9d33fc4fe9442b770d7ca8656ac80
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48107360"
---
# <a name="register-a-standard-net-framework-data-provider-ssrs"></a>Registrieren eines .NET Framework-Standarddatenproviders (SSRS)
  Wenn Sie zum Abrufen von Daten für ein [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Berichtsdataset einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Datenanbieter eines Drittanbieters verwenden möchten, müssen Sie die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieterassembly an zwei Speicherorten bereitstellen und registrieren: auf dem Berichterstellungsclient und auf dem Berichtsserver. Auf dem Berichterstellungsclient müssen Sie den Datenanbieter als Datenquellentyp registrieren und einem Abfrage-Designer zuordnen. Beim Erstellen eines Berichtsdatasets können Sie diesen Datenanbieter als Datenquellentyp auswählen. Der zugeordnete Abfrage-Designer wird geöffnet, um das Erstellen von Abfragen für diesen Datenquellentyp zu erleichtern. Der Datenanbieter muss auf dem Berichtsserver als Datenquellentyp registriert werden. Anschließend können Sie veröffentlichte Berichte verarbeiten, für die mithilfe dieses Datenanbieters Daten von einer Datenquelle abgerufen werden.  
  
 Es wird nicht notwendigerweise die gesamte Funktionalität von Drittanbieter-Datenanbietern unterstützt, die mit den Datenverarbeitungserweiterungen von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verfügbar ist. Weitere Informationen finden Sie unter [Von Reporting Services unterstützte Datenquellen &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md). Informationen zum Erweitern der Funktionalität eines .[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Datenanbieter, siehe [Implementieren von Datenverarbeitungserweiterungen](../extensions/data-processing/implementing-a-data-processing-extension.md).  
  
 Zum Installieren und Registrieren von Datenanbietern benötigen Sie Anmeldeinformationen als Administrator.  
  
## <a name="registering-a-net-framework-data-provider-on-the-report-server"></a>Registrieren eines .NET Framework-Datenanbieters auf dem Berichtsserver  
 Wenn Sie auf dem Berichtsserver veröffentlichte Berichte verarbeiten möchten, für die dieser [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieter verwendet wird, muss die Assembly auf dem Berichtsserver installiert werden. Zwei Konfigurationsdateien müssen geändert werden. Ändern Sie rsreportserver.config so, dass der Datenanbieter registriert wird. Ändern Sie rssrvpolicy.config so, dass Codezugriffsberechtigungen für die Assembly erteilt werden.  
  
#### <a name="to-install-a-data-provider-assembly-on-the-report-server"></a>So installieren Sie eine Datenanbieterassembly auf dem Berichtsserver  
  
1.  Navigieren Sie zum Standardspeicherort des BIN-Verzeichnisses auf dem Berichtsserver, auf dem Sie den [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieter verwenden möchten. Standardmäßig wird das Verzeichnis „bin“ des Berichtsservers unter dem *\<Laufwerk>*:\Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin gespeichert.  
  
2.  Kopieren Sie die Assembly aus dem Bereitstellungsverzeichnis in das BIN-Verzeichnis des Berichtsservers. Sie können die Assembly im globalen Assemblycache (Global Assembly Cache, GAC) laden. Weitere Informationen finden Sie unter dem Thema [Arbeiten mit Assemblys und dem globalen Assemblycache](http://go.microsoft.com/fwlink/?linkid=63912) in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation zur Plattform MSDN.  
  
#### <a name="to-register-a-net-data-provider-on-the-report-server"></a>So registrieren Sie einen .NET-Datenanbieter auf dem Berichtsserver  
  
1.  Erstellen Sie in dem ReportServer-Verzeichnis, das dem BIN-Verzeichnis übergeordnet ist, eine Sicherungskopie der Datei RSReportServer.config.  
  
2.  Öffnen Sie die Datei "RSReportServer.config". Sie können die Konfigurationsdatei mit öffnen [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] oder einem einfachen Text-Editor, z. B. Editor.  
  
3.  Suchen Sie die `Data` Element in der Datei "rsreportserver.config". Im folgenden Verzeichnis muss ein Eintrag für den [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieter erstellt werden:  
  
    ```  
    <Extensions>  
       <Data>  
          <Extension Your data provider configuration information goes here />  
       </Data>  
    </Extensions>  
    ```  
  
4.  Fügen Sie einen Eintrag für den [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieter hinzu.  
  
    |attribute|Description|  
    |---------------|-----------------|  
    |`Name`|Geben Sie einen eindeutigen Namen für den Datenanbieter an, z. B. **MyNETDataProvider**. Die maximale Länge für das `Name`-Attribut beträgt 255 Zeichen. Der Name muss eindeutig für sämtliche Einträge im sein der `Extension` -Element einer Konfigurationsdatei. Der hier eingeschlossene Wert wird beim Erstellen einer neuen Datenquelle in der Dropdownliste der Datenquellentypen angezeigt.|  
    |`Type`|Geben Sie eine durch Trennzeichen getrennte Liste ein, die den vollqualifizierten Namespace der Klasse enthält, die die <xref:System.Data.IDbConnection> -Schnittstelle implementiert, gefolgt vom Namen der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieterassembly (ohne die Dateinamenerweiterung DLL).|  
  
     Für eine im BIN-Verzeichnis des Berichtsservers bereitgestellte DLL-Datei kann der Eintrag beispielsweise dem Folgenden ähneln:  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly" />   
    ```  
  
     Wenn Sie die Assembly in den GAC (Global Assembly Cache, globalen Assemblycache) laden, müssen Sie die Eigenschaften für starke Namen bereitstellen. Zum Beispiel:  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly,Version=1.0.0.0, Culture=neutral, PublicKeyToken=MyPublicToken"/>  
    ```  
  
#### <a name="to-set-the-code-group-policy-for-a-net-data-provider"></a>Festlegen der Codegruppenrichtlinie für einen .NET-Datenanbieter  
  
1.  Erstellen Sie im Verzeichnis "ReportServer", das dem Verzeichnis "bin" übergeordnet ist, eine Sicherungskopie der Datei "rssrvpolicy.config".  
  
2.  Öffnen Sie die Datei "rssrvpolicy.config". Sie können die Konfigurationsdatei mit [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] oder in einem einfachen Text-Editor wie Editor öffnen.  
  
3.  Suchen Sie das `CodeGroup`-Element in der Datei rssrvpolicy.config.  
  
4.  Fügen Sie eine Codegruppe hinzu, für die datenanbieterassembly an, die gewährt `FullTrust` Berechtigung. Die Codegruppe könnte beispielsweise der Folgenden ähneln:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="ThisDataProviderCodeGroup"  
       Description="Code group for the .NET data provider">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url=  
    "C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\DataProviderAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 Die URL-Mitgliedschaft ist eine der vielen Mitgliedschaftsbedingungen, die Sie für den Datenanbieter auswählen können.  
  
### <a name="verifying-the-deployment-and-registration"></a>Überprüfen der Bereitstellung und der Registrierung  
 Sie können überprüfen, ob der Datenanbieter erfolgreich auf dem Berichtsserver bereitgestellt wurde, indem Sie den Berichts-Manager öffnen und sicherstellen, dass der Datenanbieter in der Liste verfügbarer Datenquellen vorhanden ist. Weitere Informationen zu Berichts-Manager und Datenquellen finden Sie unter [Erstellen, Ändern und Löschen von freigegebenen Datenquellen (SSRS)](create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## <a name="registering-a-net-framework-data-provider-on-the-report-designer-client"></a>Registrieren eines .NET Framework-Datenanbieters auf dem Berichts-Designer-Client  
 Wenn Sie Berichte erstellen möchten, für die dieser [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieter als Datenquelle verwendet wird, muss die Assembly auf dem Clientcomputer installiert werden, auf dem der Berichts-Designer ausgeführt wird. Zwei Konfigurationsdateien müssen geändert werden. Ändern Sie RSReportDesigner.config so, dass der Datenanbieter als Datenquelle registriert und der standardmäßige Abfrage-Designer verwendet wird. Ändern Sie RSPreviewPolicy.config so, dass Codezugriffsberechtigungen für die Datenanbieterassembly erteilt werden.  
  
#### <a name="to-install-a-data-provider-assembly-on-the-report-designer-client"></a>So installieren Sie eine Datenanbieterassembly auf dem Berichts-Designer-Client  
  
1.  Navigieren Sie zum Standardspeicherort des Verzeichnisses PrivateAssemblies auf dem Berichts-Designer-Client, auf dem Sie den [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieter verwenden möchten. Standardmäßig wird das Verzeichnis „PrivateAssemblies“ unter *\<Laufwerk>*:\Programme\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies gespeichert.  
  
2.  Kopieren Sie die Assembly aus dem Bereitstellungsverzeichnis in das Verzeichnis PrivateAssemblies des Berichts-Designer-Clients. Sie können die Assembly im globalen Assemblycache (Global Assembly Cache, GAC) laden. Weitere Informationen finden Sie unter dem Thema [Arbeiten mit Assemblys und dem globalen Assemblycache](http://go.microsoft.com/fwlink/?linkid=63912) in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation zur Plattform MSDN.  
  
#### <a name="to-register-a-net-data-provider-on-the-report-designer-client"></a>So registrieren Sie einen .NET-Datenanbieter auf dem Berichts-Designer-Client  
  
1.  Erstellen Sie eine Sicherungskopie der Datei "RSReportDesigner.config" im Verzeichnis "PrivateAssemblies".  
  
2.  Öffnen Sie die Datei "RSReportDesigner.config" mit [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] oder in einem einfachen Text-Editor wie Editor.  
  
3.  Suchen Sie das `Data`-Element in der Datei RSReportDesigner.config. Im folgenden Verzeichnis muss ein Eintrag für den Datenanbieter erstellt werden:  
  
    ```  
    <Extensions>  
       <Data>  
          <Extension Your data provider configuration information goes here />  
       </Data>  
    </Extensions>  
    ```  
  
4.  Fügen Sie einen Eintrag für den Datenanbieter hinzu.  
  
    |attribute|Description|  
    |---------------|-----------------|  
    |`Name`|Geben Sie einen eindeutigen Namen für den Datenanbieter an, z. B. **MyNETDataProvider**. Die maximale Länge für das `Name`-Attribut beträgt 255 Zeichen. Der Name muss eindeutig für sämtliche Einträge im sein der `Extension` -Element einer Konfigurationsdatei. Der hier eingeschlossene Wert wird beim Erstellen einer neuen Datenquelle in der Dropdownliste der Datenquellentypen angezeigt.|  
    |`Type`|Geben Sie eine durch Trennzeichen getrennte Liste ein, die den vollqualifizierten Namespace der Klasse enthält, die die <xref:System.Data.IDbConnection> -Schnittstelle implementiert, gefolgt vom Namen der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieterassembly (ohne die Dateinamenerweiterung DLL).|  
  
     Für eine im Verzeichnis PrivateAssemblies von [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] bereitgestellte DLL-Datei kann der Eintrag beispielsweise dem Folgenden ähneln:  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly" />   
    ```  
  
     Wenn Sie die Assembly in den GAC (Global Assembly Cache, globaler Assemblycache) laden, müssen Sie die Eigenschaften für starke Namen bereitstellen. Zum Beispiel:  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly, Version=1.0.0.0, Culture=neutral, PublicKeyToken=MyPublicToken"/>  
    ```  
  
5.  Suchen Sie das `Designer`-Element in der Datei RSReportDesigner.config. Im folgenden Verzeichnis muss ein Eintrag für den [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Datenanbieter erstellt werden:  
  
    ```  
    <Extensions>  
       <Designer>  
          <Your data provider configuration information goes here>  
       </Designer>  
    </Extensions>  
    ```  
  
6.  Fügen Sie den folgenden Eintrag zur Datei RSReportDesigner.config unter dem `Designer` Element. Sie müssen nur ersetzen die `Name` Attribut mit dem Namen, die Sie in vorhergehenden Einträgen angegeben.  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
#### <a name="to-set-the-code-group-policy-for-a-net-data-provider-on-the-report-designer-client"></a>So legen Sie die Codegruppenrichtlinie für einen .NET-Datenanbieter auf dem Berichts-Designer-Client fest  
  
1.  Erstellen Sie eine Sicherungskopie der Datei "RSPreviewPolicy.config" im Verzeichnis "PrivateAssemblies".  
  
2.  Öffnen Sie RSPreviewPolicy.config in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] oder einem einfachen Text-Editor, z. B. Editor.  
  
3.  Suchen Sie das `CodeGroup`-Element in der Datei RSPreviewPolicy.config.  
  
4.  Fügen Sie eine Codegruppe für die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -datenanbieterassembly an, die gewährt `FullTrust` Berechtigung. Die Codegruppe könnte beispielsweise der Folgenden ähneln:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="ThisDataProviderCodeGroup"  
       Description="Code group for the .NET data provider">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url=  
    " C:\Program Files\Microsoft Visual Studio 9\Common7\IDE\PrivateAssemblies\DataProviderAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 Die URL-Mitgliedschaft ist eine der vielen Mitgliedschaftsbedingungen, die Sie für den Datenanbieter auswählen können.  
  
### <a name="verifying-the-deployment-and-registration-on-the-report-designer-client"></a>Überprüfen der Bereitstellung und der Registrierung auf dem Berichts-Designer-Client  
 Sie können die Bereitstellung erst überprüfen, wenn Sie alle Instanzen von [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] auf Ihrem lokalen Computer geschlossen haben. Wenn Sie alle aktuelle Sitzungen beendet haben, können Sie überprüfen, ob es sich bei Ihren Datenanbieter erfolgreich auf Berichts-Designer bereitgestellt wurde, erstellen Sie ein neues Berichtsprojekt in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Der Datenanbieter sollte beim Erstellen eines neuen Datasets für den Bericht in der Liste der verfügbaren Datenquellentypen aufgeführt werden.  
  
## <a name="platform-considerations"></a>Bedingungen bezüglich der Plattform  
 Auf einer 64-Bit-Plattform (x64) wird [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] im 32-Bit-WOW-Modus ausgeführt. Wenn Sie Berichte auf einer x64-Plattform erstellen, müssen auf dem Berichterstellungsclient 32-Bit-Datenanbieter installiert sein, um eine Vorschau der Berichte zu ermöglichen. Wenn Sie den Bericht in demselben System veröffentlichen, benötigen Sie x64-Datenanbieter zum Anzeigen des Berichts im Berichts-Manager.  
  
 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] wird für [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]-basierte Plattformen nicht unterstützt.  
  
 Die mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installierten Datenverarbeitungserweiterungen müssen für jede Plattform systemintern kompiliert und in den richtigen Verzeichnissen installiert werden. Wenn Sie einen benutzerdefinierten Datenanbieter oder einen [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Standarddatenanbieter registrieren, muss dieser systemintern für die betreffende Plattform kompiliert und im entsprechenden Verzeichnis installiert werden. Wenn Sie diesen auf einer 32-Bit-Plattform ausführen, muss der Datenanbieter für eine 32-Bit-Plattform kompiliert werden. Wenn Sie ihn auf einer 64-Bit-Plattform ausführen, muss der Datenanbieter für die 64-Bit-Plattform kompiliert werden. Sie können keinen 32-Bit-Datenanbieter verwenden, der in 64-Bit-Schnittstellen für eine 64-Bit-Plattform eingeschlossen ist. Überprüfen Sie Ihre Drittanbietersoftware auf Informationen dazu, ob der Datenanbieter für die installierte Plattform verwendet werden kann. Weitere Informationen zu Datenanbietern und zur Plattformunterstützung finden Sie unter [Von Reporting Services unterstützte Datenquellen (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren und Verwalten eines Berichtsservers &#40;einheitlicher SSRS-Modus&#41;](../report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Implementieren von Datenverarbeitungserweiterungen](../extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Konfigurationsdateien](../report-server/reporting-services-configuration-files.md)   
 [Code Access Security in Reporting Services (Codezugriffssicherheit in Reporting Services)](../extensions/secure-development/code-access-security-in-reporting-services.md)  
  
  
