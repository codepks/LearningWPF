# Starting
MainWindow.xaml is the xaml file to start with.

# Basics
```
<Button FontWeight="Bold" Content="A button" />
```

The above code can be written in **Control-Dot-Property** notation

```
<Button>
    <Button.FontWeight>Bold</Button.FontWeight>
    <Button.Content>A button</Button.Content>
</Button>
```

## WrapPanel
The Content property only allows for a single child element, so we use a WrapPanel to contain the differently colored blocks of text.
```
<Button>
    <Button.FontWeight>Bold</Button.FontWeight>
    <Button.Content>
        <WrapPanel>
            <TextBlock Foreground="Blue">Multi</TextBlock>
            <TextBlock Foreground="Red">Color</TextBlock>
            <TextBlock>Button</TextBlock>
        </WrapPanel>
    </Button.Content>
</Button>
```

# WPF Tutorial
![image](https://github.com/codepks/LearningWPF/assets/17923311/4e708224-ac44-4500-9b73-433519d3e12d)

1. Create **WPF Application** from the Visual Studio
2. We will start by putting the elements in **stackPanel** to stack the elements one after the another
3. Change the <Grid> to **<StackPanel>** as it puts the elements one above the another
```
<StackPanel>
    <Button Content="Test"/>
    <Button Content="Test"/>
    <Button Content="Test"/> 
</StackPanel>
```
4.  **<Grid>** on the other hands puts the elements in overlap as Grid is one element or one row thing
```
<Grid>
    <Button Content="Test"/>
    <Button Content="Test"/>
    <Button Content="Test"/>
</Grid>
```
5. In the above requirement, we need two degrees of stackPanel one for the outer for stacking up groups and one for the elements

![image](https://github.com/codepks/LearningWPF/assets/17923311/6fd42592-989e-405d-9091-23896dd013fb)

6. But 2nd degree of stacking would not equally divide our grid, so we can achieve this using **Grid** and **ColumnDefinitions**
- First make the column definition
- put buttons inside the column definition 
```
<StackPanel>
    <Grid >
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*"/>
            <ColumnDefinition Width="*"/>
            <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>

        <Button Grid.Column="0" Content="Apply"/>
        <Button Grid.Column="1" Content="Reset"/>
        <Button Grid.Column="2" Content="Refresh"/>
    </Grid>
</StackPanel>
```
**"*"** denotes the equal ration thing when diving the column width wise

7. Overall Padding : To put a good padding around whole code we can use **<Border Padding = " ">**
```
<Border Padding="10">
<StackPanel>
    <Grid >
```

8. To put padding around the buttons, we can use **Margin** inside the buttons
```
<Button Margin="10 0 10 0" Grid.Column="0" Content="Apply"/>
```
9. Note : Padding goes inside whereas margin goes outside.

10. To increase the size of textbox we can use padding instead of margin(which will reduce its size)

11. In this example we mostly decide between StackPanel or Grid. If there is more than one element in row then it would be Grid else STackPAnel in case of StackPanel.

12. In order to enter multiple elements in rows and columns (it cnabe visually identified) make a grid and add row and column definitions
    - In general start with Grid.ColumnDefinitions and within column one can add stack of items

13. For combo box and selecting the default one:
```
<ComboBox Padding="2" SelectedIndex="0" Margin="0 0 0 10" >
    <ComboBoxItem>Rubber</ComboBoxItem>
    <ComboBoxItem>Not Rubber</ComboBoxItem>
</ComboBox>
```

14. For adding controller to the element be it button or checkbox you need to have its listener in the source code and a controller which you mention with the name of the checkbox using **x:Name=""**

15. On Adding events like **Click** and **Checked** the source code will automatically add the listener function in source code through which the events will be recieved. You can adjust the name to make it customized as per your needs.

In the code below we are trying to display some text on the Desciption box on click of apply button
_xaml code_
```
 <TextBox x:Name="DescriptionTextBox" Padding="2"/>

 <Button x:Name="ApplyButton" Click="ApplyButton_Click" Margin="0 0 10 0" Grid.Column="0" Content="Apply" />
```
_added source code_
```
 private void Apply_Button_Click(object sender, RoutedEventArgs e)
 {
     this.DescriptionTextBox.Text = "Apply Button Clicked";
 }
```


16. **Events**
    -  for Button is **Click** and
    -  for Checkbox is **Checked**

17. The **xName** given is a controlled and can be accessed via
```
this.TextController
```
18. How to get the handle of the element from the listener function:
```
private void Checkbox_Checked(object sender, RoutedEventArgs e)
{
    this.LengthText.Text += ((CheckBox)sender).Content;
}
```
here **sender** is the checkbox itself (parent)which needs to be typecasted to the checkbox before being used as the type Checkbox

Note: + operator is necessary here because you _add to_ what is already in there instead of overwriting it.

19. Similary for retrieving item from Dropdown and displaying it on a TextBlock
selectionChanged is the _event handler_ here
```
<ComboBox SelectionChanged="ComboBox_SelectionChanged_Purchase"  Padding="2" SelectedIndex="0" Margin="0 0 0 10" >
    <ComboBoxItem>Rubber</ComboBoxItem>
    <ComboBoxItem>Not Rubber</ComboBoxItem>
</ComboBox>

<TextBlock Text="Supplier Name"/>
<TextBox x:Name="PurchaseNote" Margin="0 0 0 10"/>
```

```
private void ComboBox_SelectionChanged_Purchase(object sender, SelectionChangedEventArgs e)
{
    if (PurchaseNote == null)
        return;

    var combo = (ComboBox)sender;
    var selectedValue = (ComboBoxItem)combo.SelectedValue;

    this.PurchaseNote.Text += (string)selectedValue.Content;
}
```
Note:
- We check for null as on UI load the combobox is null, so to avoid crash we check for null.
- The sequestion is :
    a. Get the combo
    b. Get the selected value as ComboItem from the combo
    c. Get the content from the ComboItem and cast it to a string

20. 









