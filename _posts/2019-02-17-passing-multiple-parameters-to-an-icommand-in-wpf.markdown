---
layout: post
title: Passing multiple parameters to an ICommand in WPF
date: '2019-02-17 13:22:10'
image: /images/posts/hannah-joshua-644247-unsplash-min.jpg
tags:
- c
- wpf
- developer
---

The project I am currently working on is a sizable line-of-business desktop program written using the WPF framework; a framework I particularly like working with due to its extensibility and ease of design (via XAML).  
One of the powerful parts of WPF is the ICommand system for binding buttons to ViewModel methods; I won't go into the details of it here as it deserves an article of its own. However one of its basic functions is the ability to pass a parameter from the UI back to the ViewModel's ICommand property, such as the selected item in a data table.

The application I am currently working on has lots of nested UI components, and some of the button events need to pass back multiple parameters (something I had not done before). It seems that it is perfectly possible to pass more than one parameter from the XAML View up to the ViewModel.  
The XAML is simple, you nest a MultiValueConverter inside your buttons CommandParameter element; you also need to provide a reference to an IMultiValueConverter (which you can define statically in a resource elsewhere in your application).

<!--kg-card-begin: markdown-->

    <Button Command="{Binding DeleteQuestionRuleCommand}" Content="Delete">
      <Button.CommandParameter>
        <MultiBinding Converter="{StaticResource ArrayMultiValueConverter}">
    	  <Binding Path="SelectedItem" ElementName="comboPages" />
    	  <Binding Path="SelectedItem" ElementName="gridQuestions" />
    	  <Binding Path="SelectedItem" ElementName="gridRules" />
    	</MultiBinding>
      </Button.CommandParameter>
    </Button>

<!--kg-card-end: markdown-->

The easiest way to pass multiple parameters is as a simple object array; you can then test the objects are there and are the correct type in your CanExecute method. To do this you require an instance of an IMutiValueConverter; the following provides for the array based approach.

<!--kg-card-begin: markdown-->

    public class ArrayMultiValueConverter : IMultiValueConverter {
    	#region interface implementations
    
    	public object Convert(object[] values, Type targetType, object parameter, CultureInfo culture) {
    		return values.Clone();
    	}
    
    	public object[] ConvertBack(object value, Type[] targetTypes, object parameter, CultureInfo culture) {
    		throw new NotImplementedException();
    	}
    
    	#endregion
    }

<!--kg-card-end: markdown-->

Once your XAML and IMultiValueConverter are setup you will need to access the values within both your CanExecure and OnExecute methods, something which you can simply achieve by casting the passed in object argument to an object array.

<!--kg-card-begin: markdown-->

    private bool CanDeletePageRule(object obj) {
    	if (obj is object[] parameters) {
    		if (!(parameters[0] is QnaPageDefWrapper)) {
    			return false;
    		}
    
    		if (!(parameters[1] is QnaRuleDefWrapper)) {
    			return false;
    		}
    	}
    	return true;
    }
    
    private void OnDeletePageRule(object obj) {
    	if (!CanDeletePageRule(obj)) {
    		return;
    	}
    
    	var parameters = (object[]) obj;
    
    	var ruleToDelete = (QnaRuleDefWrapper) parameters[1];
    	var pageToDeleteFrom = (QnaPageDefWrapper) parameters[0];
    
    	pageToDeleteFrom.Rules.RemoveItem(r => r.RuleId == ruleToDelete.RuleId);
    
    	RaiseUpdateMessage?.Invoke(this, "SelectedPageRule");
    }

<!--kg-card-end: markdown-->

It really is that simple, two or more parameters can easily be passed using this approach.

The header image for this post was provided for free on [unsplash.com](https://unsplash.com) by [Hannah Joshua](https://unsplash.com/@hannahjoshua). Thanks Hannah!

