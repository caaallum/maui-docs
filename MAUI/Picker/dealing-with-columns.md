---
layout: post
title: Columns with .NET MAUI Picker Control | Syncfusion
description: Learn here all about columns with Syncfusion .NET MAUI Picker (SfPicker) control.
platform: maui
control: SfPicker
documentation: ug
---

# Dealing with Columns in .NET MAUI Picker (SfPicker)

This section explains the customization of picker columns.

## Columns customization 

You can customize various properties, including `DisplayMemberPath`, `Width`, `SelectedIndex`, `ItemsSource`, and `HeaderText` for enhanced control and flexibility by the following code.

## DisplayMemberPath

When you have a collection of objects, and you want to display a specific property of those objects rather than the entire object by using the [DisplayMemberPath](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html#Syncfusion_Maui_Picker_PickerColumn_DisplayMemberPath) property in the [PickerColum](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html) class.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}

    <sfPicker:SfPicker x:Name="Picker">
    </sfPicker:SfPicker>

{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}

    public MainPage()
    {
        InitializeComponent();
        ObservableCollection<CountryInfo>  countryDetails = new ObservableCollection<CountryInfo>
        {
            new CountryInfo { Language = "Tamil", StateName = "Tamil Nadu" },
            new CountryInfo { Language = "Hindi", StateName = "Uttar Pradesh" },
            new CountryInfo { Language = "Bengali", StateName = "West Bengal" },
            new CountryInfo { Language = "Telugu", StateName = "Andhra Pradesh" },
            new CountryInfo { Language = "Marathi", StateName = "Maharashtra" },
            new CountryInfo { Language = "Kannada", StateName = "Karnataka" },
            new CountryInfo { Language = "Gujarati", StateName = "Gujarat" },
            new CountryInfo { Language = "Punjabi", StateName = "Punjab" },
            new CountryInfo { Language = "Odia", StateName = "Odisha" },
            new CountryInfo { Language = "Malayalam", StateName = "Kerala" },
            new CountryInfo { Language = "Assamese", StateName = "Assam" },
        };
        PickerColumn pickerColumn = new PickerColumn()
        {
            DisplayMemberPath = "Language",
            HeaderText = "Select Languages",
            ItemsSource = countryDetails,
            SelectedIndex = 1,
        };
        this.Picker.Columns.Add(pickerColumn);

{% endhighlight %}
{% highlight c# tabtitle="CountryInfo.cs" %}

    public class CountryInfo
    {
        public string Language { get; set; }
        public string StateName { get; set; }
    }
    
{% endhighlight %}
{% endtabs %}

### Width customization

Customize the [Width](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html#Syncfusion_Maui_Picker_PickerColumn_Width) of every column by setting the `Width` property in the [PickerColumn](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html). The default value of width is `-1`.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}

    <sfPicker:SfPicker x:Name="Picker">
    </sfPicker:SfPicker>

{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}

    this.Picker.Columns[0].Width = 150;
    
{% endhighlight %}
{% endtabs %}
 
### SelectedIndex customization

Customize the SelectedIndex of every column by setting the `SelectedIndex` property in the [PickerColumn](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html). The default value of the [SelectedIndex](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html#Syncfusion_Maui_Picker_PickerColumn_SelectedIndex) property is `0`.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}

    <sfPicker:SfPicker x:Name="Picker">
    </sfPicker:SfPicker>

{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}

    this.Picker.Columns[0].SelectedIndex = 5;

{% endhighlight %}
{% endtabs %}

### HeaderText customization

Customize the Header text of every column by setting the `HeaderText` property in the [PickerColumn](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html). The default value of the [HeaderText](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html#Syncfusion_Maui_Picker_PickerColumn_HeaderText) property is `string.empty`.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}

    <sfPicker:SfPicker x:Name="Picker">
    </sfPicker:SfPicker>

{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}

    this.Picker.Columns[0].HeaderText = "Languages";
    
{% endhighlight %}
{% endtabs %}

### ItemsSource customization

Customize the ItemSource of every column by setting the `ItemSource` property in the [PickerColumn](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html). The default value of the [ItemSource](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.Picker.PickerColumn.html#Syncfusion_Maui_Picker_PickerColumn_ItemsSource) property is `null`.

{% tabs %}
{% highlight xaml tabtitle="MainPage.xaml" %}

    <sfPicker:SfPicker x:Name="Picker">
    </sfPicker:SfPicker>

{% endhighlight %}
{% highlight c# tabtitle="MainPage.xaml.cs" %}

    ObservableCollection<string> languages = new ObservableCollection<string> { "Spanish", "French", "Tamil", "English", "German", "Chinese", "Telegu", "Japanese", "Arabic", "Russian", "Portuguese", "Italian" };
    this.Picker.Columns.Add(languages);

{% endhighlight %}
{% endtabs %}

