---
layout: post
title: Hyperlink navigation in .NET MAUI PDF Viewer control | Syncfusion
description: Learn here all about how to perform hyperlink navigation in the PDF documents using the Syncfusion .NET MAUI PDF Viewer (SfPdfViewer).
platform: MAUI
control: SfPdfViewer
documentation: ug
---

# Hyperlink navigation in .NET MAUI PDF Viewer (SfPdfViewer)

The [SfPdfViewer](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.PdfViewer.SfPdfViewer.html) allows you to open URLs or website links in the default browser. When a user taps or clicks a hyperlink on a PDF page, the SfPdfViewer recognizes the link and prompts a hyperlink dialog asking the user if they want to open the link.

Follow the instructions below to apply localization to the `SfPdfViewer`.

## Handling hyperlink navigation

The `HyperlinkClicked` event occurs when a hyperlink is tapped or clicked and allows you to handle the hyperlink navigation at the application level in your own way. Set the `Handled` property of the `HyperlinkClickedEventArgs` to `true` to suppress the default hyperlink dialog and handle your logic with the hyperlink information. The following example explains how to open a link directly in the system default browser without any confirmation prompts.

{% tabs %}
{% highlight XAML hl_lines="3" %}

            <syncfusion:SfPdfViewer 
                x:Name="PdfViewer"
                HyperlinkClicked="PdfHyperlinkClicked"/>
			
{% endhighlight %}
{% highlight C# hl_lines="4" %}

	public MainPage()
	{
		InitializeComponent();
        PdfViewer.HyperlinkClicked += PdfHyperlinkClicked;
    }

    private async void PdfHyperlinkClicked(object sender, HyperlinkClickedEventArgs e)
    {
        e.Handled = true;
        await Browser.Default.OpenAsync(e.Uri, BrowserLaunchMode.SystemPreferred);
    }
	
{% endhighlight %}
{% endtabs %}

## Enable or disable the hyperlink navigation

You can enable or disable the recognition of hyperlinks in PDF documents using the `EnableHyperlinkNavigation` property. The following code explains the same.

{% tabs %}
{% highlight XAML %}

            <syncfusion:SfPdfViewer 
                x:Name="PdfViewer" 
                EnableHyperlinkNavigation="False"/>
			
{% endhighlight %}
{% highlight C# %}

	PdfViewer.EnableHyperlinkNavigation = false;
	
{% endhighlight %}
{% endtabs %}