---
layout: post
title: Getting Started with .NET MAUI Navigation Drawer control | Syncfusion
description: Learn here about getting started with Syncfusion .NET MAUI Navigation Drawer (SfNavigationDrawer) control, its elements and more.
platform: maui
control: NavigationDrawer
documentation: ug
---

# Getting Started with .NET MAUI Navigation Drawer (SfNavigationDrawer)

This section explains how to add the `.NET MAUI NavigationDrawer control.` This section covers only the basic features needed to get started with Syncfusion .NET MAUI NavigationDrawer.

## Adding a .NET MAUI SfNavigationDrawer reference

Syncfusion .NET MAUI controls are available in [Nuget.org](https://www.nuget.org/). To add `.NET MAUI NavigationDrawer` to your project, open the NuGet package manager in Visual Studio, search for `Syncfusion.Maui.NavigationDrawer` and then install it.

## Handler registration 

 In the MauiProgram.cs file, register the handler for Syncfusion core.

{% highlight c# hl_lines="6 17" %}
using Microsoft.Maui;
using Microsoft.Maui.Hosting;
using Microsoft.Maui.Controls.Compatibility;
using Microsoft.Maui.Controls.Hosting;
using Microsoft.Maui.Controls.Xaml;
using `Syncfusion.Maui.Core.Hosting;`

namespace NavigationDrawerSample
{
    public static class MauiProgram
    {
    public static MauiApp CreateMauiApp()
    {
        var builder = MauiApp.CreateBuilder();
        builder
        .UseMauiApp<App>()
        `.ConfigureSyncfusionCore()`
        .ConfigureFonts(fonts =>
        {
            fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
        });

        return builder.Build();
        }      
    }
}     

{% endhighlight %} 

## Create a Simple .NET MAUI NaviagtionDrawer

The .NET MAUI NaviagtionDrawer control is configured entirely in C# code or by using XAML markup. The following steps explain how to create a .NET MAUI NaviagtionDrawer (SfNaviagtionDrawer) and configure its elements:

### Adding the .NET MAUI NaviagtionDrawer control

Step 1: Add the NuGet to the project as discussed in the above reference section. 

Step 2: Add the namespace as shown in the following code sample:

{% tabs %}

{% highlight xaml %}

    xmlns:navigationdrawer="clr-namespace:Syncfusion.Maui.NavigationDrawer;assembly=Syncfusion.Maui.NavigationDrawer"
	
{% endhighlight %}

{% highlight c# %}

    using Syncfusion.Maui.NavigationDrawer;

{% endhighlight %}

{% endtabs %}

Step 3: Set the control to content in `ContentPage.`

{% tabs %}

{% highlight xaml %}


<navigationdrawer:SfNavigationDrawer x:Name="navigationDrawer">
    <navigationdrawer:SfNavigationDrawer.ContentView>
        <Grid/>
    </navigationdrawer:SfNavigationDrawer.ContentView>
</navigationdrawer:SfNavigationDrawer>


{% endhighlight %}

{% highlight c# %}
          
SfNavigationDrawer navigationDrawer = new SfNavigationDrawer();
Grid grid = new Grid();
navigationDrawer.ContentView = grid;
this.Content = navigationDrawer; 

{% endhighlight %}

{% endtabs %}

N> It is mandatory to set `ContentView` for `SfNavigationDrawer` on initializing.

## Adjust Drawer Size

The default position of the navigation pane is on the left, so change the drawer width to 250 by using the `DrawerWidth` property.

{% tabs %}	
{% highlight xaml %}

<navigationdrawer:SfNavigationDrawer x:Name="navigationDrawer">
    <navigationdrawer:SfNavigationDrawer.DrawerSettings>
        <navigationdrawer:DrawerSettings DrawerWidth="250"/>
    </navigationdrawer:SfNavigationDrawer.DrawerSettings>
    <navigationdrawer:SfNavigationDrawer.ContentView>
        <Grid/>
    </navigationdrawer:SfNavigationDrawer.ContentView>
</navigationdrawer:SfNavigationDrawer>
	
{% endhighlight %}
{% highlight c# %} 

using Syncfusion.Maui.NavigationDrawer;

namespace NavigationSample;

public partial class NavigationDrawerPage : ContentPage
{
	public NavigationDrawerPage()
	{
		InitializeComponent();
        SfNavigationDrawer navigationDrawer = new SfNavigationDrawer();
        Grid grid = new Grid();
        navigationDrawer.ContentView = grid;
        navigationDrawer.DrawerSettings = new DrawerSettings()
        {
            DrawerWidth = 250,
        };
        this.Content = navigationDrawer;
    }
}

{% endhighlight %}

{% endtabs %}


N> To change the side of the navigation pane, utilize the `Position` property. Adjust the drawer height in the Top and Bottom positions using the `DrawerHeight` property.

## Add Hamburger Menu for Toggling Drawer

Create an ImageButton and set the required image to the `Source` property. Subscribe Clicked event of the button and invoke the `ToggleDrawer()` method to toggle the drawer. Properly align the layout of `ContentView` to position the hamburger icon at the top left, as demonstrated in the following code.

{% tabs %}	

{% highlight xaml %}

<navigationdrawer:SfNavigationDrawer x:Name="navigationDrawer">
    <navigationdrawer:SfNavigationDrawer.DrawerSettings>
        <navigationdrawer:DrawerSettings DrawerWidth="250"/>
    </navigationdrawer:SfNavigationDrawer.DrawerSettings>
    <navigationdrawer:SfNavigationDrawer.ContentView>
        <Grid x:Name="mainContentView" 
          BackgroundColor="White" RowDefinitions="Auto,*">
            <HorizontalStackLayout BackgroundColor="#1aa1d6" Spacing="10" Padding="5,0,0,0">
                <ImageButton x:Name="hamburgerButton"
                             HeightRequest="50"
                             WidthRequest="50"
                             HorizontalOptions="Start"
                             Source="hamburgericon.png"
                             BackgroundColor="#1aa1d6"
                             Clicked="hamburgerButton_Clicked"/>
                <Label x:Name="headerLabel" 
                   HeightRequest="50" 
                   HorizontalTextAlignment="Center" 
                   VerticalTextAlignment="Center" 
                   Text="Home" FontSize="16" 
                   TextColor="White" 
                   BackgroundColor="#1aa1d6"/>
            </HorizontalStackLayout>
            <Label Grid.Row="1" 
              x:Name="contentLabel" 
              VerticalOptions="Center" 
              HorizontalOptions="Center" 
              Text="Content View" 
              FontSize="14" 
              TextColor="Black"/>
        </Grid>
    </navigationdrawer:SfNavigationDrawer.ContentView>
</navigationdrawer:SfNavigationDrawer>
	
{% endhighlight %}
	
{% highlight c# %} 

namespace NavigationSample;

public partial class NavigationDrawerPage : ContentPage
{
	public NavigationDrawerPage()
	{
		InitializeComponent();
    }

    private void hamburgerButton_Clicked(object sender, EventArgs e)
    {
        navigationDrawer.ToggleDrawer();
    }
}

{% endhighlight %}

{% endtabs %}

## Set ListView as Drawer Content

Create a ListView with items and set it as `DrawerContentView.` 

{% tabs %}	

{% highlight xaml %}

<navigationdrawer:SfNavigationDrawer x:Name="navigationDrawer">
    <navigationdrawer:SfNavigationDrawer.DrawerSettings>
        <navigationdrawer:DrawerSettings DrawerWidth="250"
                                         DrawerHeaderHeight="160">
            <navigationdrawer:DrawerSettings.DrawerHeaderView>
                <Grid BackgroundColor="#1aa1d6" RowDefinitions="120,40">
                    <Image Source="user.png"
                           HeightRequest="110"
                           Margin="0,10,0,0"
                           BackgroundColor="#1aa1d6"
                           VerticalOptions="Center"
                           HorizontalOptions="Center"/>
                    <Label Text="James Pollock"
                           Grid.Row="1"
                           HorizontalTextAlignment="Center"
                           HorizontalOptions="Center"
                           FontSize="20"
                           TextColor="White"/>
                </Grid>
            </navigationdrawer:DrawerSettings.DrawerHeaderView>
            <navigationdrawer:DrawerSettings.DrawerContentView>
                <ListView x:Name="listView"
                          ItemSelected="listView_ItemSelected">
                    <ListView.ItemTemplate>
                        <DataTemplate>
                            <ViewCell>
                                <VerticalStackLayout HeightRequest="40">
                                    <Label Margin="10,7,0,0"
                                           Text="{Binding}"
                                           FontSize="16"/>
                                </VerticalStackLayout>
                            </ViewCell>
                        </DataTemplate>
                    </ListView.ItemTemplate>
                </ListView>
            </navigationdrawer:DrawerSettings.DrawerContentView>
        </navigationdrawer:DrawerSettings>
    </navigationdrawer:SfNavigationDrawer.DrawerSettings>
    <navigationdrawer:SfNavigationDrawer.ContentView>
        <Grid x:Name="mainContentView" 
          BackgroundColor="White" RowDefinitions="Auto,*">
            <HorizontalStackLayout BackgroundColor="#1aa1d6" Spacing="10" Padding="5,0,0,0">
                <ImageButton x:Name="hamburgerButton"
                             HeightRequest="50"
                             WidthRequest="50"
                             HorizontalOptions="Start"
                             Source="hamburgericon.png"
                             BackgroundColor="#1aa1d6"
                             Clicked="hamburgerButton_Clicked"/>
                <Label x:Name="headerLabel" 
                   HeightRequest="50" 
                   HorizontalTextAlignment="Center" 
                   VerticalTextAlignment="Center" 
                   Text="Home" FontSize="16" 
                   TextColor="White" 
                   BackgroundColor="#1aa1d6"/>
            </HorizontalStackLayout>
            <Label Grid.Row="1" 
              x:Name="contentLabel" 
              VerticalOptions="Center" 
              HorizontalOptions="Center" 
              Text="Content View" 
              FontSize="14" 
              TextColor="Black"/>
        </Grid>
    </navigationdrawer:SfNavigationDrawer.ContentView>
</navigationdrawer:SfNavigationDrawer>

  	
{% endhighlight %}
	
{% highlight c# %}

namespace NavigationSample;

public partial class NavigationDrawerPage : ContentPage
{
	public NavigationDrawerPage()
	{
		InitializeComponent();
        List<string> list = new List<string>();
        list.Add("Home");
        list.Add("Profile");
        list.Add("Inbox");
        list.Add("Out box");
        list.Add("Sent");
        list.Add("Draft");
        listView.ItemsSource = list;
    }

    private void hamburgerButton_Clicked(object sender, EventArgs e)
    {
        navigationDrawer.ToggleDrawer();
    }

    private void listView_ItemSelected(object sender, SelectedItemChangedEventArgs e)
    {
        // Your codes here
        navigationDrawer.ToggleDrawer();
    }
}

{% endhighlight %}

{% endtabs %}

You can find the Getting Started Sample from this [`link.`](https://github.com/SyncfusionExamples/Getting-started-sample-for-.NET-MAUI-NavigationDrawer)