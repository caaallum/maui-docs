---
layout: post
title: BindableLayout | Accordion for .NET MAUI | Syncfusion
description: This section describes how to bind AccordionItem to .NET MAUI Accordion (SfAccordion) using BindableLayout.
platform: MAUI
control: SfAccordion
documentation: ug
---

# BindableLayout in .NET MAUI Accordion (SfAccordion)

The `SfAccordion` allows you to set a collection of items by setting the `BindableLayout.ItemsSource` and `BindableLayout.ItemTemplate` properties.

## Creating Data Model

Create a simple data model to bind the data for SfAccordion as shown in the following code example in a new class file, and save it as `EmployeeInfo.cs` file:

{% tabs %}
{% highlight c# %}
public class EmployeeInfo
{
    #region Constructor

    public EmployeeInfo(string name, string image, string position, string organizationunit, string dateofbirth, string location, string phone, bool isexpanded, string description)
    {
        Name = name;
        Image = image;
        Position = position;
        OrganizationUnit = organizationunit;
        DateOfBirth = dateofbirth;
        Location = location;
        Phone = phone;
        IsExpanded = isexpanded;
        Description = description;
    }

    #endregion

    #region Properties

    public string Name { get; set; }

    public string Image { get; set; }

    public string Position { get; set; }

    public string OrganizationUnit { get; set; }

    public string DateOfBirth { get; set; }

    public string Location { get; set; }

    public string Phone { get; set; }

    public bool IsExpanded { get; set; }

    public string Description { get; set; }

    #endregion
}
{% endhighlight %}
{% endtabs %}

Create a model repository class with the EmployeeInfo collection property initialized with required number of data objects in a new class file, as shown in the following code example, and save it as `EmployeeDetails.cs` file.

{% tabs %}
{% highlight c# %}
public class EmployeeDetails
    {
        #region Fields

        private ObservableCollection<EmployeeInfo>? _employee;

        string[] Description = new string[]
        {
        "Robin Rane, Chairman of ABC Inc., leads with dedication and vision.Under his guidance, the company thrives and continues to make a significant impact in the industry.",
        "Paul Vent, General Manager of XYZ Corp., oversees daily operations, ensuring the company's success and growth through strategic planning and effective management practices.",
        "Clara Venus, Asst. Manager at ABC Inc., efficiently handles multiple tasks. With her strong skill set and dedication, she contributes significantly to the company's growth and success.",
        "Maria Even, a highly experienced professional, holds the position of Executive Manager at XYZ Corp. She oversees crucial operations, enforcing company policies and practices.",
        "Mark Zuen, Senior Executive at ABC Inc., skillfully manages business operations. He is adept at leadership and strategic thinking.",
        "Eric John, Technical Manager at ABC Inc., expertly leads his team to develop innovative solutions, creating value for the company",
        "Chris Marker serves as the Senior Accountant at XYZ Corp. With extensive experience, he skillfully manages the company's financial matters, ensuring accuracy and compliance.",
        "Seria Stein, an Account Executive at ABC Inc., adeptly manages client portfolios, ensuring their satisfaction. She is a great communicator, skilled in building relationships.",
        "Angelina Justin, HR Manager at XYZ Corp., expertly handles workplace dynamics with her exceptional communication and problem-solving skills, fostering a positive work environment"
        };

        #endregion

        #region Constructor

        public EmployeeDetails()
        {
            Employees = new ObservableCollection<EmployeeInfo>();
            Employees.Add(new EmployeeInfo("Robin Rane", "emp_01.png", "Chairman", "ABC Inc.", "09/17/1973", "Boston", "(617) 555-1234", false, Description[0]));
            Employees.Add(new EmployeeInfo("Paul Vent", "emp_02.png", "General Manager", "XYZ Corp.", "05/27/1985", "New York", "(212) 555-1234", true, Description[1]));
            Employees.Add(new EmployeeInfo("Clara Venus", "emp_03.png", "Assistant Manager", "ABC Inc.", "07/22/1988", "California", "(415) 123-4567", false, Description[2]));
            Employees.Add(new EmployeeInfo("Maria Even", "emp_04.png", "Executive Manager", "XYZ Corp.", "04/16/1970", "New York", "(516) 345-6789", false, Description[3]));
            Employees.Add(new EmployeeInfo("Mark Zuen", "emp_05.png", "Senior Executive", "ABC Inc.", "09/11/1983", "Boston", "(617) 123-4567", false, Description[4]));
            Employees.Add(new EmployeeInfo("Eric John", "emp_06.png", "Technical Manager", "ABC Inc.", "12/09/1985", "New Jersey", "(201) 555-1234", false, Description[5]));
            Employees.Add(new EmployeeInfo("Chris Marker", "emp_07.png", "Senior Accountant", "XYZ Corp.", "03/14/1986", "California", "(714) 555-5678", false, Description[6]));
            Employees.Add(new EmployeeInfo("Seria Stein", "emp_08.png", "Account Executive", "XYZ Corp.", "02/07/1985", "New York", "(646) 987-6543", false, Description[7]));
            Employees.Add(new EmployeeInfo("Angelina Justin", "emp_09.png", "HR Manager", "XYZ Corp.", "07/11/1972", "Boston", "(617) 987-6543", false, Description[8]));
        }

        #endregion

        #region Properties

        public ObservableCollection<EmployeeInfo>? Employees
        {
            get { return _employee; }
            set { _employee = value; }
        }

        #endregion        
    }
{% endhighlight %}
{% endtabs %}

Set the ViewModel instance as the `BindingContext` of your page to bind properties of the ViewModel to `SfAccordion`.

{% tabs %} 
{% highlight xaml %}
<ContentPage.BindingContext>
    <local:EmployeeDetails/>
</ContentPage.BindingContext>
{% endhighlight %}
{% highlight c# %}
this.BindingContext = new EmployeeDetails();      
{% endhighlight %}
{% endtabs %}

## Binding data to SfAccordion

`SfAccordion` can be bound with data by setting the ItemsSource property of the BindableLayout.

The following code example binds the collection created in the previous step to the `Bindable.ItemsSource` property.

{% tabs %}
{% highlight xaml %}
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:syncfusion="clr-namespace:Syncfusion.Maui.Accordion;assembly=Syncfusion.Maui.Expander"
             xmlns:local="clr-namespace:AccordionBindableLayout"
             x:Class="AccordionBindableLayout.MainPage">
    <syncfusion:SfAccordion x:Name="Accordion" BindableLayout.ItemsSource="{Binding Employees}"/>
</ContentPage>      
{% endhighlight %}
{% highlight c# %}
SfAccordion Accordion = new SfAccordion();
BindableLayout.SetItemsSource(Accordion, viewModel.Employees);
{% endhighlight %}
{% endtabs %}

## Defining the AccordionItem

The `SfAccordion` accepts the `AccordionItem` as its child element. The appearance of each `AccordionItem` can be defined by setting the `BindableLayout.ItemTemplate` property.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfAccordion  x:Name="accordion" BindableLayout.ItemsSource="{Binding Employees}" >
    <BindableLayout.ItemTemplate>
        <DataTemplate>
            <syncfusion:AccordionItem IsExpanded="{Binding IsExpanded}">
                <syncfusion:AccordionItem.Header>
                    <Grid  HeightRequest="48">
                        <Label Text="{Binding Name}" Margin="16,14,0,14" CharacterSpacing="0.25" FontFamily="Roboto-Regular"  FontSize="14" />
                            </Grid>
                </syncfusion:AccordionItem.Header>
                <syncfusion:AccordionItem.Content>
                    <Grid ColumnSpacing="10" RowSpacing="2" BackgroundColor="#f4f4f4"  >
                        <Grid Margin="16,6,0,0">
                            <Grid.Resources>
                                <Style TargetType="Label">
                                            <Setter Property="FontFamily" Value="Roboto-Regular"/>
                                </Style>
                            </Grid.Resources>
                            <Grid.RowDefinitions >
                                <RowDefinition Height="25"/>
                                <RowDefinition Height="25"/>
                                <RowDefinition Height="25"/>
                                <RowDefinition Height="25"/>
                                <RowDefinition Height="{OnPlatform Default=90,Android=90,WinUI=70, iOS=100,MacCatalyst=70 }"/>
                                <RowDefinition Height="Auto"/>
                            </Grid.RowDefinitions>
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="100"/>
                                <ColumnDefinition Width="100"/>
                                <ColumnDefinition Width="*"/>
                            </Grid.ColumnDefinitions>
                            <Frame  Grid.RowSpan="4" BorderColor="Transparent" Grid.Row="0" Grid.Column="0"  Padding="0" Margin="0,0,0,7">
                                <Image  Source="{Binding Image}"/>
                            </Frame>
                            <Label Text="Position" Grid.Column="1" Grid.Row="0" Margin="6,0,0,0"/>
                            <Label Text="{Binding Position}" Grid.Row="0" Grid.Column="2"/>
                            <Label Text="Organization " Grid.Row="1" Grid.Column="1" Margin="6,0,0,0"/>
                            <Label Text="{Binding OrganizationUnit}" Grid.Row="1" Grid.Column="2"/>
                            <Label Text="Date Of Birth " Grid.Row="2" Grid.Column="1" Margin="6,0,0,0"/>
                            <Label Text="{Binding DateOfBirth}" Grid.Row="2" Grid.Column="2"/>
                            <Label Text="Location " Grid.Row="3" Grid.Column="1" Margin="6,0,0,0"/>
                            <Label Text="{Binding Location}" Grid.Row="3" Grid.Column="2"/>
                            <Label Padding="0,10,0,10" Grid.Row="4" Grid.ColumnSpan="3"  LineBreakMode="WordWrap"  
                                            FontSize="14" CharacterSpacing="0.25" VerticalTextAlignment="Center" 
                                                Text="{Binding Description}">
                            </Label>
                            <StackLayout Grid.Row="5" Orientation="Horizontal" Margin="0,0,0,12">
                                <Label Text="&#xe700;" FontSize="16" Margin="0,2,2,2"
                                           FontFamily='{OnPlatform Android=AccordionFontIcons.ttf#,WinUI=AccordionFontIcons.ttf#AccordionFontIcons,MacCatalyst=AccordionFontIcons,iOS=AccordionFontIcons}'
                                                   VerticalOptions="Center" VerticalTextAlignment="Center"/>
                                <Label Text="{Binding Phone}" Grid.Column="1" VerticalOptions="Center" CharacterSpacing="0.25" FontSize="14"/>
                            </StackLayout>
                        </Grid>
                    </Grid>
                </syncfusion:AccordionItem.Content>
            </syncfusion:AccordionItem>
        </DataTemplate>
    </BindableLayout.ItemTemplate>
</syncfusion:SfAccordion>    
{% endhighlight %}
{% highlight c# %}
SfAccordion accordion = new SfAccordion();
DataTemplate ItemTemplate = new DataTemplate(() =>
{
    var accordionItem = new AccordionItem();
    var headerGrid = new Grid();
    var headerLabel = new Label() { Text = "Robin Rane", Margin = new Thickness(16, 14, 0, 14), CharacterSpacing = 0.25, FontFamily = "Roboto-Regular", FontSize = 14 };
    headerLabel.SetBinding(Label.TextProperty, new Binding("Name"));
    headerGrid.Children.Add(headerLabel);
    headerGrid.HeightRequest = 48;
    accordionItem.Header = headerGrid;

    var content = new Grid();
    content.ColumnSpacing = 10;
    content.RowSpacing = 2;
    content.BackgroundColor = Color.FromArgb("#f4f4f4");
    var contentGrid = new Grid();
    contentGrid.Margin = new Thickness(16, 6, 0, 0);
    contentGrid.RowDefinitions.Add(new RowDefinition() { Height = 25 });
    contentGrid.RowDefinitions.Add(new RowDefinition() { Height = 25 });
    contentGrid.RowDefinitions.Add(new RowDefinition() { Height = 25 });
    contentGrid.RowDefinitions.Add(new RowDefinition() { Height = 25 });
    contentGrid.RowDefinitions.Add(new RowDefinition() { Height = DeviceInfo.Platform == DevicePlatform.WinUI || DeviceInfo.Platform == DevicePlatform.MacCatalyst ? 70 : DeviceInfo.Platform == DevicePlatform.Android ? 90 : DeviceInfo.Platform == DevicePlatform.iOS ? 100 : 90 });
    contentGrid.RowDefinitions.Add(new RowDefinition() { Height = GridLength.Auto });
    contentGrid.ColumnDefinitions.Add(new ColumnDefinition() { Width = 100 });
    contentGrid.ColumnDefinitions.Add(new ColumnDefinition() { Width = 100 });
    contentGrid.ColumnDefinitions.Add(new ColumnDefinition() { Width = GridLength.Star });
    var image = new Image();
    image.SetBinding(Image.SourceProperty, new Binding("Image"));
    var frame = new Frame() { BorderColor = Colors.Transparent, Padding = 0, Margin = new Thickness(0, 0, 0, 7) };
    frame.Content = image;
    contentGrid.SetRowSpan(frame, 4);
    contentGrid.SetRow(frame, 0);
    contentGrid.SetColumn(frame, 0);
    contentGrid.Children.Add(frame);
    var position = new Label() { Text = "Position", Margin = new Thickness(6, 0, 0, 0) };
    contentGrid.SetColumn(position, 1);
    contentGrid.SetRow(position, 0);
    contentGrid.Children.Add(position);
    var positionVal = new Label();
    positionVal.SetBinding(Label.TextProperty, new Binding("Position"));
    contentGrid.SetColumn(positionVal, 2);
    contentGrid.SetRow(positionVal, 0);
    contentGrid.Children.Add(positionVal);
    var organization = new Label() { Text = "Organization", Margin = new Thickness(6, 0, 0, 0) };
    contentGrid.SetColumn(organization, 1);
    contentGrid.SetRow(organization, 1);
    contentGrid.Children.Add(organization);
    var organizationVal = new Label();
    organizationVal.SetBinding(Label.TextProperty, new Binding("OrganizationUnit"));
    contentGrid.SetColumn(organizationVal, 2);
    contentGrid.SetRow(organizationVal, 1);
    contentGrid.Children.Add(organizationVal);
    var dob = new Label() { Text = "Date Of Birth", Margin = new Thickness(6, 0, 0, 0) };
    contentGrid.SetColumn(dob, 1);
    contentGrid.SetRow(dob, 2);
    contentGrid.Children.Add(dob);
    var dobVal = new Label();
    dobVal.SetBinding(Label.TextProperty, new Binding("DateOfBirth"));
    contentGrid.SetColumn(dobVal, 2);
    contentGrid.SetRow(dobVal, 2);
    contentGrid.Children.Add(dobVal);
    var location = new Label() { Text = "Location", Margin = new Thickness(6, 0, 0, 0) };
    contentGrid.SetColumn(location, 1);
    contentGrid.SetRow(location, 3);
    contentGrid.Children.Add(location);
    var locationVal = new Label();
    locationVal.SetBinding(Label.TextProperty, new Binding("Location"));
    contentGrid.SetColumn(locationVal, 2);
    contentGrid.SetRow(locationVal, 3);
    contentGrid.Children.Add(locationVal);
    var description = new Label() { Padding = new Thickness(0, 10, 0, 10), LineBreakMode = LineBreakMode.WordWrap, FontSize = 14, CharacterSpacing = 0.25, VerticalTextAlignment = TextAlignment.Center };
    description.SetBinding(Label.TextProperty, new Binding("Description"));
    contentGrid.SetRow(description, 4);
    contentGrid.SetColumnSpan(description, 3);
    contentGrid.Children.Add(description);
    var stack = new StackLayout();
    var label1 = new Label()
    {
        Text = "\ue700",
        FontSize = 16,
        Margin = new Thickness(0, 2, 2, 2),
        VerticalOptions = LayoutOptions.Center,
        VerticalTextAlignment = TextAlignment.Center,
        FontFamily = DeviceInfo.Platform == DevicePlatform.WinUI ? "AccordionFontIcons.ttf#AccordionFontIcons" : DeviceInfo.Platform == DevicePlatform.Android ? "AccordionFontIcons.ttf#" : DeviceInfo.Platform == DevicePlatform.iOS ? "AccordionFontIcons" : "AccordionFontIcons"
    };
    var label2 = new Label() { Text = "(617) 555-1234", CharacterSpacing = 0.25, FontSize = 14, VerticalOptions = LayoutOptions.Center };
    label2.SetBinding(Label.TextProperty, new Binding("Phone"));
    stack.Children.Add(label1);
    stack.Children.Add(label2);

    stack.Orientation = StackOrientation.Horizontal;
    stack.Margin = new Thickness(0, 0, 0, 12);
    contentGrid.SetRow(stack, 5);
    contentGrid.Children.Add(stack);
    content.Children.Add(contentGrid);
    accordionItem.Content = contentGrid;
    accordion.Items.Add(accordionItem);
    return accordionItem;
});
BindableLayout.SetItemTemplate(accordion, ItemTemplate);
BindableLayout.SetItemsSource(accordion, viewModel.Employees);
{% endhighlight %}
{% endtabs %}

![.NET MAUI Forms Accordion with Bindable Layout](Images/maui-accordion-with-bindablelayout.png)

## Events

### Get the index of expanded or collapsed accordion item.

You can get the index of the interacted `AccordionItem` by using the `Collapsed`. It will occur after an `AccordionItem` is collapsed when tapping the Header. The `ExpandedAndCollapsedEventArgs` properties provide data for the `Collapsed` event.  

{% tabs %}
{% highlight xaml %}
<syncfusion:SfAccordion x:Name="Accordion" Collapsed="Accordion_Collapsed">
{% endhighlight %}
{% highlight c# %}
Accordion.Collapsed += Accordion_Collapsed;
private void Accordion_Collapsed(object sender, Syncfusion.Maui.Accordion.ExpandedAndCollapsedEventArgs e)
{
    var value = e.Index.ToString();
    DisplayAlert("Index", value, "ok");
}
{% endhighlight %}
{% endtabs %}		

Using the `Expanded` event, you can get the index of the interacted `AccordionItem.` It will occur after an `AccordionItem` is expanded when tapping on the `Header`. The `ExpandedAndCollapsedEventArgs` properties provides data for the `Expanded` event.  

{% tabs %}
{% highlight xaml %}
<syncfusion:SfAccordion x:Name="Accordion" Expanded="Accordion_Expanded">
{% endhighlight %}
{% highlight c# %}
Accordion.Expanded += Accordion_Expanded;
private void Accordion_Expanded(object sender, Syncfusion.Maui.Accordion.ExpandedAndCollapsedEventArgs e)
{
    var value = e.Index.ToString();
    DisplayAlert("Index", value, "ok");
}
{% endhighlight %}
{% endtabs %}

### Restricting the accordion item expanding and collapsing 

The `Collapsing` event occurs while collapsing an `AccordionItem` when tapping on the `Header`. You can cancel the collapsing action by using the `Cancel` property in the event args. 

{% tabs %}
{% highlight xaml %}
<syncfusion:SfAccordion x:Name="Accordion" Collapsing="Accordion_Collapsing">
{% endhighlight %}
{% highlight c# %}
Accordion.Collapsing += Accordion_Collapsing;
private void Accordion_Collapsing(object sender, ExpandingAndCollapsingEventArgs e)
{
   e.cancel = true;
}
{% endhighlight %}
{% endtabs %}

You can also get the index of the interacted `AccordionItem` by using the `index` property of the `ExpandingAndCollapsingEventArgs`.

{% tabs %}
{% highlight c# %}
private void Accordion_Collapsing(object sender, ExpandingAndCollapsingEventArgs e)
{
    var value = e.Index.ToString();
    DisplayAlert("Index", value, "ok");
}
{% endhighlight %}
{% endtabs %}

The `Expanding` event occurs while expanding an `AccordionItem` when tapping on the `Header`. You can cancel the expanding action by using the `Cancel` property in the event args. 

{% tabs %}
{% highlight xaml %}
<syncfusion:SfAccordion x:Name="Accordion" Expanding="Accordion_Expanding">
{% endhighlight %}
{% highlight c# %}
Accordion.Expanding += Accordion_Expanding;
private void Accordion_Expanding(object sender, ExpandingAndCollapsingEventArgs e)
{
    e.Cancel = true;
}
{% endhighlight %}
{% endtabs %}

You can also get the index of the interacted `AccordionItem` by using the `index` property of the `ExpandingAndCollapsingEventArgs`.

{% tabs %}
{% highlight c# %}
private void Accordion_Expanding(object sender, ExpandingAndCollapsingEventArgs e)
{
    var value = e.Index.ToString();
    DisplayAlert("Index",value, "ok");
}
{% endhighlight %}
{% endtabs %}
                                                                                                                                                         
