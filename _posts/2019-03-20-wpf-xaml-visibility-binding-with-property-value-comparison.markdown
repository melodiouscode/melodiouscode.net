---
layout: post
title: WPF XAML Visibility binding with property value comparison
date: '2019-03-20 19:18:04'
image: /images/posts/daniil-kuzelev-327645-unsplash-min.jpg
tags:
- wpf
- dotnet
- c
- xaml
- mvvm
---

Following on from my previous articles about '[Passing multiple parameters to an ICommand in WPF](https://melodiouscode.net/passing-multiple-parameters-to-an-icommand-in-wpf/)' and '[Speeding up large WPF ComboBoxes](https://melodiouscode.net/speeding-up-large-wpf-comboboxes/)' the application stack I am currently working on has provided another article on a [WPF subject](https://melodiouscode.net/tag/wpf/)!

The ability to show or hide UI elements based on criteria related to other elements is nothing new; only showing an 'Other Details' text box when a drop-down value of 'Other' is selected is the bread and butter of many end-user applications. There are a number of ways of doing this in the WPF/XAML/MVVM world, the default is often the use of a property on the ViewModel relating to the visibility (or enabled state) of the UI element in question, and this is how I have been implementing it until now!

The most recent set of screens I have been working on are a lot more complicated than other parts of the application (lots of business logic fields which depend on the values of other fields). Adding lots and lots of 'IsEnabled' or 'IsVisible' properties (along with their backing fields, and INotifyProperyChanged code) seemed very messy to me, and I felt there must be a better solution. I already use an IValueConverter to convert simple boolean values (FirstNameIsVisible for example) into WPF Visibility values, so I thought I could take that one step further and perform comparisons.

## ComparisonToVisibleConverter

A simple binding to a property on your ViewModel or in the case of this example to a property on a selected dropdown list entry grants you the source for the comparison.

<!--kg-card-begin: markdown-->

    <GroupBox Header="Team Details" Margin="0,6,0,0"
      Visibility="{Binding ElementName=comboStaffMember, Path=SelectedItem.EmployeeType, 
    	Converter={StaticResource ComparisonToVisibleConverter}, ConverterParameter='Manager||SeniorManager||GroupLeader'}">
    	...
    </GroupBox>

<!--kg-card-end: markdown-->

The converter in the above code snippet is where all the magic happens; it takes the bound value and the ConverterParameter to perform the comparisons and return a Visibility value.

<!--kg-card-begin: markdown-->

    ValueConversion(typeof(bool), typeof(Visibility))]
    public class ComparisonToVisibleConverter : IValueConverter {
    	#region interface implementations
    
    	public object Convert(object value, Type targetType, object parameter, CultureInfo culture) {
    		try {
    			string inputParameter = parameter?.ToString() ?? "";
    
    			IEnumerable<string> paramList = inputParameter.Contains("||") ? inputParameter.Split(new[] {"||"}, StringSplitOptions.None) : new[] {inputParameter};
    
    			return paramList.Any(param => string.Equals(value?.ToString(), param)) ? Visibility.Visible : Visibility.Collapsed;
    		} catch {
    			return Visibility.Visible;
    		}
    	}
    
    	public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture) {
    		return value?.ToString() != Visibility.Collapsed.ToString();
    	}
    
    	#endregion
    }

<!--kg-card-end: markdown-->

To allow for an 'in' style of comparison the CommandParameter is a string that can if required to contain a double pipe ('||') as a separator. The parameter is taken and compared against the bound property (value in the above code). As a catch-all, the converter returns Visible in the case of a failure.

To reference the converter in your XAML code you need to declare it somewhere globaly or in resources local to your view.

<!--kg-card-begin: markdown-->

    <converters:ComparisonToVisibleConverter x:Key="ComparisonToVisibleConverter" />

<!--kg-card-end: markdown-->

This pattern provides for a quick, clean, and easy way to determine a UI Elements visibility based on the value of another element (or a computed value in the ViewModel).

<!--kg-card-begin: markdown-->

<small>Thank you to <a href="https://unsplash.com/photos/QRawWgV6gmo?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Daniil Kuželev</a> for providing the header image for this article for free on <a href="https://unsplash.com">Unsplash</a>.</small>

<!--kg-card-end: markdown-->