---
layout: post
title: Speeding up large WPF ComboBoxes
date: '2019-03-11 20:33:20'
image: /images/posts/jimmy-chang-670386-unsplash-min.jpg
tags:
- wpf
- dotnet
- xaml
---

The WPF application I am working on at the moment contains a questionnaire definition system; the user interface for which contains a number of ComboBoxes (drop-down lists). The nature of the application means that some of these ComboBoxes contain a large number of dynamic entries (not hardcoded, they change based on user actions).

I have found that WPF ComboBoxes with a large number of entries; particularly ones which have overridden ToString methods, can take a second or two to 'drop down' (display). This is because WPF renders the entire dropdown interface when it opens; this means if you have many entries in the list each one will be rendered regardless of its position in the list. If you have custom logic inside the ToString methods this can present a significant overhead on the UI thread.

### The Solution

The quick solution is to use a VirtualizingStackPanel to display the ComboBox items; this has the effect of delaying the rendering of each item until it is needed (when it is scrolled into view). The following code is an example of a VirtualizingStackPanel in use.

<!--kg-card-begin: markdown-->

    <ComboBox ItemsSource="{Binding SomeSourceBinding}">
    	<ComboBox.ItemsPanel>
    		<ItemsPanelTemplate>
    			<VirtualizingStackPanel />
    		</ItemsPanelTemplate>
    	</ComboBox.ItemsPanel>
    </ComboBox>

<!--kg-card-end: markdown-->

There are of course disadvantages to this approach. For example if you had a ComboBox with hundreds of options; but only 10 shown initially, scrolling down by 20 will generate another 10 item containers. When you scroll back up by 10 they will be re-generated regardless of them having already been created. This overhead is less obvious if a user just scrolls to their option and selects it; however, if they start scrolling up and down the performance hit will become more evident.

And before you ask about the header image; you try finding an image that fits with the idea of a ComboBox (or a DROP down)! Thank you to [Jimmy &nbsp;Chang](https://unsplash.com/photos/NP8gd2KUnfw?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) for providing the "drop" image on [Unsplash](https://unsplash.com/search/photos/drop-down?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText).

