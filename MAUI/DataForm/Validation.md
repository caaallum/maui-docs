---
layout: post
title: Data validation in .NET MAUI DataForm control | Syncfusion
description: Learn about the validation feature in Syncfusion .NET MAUI DataForm (SfDataForm) control in mobile and desktop applications from a single shared codebase.
platform: maui
control: SfDataForm
documentation: ug
---

# Data Validation in .NET MAUI DataForm (SfDataForm)

The data form validates the data and user input to update the correct value in the underlying data object. In invalid data, the error message is shown at the bottom of the editor.

## Built in validations

The supported built in validations such as [Data Annotations](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations?view=net-7.0), [IDataErrorInfo](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.idataerrorinfo?view=net-6.0), [INotifyDataErrorInfo](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.inotifydataerrorinfo?view=net-6.0)

### Validate using the validation attribute

#### Data annotations

Validate the data using data annotation attributes.

The String type property is validated using the [Required](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations.requiredattribute?view=netframework-4.8) and [StringLength](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.8) attributes.

{% tabs %}
{% highlight C# %}

[Required(AllowEmptyStrings = false, ErrorMessage = "Name should not be empty")]
[StringLength(15, ErrorMessage = "Name should not exceed 15 characters")]
public string Name { get; set; }

{% endhighlight %}
{% endtabs %}

Refer [here](https://help.syncfusion.com/maui/dataform/data-annotations) to know more about data annotations in DataForm.

#### Date range attribute

Validate the date time value using the date range attribute.

{% tabs %}
{% highlight C# %}

[DataType(DataType.Date)]
[DataFormDateRange(MinimumDate = "01/01/2022", MaximumDate = "31/12/2022", ErrorMessage = "Join date is invalid")]
public DateTime JoinDate { get; set; }

{% endhighlight %}
{% endtabs %}

Refer [here](https://help.syncfusion.com/maui/dataform/data-annotations#dateformdaterange-attribute) to know more about date range attribute in DataForm.

### Validate using the IDataErrorInfo interface

You can validate the data by implementing the [IDataErrorInfo](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.idataerrorinfo?view=net-6.0) interface in the data object class.

{% tabs %}
{% highlight C# %}

public class EmployeeInfo : IDataErrorInfo
{
    public string EmployeeID { get; set; }

    public string Name { get; set; }

    public string Title { get; set; }

    [Display(AutoGenerateField = false)]
    public string Error
    {
        get
        {
            return string.Empty;
        }
    }

    [Display(AutoGenerateField = false)]
    public string this[string columnName]
    {
        get
        {
            if (columnName == nameof(Title) && this.Title.Contains("Marketing"))
            {
                return "Marketing is not allowed";
            }

            return string.Empty;
        }
    }
}

{% endhighlight %}
{% endtabs %}

You can download the entire source code [here](https://github.com/SyncfusionExamples/maui-dataform/tree/master/DataErrorInfoSample)

### Validate using the INotifyDataErrorInfo interface

You can validate the data by implementing the [INotifyDataErrorInfo](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.inotifydataerrorinfo?view=net-6.0) interface in the data object class. This interface has three members,

* [HasErrors property](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.inotifydataerrorinfo.haserrors?view=net-6.0#system-componentmodel-inotifydataerrorinfo-haserrors)
* [GetErrors method](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.inotifydataerrorinfo.geterrors?view=net-6.0#system-componentmodel-inotifydataerrorinfo-geterrors(system-string))
* [ErrorsChanged event](https://learn.microsoft.com/en-us/dotnet/api/system.componentmodel.inotifydataerrorinfo.errorschanged?view=net-6.0)

{% tabs %}
{% highlight C# %}

public class EmployeeInfo : INotifyDataErrorInfo
{
    public event EventHandler<DataErrorsChangedEventArgs> ErrorsChanged;

    public string EmployeeID { get; set; }

    public string Name { get; set; }

    public string Title { get; set; }

    [Display(AutoGenerateField = false)]
    public bool HasErrors
    {
        get
        {
            return false;
        }
    }

    public IEnumerable GetErrors(string propertyName)
    {
        var list = new List<string>();
        if (propertyName == nameof(Title) && this.Title.Contains("Marketing"))
        {
            list.Add("Marketing is not allowed");
        }

        return list;
    }
}

{% endhighlight %}
{% endtabs %}

You can download the entire source code [here](https://github.com/SyncfusionExamples/maui-dataform/tree/master/NotifyDataErrorInfoSample)

## Validation mode

The [ValidationMode](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_ValidationMode) determines when the value should be validated.

The supported validation modes are as follows:

* LostFocus
* PropertyChanged
* Manual

{% tabs %}
{% highlight XAML %}
<ContentPage 
...
xmlns:dataForm="clr-namespace:Syncfusion.Maui.DataForm;assembly=Syncfusion.Maui.DataForm">
    <dataForm:SfDataForm
        x:Name="dataForm" 
        ValidationMode="LostFocus">
    </dataForm:SfDataForm>
</ContentPage>

{% endhighlight %}
{% highlight C# %}

this.dataForm.ValidationMode = DataFormValidationMode.LostFocus;

{% endhighlight %}
{% endtabs %}

#### LostFocus

If the validation mode is [LostFocus](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormValidationMode.html#Syncfusion_Maui_DataForm_DataFormValidationMode_LostFocus), the value will be validated when the editor loses its focus. By default, the [ValidationMode](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_ValidationMode) is `LostFocus`.

#### PropertyChanged

If the validation mode is [PropertyChanged](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormValidationMode.html#Syncfusion_Maui_DataForm_DataFormValidationMode_PropertyChanged), the value will be validated immediately when it is changed.

#### Manual

If the validation mode is [Manual](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormValidationMode.html#Syncfusion_Maui_DataForm_DataFormValidationMode_Manual), the value should be validated manually by calling the [SfDataForm.Validate](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_Validate) or [SfDataForm.Validate(new List())](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_Validate_System_Collections_Generic_List_System_String__) method.

The following code validates the value of all the properties in the data object:

{% tabs %}
{% highlight C# %}

this.dataForm.Validate();

{% endhighlight %}
{% endtabs %}

To validate the specific list of property value, pass the property names as argument.

{% tabs %}
{% highlight C# %}

this.dataForm.Validate(new List<string>() {"FirstName", "Age" });

{% endhighlight %}
{% endtabs %}

Determine whether the data form or property is valid by using the [Validate](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_Validate) method.

{% tabs %}
{% highlight C# %}

bool isValid = this.dataForm.Validate();

List<string> propertyNames = new List<string>();
propertyNames.Add("FirstName");
bool isPropertyValid = this.dataForm.Validate(propertyNames);

{% endhighlight %}
{% endtabs %}

If the data form or property is valid, `true` will be returned. Or else `false` will be returned.

![Error message in .NET MAUI DataForm.](images/validation/error-message.png)

N> [View sample in GitHub](https://github.com/SyncfusionExamples/maui-dataform/tree/master/ManualValidation)

## Valid message

If the values are correct, show the [ValidMessage](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormDisplayOptionsAttribute.html#Syncfusion_Maui_DataForm_DataFormDisplayOptionsAttribute_ValidMessage) like an error message, the valid message will also be displayed at the bottom of the editor.

{% tabs %}
{% highlight C# %}

[DataFormDisplayOptions(ValidMessage = "Password strength is good")]
[Required(ErrorMessage = "Please enter the password")]
[RegularExpression(@"^(?=.*[a-z])(?=.*[A-Z])[a-zA-Z\d]{8,}$", ErrorMessage = "A minimum 8-character password should contain a combination of uppercase and lowercase letters.")]
public string Password { get; set; }

{% endhighlight %}
{% endtabs %}

![Valid message in .NET MAUI DataForm.](images/validation/valid-message.png)

## Validate the data form

Get the validation details of all the editors of the data form using the [ValidateForm](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_ValidateForm) event of the data form.

N> This event will be raised once after the manual validation call using the [SfDataForm.Validate()](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_Validate) method.

{% tabs %}
{% highlight C# %}

this.dataForm.ValidateForm += this.OnDataFormValidateForm;

private void OnDataFormValidateForm(object sender, DataFormValidateFormEventArgs e)
{
    object dataObject = e.DataObject;
    var values = e.NewValues;
    var errorMessage = e.ErrorMessage;
}

{% endhighlight %}
{% endtabs %}

## Validate the specific editor

The [ValidateProperty](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_ValidateProperty) event allows you to validate specific editors in the data form. Set [IsValid](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormValidatePropertyEventArgs.html#Syncfusion_Maui_DataForm_DataFormValidatePropertyEventArgs_IsValid), [ErrorMessage](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormValidatePropertyEventArgs.html#Syncfusion_Maui_DataForm_DataFormValidatePropertyEventArgs_ErrorMessage), and [ValidMessage](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormValidatePropertyEventArgs.html#Syncfusion_Maui_DataForm_DataFormValidatePropertyEventArgs_ValidMessage) of the [DataFormValidatePropertyEventArgs](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormValidatePropertyEventArgs.html).

{% tabs %}
{% highlight C# %}

this.dataForm.ValidateProperty += this.OnDataFormValidateProperty;

private void OnDataFormValidateProperty(object sender, DataFormValidatePropertyEventArgs e)
{
    bool isValid = e.IsValid;
    string propertyName = e.PropertyName;
    object newValue = e.NewValue;
    object currentValue = e.CurrentValue;
    string errorMessage = e.ErrorMessage;
    string validMessage = e.ValidMessage;
}

{% endhighlight %}
{% endtabs %}

## Validation label appearance customization

The data form supports customizing the style of both error and valid message label style easily.

#### Customize error label text style

The error label style can be customized by changing the [ErrorLabelTextStyle](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_ErrorLabelTextStyle) property of the [SfDataForm](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html).

{% tabs %}
{% highlight XAML %}

<dataForm:SfDataForm
    x:Name="dataForm">
    <dataForm:SfDataForm.ErrorLabelTextStyle>
        <dataForm:DataFormTextStyle FontSize="10" FontAttributes="Italic" TextColor="Violet" FontFamily="Roboto"/>
    </dataForm:SfDataForm.ErrorLabelTextStyle>
</dataForm:SfDataForm>

{% endhighlight %}
{% endtabs %}

Also, customize the error label style for each editor using the [ErrorLabelTextStyle](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormItem.html#Syncfusion_Maui_DataForm_DataFormItem_ErrorLabelTextStyle) property of the [DataFormItem](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormItem.html).

{% tabs %}
{% highlight C# %}

this.dataForm.GenerateDataFormItem += OnGenerateDataFormItem;

private void OnGenerateDataFormItem(object sender, GenerateDataFormItemEventArgs e)
{
    if (e.DataFormItem != null)
    {
        if (e.DataFormItem.FieldName == "FirstName")
        {
            e.DataFormItem.ErrorLabelTextStyle = new DataFormTextStyle
            {
                TextColor = Colors.DarkSeaGreen,
                FontSize = 8,
                FontAttributes = FontAttributes.Italic,
                FontFamily = "Roboto",
            };
        }
    }
}

{% endhighlight %}
{% endtabs %}

![Error message style in .NET MAUI DataForm.](images/validation/error-message-style.png)

#### Customize valid message label text style

The valid message label style can be customized by changing the [ValidMessageLabelTextStyle](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html#Syncfusion_Maui_DataForm_SfDataForm_ValidMessageLabelTextStyle) property of the [SfDataForm](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.SfDataForm.html).

{% tabs %}
{% highlight XAML %}

<dataForm:SfDataForm
    x:Name="dataForm">
    <dataForm:SfDataForm.ValidMessageLabelTextStyle>
        <dataForm:DataFormTextStyle FontSize="10" FontAttributes="Italic" TextColor="Violet" FontFamily="Roboto"/>
    </dataForm:SfDataForm.ValidMessageLabelTextStyle>
</dataForm:SfDataForm>

{% endhighlight %}
{% endtabs %}

Also, customize the valid message label style for each editor using the [ValidMessageLabelTextStyle](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormItem.html#Syncfusion_Maui_DataForm_DataFormItem_ValidMessageLabelTextStyle) property of the [DataFormItem](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.DataForm.DataFormItem.html).

{% tabs %}
{% highlight C# %}

this.dataForm.GenerateDataFormItem += OnGenerateDataFormItem;

private void OnGenerateDataFormItem(object sender, GenerateDataFormItemEventArgs e)
{
    if (e.DataFormItem != null)
    {
        if (e.DataFormItem.FieldName == "FirstName")
        {
            e.DataFormItem.ValidMessageLabelTextStyle = new DataFormTextStyle
            {
                TextColor = Colors.DarkSeaGreen,
                FontSize = 8,
                FontAttributes = FontAttributes.Italic,
                FontFamily = "Roboto",
            };
        }
    }
}

{% endhighlight %}
{% endtabs %}

![Valid message style in .NET MAUI DataForm.](images/validation/valid-message-style.png)