---
title: Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle | Microsoft-Dokumentation
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- credentials [Reporting Services]
- security [Analysis Services], data sources
- stored credentials [Reporting Services]
- data sources [Reporting Services], stored credentials
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b0cde0748588a56421e7577bf5f9a7d9d8348ccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832498"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Speichern von Anmeldeinformationen in einer Reporting Services-Datenquelle
  Sie können gespeicherte Anmeldeinformationen, mit denen ein [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver auf externe Daten für einen Bericht zugreift, konfigurieren. Gespeicherte Anmeldeinformationen werden verwendet, wenn der unbeaufsichtigt ausgeführt, beispielsweise bei einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Abonnement, das einen Bericht als E-Mail veröffentlicht. Der Berichtsserver ruft die Anmeldeinformationen ab und verwendet sie, wenn die Berichtsverarbeitung geplant oder ausgelöst wird. In diesem Thema werden die einzelnen Schritte für die Konfiguration gespeicherter Anmeldeinformationen für Berichtsserver im einheitlichen Modus und im SharePoint-Modus dargestellt.  
  
|| |
|-|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im einheitlichen Modus &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] im SharePoint-Modus|  
  
##  <a name="bkmk_top"></a> Sicherheitsrichtlinienanforderungen für gespeicherte Anmeldeinformationen  
 ![as_powerpivot_refresh_sss_set_key](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") Für das Konto, das Sie für gespeicherte Anmeldeinformationen verwenden, muss eine der folgenden Sicherheitsrichtlinien auf dem Berichtsserver konfiguriert sein. Es wird empfohlen, dass Sie die Richtlinie mit den mindestens erforderlichen Berechtigungen für Ihre Umgebung auswählen.  
  
1.  **Lokal anmelden zulassen**. Weitere Informationen finden Sie unter [Lokal anmelden zulassen](http://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx).  
  
2.  **Anmelden als Stapelverarbeitungsauftrag**. Weitere Informationen finden Sie unter [Anmelden als Stapelverarbeitungsauftrag](http://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx).  
  
3.  Allgemeine Informationen zu Richtlinien finden Sie unter [Bearbeiten von Sicherheitseinstellungen für ein Gruppenrichtlinienobjekt](http://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx).  
  
##  <a name="bkmk_stored_credentials_data_source_native"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (einheitlicher Modus)  
  
1.  Wechseln Sie im Webportal zum Ordner, in dem der Bericht gespeichert ist. Klicken Sie auf die Auslassungspunkte (...) in der oberen rechten Ecke der Berichtskachel.  
  
2.  Klicken Sie auf **Verwalten** und dann auf **Datenquellen**.  
  
3.  Wählen Sie **Eine benutzerdefinierte Datenquelle**.  
  
4.  Wählen Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung aus, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] hergestellt wird:  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Wählen Sie für **Verbindung herstellen über**die Option **Anmeldeinformationen, die sicher auf dem Berichtsserver gespeichert sind**aus.  
  
7.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben Sie es im Format \<Domäne>\\<Konto\> an, und klicken Sie anschließend auf **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden.**  
  
    -   Wenn Benutzername und Kennwort Datenbank-Anmeldeinformationen sind, wählen Sie **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden**nicht aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, können Sie die Option **Die Identität des authentifizierten Benutzers annehmen, nachdem eine Verbindung zur Datenquelle hergestellt wurde**auswählen.  
  
8.  Klicken Sie auf **Anwenden**.  
  
     ![Pfeilsymbol mit Rückverweis auf den Seitenanfang](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [Anforderungen an Sicherheitsrichtlinien für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_data_source_sharepoint"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine berichtsspezifische Datenquelle (SharePoint-Modus)  
  
1.  Rufen Sie die Dokumentbibliothek mit den Bericht auf, und klicken Sie anschließend auf das offene Menü ![Kontextmenü der Dokumentbibliothek für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "document library context menu for ssrs items").  
  
2.  Klicken Sie auf das zweite offene Menü ![Kontextmenü der Dokumentbibliothek für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "document library context menu for ssrs items") und anschließend auf **Datenquellen verwalten**.  
  
3.  Klicken Sie auf den Namen der **benutzerdefinierten** Datenquelle, die Sie mit gespeicherten Anmeldeinformationen konfigurieren möchten.  
  
4.  Wählen Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung aus, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] hergestellt wird:  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  Wählen Sie für **Anmeldeinformationen**die Option **Gespeicherte Anmeldeinformationen**aus.  
  
7.  Geben Sie einen **Benutzernamen** und ein **Kennwort**ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben Sie es im Format \<Domäne>\\<Konto\> an, und klicken Sie anschließend auf **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden.**  
  
    -   Wenn der Benutzername und das Kennwort Datenbankanmeldeinformationen sind, wählen Sie nicht **Als Windows-Anmeldeinformationen verwenden**aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, wählen Sie ggf. die Option **Ausführungskontext für dieses Konto festlegen**aus.  
  
8.  Klicken Sie auf **OK**.  
  
     ![Pfeilsymbol mit Rückverweis auf den Seitenanfang](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [Anforderungen an Sicherheitsrichtlinien für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_native"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (einheitlicher Modus)  
  
1.  Navigieren Sie im Webportal zum freigegebenen Datenquellenelement. 
  
2.  Klicken Sie auf die Auslassungspunkte (...) in der oberen rechten Ecke der Berichtskachel und anschließend auf **Verwalten**. 
  
3.  Geben Sie in der Liste **Typ** die Datenverarbeitungserweiterung an, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
4.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, dass Sie keine Anmeldeinformationen in der Verbindungszeichenfolge angeben.  
  
     Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung zur lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank hergestellt wird:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben Sie es im Format \<Domäne>\\<Konto\> an, und klicken Sie anschließend auf **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden.**  
  
    -   Wenn Benutzername und Kennwort Datenbank-Anmeldeinformationen sind, wählen Sie **Beim Herstellen einer Verbindung mit der Datenquelle als Windows-Anmeldeinformationen verwenden**nicht aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, können Sie die Option **Die Identität des authentifizierten Benutzers annehmen, nachdem eine Verbindung zur Datenquelle hergestellt wurde**auswählen.  
  
6.  Klicken Sie auf **Anwenden**.  
  
     ![Pfeilsymbol mit Rückverweis auf den Seitenanfang](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [Anforderungen an Sicherheitsrichtlinien für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> Konfigurieren von gespeicherten Anmeldeinformationen für eine freigegebene Datenquelle (SharePoint-Modus)  
  
1.  Rufen Sie in der Dokumentbibliothek das freigegebene Datenquellelement auf. ![Freigegebenes Datenquellsymbol](../../reporting-services/report-data/media/hlp-16datasource.png "Shared data source icon")  
  
2.  Klicken Sie zunächst auf das Kontextmenü ![Kontextmenü der Dokumentbibliothek für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "document library context menu for ssrs items") und anschließend auf das zweite Kontextmenü ![Kontextmenü der Dokumentbibliothek für SSRS-Elemente](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "document library context menu for ssrs items").  
  
3.  Klicken Sie auf **Datenquellendefinition bearbeiten**.  
  
4.  Geben Sie in der Liste **Datenquellentyp** die Datenverarbeitungserweiterung an, die zum Verarbeiten von Daten aus der Datenquelle verwendet wird.  
  
5.  Geben Sie in das Feld **Verbindungszeichenfolge**die Verbindungszeichenfolge an, die vom Berichtsserver zum Herstellen der Verbindung zur Datenquelle verwendet wird. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt, dass Sie keine Anmeldeinformationen in der Verbindungszeichenfolge angeben.  
  
     Das folgende Beispiel zeigt eine Verbindungszeichenfolge, mit der eine Verbindung zur lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank hergestellt wird:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  Geben Sie einen Benutzernamen und ein Kennwort ein.  
  
    -   Wenn das Konto ein Windows-Domänenbenutzerkonto ist, geben Sie es im Format \<Domäne>\\<Konto\> an, und wählen Sie dann **Windows-Anmeldeinformationen verwenden** aus.  
  
    -   Wenn der Benutzername und das Kennwort Datenbankanmeldeinformationen sind, wählen Sie nicht **Als Windows-Anmeldeinformationen verwenden**aus. Wenn der Datenbankserver Identitätswechsel oder Delegierung unterstützt, wählen Sie ggf. die Option **Ausführungskontext für dieses Konto festlegen**aus.  
  
7.  Klicken Sie auf **OK**.  
  
     ![Pfeilsymbol mit Rückverweis auf den Seitenanfang](../../analysis-services/instances/media/uparrow16x16.gif "Arrow icon used with Back to Top link") [Anforderungen an Sicherheitsrichtlinien für gespeicherte Anmeldeinformationen](#bkmk_top)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Specify Credential and Connection Information for Report Data Sources (Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen)](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
  
