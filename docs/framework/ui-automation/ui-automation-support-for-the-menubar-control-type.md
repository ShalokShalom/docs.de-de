---
title: "UI Automation Support for the MenuBar Control Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, Menu Bar control type"
  - "control types, Menu Bar"
  - "Menu Bar control type"
ms.assetid: c1202b21-c1f0-4560-853c-7b99bd73ad97
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# UI Automation Support for the MenuBar Control Type
> [!NOTE]
>  Diese Dokumentation ist für .NET Framework\-Entwickler vorgesehen, die die verwalteten [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Klassen verwenden möchten, die im <xref:System.Windows.Automation>\-Namespace definiert sind. Aktuelle Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] finden Sie auf der Seite zur [Windows\-Automatisierungs\-API: UI\-Automatisierung](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Dieses Thema enthält Informationen über [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Unterstützung für den <xref:System.Windows.Automation.ControlType.MenuBar>\-Steuerelementtyp. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] umfasst ein Steuerelementtyp eine Reihe von Bedingungen, die ein Steuerelement erfüllen muss, damit die <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>\-Eigenschaft verwendet werden kann. Die Bedingungen schließen bestimmte Richtlinien für [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaftswerte und Steuerelementmuster ein.  
  
 Ein Beispiel für Steuerelemente, die den MenuBar\-Steuerelementtyp implementieren, sind Menüleisten\-Steuerelemente. Menüleisten geben dem Benutzer die Möglichkeit, Befehle und Optionen zu aktivieren, die in einer Anwendung enthalten sind.  
  
 In den folgenden Abschnitten werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur, \-Eigenschaften, \-Steuerelementmuster und \-Ereignisse definiert, die für den Steuerelementtyp „MenuBar“ erforderlich sind. Die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Anforderungen gelten für alle Listensteuerelemente in [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] oder [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Struktur  
 In der folgenden Tabelle werden die Steuerelementansicht und die Inhaltsansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur für Menüleisten\-Steuerelemente sowie die möglichen Inhalte der Ansichten beschrieben. Weitere Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur finden Sie unter [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Steuerelementansicht|Inhaltsansicht|  
|--------------------------|--------------------|  
|MenuBar<br /><br /> -   MenuItem \(1 oder mehr\)<br />-   Andere Steuerelemente \(0 oder viele\)|MenuBar<br /><br /> -   MenuItem \(1 oder mehr\)<br />-   Andere Steuerelemente \(0 oder viele\)|  
  
 Menüleisten\-Steuerelemente können in ihrer Struktur andere Steuerelemente enthalten \(z. B. Bearbeitungssteuerelemente und Kombinationsfelder\). Diese weiteren Steuerelemente sind oben in der Inhalts\- und der Steuerelementansicht mit „Andere Steuerelemente“ gemeint.  
  
<a name="Required_UI_Automation_Properties"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Eigenschaften  
 In der folgenden Tabelle werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaften aufgelistet, deren Wert oder Definition für ein Menüleisten\-Steuerelement besonders relevant ist. Weitere Informationen zu [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaften finden Sie unter [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Eigenschaft|Wert|Notizen|  
|----------------------------------------------------------------------------------------|----------|-------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Siehe Hinweise.|Der von dieser Eigenschaft verfügbar gemachte Wert muss sämtliche darin enthaltenen Steuerelemente umfassen.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Siehe Hinweise.|Das Menüleisten\-Steuerelement muss nur dann einen Namen haben, wenn eine Anwendung mehrere Menüleisten hat. Hat eine Anwendung mehrere Menüleisten, sollte diese Eigenschaft dazu verwendet werden, gut zu unterscheidende Namen verfügbar zu machen \(etwa „Formatierung“ oder „Gliederung“\).|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|Menüleisten\-Steuerelemente haben niemals eine Bezeichnung.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|MenuBar|Dieser Wert ist für alle Benutzeroberflächen\-Frameworks gleich.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|„Menüleiste“|Lokalisierte Zeichenfolge für den Steuerelementtyp „MenuBar“.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Das Menüleisten\-Steuerelement ist stets in der Inhaltsansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur enthalten.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Das Menüleisten\-Steuerelement ist stets in der Steuerelementansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Struktur enthalten.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|Siehe Hinweise.|Der Wert dieser Eigenschaft ist hängt davon ab, ob das Steuerelement auf dem Bildschirm angezeigt werden kann.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.OrientationProperty>|Variabel|Diese Eigenschaft gibt an, ob das Menüleisten\-Steuerelement horizontal oder vertikal verläuft.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|True|Menüleisten\-Steuerelemente können den Tastaturfokus erhalten, da die in ihnen enthaltenen Steuerelemente den Tastaturfokus übernehmen können.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.HelpTextProperty>|Siehe Hinweise.|Keine Szenarios dafür, wann Hilfetext für ein Menüleisten\-Steuerelement erforderlich ist.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AcceleratorKeyProperty>|`Null`|Menüleisten haben niemals Tastenkombinationen.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AccessKeyProperty>|„ALT“|Ein Drücken der ALT\-TASTE sollte immer bewirken, dass die Menüleiste den Fokus in der Anwendung erhält.|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Steuerelementmuster  
 In der folgenden Tabelle werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Steuerelementmuster aufgelistet, die von allen Menüleisten\-Steuerelementen unterstützt werden müssen. Weitere Informationen zu Steuerelementmustern finden Sie unter [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Steuerelementmuster|Unterstützung|Notizen|  
|-------------------------|-------------------|-------------|  
|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Variabel|Wenn das Steuerelement erweitert oder reduziert werden kann, implementieren Sie <xref:System.Windows.Automation.Provider.IExpandCollapseProvider>.|  
|<xref:System.Windows.Automation.Provider.IDockProvider>|Variabel|Wenn das Steuerelement an verschiedenen Teilen des Bildschirms angedockt werden kann, implementieren Sie <xref:System.Windows.Automation.Provider.IDockProvider>.|  
|<xref:System.Windows.Automation.Provider.ITransformProvider>|Variabel|Wenn das Steuerelement gedreht, verschoben oder in der Größe geändert werden kann, muss es <xref:System.Windows.Automation.Provider.ITransformProvider> implementieren.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Erforderliche Benutzeroberflächenautomatisierungs\-Ereignisse  
 Die folgende Tabelle enthält die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Ereignisse, die von allen Menüleisten\-Steuerelementen unterstützt werden müssen. Weitere Informationen zu Ereignissen finden Sie unter [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]\-Ereignis|Unterstützung\/Wert|Notizen|  
|-------------------------------------------------------------------------------------|-------------------------|-------------|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>\-Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte <xref:System.Windows.Automation.ExpandCollapsePatternIdentifiers.ExpandCollapseStateProperty>\-Eigenschaft ausgelöstes Ereignis.|Variabel|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Erforderlich|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Erforderlich|Keine|  
  
## Siehe auch  
 <xref:System.Windows.Automation.ControlType.MenuBar>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)